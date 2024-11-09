---
title: "[UE5] SubSystemを使いつつ、Blueprint側でロジックを実装する"
emoji: "🔧"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [UnrealEngine, "UE5"]
published: true
---

# 概要
UnrealEngineのSubSystemを使いつつ、細かいロジック等はBlueprint側で実装するための（多分）最短の方法を書いたものです。

# 環境

| 環境       | バージョン | 備考       |
|------------|------------|------------|
| UnrealEngine | 5.4.4     ||
| OS         | Windows 11 ||
| 開発ツール   | Rider 2024.1.4 | コンパイラはVisualStudio 2022だと思う|

# C++コード側
C++のコード側は極力シンプルにしたつもりです。
名前はあまりイケてないので適当なものに変更してください。
`BLANK_CPP_API`とclassの横についているのはプロジェクトの名前です。これも適当に変更してください。
（なくても動くとは思います）

``` C++:SubSystemTest.h
#pragma once

#include "CoreMinimal.h"
#include "Subsystems/GameInstanceSubsystem.h"
#include "SubSystemTest.generated.h"

// BP側のヘルパークラス
UCLASS(Blueprintable, meta = (ShowWorldContextPin))
class BLANK_CPP_API UCallBlueprintTest : public UObject
{
	GENERATED_BODY()

public:
	// BP側で実装する関数
	UFUNCTION(BlueprintImplementableEvent, BlueprintCallable)
	void PrintOnlyTest();
};

// 追加するSubSystem
UCLASS()
class BLANK_CPP_API USubSystemTest : public UGameInstanceSubsystem
{
	GENERATED_BODY()
public:
	UPROPERTY(BlueprintReadWrite, Transient, Category = "SubSystemTest")
	UCallBlueprintTest* SubSystemTestHelper;
};
```

.cpp側は実装の中身が無くて良いので下記で十分です
``` C++:SubSystemTest.cpp
#include "SubSystemTest.h"
```

# Blueprint側
ロジック側をBlueprint側で管理するので、こっちがちょっと手間が多いです。

## SubSystemで使用する関数の実装
`UCallBlueprintTest`を継承したBlueprintクラスを作成し、`PrintOnlyTest`関数をOverrideします。

下図のようなBlueprintになります。
![](https://storage.googleapis.com/zenn-user-upload/00eb5e2113b6-20241109.png)

## SubSystem内のヘルパーのプロパティを作成
GameModeやレベルブループリント等のゲームのシステム寄りなところでヘルパークラスを作成してSubSystemに渡してあげます。
今回はBP_CustomGameModeというBlueprintを作成し、その中でヘルパークラスを作成してSubSystemに渡しました。
下図のようなBlueprintになります。
![](https://storage.googleapis.com/zenn-user-upload/568ab608ed70-20241109.png)

## ゲーム内で実装した関数を呼び出す
作成したヘルパークラスを通じて`PrintOnlyTest`関数を呼び出してあげます。
とりあえずActorのTickでTick毎に呼び出してみました。

下図のようなBlueprintになります。
![](https://storage.googleapis.com/zenn-user-upload/36b751093b57-20241109.png)

## 実行結果
実行するとTick毎にPrintStringが呼ばれるので下図のようになります。
![](https://storage.googleapis.com/zenn-user-upload/ff46f866ff3f-20241109.gif)

# まとめ
システム的な呼び出し口はC++, 実際の実行するロジックはBlueprint側に分けるといったことが可能だというのが今回の記事で出来るのがわかると思います。
今回はC++側でGameInstanceSubsystemを使用しましたが、使いたいライフサイクルによって使い分けるのが良いでしょう。

# 参考資料
- [猫でも分かるUE4\.22から入ったSubsystem【第4回 UE4何でも勉強会 in 東京 2020】 \| ドクセル](https://www.docswell.com/s/EpicGamesJapan/KY18EZ-UE4_AllStudy04_Subsystem)
- [【UE5】Subsystem（サブシステム）を使ってみよう！ \- main\(\) blog](https://www.main-function.com/entry/2024/06/29/085923)
- [今更触るSubSystem（ｃ＋＋初心者向け） \#C\+\+ \- Qiita](https://qiita.com/tukigaselio/items/7641ac38aabb9996963d)
- [\[UE5\]GameInstanceSubsystemを導入してみた](https://zenn.dev/pate_techmemo/articles/673138c94a494e)
- [Unreal Engine のプログラミング サブシステム \| Unreal Engine 5\.5 ドキュメンテーション \| Epic Developer Community \| Epic Developer Community](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/programming-subsystems-in-unreal-engine)