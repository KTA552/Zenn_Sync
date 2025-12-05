---
title: "[UE5] VirtualTextureのストレージ容量とメモリ使用量の調節方法"
emoji: "📅"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [UnrealEngine, "UE5"]
published: true
---

# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.6.1            |
| OS           | Windows11   |
| Platform | Windows |

# 前提
この記事は[Unreal Engine \(UE\) \- Qiita Advent Calendar 2025 \- Qiita](https://qiita.com/advent-calendar/2025/ue)
の6日目の記事になります。
また、GPU負荷やポッピング対策などの負荷や動作への言及はこの記事ではしません。

# 概要
VirtualTexture、便利ですよね。
何かがわからない方はひとまず公式ドキュメントだったりリンク先の記事を読んでみてください。
[Unreal Engine でのストリーミング バーチャル テクスチャリング | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/streaming-virtual-texturing-in-unreal-engine)
[\[UE\] Virtual TextureとそのStreamingの仕組み、またよく頂く質問への回答 \#UE4 \- Qiita](https://qiita.com/EGJ-Nori_Shinoyama/items/4a2e84dd1d3448e81bed)
[\[UE4\]VirtualTexturingについて｜株式会社ヒストリア](https://historia.co.jp/archives/14062/)

とても便利なので使えるテクスチャには使ってメモリ使用量を抑えていくのがそこそこハイエンド以上なプラットフォーム向けの開発では主流ではないでしょうか。
ただ、今時のテクスチャアセットは4K程度あることが多く、そのままパッケージングすると当然ストレージには4Kテクスチャがそのまま乗ります。
そうなるとパッケージングしたコンテンツの容量のほとんどをテクスチャが占めてしまうということになりかねません。
また、プールしたメモリの中を上手くやりくりしてくれるシステムになっているので、実はそのプールメモリの容量が大きくなってしまい、結果的にメモリを圧迫してしまうということも起こり得る事態です。

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
12MB程度のサイズがあります。
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
ストレージに関してはテクスチャのCook時にサイズを指定します。
詳しくは下記ドキュメントを参考にしてください。
[Unreal Engine のテクスチャ形式のサポートと設定 \| Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/texture-format-support-and-settings-in-unreal-engine)

通常のテクスチャなら`MaxLODSize`が使用できますが、VirtualTextureには効きません。
VirtualTextureの場合は、`MaxLODSize_VT`を使用します。

また、UE5.6から`LODBias_VT`の設定も追加されているようです。
描画時のLODBiasの設定なのでストレージ容量には関係ありませんが、描画負荷を下げたい場合に有効になるかもしれません。

`DefaultDeviceProfiles.ini`に下記のように追加してパッケージングされた際のテクスチャの容量を見てみます。
`MaxLODSize_VT`を2048にしています。
```
[GlobalDefaults DeviceProfile]
TextureLODGroups=(Group=TEXTUREGROUP_World,MinLODSize=1,MaxLODSize=16384,LODBias=0,MaxLODSize_VT=2048,MinMagFilter=aniso,MipFilter=point,MipGenSettings=TMGS_SimpleAverage)
```

結果は下図のようになりました。
Textureの容量が全体的に減っているのと、目立っていた`T_Metal_Painted_N`のサイズが劇的に減っているのがわかると思います。
![](https://storage.googleapis.com/zenn-user-upload/42fbede1c817-20251202.png)

パッケージングしてサイズ内訳を見てみて、全体をテクスチャが占めてしまっていてサイズを減らす必要があるといった時に取れる手段の1つだと思います。

## メモリ容量
### フォーマットごとのプールメモリ
デフォルトでは各フォーマット形式ごとに64MBのプールを使用しますが、この設定は変更することが出来ます。
プロジェクト設定内のVirtualTextureの項目の中から設定が行えます。
また、プールサイズは各フォーマット形式ごとに設定することが出来ます。
![](https://storage.googleapis.com/zenn-user-upload/1ca9d30ababc-20251202.png)

「各フォーマット形式ごとに」が若干罠で、シーン上で1枚しか使用していないフォーマットのテクスチャがあったとしても、プールメモリは確保されます。
そのため、設定ミスなどでBC3とBC7が混ざってしまったりするとBC3とBC7用のプールメモリが確保されます。
意図してそのようになっているなら問題ありませんが、意図せず設定されていたりすると、メモリを逆に圧迫することになってしまいます。
ミスに関しては、Validatorを作成して予防するのがいいでしょう。

実際にメモリプールが増えているのを確認してみたいと思います。
`/Game/StackOBot/Environment/Materials/Textures/T_ConcreteTileable_BC.T_ConcreteTileable_BC`のテクスチャの圧縮タイプをBC7にしてみます。
![](https://storage.googleapis.com/zenn-user-upload/c3aa0a5bbc3b-20251202.png)

コンソールコマンドの`r.VT.DumpPoolUsage`を実行した結果が下図です。
BC7のテクスチャが1枚だけいるのがわかります。
![](https://storage.googleapis.com/zenn-user-upload/dfde030fa8d6-20251202.png)

ではUnrealInsightsを見てみましょう。
さきほどと比較して、64MB確保しているプールテクスチャが増えているのがわかるかと思います。
![](https://storage.googleapis.com/zenn-user-upload/3e23b8a62ded-20251202.png)

### プールメモリのスケーリング
プールメモリはデバイスプロファイル等でコンソール変数でスケーリングさせることが出来ます。
`r.VT.PoolSizeScale`がその設定になります。
ただ、デフォルトだと0.1にしても0.5にしても効きません。
各フォーマットのプール設定を増やし、その中の`Allow Size Scale`をONにすることで、そのプールに対してスケールが効くようになります。
![](https://storage.googleapis.com/zenn-user-upload/8e21b4a05ab1-20251202.png)

そのため、スケーリングしたいプールの設定を行い、必要なプラットフォーム等のデバイスプロファイルで`r.VT.PoolSizeScale`を調整してください。

# まとめ
VirtualTexture、非常に便利です。
ただ、何も対策せずに使うとパッケージングサイズを増大させてしまったりメモリ負荷が意外と高かったりということがあります。
しっかり対策、検証、計測、対応を行って良いVirtualTextureライフを送りましょう。


