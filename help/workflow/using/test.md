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
source-git-commit: b78db689958c9b240da9a0315060fe63bcb48e0a

---


# テスト{#test}

「**テスト**」タイプのアクティビティは、自身に関連付けられている条件を最初に満たしたトランジションを有効化します。If no condition is satisfied and if the **[!UICONTROL Use the default fork]** option is activated, the default transition will be activated.

条件は、true または false によって必ず評価される JavaScript 式です。To enter the expression, click the icon to the right of the name of the condition, and then select **[!UICONTROL Edit...]**.

![](assets/edit_test.png)

ワークフロー JavaScript 経由でアクセス可能なアプリケーションサーバーのその他すべての JavaScript 関数および SOAP メソッドの詳細については、[JSAPI ドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)を参照してください。

このエディターから変数を直接挿入することもできます。

条件は、アクティビティプロパティの編集ウィンドウから追加や削除、並べ替えるができますが、トランジションから編集することもできます。

計算結果を別の条件で再利用する場合、アクティビティの初期化スクリプトで再計算することも可能です。結果は、条件スクリプトによってアクセスされるタスクの変数（task.vars.xxx）に格納する必要があります。
