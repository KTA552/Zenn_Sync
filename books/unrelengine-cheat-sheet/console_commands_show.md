---
title: "Console Commands ~Show~"
---
# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.5.4            |
| OS           | Windows11   |
| Platform | Windows |

# コンソールコマンドとは
Stat Commandsの章でも触れましたが、実行中や実行時の挙動やパラメータを変更できるデバッグコマンドです。

# 実行方法
日本語配列のキーボードならビューポート上で`@`キーを押すことでデバッグコマンド入力欄が出てきます。
英語配列なら全角/半角切り替えキーを押すことでデバッグコマンド入力欄が出ます。（だったはず）
また、OutputLogの`Enter Console Command`と表示されているエリアに打つことでも実行できます。

Project Settingsの`Engine/Input/Console/ConsoleKey`からキーを変更したり追加することも出来ます。

# 公式のConsole Commands Reference
UnrealEngineのドキュメント内に公式リファレンスがあるので、そちらを見るのがいいでしょう。
[Unreal Engine Console Commands Reference | Epic Developer Community](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-console-commands-reference)

または、UnrealEditorのメニューバーの`Help/Console Variables`からプロジェクト内のコンソール変数一覧のページが作成できるのでそちらでも良いです。
プロジェクト内で追加されたコンソール変数も見られるためHelpから出力された一覧を使うことが多いです。

# Show Commands
コンソールコマンドは大量にあるため、画面内のオブジェクトを表示/非表示出来るShowコマンドに絞ってこのページでは紹介します。
Showコマンド自体も大量にあるため、よく使用するものだけピックアップします。
ちなみにコマンド自体は`ShowFlag.XXX`で登録されていますが、実際にコマンドで実行する際は`Show XXX`で使うことが多いです。
Editor上だと`ShowFlag.XXX`で実行できるんですが、ビューポート内の設定自体を変えてしまうので個人的にはあまり使わないです。（Editorの起動中その設定で見たい場合はOK）

| コマンド名            | 説明                     |
|-----------------------|--------------------------|
| Show SkeletalMeshes   | スケルタルメッシュを表示/非表示 |
| Show StaticMeshes     | スタティックメッシュを表示/非表示 |
| Show Bounds | Boundの表示/非表示　|
| Show Cloud | 雲(VolumetricCloud)の表示/非表示　|
| Show ContactShadows | コンタクトシャドウの表示/非表示　|
| Show Decals | デカールの表示/非表示　|
| Show DynamicShadows | DynamicShadowの表示/非表示　|
| Show Fog                   | フォグの表示/非表示       |
| Show GlobalIllumination    | グローバルイルミネーションの表示/非表示 |
| Show InstancedFoliage      | インスタンスフォリッジの表示/非表示 |
| Show InstancedGrass        | インスタンスグラスの表示/非表示 |
| Show InstancedStaticMeshes | インスタンススタティックメッシュの表示/非表示 |
| Show LandScape             | ランドスケープの表示/非表示 |
| Show LightFunctions        | ライトファンクションの表示/非表示   |
| Show Lighting              | ライティングの表示/非表示 |
| Show LumenReflections      | Lumenリフレクションの表示/非表示 |
| Show NaniteMeshes          | Naniteメッシュの表示/非表示 |
| Show NaniteStreamingGeometry | Naniteストリーミングジオメトリの表示/非表示 |
| Show Niagara               | Niagaraの表示/非表示   |
| Show OnScreenDebug         | オンスクリーンデバッグの表示/非表示 |
| Show Particles             | パーティクルの表示/非表示 |
| Show PointLights           | ポイントライトの表示/非表示 |
| Show PostProcessing        | ポストプロセッシングの表示/非表示 |
| Show PostProcessMaterial   | ポストプロセスマテリアルの表示/非表示 |
| Show ReflectionEnvironment | ReflectionEnvironment（リフレクションに使用する環境マップ）の表示/非表示。（Lumen以降使ったことはないかも）|
| Show ShadowFrustums        | シャドウフラスタムの表示/非表示 |
| Show SkyLighting           | スカイライティングの表示/非表示 |
| Show SpotLights            | スポットライトの表示/非表示 |
| Show Translucency          | トランスルーセントの表示/非表示 |
| Show VisualizeLumen        | ルーメンのVisualize（デバッグ表示）の表示/非表示 |
| Show VisualizeNanite       | ナナイトのVisualize（デバッグ表示）の表示/非表示 |
| Show VisualizeTSR          | TSRのVisualize（デバッグ表示）の表示/非表示  |
| Show VolumetricFog         | ボリューメトリックフォグの表示/非表示 |
| Show WidgetComponents      | ウィジェットコンポーネントの表示/非表示 |

# Slate.GameLayer.XXX
Showコマンドとは違いますが、便利なのでこちらで紹介。
Widgetの表示/表示を一括で切り替えます。
- Slate.GameLayer.DebugCanvasVisible
- Slate.GameLayer.PlayerCanvasVisible
- Slate.GameLayer.ViewportSlotVisible
- Slate.GameLayer.AllCanvasesVisible

さらに具体的な説明は下記リンクを参考にしてください。
[\[UE5\] Canvasの表示切り替えコマンド \#UnrealEngine \- Qiita](https://qiita.com/EGJ-Ken_Kuwano/items/d9292fd211902c6cada4)