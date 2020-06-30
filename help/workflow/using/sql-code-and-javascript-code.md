---
title: SQL コードと JavaScript コード
seo-title: SQL コードと JavaScript コード
description: SQL コードと JavaScript コード
seo-description: null
page-status-flag: never-activated
uuid: 20a39bbf-c6b0-4697-97b4-c07609cfb048
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: action-activities
discoiquuid: 1afa75c2-7377-4d03-9105-11bcc9e3206c
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 26ba86073e4f1569bf05a7d8aa864ca87baed3ea
workflow-type: ht
source-wordcount: '234'
ht-degree: 100%

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

>[!NOTE]
>
>デフォルトでは、**[!UICONTROL JavaScript コード]**&#x200B;と&#x200B;**[!UICONTROL 高度な JavaScript コード]**&#x200B;アクティビティの実行段階は 1 時間を超えることはできません。この遅延の後、エラーメッセージが表示されてプロセスが中止され、アクティビティの実行が失敗します。
>
>この遅延は、アクティビティのプロパティの「**[!UICONTROL 次の時間後に実行を停止]**」フィールドで変更できます。

* **[!UICONTROL JavaScript コード]**

   ![](assets/javascript_code.png)

   * **[!UICONTROL スクリプト]**：エディターの中央部に、実行されるスクリプトが含まれています。
   * **[!UICONTROL 処理エラー]**：「[処理エラー](../../workflow/using/monitoring-workflow-execution.md#processing-errors)」を参照してください。

* **[!UICONTROL 高度な JavaScript コード]**

   ![](assets/advanced_javascript_code.png)

   * **[!UICONTROL 最初の呼び出し]**：エディターの最初のゾーンには、最初の呼び出し時に実行するスクリプトが含まれます。
   * **[!UICONTROL 次の呼び出し]**：エディターの 2 番目のゾーンには、2 回目以降の呼び出し時に実行するスクリプトが含まれます。
   * **[!UICONTROL トランジション]**：アクティビティの出力トランジションを複数定義できます。
   * **[!UICONTROL スケジュール]**：「**[!UICONTROL スケジュール]**」タブでは、アクティビティをトリガーするタイミングをスケジュール設定できます。
