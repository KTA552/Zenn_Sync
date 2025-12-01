---
title: "[UE5] VirtualTextureのストレージ容量とメモリ使用量の調節方法"
emoji: "📅"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [UnrealEngine, "UE5"]
published: false
---

# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.6.1            |
| OS           | Windows11   |
| Platform | Windows |

# 概要
VirtualTexture、便利ですよね。
何かがわからない方はひとまず公式ドキュメントだったりリンク先の記事を読んでみてください。
[Unreal Engine でのストリーミング バーチャル テクスチャリング | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/streaming-virtual-texturing-in-unreal-engine)
[\[UE\] Virtual TextureとそのStreamingの仕組み、またよく頂く質問への回答 \#UE4 \- Qiita](https://qiita.com/EGJ-Nori_Shinoyama/items/4a2e84dd1d3448e81bed)
[\[UE4\]VirtualTexturingについて｜株式会社ヒストリア](https://historia.co.jp/archives/14062/)

とても便利なので使えるテクスチャには使ってメモリ使用量を抑えられるメリットがあるのですが、今時のテクスチャアセットは4K程度あることが多く、そのままパッケージングすると当然ストレージには4Kテクスチャがそのまま乗っかります。
そうなるとパッケージングしたコンテンツの容量のほとんどをテクスチャが占めてしまうということになりかねません。
また、プールしたメモリの中を上手くやりくりしてくれるシステムになっているので、実はそのプールメモリの容量が大きくなってしまって結果的にメモリを圧迫してしまうということも起こり得る事態です。

その辺り、設定方法があるのでそれを共有したいというのが目的の記事になっています。

## 検証
プロジェクトは最近公式に追加された[Stack O Bot \| Fab](https://www.fab.com/ja/listings/b4dfff49-0e7d-4c4b-a6c5-8a0315831c9c)を使用します。

# ストレージ容量の検証

何も手を加えずパッケージングしてその中のアセット容量の内訳を見てみます。
アセットの内訳の確認方法は少し前に書いた下記記事を参考にしてください。
[\[UE5\] パッケージの中のアセットのサイズ内訳を確認する方法](https://zenn.dev/kta552/articles/ue-package-size)

Asset Disk Sizeで中身を見てみると、下図のような結果になりました。
![](https://storage.googleapis.com/zenn-user-upload/5fe45ea35af2-20251201.png)

わかりやすいのが選択している`T_Metal_Painted_N`という名前のテクスチャでしょうか。
12MB程度容量があります。
中身はBC5で圧縮されるノーマルマップの4Kテクスチャです。

問題ない場合は特に何もする必要はありませんが、パッケージサイズを出来るだけ小さくしたい場合は問題になることがあります。

# メモリ容量の検証
Unreal InsightsのMemoryInsightsで確認します。
これも各アセットの使用メモリ内訳の確認方法に関しては記事を書いているので、それを参考にしてください。
[\[UE5\] Memory Insightsの使い方とアセット使用状況の表示方法](https://zenn.dev/kta552/articles/ue-memory-insights-how-to-use)

タイトル画面→Playを押したゲームが動いているところのスタート地点で計測しています。
![](https://storage.googleapis.com/zenn-user-upload/c1059a27268d-20251201.png =480x)

下図のようになりました。
![](https://storage.googleapis.com/zenn-user-upload/5d16701b5d27-20251201.png)

この中で63~65MB確保しているところがVirtualTextureで使用するプールテクスチャになります。（そのはず）
テクスチャを全て読み込むのと比較すると圧倒的に省メモリなのですが、テクスチャフォーマットによってプールが必要だったり、プラットフォーム毎にサイズを変更したいというニーズもあると思います。
その設定方法を書いていきたいと思います。

# 設定方法と結果

## ストレージ容量
ストレージに関してはテクスチャのCook時にサイズを指定する方法があります。
通常のテクスチャならXXXが使えていましたが、VirtualTextureには効きません。
VirtualTexutreのサイズを設定する場合はXXX_VTを使用する必要があります。

また、5.6からLODBiasの設定も追加されているようです。

## メモリ容量

デフォルトでは各フォーマット形式ごとに64MBのプールを使用しますが、この設定は変更することが出来ます。
VirtualTextureの中に設定がある。

「各フォーマット形式ごとに」が若干罠で、シーン上で1枚しか使用していないフォーマットのテクスチャがあったとしても、プールメモリは確保されます。
そのため、設定ミスなどでBC3とBC7が混ざってしまったりするとBC3とBC7用のプールメモリが確保されます。
意図してそのようになっているなら問題ありませんが、意図せず設定されていたりすると、メモリを逆に圧迫することになってしまいます。
ミスに関しては、Validatorを作成して予防するのがいいでしょう。

iniのテクスチャグループの設定。
Scaleさせるかどうかをそもそも決めるためのフラグがある
プールサイズのスケールのコンソール変数を調整


