---
title: "[UE5] UE5.6以降のProfileGPU, GPU Insightsの使い方"
emoji: "📊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [UnrealEngine, "UE5"]
published: true
---

# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.6.0            |
| OS           | Windows11   |
| Platform | Windows |

# はじめに
ReleaseNoteやProductBoardでも周知されているように、UE5.6からProfileGPUコマンドの挙動が変わりました。
ProfileGPUの挙動が変わったというよりは、GPUプロファイリングの方法が少し変わったと言った方が正しいかもしれません。
どんなことが変わったのか、何を見るべきなのかを紹介したいと思います。

# 検証シーン
LyraのPerformance Test Mapのマップで実行しています。
![](https://storage.googleapis.com/zenn-user-upload/f4ea6636b513-20250628.png)

# ProfileGPU
ConsoleCommandで"ProfileGPU"を実行します。

## 5.5以前のProfileGPU
OutputLogにTreeでフレーム内のGPU負荷、Editorの場合GPU Visualizerが表示されます。
![](https://storage.googleapis.com/zenn-user-upload/be68442ea0e2-20250628.png)
![](https://storage.googleapis.com/zenn-user-upload/b717a09f3059-20250628.png)

## 5.6のProfileGPU
OutputLogに表になってフレーム内のGPU負荷が表示されます。
注目すべきは表がわかれているところでしょうか。
恐らくGPU内で並列処理されている部分(Compute)と、メインのGPUで動作している部分(Graphics)で分かれていると思います。
「どっちを見ればいいか」ではなく「どちらも見た上で」、総合的にGPU負荷のボトルネックを探す形になると思います。
![](https://storage.googleapis.com/zenn-user-upload/0e88e337f3d8-20250628.png)

ちなみにr.ShowMaterialDrawEventsをONにすると下図のような出力になるので、今まで通りマテリアル単位での表示というのも出来ています。
![](https://storage.googleapis.com/zenn-user-upload/29c32334e49f-20250628.png)

# Stat GPU
ConsoleCommandで"Stat GPU"を実行します

## 5.5以前のStat GPU
"STATGROUP_GPU"という1つのカテゴリでGPUの負荷が表示されます
![](https://storage.googleapis.com/zenn-user-upload/ec7d7e8086fc-20250628.png)

## 5.6のStat GPU
ProfileGPUと同じように、GraphicsとComputeのカテゴリに分かれて表示がされます。
![](https://storage.googleapis.com/zenn-user-upload/3aa675d93f4e-20250628.png)


# Unreal Insights
Editorの下部メニューにあるボタンからトレースを開始するか、"Trace.Start", "Trace.Stop"コマンドを実行します。
その後、UnrealInsightsのSessionBrowser内から保存されたトレース情報を開きます。

## 5.5のGPU Insights
GPUの負荷の内訳とどんな順番で実行されているかが確認できます。
![](https://storage.googleapis.com/zenn-user-upload/8869dee87cf5-20250628.png)

## 5.6のGPU Insights
ProfileGPUと同じように、GraphicsとComputeで分かれてInsights内で表示が行われます。
かなり情報量が増えました。
![](https://storage.googleapis.com/zenn-user-upload/3fcbd0546720-20250628.png)

この際、負荷を表示している項目をクリックすると、その項目が何に依存して処理されているかの矢印が表示されます。
「Graphics側の負荷を下げたけど、全体の負荷が下がらない」といった時、依存してる側が実はボトルネックになってしまっていて、それを待っているということがあるかもしれません。
![](https://storage.googleapis.com/zenn-user-upload/5d7aa674124b-20250628.png)

# まとめ
UE5.6以降で変わったProfileGPU, Stat GPU, GPU Insightsの紹介をしました。
GPUは並列で処理されているものが多く、UE5.5までだと1つのカテゴリ内で負荷を表示していましたが、
その中以外で負荷として計上すべきものが多くなったため、5.6で並列処理しているものも表示されるようになったように思います。

ProfileGPUの紹介の中で触れましたが、総合的に見てボトルネックを探して負荷軽減をしていけるようにしましょう。

