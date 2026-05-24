---
title: "[UE5] ダサく見えないEUWのツールを作るために気を付けていること"
emoji: "🎛️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [UnrealEngine, "UE5"]
published: false
---

# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.7.4            |
| OS           | Windows11   |
| Platform | Windows |

# 概要
色んな効率化をするためにEditorUtilityWidgetでツールを作る、というのをよくやります。
その時に「なんか見た目がダサくて使いにくい」ツールにしないようにそこそこ気を付けているポイントがいくつかあります。
そのポイントの共有をする記事です。

# 作ったサンプル
![](/images/ue-smarteuw-how-to-article/smart-euw-sample00.png)

想定してるのはありがちな「何かしらのアセットを選択して、オプションを何か選択して実行するツール」です。
