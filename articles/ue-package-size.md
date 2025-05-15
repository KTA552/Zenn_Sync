---
title: "[UE5] パッケージの中のアセットのサイズ内訳を確認する方法"
emoji: "📦"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [UnrealEngine, "UE5"]
published: true
---

# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |


# 概要
パッケージングしたけど、なんかサイズが大きい！
何が原因で大きくなっちゃってるのかわからない！といった場合にパッケージの内訳を確認する方法です。

実際にはここからプラットフォーム毎の圧縮なのかOodleの圧縮が入るのかちょっとサイズは異なりますが、
中身の把握には十分役に立つと思います。

# やり方
UnrealEngine5.1から入ったらしい`AssetSizeQuery`コマンドレットを使います。

## ProjectSettings
![](https://storage.googleapis.com/zenn-user-upload/716922dcd6c0-20250502.png)
`ProjectSettings/Packaging/Write Back Metadata to Asset Registry`をOriginal Fileにします。
プロジェクト設定のiniファイルが書き換わるので戻し忘れに注意してください。
もしくはコマンドラインでビルド時にiniを書き換えるようにしてください。
参考 : [Cook And Package Options｜Unreal Engine Cheat Sheet](https://zenn.dev/kta552/books/unrelengine-cheat-sheet/viewer/content_cook_and_package_options#-ini%3A)

## Stageビルド
通常通りStageビルドを行います。
Editorからでも問題ないですが、コマンドからは下記のように実行します。
`-project`には適切なプロジェクトのパスを設定してください。
```
.\Engine\Build\BatchFiles\RunUAT.bat BuildCookRun -project="C:\Projects\UnrealProjects\Blank_Cpp\Blank_Cpp.uproject" -clientconfig=Development -platform=Win64 -cook -build -stage -iostore -pak
```

ビルド後、下記の場所に`DevelopmentAssetRegistry.bin`ファイルが出来ているはずです。
```
${ProjectDir}/Saved/Coocked/Win64/${ProjectName}/MetaDeta/DevelopmentAssetRegistry.bin
```

## CSV出力
下準備は終わったので実際にデータを出力します。
下記のようなコマンドをUnrealEditor-Cmd.exeにオプションを付けて実行してください。
```
.\Engine\Binaries\Win64\UnrealEditor-cmd.exe -run=AssetSizeQuery -AssetRegistry="C:\Projects\UnrealProjects\Blank_Cpp\Saved\Cooked\Windows\Blank_Cpp\Metadata\DevelopmentAssetRegistry.bin" -CSV="C:\Projects\UnrealProjects\Blank_Cpp\Saved\AssetSize.csv" -CSVType=Assets
```

`-AssetRegistry`に先ほどStageビルドした際に作成されたAssetRegistry.binを指定。
`-CSV`にはCSVの出力先を指定。
`-CSVType`にはAssetsを指定。またはClassesを指定。用途によって使い分けましょう。

ログに全体の概要が出力され、-CSVで指定したパスにCSVファイルが出力されます。
![](https://storage.googleapis.com/zenn-user-upload/309df574ee84-20250502.png)
CSVにはアセット単位のサイズが出力されているので、具体的に何のアセットがどれくらいのサイズになっているかわかると思います。
![](https://storage.googleapis.com/zenn-user-upload/07b38671d229-20250502.png)

## Editorでの確認方法
UE5.4から`DevelopmentAssetRegistry.bin`の情報を表示出来るツールが実装されているので、そちらでも確認できます。
![](https://storage.googleapis.com/zenn-user-upload/4d596f5be68a-20250515.png)
メニューバーの`Tools/Audit/Asset Disk Size1`を選択します。(1でも2でも機能は一緒みたいなのでどちらでもいいです)

![](https://storage.googleapis.com/zenn-user-upload/a1134d29b7e0-20250515.png)
パッケージかStageビルドした際に出力した`DevelopmentAssetRegistry.bin`を選択して開きます。
ツールを開いたときにダイアログが出ますが、デフォルトでは`.ucookmeta`を開くようになっているので切り替えましょう。

![](https://storage.googleapis.com/zenn-user-upload/76c756c0dbac-20250515.png)
ファイルを開いた後、アセットのタイプ毎にグループ表示を切り替えればパッケージ内のアセットの内訳が表示されます。






# 参考リンク
[Unreal Engine 5\.1 リリース ノート \| Unreal Engine 5\.1 ドキュメンテーション \| Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/unreal-engine-5.1-release-notes?application_version=5.1)
[[UE4] シングルパックファイル内のアセットリストを取得する #UnrealEngine - Qiita](https://qiita.com/donbutsu17/items/c0efe626f232652dd248)
[Unreal Engine 5\.4 リリース ノート \| Unreal Engine 5\.4 ドキュメンテーション \| Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/unreal-engine-5.4-release-notes?application_version=5.4#editor)