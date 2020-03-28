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
translation-type: ht
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# コンテキストの使用{#using-the-context}

データを&#x200B;**[!UICONTROL テーブル]**&#x200B;や&#x200B;**[!UICONTROL グラフ]**&#x200B;の形式で表す場合は、新しいクエリ（[データに対する直接フィルターの定義](#defining-a-direct-filter-on-data)を参照）またはレポートコンテキスト（[コンテキストデータの使用](#using-context-data)を参照）の 2 つのソースからデータを取得できます。

## データに対する直接フィルターの定義 {#defining-a-direct-filter-on-data}

### データのフィルター {#filtering-data}

レポートを作成する際、**[!UICONTROL クエリ]**&#x200B;タイプのアクティビティの使用は、必須ではありません。レポートを構成するテーブルやグラフで、データを直接フィルターできます。

これによって、レポートに表示するデータを、レポートの&#x200B;**[!UICONTROL ページ]**&#x200B;アクティビティを通じて直接選択できます。

それには、「**[!UICONTROL データ]**」タブの「**[!UICONTROL データをフィルター]**」リンクをクリックします。式エディターが開き、分析対象となるデータに対するクエリを定義できます。

![](assets/reporting_filter_data_from_page.png)

### 例：グラフでフィルターを使用する {#example--use-a-filter-in-a-chart}

次の例では、フランスに居住し、この 1 年間に買い物をした受信者のプロファイルのみを表示するグラフを作成します。

このフィルターを定義するには、チャートにページアクティビティを追加し、それを編集します。「**[!UICONTROL データをフィルター]**」リンクをクリックし、表示するデータに合致するフィルターを作成します。Adobe Campaign でのクエリの作成について詳しくは、[この節](../../platform/using/about-queries-in-campaign.md)を参照してください。

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
1. 「**[!UICONTROL データ]**」タブに移動し、使用するキューブを選択します。
1. 「**[!UICONTROL データをフィルター]**」リンクをクリックし、会社のリストから ADOBE を削除するように次のようなクエリを定義します。

   ![](assets/s_ncs_advuser_report_display_03.png)

フィルター条件を満たす受信者のみレポートに表示されます。

![](assets/s_ncs_advuser_report_display_04.png)

## コンテキストデータの使用 {#using-context-data}

データを&#x200B;**[!UICONTROL テーブル]**&#x200B;や&#x200B;**[!UICONTROL グラフ]**&#x200B;の形式で表す場合は、そのデータをレポートコンテキストから取得できます。

テーブルやグラフを含んだページでは、「**[!UICONTROL データ]**」タブでデータソースを選択できます。

![](assets/s_ncs_advuser_report_datasource_3.png)

* 「**[!UICONTROL 新しいクエリ]**」オプションを選択すると、データを収集するためのクエリを作成できます。詳しくは、[データに対する直接フィルターの定義](#defining-a-direct-filter-on-data)を参照してください。
* 「**[!UICONTROL コンテキストデータ]**」オプションを選択すると、入力データを使用できます。レポートのコンテキストは、グラフやテーブルを含むページのインバウンドトランジションに含まれる情報と一致します。このコンテキストには、例えば、**[!UICONTROL ページ]**&#x200B;アクティビティの前に配置された&#x200B;**[!UICONTROL クエリ]**&#x200B;アクティビティで収集されたデータが含まれている可能性があります。その場合、レポートに関係のあるテーブルやフィールドを指定する必要があります。

例えば、クエリボックスで、受信者に次のようなクエリを作成します。

![](assets/s_ncs_advuser_report_datasource_2.png)

次に、レポートのデータソースを指定します。ここでは、「**[!UICONTROL コンテキストのデータ]**」とします。

データの場所は自動的に推測されます。必要に応じて、データパスを指定できます。

![](assets/s_ncs_advuser_report_datasource_4.png)

統計に関係のあるデータを選択する場合、使用可能なフィールドは、クエリで指定されたデータと一致します。

![](assets/s_ncs_advuser_report_datasource_1.png)

