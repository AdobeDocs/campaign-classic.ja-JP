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
translation-type: tm+mt
source-git-commit: 16e35b62cdf42c04139cc17645095a3d1f6e0fa7

---


# SQL コードと JavaScript コード{#sql-code-and-javascript-code}

## SQL コード {#sql-code}

*アクティビティは&#x200B;*[!UICONTROL SQL code*]* 、SQLスクリプトを実行します。 スクリプトは、JST テンプレートです。

![](assets/sql_code.png)

* **[!UICONTROL Script]**

   エディターの中央部に、実行されるスクリプトが含まれています。このスクリプトは、JST テンプレートであり、ワークフローのコンテキストに応じて設定できます。

* **[!UICONTROL Processing errors]**

   詳しくは、処理エ [ラーを参照してくださ](../../workflow/using/monitoring-workflow-execution.md#processing-errors)い。

## JavaScriptコードおよび高度なJavaScriptコード {#javascript-code}

**[!UICONTROL JavaScript code]** アクティビテ **[!UICONTROL Advanced JavaScript code]** ィは、ワークフローのコンテキストでJavaScriptスクリプトを実行します。 スクリプティングについて詳しくは、 [JavaScriptスクリプトとテンプレートの節を参照してください](../../workflow/using/javascript-scripts-and-templates.md) 。

>[!NOTE]
>
>デフォルトでは、およびアクティビティの実 **[!UICONTROL JavaScript code]** 行フェー **[!UICONTROL Advanced JavaScript code]** ズは1時間を超えることはできません。 この遅延の後、エラーメッセージが表示されてプロセスが中止され、アクティビティの実行が失敗します。
>
>この遅延は、アクティビティのプロパテ **[!UICONTROL Stop execution after]** ィで使用可能なフィールドで変更できます。

* **[!UICONTROL JavaScript code]**

   ![](assets/javascript_code.png)

   * **[!UICONTROL Script]**:エディターの中央の領域には、実行するスクリプトが含まれます。
   * **[!UICONTROL Processing errors]**:詳しくは、処理エ [ラーを参照してくださ](../../workflow/using/monitoring-workflow-execution.md#processing-errors)い。

* **[!UICONTROL Advanced JavaScript code]**

   ![](assets/advanced_javascript_code.png)

   * **[!UICONTROL First call]**:エディターの最初の領域には、最初の呼び出し時に実行するスクリプトが含まれます。
   * **[!UICONTROL Next calls]**:エディターの2番目の領域には、次の呼び出し時に実行するスクリプトが含まれます。
   * **[!UICONTROL Transitions]**:複数のアクティビティ出力トランジションを定義できます。
   * **[!UICONTROL Schedule]**:このタ **[!UICONTROL Schedule]** ブでは、アクティビティをトリガーするタイミングをスケジュールできます。
