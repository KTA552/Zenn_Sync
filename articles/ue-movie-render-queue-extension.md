---
title: "[UE5] MovieRenderQueueのSettingsに独自の設定を追加する方法"
emoji: "🎬"
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

# MovieRenderQueueとは
シーケンサーから動画や連番画像を出力できるようにするプラグインです。
デフォルトではONになっていないので、プラグインから`Movie Render Queue`を検索してONにしましょう。
（再起動が必要）
![](https://storage.googleapis.com/zenn-user-upload/7a29683c1234-20250503.png)

公式ドキュメントは下記。
[Unreal Engine でムービー レンダー キューを使用して高品質なレンダリングを行う方法 | Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/rendering-high-quality-frames-with-movie-render-queue-in-unreal-engine)

## Settingsとは
![](https://storage.googleapis.com/zenn-user-upload/50f0f5c57705-20250503.png)
MovieRenderQueueからレンダリング設定を行うとき、アンチエイリアスやコンソール変数、出力する画像の形式等の設定が行えます。
（画像の赤枠で囲んだ部分）
デフォルトではエンジンが用意した機能だけ存在していますが、ここに独自の機能を追加することが出来ます。

# やり方
## Settingsの場合
あまり難しいことはなく、MovieRenderQueue側が提供している基底クラスを継承して、関数をOverrideすれば済みます。
ただしC++が必要になります。

追加するプラグインかゲームのBuild.csに`MovieRenderPipelineCore`のモジュールを追加します。
```
PublicDependencyModuleNames.AddRange(
new string[]
    {
        "Core", 
        "MovieRenderPipelineCore",
        // ... add other public dependencies that you statically link with here ...
    }
);
```

下記クラスのように`UMoviePipelineSetting`を継承したクラスを作成し、`IsValidOnShots`か`IsValidOnPrimary`でtrueを返すようにしてください。
`SetupForPipelineImpl`がレンダリング開始時に呼ばれるので拡張したい機能を実装すればOKです。

https://github.com/KTA552/UE-MRQ_Extensions/blob/main/Source/MRQ_Extensions/Public/MyMRQSetting.h
https://github.com/KTA552/UE-MRQ_Extensions/blob/main/Source/MRQ_Extensions/Private/MyMRQSetting.cpp

## 結果
![](https://storage.googleapis.com/zenn-user-upload/77d965c2f73c-20250503.png =300x)
Settingsの中に独自に追加したSettingが追加されます。

![](https://storage.googleapis.com/zenn-user-upload/c834269653de-20250503.png)
追加した結果。UPROPERTYが付いたプロパティはちゃんとパラメータとして追加されます。

# サンプルプロジェクト
プラグインとして実装していますが、プロジェクトの中に入れるのが面倒なのでプラグインにしてあります。
実際に実装する際は、プロジェクトの中のソースコードに直接追加しても問題ありません。
https://github.com/KTA552/UE-MRQ_Extensions


# 参考リンク
[【初心者向け】UE5 シーケンサーと Movie Render Queue の使い方【Cinematic Dive 2023】 \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/Z7V32W-cinematicdive-epic)
[\[UE4\] 映像向け機能 Movie Render Queue について \#UnrealEngine \- Qiita](https://qiita.com/EGJ-Syuya_Mukai/items/8af5b80f250d93299e54)