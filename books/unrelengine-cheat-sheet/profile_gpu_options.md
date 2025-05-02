---
title: "ProfileGPU Options"
---
# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |

# ProfileGPUとは
GPUの負荷を調べるためのデバッグコマンド（コンソールコマンド）。
Stat GPUよりもより詳細な情報が見える。

# 使い方
`ProfileGPU`をデバッグコマンドで実行。
結果がログに表示される。Editorで実行した場合はGPU Visualizerでも表示される。

# オプション
## r.ProfileGPU.Sort
負荷が高い順にソート行う等のオプションが設定できる。
下記のようにすると実行時間によるソートが行われる。
```
r.ProfileGPU.Sort 1
```
## r.ProfileGPU.ThresholdPercent
出力する項目のしきい値の設定。
負荷が大きいものだけピックアップしたい際に使用。

## r.ShowMaterialDrawEvents
マテリアル単位での負荷を見たいときに使用。
全体の計測結果は上がってしまうので、詳細をプロファイルする際に使用。

# 参考リンク
[Unreal Engine \- プロファイリング＆最適化の始め方 \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/ZJDQ1Z-UE_profiling_and_optimization)
[UE5の最新グラフィクスを使いこなすためのN個の勘所 \| EGC2024 \(Yutaro Sawada & Nori Shinoyama\) \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/5ENRE6-EGC2024_NGraphicsTips)
[Unreal InsightsとProfileGPUから見るLumenとNanite ＋ 5\.4までのアップデート \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/K3G48Y-UnrealInsightsProfileGPULumenNanite)
[Unreal Engine の GPUDump ビューア ツール \| Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/gpudump-viewer-tool-in-unreal-engine)