---
title: コンテキストの使用
seo-title: コンテキストの使用
description: コンテキストの使用
seo-description: null
page-status-flag: never-activated
uuid: ac8c7068-d640-4934-b7f5-bc91b98eab4c
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: creating-new-reports
discoiquuid: 72fe6df0-0271-48f9-bd6d-bb1ff25fbdf3
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# コンテキストの使用{#using-the-context}

またはの形式でデータを表す場合、2つ **[!UICONTROL tables]** のソ **[!UICONTROL charts]**&#x200B;ースからデータを取得できます。新しいクエリー(「データに対する直接 [フィルターの定義](#defining-a-direct-filter-on-data)」を参照)またはレポートコンテキスト [(「コンテキストデータの使用](#using-context-data)」を参照)。

## データに対する直接フィルターの定義 {#defining-a-direct-filter-on-data}

### データのフィルター {#filtering-data}

Using a **[!UICONTROL Query]** type activity isn&#39;t mandatory when building a report. レポートを構成するテーブルやグラフで、データを直接フィルターできます。

This enables you to select the data to display in the report directly via the **[!UICONTROL Page]** activity of the report.

To do this, click the **[!UICONTROL Filter data...]** link in the **[!UICONTROL Data]** tab: this link lets you access the expressions editor to define a query on the data to be analyzed.

![](assets/reporting_filter_data_from_page.png)

### 例：グラフでフィルターを使用する {#example--use-a-filter-in-a-chart}

次の例では、フランスに居住し、この 1 年間に買い物をした受信者のプロファイルのみを表示するグラフを作成します。

このフィルターを定義するには、チャートにページアクティビティを追加し、それを編集します。Click the **[!UICONTROL Filter data]** link and create the filter that matches the data you want to display. Adobe Campaign でのクエリの作成について詳しくは、[この節](../../platform/using/about-queries-in-campaign.md)を参照してください。

![](assets/s_ncs_advuser_report_wizard_029.png)

ここでは、選択した受信者の市区町村別の分類を表示します。

![](assets/reporting_graph_with_2vars.png)

レンダリングは、次のようになります。

![](assets/reporting_graph_with_2vars_preview.png)

### 例：ピボットテーブルでフィルターを使用する {#example--use-a-filter-in-a-pivot-table}

この例では、フィルターを使用することで、パリ以外に居住している顧客のみをピボットテーブルに表示できます。事前に別のクエリを使用する必要はありません。

次の手順に従います。

1. チャートにページアクティビティを追加し、編集します。
1. ピボットテーブルを作成します。
1. Go to the **[!UICONTROL Data]** tab and select the cube to be used.
1. Click the **[!UICONTROL Filter data...]** link and define the following query to remove Adobe from the list of companies.

   ![](assets/s_ncs_advuser_report_display_03.png)

フィルター条件を満たす受信者のみレポートに表示されます。

![](assets/s_ncs_advuser_report_display_04.png)

## コンテキストデータの使用 {#using-context-data}

To represent data in the form of a **[!UICONTROL table]** or a **[!UICONTROL chart]**, the data can come from the report context.

In the page that contains the table or the chart, the **[!UICONTROL Data]** tab lets you select the data source.

![](assets/s_ncs_advuser_report_datasource_3.png)

* The **[!UICONTROL New query]** option lets you build a query to collect data. 詳しくは、「データに対する直接フィ [ルターの定義」を参照してください](#defining-a-direct-filter-on-data)。
* The **[!UICONTROL Context data]** option lets you use the input data: the context of the report coincides with the information contained in the inbound transition of the page that contains the chart or the table. This context may, for instance, contain data collected via a **[!UICONTROL Query]** activity placed before the **[!UICONTROL Page]** activity and for which you need to specify the table and the fields that the report concerns.

例えば、クエリボックスで、受信者に次のようなクエリを作成します。

![](assets/s_ncs_advuser_report_datasource_2.png)

Then indicate the source of the data in your report, in this case: **[!UICONTROL Data from the context]**.

データの場所は自動的に推測されます。必要に応じて、データパスを指定できます。

![](assets/s_ncs_advuser_report_datasource_4.png)

統計に関係のあるデータを選択する場合、使用可能なフィールドは、クエリで指定されたデータと一致します。

![](assets/s_ncs_advuser_report_datasource_1.png)

