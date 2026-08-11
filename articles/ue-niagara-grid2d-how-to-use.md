---
title: "[UE5] Niagara Grid2Dを使用するサンプル"
emoji: "🪄"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [UnrealEngine, "UE5"]
published: true
---

# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.8.1            |
| OS           | Windows11   |
| Platform | Windows |

# 概要
特定のエリア内のシーン情報を書き込み/読み込みをしてRenderTargetに反映させるにはSceneCapture2Dが便利ですが、
SceneCapture2Dを使用するとそのActor視点からの再描画をするため、設定によっては半端なくGPU負荷が高くなるという問題があります。

そこでNiagaraのGrid2Dを使用してもっとシンプルな情報を書き込むことは出来ないかと思いつくのですが、Grid2Dに関する情報がかなり少ないのも問題です。
ということで、「Actorの動いた軌跡をGrid2Dに書く→RenderTargetへ書き戻し→Materialで使用」の極力シンプルなサンプルの用意と何をしているかの解説をしていきます。

# サンプルプロジェクト
## 実行時
![](/images/ue-niagara-grid2d-how-to-use/overview_00.gif)

## プロジェクト
プロジェクト自体を見て動かすのが良さそうなので、今回はBOOTHに置いてみました。
コードは書いてないのでダウンロードしてプロジェクト実行すれば動くと思います。
https://kta552.booth.pm/items/8705508

# 構成
## Blueprint
シーン内にNiagaraを管理するBlueprintが存在しています。
やってることはNiagaraのSpawnと、PlayerPositionと管理エリアの大きさをNiagaraに送るだけです。
![](/images/ue-niagara-grid2d-how-to-use/sample_01.png)

## Niagara
一番のキモなので詳細は後述しますが、PlayerPositionをGrid2Dに描画、RenderTargetへGrid2Dの情報を描画するEmitterが居ます。
![](/images/ue-niagara-grid2d-how-to-use/sample_02.png)

## Material
Niagaraで描画されたRenderTargetの描画を行います。
UVはNiagaraで設定されたエリアサイズでUV計算をします。
![](/images/ue-niagara-grid2d-how-to-use/sample_03.png)

# Grid2D Collectionとは
公式ドキュメントが見当たらないので「こうだと思ってる」で書きます。
Grid2DはNiagaraのシミュレーションから読み書きできる2次元配列だと思ってます。
各テクセル単位に情報を詰めることが出来て、Niagaraのシミュレーションステージで加工することが出来ます。
加工後、RenderTargetに情報を書き出すことも出来るので今回使用しています。

# Niagara詳細
## Grid2Dの初期化
**一番重要です。**
Grid2Dは縦横のサイズを指定して初期化する必要があります。
ありますがサイズ指定はプロパティに出ていないのでスクラッチパッドからする必要があります。
![](/images/ue-niagara-grid2d-how-to-use/sample_04.png)
![](/images/ue-niagara-grid2d-how-to-use/sample_05.png)

たまにやりがちなミスとして、スクラッチパッドの入力として用意したけど設定するのを忘れるというのがあるので、設定ミスに注意しましょう。
![](/images/ue-niagara-grid2d-how-to-use/sample_06.png)

## PlayerPositionをGrid2Dへ書き込み
Stage的には1つ手前にDecayの処理がありますが、こっちが本丸なので先に書きます。

Stageを新しく作り、IterationSourceをDataInterfaceにして、DataInterfaceを用意したGrid2Dに設定します。
![](/images/ue-niagara-grid2d-how-to-use/sample_07.png)

PlayerPositionがGrid2DのUV空間内(0~1)のどこにあるかを計算して保存しておきます。
![](/images/ue-niagara-grid2d-how-to-use/sample_08.png)

DataInterfaceをGrid2Dにすることで、Stageの処理はGrid2Dの各テクセルごとに行われます。
なので、Grid2Dの各テクセルごとのUV座標と保存しておいたUV座標で差分を取ってUV座標単位での差を計算します。
UV座標単位の計算後、管理するエリアのサイズを掛けることでワールド座標単位での差にします。
ワールド座標単位での差にすることで、「計算しているテクセル座標とプレイヤー座標はどれぐらいの距離があるか」を計算出来るようになります。
なのでそのベクトルのlengthを計算して、指定したRadius（プレイヤーの足のサイズと仮定）範囲内だったらマスクになるようにしておきます。
![](/images/ue-niagara-grid2d-how-to-use/sample_09.png)

コード的には下記です。
```
float2 PixelUV = Grid2D.ExecutionIndexToUnit(); // Grid2Dの0~1のUV座標が取れる
float2 DeltaUV = PixelUV - FootUV;
float2 DeltaWS = (PixelUV - FootUV) * User.GridWorldSize;
float Dist = length(DeltaWS);    
float Stamp = 1.0 - smoothstep(User.FootRadius * 0.7, User.FootRadius, Dist);
```

処理するGrid2Dのテクセルのマスク情報が出来たので、その情報をGrid2Dに書き込みしていきます。
Grid2DのPreviousFloatValueを使用すると保存済みのGrid2Dの情報が取れるので、その情報と今回のマスク情報のMaxを書き込みます。
保存済みの情報とのMaxにすることで、軌跡にすることが出来ます。
書き込みはStackContextのNamespaceにすることで書き込みが出来ます。
重要なポイントですが、保存するStackContextの変数名がそのままGrid2DのAttributeになります。
なので、書き込みした名前と読み込み時のAttributeの名前は揃える必要があります。
![](/images/ue-niagara-grid2d-how-to-use/sample_10.png)

## Grid2Dへ書いた情報を徐々にフェードさせる
ほぼおまけです。
Stage_CacheのSPM_Grid_Decayの処理です。
Grid2Dに書いた情報を読んで、適当な1.0未満の係数を掛けて再度書き込みをすることで徐々にフェードアウトさせています。
![](/images/ue-niagara-grid2d-how-to-use/sample_11.png)

## Grid2Dへ書いた情報をRenderTargetへ書き込みする
説明通りです。
ここもDataInterfaceをGrid2DにしてGrid2Dのテクセル単位で処理が行われるようにします。
そのテクセルの情報をRenderTargetのピクセルに書き込みしています。
これでマテリアルからRenderTargetを参照すれば、プレイヤー位置の軌跡がマスク情報として参照できるようになります。
![](/images/ue-niagara-grid2d-how-to-use/sample_11.png)

# まとめ
Grid2Dに関係する情報は調べれば多少あるのですが、今のUEバージョンに近いものがなかったので作りました。
アイディア次第では色々面白そうなことが出来ると思うので、使えるようになると便利だと思います。

# 参考
[【UE4.26】Niagara Advanced 解説基礎編~Grid2D Collection~](https://heyyocg.link/ue4-26-niagara-adavanced-grid2d-collection-basic/)
[Niagara Grid 2D feels like a superpower! Drawing Locations To a Render Target in Unreal 5.1](https://zukomedia.com/articles/niagara-grid-2d-feels-like-a-superpower-drawing-locations-to-a-render-target-in-unreal-5-1/)
[GameDev UE5 Filming Tutorials about Niagara Grid2D compute shaders oooo fancy](https://www.youtube.com/watch?v=iLT-53dR_ws)
[Creating Snow Trails in Unreal Engine 4](https://www.kodeco.com/5760-creating-snow-trails-in-unreal-engine-4)



