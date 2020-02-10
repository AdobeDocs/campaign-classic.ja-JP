---
title: レポートの処理
seo-title: レポートの処理
description: レポートの処理
seo-description: null
page-status-flag: never-activated
uuid: af8f1101-135f-49ce-bada-bd19fe32053b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: analyzing-populations
discoiquuid: 667746cb-b553-4a71-8523-6b2695047ab6
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 62b2f1f6cfcaadd10880d428b8b94d73d2addcdb

---


# 分析レポートの使用{#processing-a-report}

## 分析レポートの保存 {#saving-an-analysis-report}

適切な権限がある場合は、テンプレートから作成した分析レポートを保存できます。また、Excel、PDF、OpenOffice のいずれかのフォーマットでレポートをエクスポートすることもできます。

To save your report, click **[!UICONTROL Save]** and give your report a label.

Select **[!UICONTROL Also save data]** if you wish to create a history of your report and see the values of the report at the time of saving. For more on this, refer to [Archiving analysis reports](#archiving-analysis-reports).

このオプシ **[!UICONTROL Share this report]** ョンを使用すると、他の演算子もレポートにアクセスできます。

![](assets/s_ncs_user_report_wizard_010.png)

保存後は、このレポートを再利用して、他の分析レポートを生成できます。

![](assets/s_ncs_user_report_wizard_08a.png)

To make changes to this report, edit the **[!UICONTROL Administration > Configuration > Adobe Campaign tree reports]** node of the Adobe Campaign tree (or the first &#39;Reports&#39; type folder for which the operator has editing rights). 詳しくは、「分析レポートのレ [イアウトの設定」を参照してください](#configuring-the-layout-of-a-descriptive-analysis-report)。

## 分析レポートの追加設定 {#analysis-report-additional-settings}

記述的分析レポートをいったん保存したら、そのレポートのプロパティを編集したり、追加オプションにアクセスしたりできます。

![](assets/s_ncs_user_report_wizard_08b.png)

これらのオプションは標準レポートの場合と同じです。詳しくは、[このページ](../../reporting/using/properties-of-the-report.md)を参照してください。

## 記述的分析レポートのレイアウトの設定 {#configuring-the-layout-of-a-descriptive-analysis-report}

記述的分析のグラフやテーブルにおけるデータの表示やレイアウトをパーソナライズできます。All options are accessed via the Adobe Campaign tree, in the **[!UICONTROL Edit]** tab of each report.

### 分析レポートの表示モード {#analysis-report-display-mode}

When you create a report using the **[!UICONTROL qualitative distribution]** template, table and chart display modes are selected by default. 1 つの表示モードだけでよい場合は、それ以外のボックスのチェックをオフにします。つまり、チェックを入れた表示モードのタブだけが使用可能になります。

![](assets/s_ncs_advuser_report_display_01.png)

To change the schema of the report, click the **[!UICONTROL Select the link]** and select another table from the database.

![](assets/s_ncs_advuser_report_display_02.png)

### 分析レポートの表示設定 {#analysis-report-display-settings}

統計や小計の表示／非表示を切り替えたり、統計の方向を選択したりできます。

![](assets/s_ncs_advuser_report_display_05.png)

統計を作成するときに、そのラベルをパーソナライズできます。

![](assets/s_ncs_advuser_report_display_06.png)

その名前はレポートに表示されます。

![](assets/s_ncs_advuser_report_display_07.png)

ただし、ラベルと小計の表示オプションのチェックをオフにした場合、それらはレポートには表示されません。テーブルのセルの上にマウスポインターを置くと、統計の名前がツールチップに表示されます。

![](assets/s_ncs_advuser_report_display_08.png)

デフォルトでは、統計はオンラインで表示されます。統計の方向を変更するには、ドロップダウンリストから適切なオプションを選択します。

![](assets/s_ncs_advuser_report_wizard_035a.png)

次の例では、統計が各列に表示されています。

![](assets/s_ncs_advuser_report_wizard_035.png)

### 分析レポートのデータレイアウト {#analysis-report-data-layout}

記述的分析テーブルで直接データのレイアウトをパーソナライズできます。それには、対象となる変数を右クリックします。以下のうち、使用可能なオプションをドロップダウンメニューから選択します。

* **[!UICONTROL Pivot]** をクリックして、変数の軸を変更します。
* **[!UICONTROL Up]** /を指定 **[!UICONTROL Down]** すると、変数が行で置き換えられます。
* **[!UICONTROL Move to the right]** /を指定 **[!UICONTROL Move to the left]** すると、列内の変数が置き換えられます。
* **[!UICONTROL Turn]** を使用して、変数軸を反転させます。
* **[!UICONTROL Sort from A to Z]** を使用して、変数の値を低い順に並べ替えます。
* **[!UICONTROL Sort from Z to A]** を使用して、変数の値を高い順に並べ替えます。

   ![](assets/s_ncs_advuser_report_wizard_016.png)

初期の表示に戻すには、表示を更新します。

### 分析レポートのグラフオプション {#analysis-report-chart-options}

グラフにおけるデータの表示をパーソナライズできます。To do this, click the **[!UICONTROL Variables...]** link available during the chart type selection stage.

![](assets/s_ncs_advuser_report_wizard_3c.png)

次のオプションを使用できます。

* ウィンドウの上部のセクションでグラフの表示領域を変更できます。
* デフォルトでは、グラフにラベルが表示されます。You can hide them by un-checking the **[!UICONTROL Show values]** option.
* The **[!UICONTROL Accumulate values]** option lets you add up values from one series to another.
* グラフの凡例を表示するかどうかを決めることができます。凡例を非表示にするには、該当するオプションのチェックをオフにします。デフォルトでは、凡例はグラフの外側の右上隅に表示されます。

   表示スペースの節約のために、凡例をグラフの上部に表示することもできます。To do this, select the option **[!UICONTROL Include in the chart]**

   Select the vertical and horizontal alignment in the **[!UICONTROL Caption position]** drop-down list.

   ![](assets/s_ncs_advuser_report_wizard_3d.png)

## 分析レポートのエクスポート {#exporting-an-analysis-report}

分析レポートのデータをエクスポートするには、ドロップダウンリストをクリックし、希望する出力フォーマットを選択します。

![](assets/s_ncs_user_report_wizard_09.png)

詳しくは、[このページ](../../reporting/using/actions-on-reports.md)を参照してください。

## 既存のレポートおよび分析の再利用 {#re-using-existing-reports-and-analyses}

Adobe Campaign に既に格納されている既存のレポートを使用して、データに関する記述的分析レポートを作成できます。このモードが可能なのは、分析が既に保存されている場合か、レポートが既に作成されて記述的分析ウィザードでアクセスできるように設定されている場合です。

詳細分析の保存方法については、「分析レポートの保 [存」を参照してください](#saving-an-analysis-report)。

To create descriptive analysis reports, the descriptive analysis wizard must be executed via a workflow transition or via the **[!UICONTROL Tools > Descriptive analysis]** menu.

1. を選択し、 **[!UICONTROL Existing analyses and reports]** をクリックしま **[!UICONTROL Next]**&#x200B;す。
1. これで、使用可能なレポートのリストにアクセスできます。生成するレポートを選択します。

   ![](assets/s_ncs_user_report_wizard_01.png)

## 分析レポートのアーカイブ {#archiving-analysis-reports}

既存の分析に基づいて記述的分析を作成する場合は、アーカイブを作成してデータを格納したりレポートの結果を比較したりできます。

履歴を作成するには、次の手順に従います。

1. 既存の分析を開くか、新しい記述的分析ウィザードを作成します。
1. レポート表示ページで、次に示すように、ツールバーにある履歴作成ボタンをクリックして、確認します。

   ![](assets/reporting_descriptive_historize_icon.png)

1. アーカイブアクセスボタンを使用すると、以前の分析を表示できます。

   ![](assets/reporting_descriptive_historize_access.png)

