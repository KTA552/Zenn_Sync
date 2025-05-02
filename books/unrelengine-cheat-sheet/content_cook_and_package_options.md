---
title: "Cook And Package Options"
---
# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |

# はじめに
Cookだったりパッケージングだったりの用語については公式ドキュメントを見てください。
[Unreal Engine でのゲームのパッケージングとクック | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/packaging-and-cooking-games-in-unreal-engine)

すごいざっくり言うとCookは各アセットを各プラットフォーム用のデータに再出力することで、
パッケージングは最終的に全てをまとめた実行ファイルを作ることです。

Cookしたデータを元にパッケージングを行うため、パッケージングを行うには前段階としてCookが必要です。

# Cook、パッケージングの方法
Editorが立ち上がっているならEditorから行うのが早いです。
![](https://storage.googleapis.com/zenn-user-upload/e24230320163-20250502.png)
Editor上部のメニューから`Platforms/${Platform}/CookContent or PackageProject`から行うのがいいでしょう。
このページではもう少し細かい制御が行えるコマンドラインからの実行方法について書きます。

# コマンドで行う
## 使い方
UnrealEditor.exeやUnrealEditor-Cmd.exeにオプションを渡してもいいですが、RunUATを今回は使います。
デフォルトでは下記場所にあります。(UE自体やバージョンは適切なところを見てください)
```
C:\Program Files\Epic Games\UE_5.5\Engine\Build\BatchFiles\RunUAT.bat
```

RunUATはUnrealAutomationToolを実行するためのバッチファイルになっています。
今回はBuildCookRunを使用します。下記のようになります。
```
C:\Program Files\Epic Games\UE_5.5\Engine\Build\BatchFiles\RunUAT.bat BuildCookRun
```
BuildCookRun以降に様々なオプションを付けていきます。
オプション一覧は`-help`を付ければ出力されます。
```
C:\Program Files\Epic Games\UE_5.5\Engine\Build\BatchFiles\RunUAT.bat BuildCookRun -help
```

## 実際に使用する例
実際にパッケージングまで行うオプションだと下記のようになります。
ここからオプションを付けたり外したりして使います。
```
RunUAT.bat BuildCookRun -project="C:\Projects\UnrealProjects\Blank_Cpp\Blank_Cpp.uproject" -clientconfig=Development -platform=Win64 -cook -build -stage -pak -package
```
たまにやるので一応注意ですが、Editorが立ち上がってる状態だと失敗するので一旦Editorは終了しておきましょう。

# よく使用するオプション
## -skipcook
Cookをスキップします。使用する際は-cookを外しましょう。
「アセットは今手元にあるCookされたものを使うが、設定変えたので実行ファイルだけ変えたい」といった場合に使用します。

## -iterate
変更があったアセットのみをCookします。
一旦変更したアセットを反映させてチェックしたいといった場合に使用します。
ちゃんとした動作確認や製品出荷時等には使用しないようにしましょう。

## -clientconfig
ビルドモードの指定を行います。
`Debug, Development, Test, Shipping`の中から指定します。

## -package
文字通りパッケージングを行います。
Stageビルドだけ必要な場合は外しましょう。

## -AdditionalCookerOptions
Cookする際の追加オプションです。オプションのオプションのようなもの。
### -cooksinglepackage
1ファイルと関連しているアセットだけCookします。
全体でCookするのは時間がかかる場合に使用します。
使い方は下記リンクが詳しいです。
[\[UE4\] 1ファイル\(と関連しているアセット\)だけをクックする \#UnrealEngine4 \- Qiita](https://qiita.com/EGJ-Takashi_Suzuki/items/ca9ab04c5b146e3ba5bd)

## -ini:
パッケージングや実行する際に.iniファイルにある設定を変えることが出来ます。
「手元のビルド時にだけある設定をOFFにしたいけどiniファイル自体は書き換えたくない」といった場合に使用出来ます。
下記リンクが詳しいです。
[UE4又はUE5で\.iniファイルの設定をコマンド引数で上書きする方法 \- だらけ者だらけ](https://darakemonodarake.hatenablog.jp/entry/2018/04/20/021034)
[第006回 コマンドラインからConfig設定を上書きする時の注意点 \| CC2の楽屋裏](https://www.cc2.co.jp/blog/?p=21872)

# 参考リンク
[Cooking Content in UnrealEngine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cooking-content-in-unreal-engine)
[［UE4］AutomationToolを使ってみる](https://zenn.dev/kihoku/articles/ad7be2c491cd34)
[Unreal Engine 5 \- プロジェクトの自動化と最適化戦略 \- \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/KYW623-2023-12-21-194650#p24)
[「Press Button, Drink Coffee」 UE4における ビルドパイプラインとメンテナンスの全体像【CEDEC 2019】 \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/KLGQ75-UE4_CEDEC19_BuildPipeline)
[【UE5\.4】 UATコマンドを使ったエディタ拡張の基礎知識 \| Alche, Inc](https://blog.alche.studio/posts/PfeUMj1h44tlMJqJNyEJB/)
[\[UE5\] パッケージビルド時のコマンドライン引数で \.Target\.cs の処理を分岐する｜株式会社ヒストリア](https://historia.co.jp/archives/37811/)
[UE5のパッケージ工程とステージビルドデバッグの勧め – 株式会社ロジカルビート](https://logicalbeat.jp/blog/18908/)
[Unreal Engine 5 イテレーション改善のための新機能とバックエンド技術紹介【CEDEC 2023】 \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/5W1L11-UE5_CEDEC2023_ImproveIteration)
[\[UE4\] デバッグに関するTips \#UnrealEngine \- Qiita](https://qiita.com/donbutsu17/items/93dcf3c3638cd603976f#%E3%82%A4%E3%83%86%E3%83%AC%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3)

