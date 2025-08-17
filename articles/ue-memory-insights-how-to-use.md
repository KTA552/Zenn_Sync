---
title: "[UE5] Memory Insightsの使い方とアセット使用状況の表示方法"
emoji: "🪄"
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

# 概要

UnrealEngineでの負荷計測にはUnrealInsightsを使用するのが便利です。
CPUやGPUの方は語られることが多いのですが、今回はMemoryInsightsの使い方について少し触れたいと思います。
具体的にはシーン内で使用しているアセットのメモリ内訳の出し方がようやくわかったので共有したいというのがモチベーションです。

# 使い方

MemoryInsightsを使用するには、**起動時に**コマンドライン引数を与える必要があります。
MemoryInsightsを使用するだけの場合、下記パラメータを設定して実行します。
```
-tracefile -trace=default,memory
```

実行すると、`Saved/Profiling/`フォルダに.utraceファイルが生成されます。
この.utraceファイルをUnrealInsightsのSessionFrontendに読み込ませてトレース結果を確認します。
SessionFrontendはEditorの下部メニュー内から起動できます。
![](https://storage.googleapis.com/zenn-user-upload/54411bd26fd9-20250817.png =400x)

memoryトレースが有効になっていると、トレース結果が表示されるときにMemoryInsightsのタブが表示され、各カテゴリごとにどれぐらいメモリを消費しているかがわかります。
また、リークの検出にも便利です。
![](https://storage.googleapis.com/zenn-user-upload/c7656463615d-20250817.png =600x)

ただ、このままだとカテゴリごとのメモリ消費量はわかるのですが、「何のアセットが」「どれぐらい」メモリを取っているのかがわかりません。
下図はSkeletalMeshのTag内を表示しようとしたものです。
![](https://storage.googleapis.com/zenn-user-upload/551a17355a1b-20250817.png)

アセットの情報を取得するには、`metadata,assetmetadata`パラメータを追加する必要があります。
下記のようにします。
```
-tracefile -trace=default,memory,metadata,assetmetadata
```
こうすると、Invesigationの中の情報にAssetとPackageの情報が含まれるようになるのでカテゴライズすることが出来ます。
先ほどの図では情報がなかったSkeletalMeshの中の情報が見えるようになったのがわかるかと思います。
![](https://storage.googleapis.com/zenn-user-upload/70adffe084a7-20250817.png)

この情報を追っていけば、メモリ消費量が高いものやリークしてしまっているアセットの詳細情報まで掴むことが出来るはずです。

# 参考
[Unreal Engine の Memory Insights | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/memory-insights-in-unreal-engine)
[Unreal Insightsを使用したパフォーマンス分析と最適化マスタリー \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/ZQX8RN-2025-07-31-143312#p74)
[\[UE4\] Memory Insightsを使用したメモリトラッキング \#UnrealEngine4 \- Qiita](https://qiita.com/EGJ-Ken_Kuwano/items/83425f450f6da100a9d0)
[Memory insights and tracing with callstacks for Android \| Epic Developer Community](https://dev.epicgames.com/community/learning/tutorials/Zbkz/unreal-engine-memory-insights-and-tracing-with-callstacks-for-android)