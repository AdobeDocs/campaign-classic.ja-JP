---
solution: Campaign Classic
product: campaign
title: SQL コードと JavaScript コード
description: SQL と JavaScript コードワークフローアクティビティの詳細を説明します
audience: workflow
content-type: reference
topic-tags: action-activities
translation-type: tm+mt
source-git-commit: 8bcfc8826a66517e6a648dbc57b681778718c33c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 76%

---


# SQL コードと JavaScript コード{#sql-code-and-javascript-code}

## SQL コード {#sql-code}

「**[!UICONTROL SQL コード]**」アクティビティは、SQL スクリプトを実行します。スクリプトは、JST テンプレートです。

![](assets/sql_code.png)

* **[!UICONTROL スクリプト]**

   エディターの中央部に、実行されるスクリプトが含まれています。このスクリプトは、JST テンプレートであり、ワークフローのコンテキストに応じて設定できます。

* **[!UICONTROL エラーを処理]**

   [エラーを処理](../../workflow/using/monitoring-workflow-execution.md#processing-errors)を参照してください。

## JavaScript コードと高度な JavaScript コード {#javascript-code}

**[!UICONTROL JavaScript コード]**&#x200B;と&#x200B;**[!UICONTROL 高度な JavaScript コード]**&#x200B;アクティビティは、ワークフローのコンテキストで JavaScript スクリプトを実行します。スクリプティングについて詳しくは、[JS のスクリプトとテンプレート](../../workflow/using/javascript-scripts-and-templates.md)の節を参照してください。

### 実行遅延{#exec-delay}

20.2リリース以降、**[!UICONTROL JavaScriptコード]**&#x200B;と&#x200B;**[!UICONTROL 高度なJavaScriptコード]**&#x200B;のアクティビティに実行遅延が追加されました。 デフォルトでは、実行フェーズは1時間を超えることはできません。 この遅延の後、エラーメッセージが表示されてプロセスが中止され、アクティビティの実行が失敗します。

この遅延は、これらのアクティビティーで利用可能な&#x200B;**[!UICONTROL 「]**&#x200B;後に実行を停止」フィールドで変更できます。

この制限を無視するには、値を&#x200B;**0**&#x200B;に設定する必要があります。

### JavaScript コード {#js-code-desc}

![](assets/javascript_code.png)

* **[!UICONTROL スクリプト]**：エディターの中央部に、実行されるスクリプトが含まれています。

* **[!UICONTROL プロセスエラー]**:「 [処理エラー](../../workflow/using/monitoring-workflow-execution.md#processing-errors)」を参照してください。

### 高度な JavaScript コード {#adv-js-code-desc}

![](assets/advanced_javascript_code.png)

* **[!UICONTROL 最初の呼び出し]**：エディターの最初のゾーンには、最初の呼び出し時に実行するスクリプトが含まれます。
* **[!UICONTROL 次の呼び出し]**：エディターの 2 番目のゾーンには、2 回目以降の呼び出し時に実行するスクリプトが含まれます。
* **[!UICONTROL トランジション]**：アクティビティの出力トランジションを複数定義できます。
* **[!UICONTROL スケジュール]**：「**[!UICONTROL スケジュール]**」タブでは、アクティビティをトリガーするタイミングをスケジュール設定できます。
