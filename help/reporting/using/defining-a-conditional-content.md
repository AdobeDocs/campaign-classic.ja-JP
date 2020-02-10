---
title: 条件付きコンテンツの定義
seo-title: 条件付きコンテンツの定義
description: 条件付きコンテンツの定義
seo-description: null
page-status-flag: never-activated
uuid: 2b49958d-6429-445d-a7dc-caaca072f4e4
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: creating-new-reports
discoiquuid: 0ca5e0f6-cc81-4da9-aecf-a095cc1a19f9
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 209ac4d81d2d27c264ee6b288bcb7fcb1900ffc5

---


# 条件付きコンテンツの定義{#defining-a-conditional-content}

レポートの特定の項目やページの表示に条件を付けることができます。

特定の項目を条件付きにするには、それらの項目の表示設定を調整します。For more on this, refer to [Conditioning item display](#conditioning-item-display).

To make the display of one or more pages conditional, use a **[!UICONTROL Test]** type activity. 詳しくは、[ページ表示の条件付け](#conditioning-page-display)を参照してください。

## 項目表示の条件付け {#conditioning-item-display}

レポートの一部分の表示を条件付きにするには、その項目の表示条件を定義する必要があります。それらの条件が満たされない場合、その項目は表示されません。

表示条件は、オペレーターの状況や、レポートページで選択または入力された項目によって異なる場合があります。

ページ上の項目の条件付き表示を示す例については、[この節](../../web/using/form-rendering.md#defining-fields-conditional-display)を参照してください。

次の例では、表示条件は言語に依存します。

![](assets/reporting_display_condition.png)

## ページ表示の条件付け {#conditioning-page-display}

In the chart of a report, the **[!UICONTROL Test]** activity lets you change the sequence of pages depending on one or more conditions.

このアクティビティの動作の仕組みは次のとおりです。

1. Place a **[!UICONTROL Test]** in a chart and edit it.
1. Click the **[!UICONTROL Add]** button to create the various possible cases.

   ![](assets/reporting_test_sample.png)

   For each case, an output transition is added to the **[!UICONTROL Test]** activity.

   ![](assets/reporting_test_transitions.png)

1. Select the **[!UICONTROL Enable default transition]** to add a transition, in case one of the configured conditions isn&#39;t met.

   詳しくは、[この節](../../web/using/defining-web-forms-page-sequencing.md#conditional-page-display)を参照してください。

A **[!UICONTROL Test]** activity can be placed at the start of the chart to condition the display depending on context or operator profile for instance.
