---
title: テスト
seo-title: テスト
description: テスト
seo-description: null
page-status-flag: never-activated
uuid: 3522f4ac-3a72-4ff1-b3aa-1b4c283ef2bd
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: flow-control-activities
discoiquuid: 78c70ef4-807d-45d4-ac87-2b741c0ef5cb
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: f7ed7e59be2cfbde467b0c80d21cfbf52016a2b8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 93%

---


# テスト{#test}

「**テスト**」タイプのアクティビティは、自身に関連付けられている条件を最初に満たしたトランジションを有効化します。条件が 1 つも満たされず、「**[!UICONTROL デフォルト分岐を使用]**」オプションが有効化されている場合、デフォルトのトランジションが有効化されます。

条件は、true または false によって必ず評価される JavaScript 式です。式を入力するには、条件名の右にあるアイコンをクリックし、「**[!UICONTROL 編集...]**」を選択します。

![](assets/edit_test.png)

ワークフロー JavaScript 経由でアクセス可能なアプリケーションサーバーのその他すべての JavaScript 関数および SOAP メソッドの詳細については、[JSAPI ドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)を参照してください。

このエディターから変数を直接挿入することもできます。For more  information on how to work with variables, refer to [this section](../../workflow/using/javascript-scripts-and-templates.md#variables).

条件は、アクティビティプロパティの編集ウィンドウから追加や削除、並べ替えるができますが、トランジションから編集することもできます。

計算結果を別の条件で再利用する場合、アクティビティの初期化スクリプトで再計算することも可能です。結果は、条件スクリプトによってアクセスされるタスクの変数（task.vars.xxx）に格納する必要があります。
