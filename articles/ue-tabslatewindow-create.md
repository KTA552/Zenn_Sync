---
title: "[UE5] Tab付きSlateWindowの作成方法"
emoji: "🪟"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [UnrealEngine, "UE5"]
published: true
---

# 記事執筆時環境
| 項目              | バージョン       |
|-------------------|------------------|
| Unreal Engine     | 5.6.1            |
| OS           | Windows11   |
| Platform | Windows |

# 概要
SlateでWindowを作成する機会がたまにあります。
その中で機能ごとにTabを分けたいなと思うことが結構あります。
作り方はエンジンの他のツールがどう作られているかを見るのが一番実用的ではあるのですが、
正直そこまで見るのは結構しんどいので最もシンプルなサンプルを作成したので軽い解説をしていきます。

# 作ったもの
下図のようなほぼ何もないシンプルなウインドウです。
メニューバー想定のTextBoxとタブが2つ入っています。
![](https://storage.googleapis.com/zenn-user-upload/fcf8100574a3-20251005.png)

地味にウインドウレイアウトの復元も実装してあるので、タブのレイアウトを変えてウインドウを再起動してみてください。
終了時のレイアウトで立ち上がると思います。

# ソースコード
コードは下記で公開しています。
実行する際はプロジェクト内にPluginsフォルダを作成してその中にCloneしてビルドして実行してください。
https://github.com/KTA552/UE-SlateTabWindowSample

肝心なところは下記cpp内に入っているので、コードだけ見たい人はそちらを見てください。
https://github.com/KTA552/UE-SlateTabWindowSample/blob/main/Source/SlateTabWindowSample/Private/TabWindow.cpp

# Tab付きWindowを作る手順
## Windowを作成したTabからTabManagerを作成
ここはやり方他にあるかもですが、これが一番早いのでこの方法を取ってます。
ConstructにTabを渡して、そこからTabManagerを生成します。
https://github.com/KTA552/UE-SlateTabWindowSample/blob/12d1c77a4d5fd93497ec5ffe9d90256455baf4c0/Source/SlateTabWindowSample/Private/SlateTabWindowSample.cpp#L15-L16
https://github.com/KTA552/UE-SlateTabWindowSample/blob/12d1c77a4d5fd93497ec5ffe9d90256455baf4c0/Source/SlateTabWindowSample/Private/TabWindow.cpp#L9-L11

## ウインドウレイアウトの設定
TabManagerLayoutを作成して、その中をどうレイアウトするかの設定をします。
横並びにするか縦並びにするかもここで設定しておきます。
ここで作成しているStackにTabを追加していきます。
https://github.com/KTA552/UE-SlateTabWindowSample/blob/12d1c77a4d5fd93497ec5ffe9d90256455baf4c0/Source/SlateTabWindowSample/Private/TabWindow.cpp#L20-L21
https://github.com/KTA552/UE-SlateTabWindowSample/blob/12d1c77a4d5fd93497ec5ffe9d90256455baf4c0/Source/SlateTabWindowSample/Private/TabWindow.cpp#L38-L47

## タブの作成、設定
作成したレイアウトに対してTabを作成して登録します。
肝心なのは`TabManager->RegisterTabSpawner`と`Stack->AddTab`です。
Tabの登録、Tabの表示設定をここでします。

https://github.com/KTA552/UE-SlateTabWindowSample/blob/12d1c77a4d5fd93497ec5ffe9d90256455baf4c0/Source/SlateTabWindowSample/Private/TabWindow.cpp#L49-L59

## 子要素の設定
ウインドウの中に作りたい子要素を設定していきます。
大事なのは`TabManager->RestoreFrom`です。これでTabの中をまとめて登録します。
https://github.com/KTA552/UE-SlateTabWindowSample/blob/12d1c77a4d5fd93497ec5ffe9d90256455baf4c0/Source/SlateTabWindowSample/Private/TabWindow.cpp#L74-L107

## ウインドウレイアウト復元の設定
これはオマケです。
こうしたらウインドウレイアウトの保存、復元が出来ますよというサンプルです。
FLayoutSaveRestoreでコンフィグに保存しておいて、保存したレイアウトを復元してTabManagerLayoutを上書きします。
**やる場合、これをやってからRestoreFromを呼んでください。大事。**
https://github.com/KTA552/UE-SlateTabWindowSample/blob/12d1c77a4d5fd93497ec5ffe9d90256455baf4c0/Source/SlateTabWindowSample/Private/TabWindow.cpp#L13-L31
https://github.com/KTA552/UE-SlateTabWindowSample/blob/12d1c77a4d5fd93497ec5ffe9d90256455baf4c0/Source/SlateTabWindowSample/Private/TabWindow.cpp#L71-L72

# まとめ
Slate、取っ付きにくさは正直あるんですがある程度わかりはじめるとImmdiateGUI的な感じで機能を登録出来て便利です。
エンジンの機能を呼ぶにはC++が必要になる場面もあるので使うことはまぁまぁあるかなと思います。
ちょっとちゃんとしたツールの見た目にするにはタブがあるとそれっぽく見えるのでその作り方の紹介でした。
参考になれば幸いです。