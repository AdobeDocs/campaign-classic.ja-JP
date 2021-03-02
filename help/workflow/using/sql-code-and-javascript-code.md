---
solution: Campaign Classic
product: campaign
title: SQL コードと JavaScript コード
description: SQL と JavaScript コードワークフローアクティビティの詳細を説明します
audience: workflow
content-type: reference
topic-tags: action-activities
translation-type: tm+mt
source-git-commit: add0efb4efd5a37129c649b942799622947f3143
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 87%

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

### 実行遅延 {#exec-delay}

20.2 リリース以降、**[!UICONTROL JavaScript コード]**&#x200B;と&#x200B;**[!UICONTROL 高度な JavaScript コード]**&#x200B;のアクティビティに実行遅延が追加されました。 デフォルトでは、実行フェーズは 1 時間を超えることはできません。 この遅延の後、エラーメッセージが表示されてプロセスが中止され、アクティビティの実行が失敗します。

この遅延は、アクティビティの「**[!UICONTROL 次の時間後に実行を停止]**」フィールドで変更できます。

この制限を無視するには、値を **0** に設定する必要があります。

### JavaScript コード {#js-code-desc}

![](assets/javascript_code.png)

* **[!UICONTROL スクリプト]**：実行されるスクリプトがエディターの中央部に記述されています。

* **[!UICONTROL エラーを処理]**：[エラーの処理](../../workflow/using/monitoring-workflow-execution.md#processing-errors)を参照してください。

### 高度な JavaScript コード {#adv-js-code-desc}

![](assets/advanced_javascript_code.png)

* **[!UICONTROL 最初の呼び出し]**：エディターの最初のゾーンには、最初の呼び出し時に実行するスクリプトが含まれます。
* **[!UICONTROL 次の呼び出し]**：エディターの 2 番目のゾーンには、2 回目以降の呼び出し時に実行するスクリプトが含まれます。
* **[!UICONTROL トランジション]**：アクティビティの出力トランジションを複数定義できます。
* **[!UICONTROL スケジュール]**：「**[!UICONTROL スケジュール]**」タブでは、アクティビティをトリガーするタイミングをスケジュール設定できます。

高度なJavaScriptは永続的なタスクで、完了とマークされていない場合は定期的に呼び出されます。 タスクを終了し、今後の呼び出しを防ぐには、**[!UICONTROL 次の呼び出し]**&#x200B;セクションで&#x200B;**タスク.setCompleted()**&#x200B;メソッドを使用する必要があります。

```
task.postEvent(task.transitionByName("ok")); // to transition to Ok branch
task.setCompleted();

return 0;
```
