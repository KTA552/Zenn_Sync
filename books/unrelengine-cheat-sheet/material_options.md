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
このページでは「聞かないと知らなかった」ぐらいのものをトピックとして取り上げます。
Tipsらしいですね。

# Parameter
## Use Material Attribute
[Unreal Engine でのマテリアル属性表現式 | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/material-attributes-expressions-in-unreal-engine)
マテリアルの出力にAttributeを使用する場合にONにします。
ONにすると出力がAttributeの形式になるので、`MakeMaterialAttributes`や`SetMaterialAttributes`でAttributeを作成します。
Attributeは`BreakMaterialAttributes`で分解することが出来ます。

## Has Pixel Animation
[Unreal Engine のテンポラル スーパー解像度 | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/temporal-super-resolution-in-unreal-engine#%E3%83%94%E3%82%AF%E3%82%BB%E3%83%AB%E3%82%A2%E3%83%8B%E3%83%A1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%82%92%E5%90%AB%E3%82%80%E3%83%9E%E3%83%86%E3%83%AA%E3%82%A2%E3%83%AB)
UnrealEngineのTSRを使用する場合は様々な情報をTSRに渡してアンチエイリアス処理を行ってもらいますが、重要な情報にVelocityがあります。
UVスクロールを行うようなマテリアルの場合、その情報の差分がVelocityとして出力されないため、激しいゴーストが発生します。
HasPixelAnimationをONにするとTSRでアンチエイリアス処理をある程度スキップするため、ゴーストが軽減されます。（なくなる訳ではないことに注意）

![](https://storage.googleapis.com/zenn-user-upload/9a41892f1df8-20250504.png)
横方向にUVスクロールしている際のON/OFFのサンプル。
上のPlaneのマテリアルはON、下のPlaneのマテリアルはOFFです。
静止画でもゴーストが起きているのがわかり、軽減されているのがわかると思います。

## Output Depth and Velocity
半透明マテリアル(Translucency)にした際に変更が可能になります。
半透明マテリアルはDepthやVelocityを描画しないのですが、HasPixelAnimationと同様にゴーストが出る場合があります。
その際、このオプションをONにすると軽減できる場合があります。
ただし、DepthとVelocityを描画する必要があるのでGPUの描画負荷は上がります。
描画結果の前後関係がおかしくなる可能性もあるので使用する際は注意を払いましょう。

## Allow Custom Depth Writes
半透明マテリアル(Translucency)にした際に変更が可能になります。
カスタムデプスを描画するかどうかのオプション。
カスタムデプスについては下記リンクを参考。
[UE4 CustomDepth についてのメモ \#UnrealEngine4 \- Qiita](https://qiita.com/unknown_ds/items/2137bd2cb03df6e0bbd1)
[Custom Depth Stencil Valueで複数ポストプロセスを使い分ける \| TECH ART ONLINE](https://tech-art.online/ue-custom-depth-stencil-value/)
[Using Custom Stencil to Selectively Bypass Postprocessing \| Epic Developer Community](https://dev.epicgames.com/community/learning/tutorials/LEKn/unreal-engine-using-custom-stencil-to-selectively-bypass-postprocessing)

## Parameter Group Data
マテリアル内でパラメータとして設定したオブジェクトのグループのソート順番を設定出来ます。

## Output Alpha
ポストプロセスマテリアルにした場合に変更が可能になります。
ポストプロセスマテリアルのEmissiveColorのアルファを書き込むかどうかのオプションです。
あらかじめ`ProjectSettings/Engine - Rendering/Alpha Output`をONにする必要があります。

## Compatible With Light Function Atlas
[Unreal Engine のライト関数を使用する | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/using-light-functions-in-unreal-engine)
マテリアルをライトファンクションとして使用するとファンクション内でマテリアルが使用出来ます。
`ProjectSettings/Engine - Rendering/Light Function Atlas Format`を8bits RGB Colorに設定するとマテリアルの色情報がライトファンクションに反映されます。
この際、マテリアルなのでテクスチャが使用出来るのですが**UV計算が出来ません。**
（UV計算をすると色情報が反映されない）
UV計算を有効にするにはこのオプションをONにする必要があります。
UV計算を行わなければ特に問題はありません。

![](https://storage.googleapis.com/zenn-user-upload/b88065ebaa8c-20250504.png)
UV計算をしているマテリアルで、左がON、右がOFFにした結果です。

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

- ShaderPlatformInfo Switch
- Feature Level Switch
- Quality Switch
- Shader Stage Switch
- Nanite Pass Switch
- Reflection Capture Pass Switch
- Shadow Pass Switch
- Shader Stage Switch
- Shading Pass Switch
- PathTracingQualitySwitchReplace
- PathTracingRayTypeSwitch
- VirtualTextureFeatureSwitch

画像のコメントによるカテゴリ分けは個人の主観です。
使用例は下記リンクを参考にしてみてください。
[UE5\.1 アップデート ~ Rendering / Effect ~ \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/Z84G15-UE5_1_Rendering%20_Effect?ref=rss#p45)
[マルチデバイス対応 UEFN\.Tokyo\#1 \| ドクセル](https://www.docswell.com/s/Taiki/5JLWGV-uefn.tokyo_1.taiki)
[キャラを透過なんかさせなくても良いんじゃね？ \#UnrealEngine \- Qiita](https://qiita.com/dgtanaka/items/02d4a85c70651ac49991)

# MaterialEditor
## PreviewSceneSettings
`Window/Preivew Scene Settings`を選択するとタブが開きます。
マテリアルエディターの左上のプレビュー画面のカスタマイズが行えます。
PostProcessMaterialの追加も行えるので、「ゲーム内で必ず掛けるPostProcessがある」といった場合に便利。

# 参考リンク
[Unreal Engine Materials | Epic Developer Community](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials)
