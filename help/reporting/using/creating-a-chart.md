---
title: グラフの作成
seo-title: グラフの作成
description: グラフの作成
seo-description: null
page-status-flag: never-activated
uuid: 516ec707-207e-4320-8d70-fd410425bd4b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: creating-new-reports
discoiquuid: 70e4e63d-354d-4912-b75a-dba38e1c0b03
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# グラフの作成{#creating-a-chart}

データベース内のデータを収集してグラフに表示することもできます。Adobe Campaign では、様々なグラフ表示が可能です。次に、それらの設定について説明します。

グラフは、右クリックメニューまたはツールバーでレポートページに直接挿入します。

## 作成ステップ {#creation-steps}

レポートにグラフを作成するには、次の手順に従います。

1. グラフを表示するページを編集し、ツールバーでグラフタイプを選択します。

   ![](assets/s_advuser_report_page_activity_04.png)

1. 名前とキャプションを入力します。必要に応じて、ドロップダウンリストを使用してキャプションの位置を変更できます。

   ![](assets/s_ncs_advuser_report_wizard_018.png)

1. Click the **[!UICONTROL Data]** tab to define the data source and the series to be calculated.

   The statistics to be displayed in the chart can be calculated based on a query or on the context data, i.e. the data provided by the inbound transition of the current page (for more on this, refer to [Using context data](../../reporting/using/using-the-context.md#using-context-data)).

   * Click the **[!UICONTROL Filter data...]** link to define filtering criteria for the data in the database.

      ![](assets/reporting_graph_add_filter.png)

   * To used contextual data, select this option and click the **[!UICONTROL Advanced settings...]** link. 次に、統計に関係するデータを選択します。

      ![](assets/reporting_graph_from_context.png)

      コンテキストデータにアクセスして、グラフに表示する値を定義できるようになります。

      ![](assets/reporting_graph_select-from_context.png)

## グラフのタイプとバリエーション {#chart-types-and-variants}

Adobe Campaign では、様々なタイプのグラフ表示が可能です。次に、それらについて説明します。

グラフタイプは、グラフをページに挿入する際に選択します。

![](assets/s_advuser_report_page_activity_04.png)

It can also be altered via the **[!UICONTROL Chart type]** section of the **[!UICONTROL General]** tab in the chart.

![](assets/reporting_change_graph_type.png)

バリエーションは、選択したグラフタイプによって異なります。They are selected via the **[!UICONTROL Variants...]** link.

### 分類：円グラフ {#breakdown--pie-charts}

このタイプのグラフでは、測定された要素の概要を表示できます。

円グラフでは、1 つの変数のみ分析できます。

![](assets/reporting_graph_type_sector_1.png)

The **[!UICONTROL Variants]** link lets you personalize the overall rendering of the chart.

![](assets/reporting_graph_type_sector_2.png)

円グラフでは、該当するフィールドに内側の半径の値を入力できます。

次に例を示します。

0.00 の場合は、完全な円。

![](assets/s_ncs_advuser_report_sector_exple1.png)

0.40 の場合は、内側の半径が全体の 40% になる円。

![](assets/s_ncs_advuser_report_sector_exple2.png)

1.00 の場合は、円の外周のみ。

![](assets/s_ncs_advuser_report_sector_exple3.png)

### 変化：折れ線グラフと面グラフ {#evolution--curves-and-areas}

このタイプのグラフでは、1 つまたは複数の測定値の時間的変化を把握できます。

![](assets/reporting_graph_type_curve.png)

### 比較：ヒストグラム {#comparison--histograms}

ヒストグラムでは、1 つまたは複数の変数の値を比較できます。

For these types of charts, the following options are offered in the **[!UICONTROL Variants]** window:

![](assets/reporting_select_graph_var.png)

Check the **[!UICONTROL Display caption]** option to show the caption with the chart and choose its position:

![](assets/reporting_select_graph_legend.png)

該当する場合は、複数の値を積み重ねることができます。

![](assets/reporting_graph_type_histo.png)

必要に応じて、値の表示順を逆にできます。To do this, select the **[!UICONTROL Reverse stacking]** option.

### コンバージョン：ファネル {#conversion--funnel}

このタイプのグラフでは、測定された要素のコンバージョン率を追跡できます。

### 進捗状況：ゲージ {#progress--gauge}

このタイプのグラフでは、定義された目標値と比較した値の進捗状況を表示できます。次の例では、目標とする 100 件の配信のうち、正常に送信された配信の数（76）が黒い目盛り盤に表示されています。このゲージは、特定の状況に対応する 3 つの範囲に分かれています。

![](assets/reporting_graph_type_gauge.png)

グラフの設定時に次の要素を定義します。

![](assets/reporting_graph_type_gauge1.png)

* The **[!UICONTROL Value]** field is represented by a black dial in the chart. 進捗状況の計算対象となる要素を表します。表す値は既に保存されている必要があります。
* The **[!UICONTROL Goal]** field represents the maximum value to achieve.
* Using the **[!UICONTROL Other mark]** field you can add a second indicator to the chart.
* The **[!UICONTROL Display range]** fields let you specify the values between which the report is calculated.
* The **[!UICONTROL Value ranges]** field lets you attribute statuses (None, Bad, Acceptable, Good) to a set of values to better illustrate the progress.

In the **[!UICONTROL Display settings]** section, the **[!UICONTROL Change appearance...]** lets you configure the way the chart is displayed.

![](assets/reporting_graph_type_gauge2.png)

このオ **[!UICONTROL Display the value below the gauge]** プションを使用すると、値の進行状況をグラフの下に表示できます。

The **[!UICONTROL Aperture ratio]** field, which must be between 0 and 1, lets you edit the report&#39;s aperture in a more or less complete circle. 上図の例の場合、値 0.50 は半円に対応します。

The **[!UICONTROL Width]** field lets you edit the chart size.

## グラフとのインタラクション {#interaction-with-the-chart}

ユーザーがグラフをクリックしたときのアクションを定義できます。Open the **[!UICONTROL Interaction events]** window and select the action you want to perform.

選択可能なインタラクションタイプとそれらの設定について詳しくは、[この節](../../web/using/static-elements-in-a-web-form.md#inserting-html-content)を参照してください。

![](assets/s_ncs_advuser_report_wizard_017.png)

## 統計の計算 {#calculating-statistics}

グラフでは、収集したデータに関する統計を表示できます。

These statistics are defined via the **[!UICONTROL Series parameters]** section of the **[!UICONTROL Data]** tab.

To create a new statistic, click the **[!UICONTROL Add]** icon and configure the appropriate window. 次に、使用可能な計算タイプについて説明します。

![](assets/reporting_add_statistics.png)

詳しくは、[この節](../../reporting/using/using-the-descriptive-analysis-wizard.md#statistics-calculation)を参照してください。
