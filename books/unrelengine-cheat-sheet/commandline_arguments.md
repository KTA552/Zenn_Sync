---
title: "Command-Line Arguments"
---
# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |

# コマンドライン引数とは
UnrealEditorやゲーム実行時に追加することで挙動を制御したりオプションを追加出来るパラメータ。
公式ドキュメントは下記。
[Unreal Engine のコマンドライン引数 | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/command-line-arguments-in-unreal-engine)

# 使い方
## Editorの場合
下記のような使い方をします。
```
UnrealEditor.exe MyGame.uproject -オプション
```

自分の今の環境だと下記のようなコマンドになります。
UnrealEngineの場所やプロジェクトの場所は環境に応じて変更してください。
```
"C:\Program Files\Epic Games\UE_5.5\Engine\Binaries\Win64\UnrealEditor.exe" C:\Projects\UnrealProjects\Blank_Cpp\Blank_Cpp.uproject -オプション
```

## ゲーム実行ファイルの場合
下記のような使い方をします。
```
MyGame.exe -オプション
```
当然ながらShippingビルドやDevelopmentビルドで使用出来るパラメータは異なります。

# よく使う引数
## -FullCrashDumpAlways
Editorやゲーム実行時にクラッシュした際、フルダンプを出力するオプション。
ダンプファイルは`${ProjectDir}\Saved\Crashes`に出力されます。
サイズが非常に大きくなる（数十GBレベル）ので、クラッシュした際はある程度気長に待つ必要があります。
ダンプファイルを使ってのデバッグは下記記事が詳しい。
[\[UE4\] デバッグに関するTips - Qiita](https://qiita.com/donbutsu17/items/93dcf3c3638cd603976f)

## -WaitForDebugger
アプリケーションが起動する際、デバッガからのアタッチを待ってから起動してくれます。
初期化時に何か不具合が起きているが、起動からのアタッチではもう処理が通過している場合などで便利。
アタッチはVisualStudioやRider等のIDEから行いましょう。

## -AttachRenderDoc
RenderDocのアタッチを有効にする。
引数から行わないとProjectSettingsのiniファイルを書き換えることになるので、引数から行うのがベター。
RenderDocについては下記。
[Unreal Engine で RenderDoc を使用する | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/using-renderdoc-with-unreal-engine)
[アーティストの為のプロファイル入門！~楽しいRenderDocの使い方~【出張ヒストリア！ ゲーム開発勉強会 2019】 \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/59GRJK-UE4_HistoriaCaravan19_RenderDoc)
[Unreal Engine 5 における レンダリング & デバッグTips \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/5Q8Q67-2023-12-21-185240#p149)

## -dx11
DirectX11で実行。
たまにDX12でだけ起きる描画不具合があるので問題切り分けやRenderDoc使用時に使う。

## -dx12
DirectX12で実行。

## -LLM
stat llmで使用するメモリトラッカーの有効化。

## -RenderOffScreen
よくは使わないがJenkinsから実行する際に使用する。
Jenkinsから実行する際にこれを付けないとゲームがクラッシュするため。

## -trace
UnrealInsightでトレースするチャンネルの指定。
MemoryInsightsを使用する際に指定。下記のような形。
```
UnrealEditor.exe MyGame.uproject -trace=default,memory
```
公式ドキュメントは下記。
[Unreal Engine の Memory Insights | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/memory-insights-in-unreal-engine)

# IDEからの引数の簡単な設定方法
## Rider
EzArgsプラグインを使うと起動時に引数としてパラメータを設定できます。

## VisualStudio
Visual Studio Tools for UnrealEngineをインストールして使いましょう。
[Visual Studio Tools for Unreal Engine をインストールする \| Microsoft Learn](https://learn.microsoft.com/ja-jp/visualstudio/gamedev/unreal/get-started/vs-tools-unreal-install)
[クイック スタート: Visual Studio Tools for Unreal Engine \| Microsoft Learn](https://learn.microsoft.com/ja-jp/visualstudio/gamedev/unreal/get-started/vs-tools-unreal-quickstart#command-line-argument-dropdown)
[Visual Studio Integration Tool](https://zenn.dev/posita33/books/ue5_starter_cpp_and_bp_001/viewer/chap_01_vs2022_integration_tool)


# 参考リンク
[Unreal Engine のコマンドライン引数 | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/command-line-arguments-in-unreal-engine)
[Unreal Engine Command\-Line Arguments Reference | Epic Developer Community](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-command-line-arguments-reference)
（2025/5/2時点では日本語のドキュメントはレイアウトが激しく崩れているので英語版が良い）
[Unreal Engine の Commandline Interface \- ushell \- International / 日本語 \(Japanese\) \- Epic Developer Community Forums](https://forums.unrealengine.com/t/unreal-engine-commandline-interface-ushell/1993246)