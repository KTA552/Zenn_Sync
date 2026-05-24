---
title: "[UE5] ある程度ダサく見えないEUWのツールを作るために気を付けていること"
emoji: "🎛️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [UnrealEngine, "UE5"]
published: true
---

# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.7.4            |
| OS           | Windows11   |
| Platform | Windows |

# 概要
色んな効率化をするためにEditorUtilityWidgetでツールを作るというのをよくやります。
その時に「なんか見た目がダサくて使いにくい」ツールにしないようにそこそこ気を付けているポイントがいくつかあります。
そのポイントの共有をする記事です。

# 作ったサンプル
想定してるのはありがちな「何かしらのアセットを選択して、オプションを何か選択して実行するツール」です。
https://github.com/KTA552/UE-SmartEUW-Sample

## 実行時
![](/images/ue-smarteuw-how-to-article/smart-euw-sample00.png)
## ヒエラルキー
![](/images/ue-smarteuw-how-to-article/smart-euw-sample01.png)


# 気を付けているポイント
## 1. ウインドウが縮小して要素がはみ出した時にスクロール出来るようにする
デフォルトで入ってないですが、わりと重要です。
対応はEditorUtilityScrollBoxを入れてSizeをFillにするだけです。

![](/images/ue-smarteuw-how-to-article/smart-euw-sample02.png)
ないとこうなります。「ウインドウを小さくするとツールが使えない」になり得るのでなかなかダサいです。

## 2. ボタンやテキストの配置はVerticalBoxやHorizontalBoxを使う
1のウインドウ縮小・拡大に関係あることですが、自由にボタン配置するとレイアウトは簡単に崩れます。
崩れないように設計すればいいですが、ツールのUIのレイアウトはローコストでいい感じになってくれるのがベストです。
なので、ある程度自動でレイアウトしてくれるVerticalBoxやHorizontalBoxを親にして、その下にボタンやテキストを配置するのが良いでしょう。

1,2を合わせると下図のようなヒエラルキーになります。
大体これでそれっぽいツールのレイアウトになっていきます。
![](/images/ue-smarteuw-how-to-article/smart-euw-sample03.png)

## 3. ツール上にパラメータを表示、調整するときはSinglePropertyViewやDetailViewを活用する
SpinBoxやCheckBoxを並べてパラメータ調整できるようにするのもありですが、
それはそれでHoizontalBox置いて子供にText配置、SpacerでPadding設定して、SpinBox置いて・・・というひと手間が発生します。
SinglePropertyViewやDetailViewを使用することで、UEデフォルトのUIレイアウトと操作感をユーザーに与えることが出来ます。

サンプル画像で言うとStaticMeshの設定とOptionsの項目がSinglePropertyViewとDetailViewで表示されています。

## 4. 実行した結果のログ表示
1~3まではほぼ必須でやっているものなのですが、これ以降は「こうしてるとちょっと便利に見える気がする」ものになります。

EUWを使う場合は「何かしらの処理をまとめて行う」のが大半だと思うのですが、その結果はOutputLogとツール上に出すと便利です。
OutputLogを常に出している人は少ないので、ツールが正常に動作したのかの確認だったり不具合が起きている場合の調査に役立ちます。

その際、表示はEditorUtilityMultiLineEditableTextにテキストを表示させて、IsReadOnlyをONにしています。
IsReadOnlyはONにしておかないとログ目的で表示しているテキストの編集が出来てしまいます。
また、EditorUtilityMultiLineEditableTextをBorderで囲っておくと「ログエリア」っぽさが出るのでオススメです。

BorderのDrawAsをBorderにして、Marginを0以上にしておくとテキストエリアを囲うBorderになります。
![](/images/ue-smarteuw-how-to-article/smart-euw-sample04.png)

## 5. ツール自体の名前とヘルプボタンの配置
「このツールは何をしてくれるツールなのか」という名前を付けてツールの先頭に表示します。
そのエリアの右端に使い方のドキュメントのページにジャンプさせるボタンを置いておきます。

ここはツールの名前表示よりもどちらかと言えばヘルプボタンの配置の方が重要だと思ってます。
ツールの使い方のドキュメントは大抵の場合用意すると思うのですが、ツールとリンクしてないと「使い方を知ってる人だけが使うツール」になります。
BPにLaunchURLというノードがあるので、ここにドキュメントのURLを記載しておくとボタンを押したときにブラウザが開いてURLにジャンプしてくれます。

# まとめ
EUWでツールを作っておくと便利機能をまとめられるので非常に便利です。
ただツールの見た目だったり使い心地がちょっと・・・だと使用頻度が低いツールになってしまうので、せっかく作ったのにもったいないということになりがちです。
紹介したポイントを押さえておくと、ある程度それらしい見た目になってくれるのでお勧めです。

# 宣伝
作成したEditorUtilityWidgetが増えた場合に立ち上げるのが面倒くさいと感じていて、EUWのショートカットを登録できるツールをFabで公開中です。
https://www.fab.com/listings/c9f87865-9670-4be0-a79f-6f28587e10f6

コードも公開してあります。
https://github.com/KTA552/UE-WidgetLauncher

# 参考
[EditorUtilityWidgetPetitDeepDive \| ドクセル](https://www.docswell.com/s/kinnaji/5P9NWL-euw-petit-deep-dive)
[【UE5】UE5版 EditorUtilityWidgetについてのあれこれ \| キンアジのブログ](https://kinnaji.com/2024/05/06/unreal-engine-meetup-connect-vol-2/)
[UE5：Editor Utilityを活用したツール制作術 \| CG・映像の専門情報サイト \| CGWORLD\.jp](https://cgworld.jp/regular/unreal_engine_5_editor_utility/)
[Editor Utility Widget & エディタ拡張 \| UE5攻略リンク](https://ue5study.com/unrealengine-editorutility/)














