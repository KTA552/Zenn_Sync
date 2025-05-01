---
title: "Stat Commands"
---
# 記事執筆時環境

| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |

# Stat Commandとは
実行している環境の統計情報(statistics)を画面に表示するためのデバッグコマンド（コンソールコマンド）です。
`stat xxx`と実行することが多いのでstat commandと呼びます。

公式ドキュメントは下記リンク。
[Unreal Engine の Stat コマンド | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/stat-commands-in-unreal-engine)

# 実行方法
日本語配列のキーボードならビューポート上で`@`キーを押すことでデバッグコマンド入力欄が出てきます。
英語配列なら全角/半角切り替えキーを押すことでデバッグコマンド入力欄が出ます。（だったはず）
また、OutputLogの`Enter Console Command`と表示されているエリアに打つことでも実行できます。

Project Settingsの`Engine/Input/Console/ConsoleKey`からキーを変更したり追加することも出来ます。

# よく使用するコマンド
一覧とその概要は公式ドキュメントを見てください。
実際によく使用するコマンドを列挙します。

## Stat FPS
![](https://storage.googleapis.com/zenn-user-upload/42770b779e58-20250501.png)
画面右上にFPSの表示
## Stat Unit, Stat UnitGraph
![](https://storage.googleapis.com/zenn-user-upload/42770b779e58-20250501.png)
画面右上に全体のフレーム時間、ゲームスレッド、GPU負荷、メモリ等の表示。
UnitGraphの場合は画面左下にグラフが表示される。
## Stat Engine
![](https://storage.googleapis.com/zenn-user-upload/765f4447d67f-20250501.png)
エンジン内の全体的なレンダリング関係のstat
Counters内の`StaticMeshTris`でStaticMeshで描画しているポリゴン数が見える。

## Stat Game
![](https://storage.googleapis.com/zenn-user-upload/2d2b970d463f-20250501.png)
ゲーム内のCPUの全体的な負荷情報が見える。
詳細を見たいときはUnrealInsightsを使うのが良い。

## Stat GPU
![](https://storage.googleapis.com/zenn-user-upload/f1c9f3d5d036-20250501.png)
ゲーム内のGPUの全体的な負荷情報が見える。
もう少し詳細を見たい際は`ProfileGPU`かUnrealInsightsを使用するのが良い。

## Stat Memory
![](https://storage.googleapis.com/zenn-user-upload/6257b9cd68de-20250501.png)
ゲーム内のメモリの全体的な消費量が見える。
ここで表示されている消費量が物理メモリの消費量とは一致しない点に注意。

## Stat LLM
![](https://storage.googleapis.com/zenn-user-upload/62232327d56c-20250501.png)
各カテゴリ（LLM Tag）毎のメモリ消費量が見える。

## Stat RHI
![](https://storage.googleapis.com/zenn-user-upload/9e505b5fa81e-20250501.png)
RHI（UnrealEngine内のグラフィックシステム）のメモリやパフォーマンス情報が見える。

## Stat SceneRendering
![](https://storage.googleapis.com/zenn-user-upload/4df1975c10a6-20250501.png)
今のシーンレンダリング情報が見える。
`stat initviews`と併用することが多いかもしれない。


# 参考リンク集
[Unreal Engine Console Commands Reference | Epic Developer Community](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-console-commands-reference)
[\[UE4\] コンソールコマンドの使い方＆よく使うコマンド一覧｜株式会社ヒストリア](https://historia.co.jp/archives/1342/)
[\[UE4\] Statコマンドに情報を追加しよう｜株式会社ヒストリア](https://historia.co.jp/archives/14778/)
[Unreal Engine \- プロファイリング＆最適化の始め方 \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/ZJDQ1Z-UE_profiling_and_optimization)
[UE5でプロファイリングを行う 〜CPU編〜 \- 電通総研 テックブログ](https://tech.dentsusoken.com/entry/ue5_profile_cpu)
[UE5でプロファイリングを行う 〜GPU編〜 \- 電通総研 テックブログ](https://tech.dentsusoken.com/entry/ue5_profile_gpu)