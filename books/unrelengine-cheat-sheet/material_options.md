---
title: "Material Options"
---
# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |

# マテリアルとは
翻訳すると「材質」なんですが、その名の通り描画するオブジェクトの材質を示します。
描画するオブジェクトにはほぼ全てマテリアルが割り当てられるため、StaticMesh, Skeletal, UI, PostProcess等で同じ「マテリアル」を使用します。
公式ドキュメントは下記。
[Unreal Engine のマテリアル | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/unreal-engine-materials)

マテリアルの機能が巨大になってるため「実はオプションとして存在してました」な機能もあります。
このページでは「基本的には使わないけど困った時にオプションとして使うこともある」ぐらいのものをトピックとして取り上げます。
Tipsらしいですね。

# Parameter

# Node
## Start Previewing Node
ノードではないんですが、知らないと使わないのでここに。
MaterialEditorの左上にはマテリアルの描画結果が表示されていますが、ここに表示するノードを指定出来ます。
具体的にはプレビューしたいノードを右クリック→Start Previewing Nodeを選択。
そのノードの描画結果が画面左上のプレビューに反映されます。

## Named Reroute Node
![](https://storage.googleapis.com/zenn-user-upload/e6ed905423a2-20250503.png =400x)
![](https://storage.googleapis.com/zenn-user-upload/5c53cb828442-20250503.png)
マテリアル内のノードからの出力を一時変数に出来ます。

## Switch
![](https://storage.googleapis.com/zenn-user-upload/5269d88931d2-20250503.gif)
引数を配列として見て、SwitchValueでその配列のインデックスを指定して出力を変えます。
詳しくは下記リンクを参考にしてください。
[\[UE5\] 新規追加されたマテリアルノード「Switch」｜株式会社ヒストリア](https://historia.co.jp/archives/34433/)

## XXX Switch
![](https://storage.googleapis.com/zenn-user-upload/67f82a1d1dd6-20250503.png)
マテリアル内でプラットフォームやクォリティ、描画パスに応じて処理を分けるために使用します。
気付いたら増えてました。
画像のコメントによるカテゴリ分けは個人の主観です。
使用例は下記リンクを参考にしてみてください。
[UE5\.1 アップデート ~ Rendering / Effect ~ \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/Z84G15-UE5_1_Rendering%20_Effect?ref=rss#p45)
[マルチデバイス対応 UEFN\.Tokyo\#1 \| ドクセル](https://www.docswell.com/s/Taiki/5JLWGV-uefn.tokyo_1.taiki)
[キャラを透過なんかさせなくても良いんじゃね？ \#UnrealEngine \- Qiita](https://qiita.com/dgtanaka/items/02d4a85c70651ac49991)

# MaterialEditor
## PreviewSceneSettings

# 参考リンク
