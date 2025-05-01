---
title: "Editor Preferences"
---
# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |

# Editor Preferencesとは
UnrealEngineのEditorの設定関係が行えるツールウィンドウ。
メニューバーの`Edit/Editor Preferences...`から起動できる。
環境ごとに設定が保存される。
設定は`${ProjectDir}\Saved\Config\WindowsEditor\EditorPerProjectUserSettings.ini`に大体保存される。
（プラグインによっては独自の.iniファイルを定義している場合もある）

# よく使う設定
## Editor上でのFPSとメモリ消費の表示
![](https://storage.googleapis.com/zenn-user-upload/093a8fc0d340-20250501.png)
`Perfomance/Editor Performance/Show Frame Rate and Memory`をONにすることで、Editorの右上にFPSとメモリ消費量が表示されるようになる。

## Editor上でのUIのスケール表示変更
![](https://storage.googleapis.com/zenn-user-upload/30a86ae06771-20250501.png)
`Appearance/User Interface/Application Scale`からEditorのUIのスケールを変更できる。
大きな4K以上のモニターに写しているが文字が小さい場合等に使用する。

## Assetを開く際のウインドウの挙動の設定
![](https://storage.googleapis.com/zenn-user-upload/f435bfeaeb2c-20250501.png)
Blueprint等のアセットを開く際のウインドウを新しく開くか、タブを追加するか等の設定。

## ソースコードを開く際のIDEの設定
![](https://storage.googleapis.com/zenn-user-upload/6e0588669e96-20250501.png)
Blueprintノードをダブルクリックした際などにC++のコードが開かれますが、開くアプリケーションの設定。
VisualStudioを使っているならそのバージョンを、Riderを使っているならRiderを設定しましょう。

# 参考リンク
[Unreal Editor の環境設定 | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/unreal-editor-preferences)