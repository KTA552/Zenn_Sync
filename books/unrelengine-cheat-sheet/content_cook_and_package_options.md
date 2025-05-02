---
title: "Cook And Package Options"
---
# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |

# はじめに
Cookだったりパッケージングだったりの用語については公式ドキュメントを見てください。
[Unreal Engine でのゲームのパッケージングとクック | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/packaging-and-cooking-games-in-unreal-engine)

すごいざっくり言うとCookは各アセットを各プラットフォーム用のデータに再出力することで、
パッケージングは最終的に全てをまとめたexeを作ることです。

Cookしたデータを元にパッケージングを行うため、パッケージングを行うには前段階としてCookが必要です。

# Cook、パッケージングの方法
Editorが立ち上がっているならEditorから行うのが早いです。
![](https://storage.googleapis.com/zenn-user-upload/e24230320163-20250502.png)
Editor上部のメニューから`Platforms/${Platform}/CookContent or PackageProject`から行うのがいいでしょう。
このページではもう少し細かい制御が行えるコマンドラインからの実行方法について書きます。

# コマンドで行う
## 使い方

## オプション

# 参考リンク
