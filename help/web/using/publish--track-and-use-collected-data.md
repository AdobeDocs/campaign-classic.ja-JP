---
title: 収集したデータのパブリッシュ、トラッキングおよび使用
seo-title: 収集したデータのパブリッシュ、トラッキングおよび使用
description: 収集したデータのパブリッシュ、トラッキングおよび使用
seo-description: null
page-status-flag: never-activated
uuid: eac16f2c-0423-4727-a2da-3af1d6c616ec
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: online-surveys
discoiquuid: 434a4bda-0907-42a7-8a75-2db658bba046
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# 収集したデータのパブリッシュ、トラッキングおよび使用{#publish-track-and-use-collected-data}

フォームが作成、設定および発行されたら、リンクをオーディエンスと共有し、回答を追跡できます。

>[!NOTE]
>
>Adobe Campaign の調査のライフサイクルと、そのパブリッシュおよび配信モードは、Web フォームに似ています。詳しくは、[この節](../../web/using/about-web-forms.md)を参照してください。

## 調査ダッシュボード {#survey-dashboard}

各調査には、ステータス、説明、パブリック URL および利用スケジュールを表示できる独自のダッシュボードがあります。また、利用可能なレポートを表示できます。For more on this, refer to [Reports on surveys](#reports-on-surveys).

調査のパブリック URL は、ダッシュボードに表示されます。

![](assets/survey_public_url.png)

## 回答のトラッキング {#response-tracking}

調査の回答をログおよびレポートでトラッキングできます。

### 調査ログ {#survey-logs}

For each survey delivered, you can track the responses in the **[!UICONTROL Logs]** tab. このタブには、調査を完了したユーザーとその接触チャネルのリストが表示されます。

![](assets/s_ncs_admin_survey_logs.png)

行をダブルクリックして、回答者が入力した調査フォームを表示します。すべての調査を参照して、すべての回答にアクセスできます。これらは、外部ファイルにエクスポートできます。For more on this, refer to [Exporting answers](#exporting-answers).

接触チャネルは、次の文字を追加することで、調査 URL に示されます。

```
?origin=xxx
```

while the survey is being edited, its URL contains the parameter **[!UICONTROL __uuid]**, which indicates that it is in a test phase and not yet online. この URL で調査にアクセスする場合、作成されたレコードは、トラッキング（レポート）で考慮されません。The origin is forced to the value **[!UICONTROL Adobe Campaign]**.

URL パラメーターについて詳しくは、[このページ](../../web/using/defining-web-forms-properties.md#form-url-parameters)を参照してください。

### 調査のレポート {#reports-on-surveys}

「ダッシュボード」タブを使用すると、調査レポートにアクセスできます。レポート名をクリックすると、表示されます。

![](assets/s_ncs_admin_survey_report_doc.png)

The structure of the survey is visible in the **[!UICONTROL Documentation]** report.

Two other reports on Web surveys are available in the **[!UICONTROL Reports]** tab of the surveys: **[!UICONTROL General]** and **[!UICONTROL Breakdown of responses]**.

* 一般

   このレポートには、調査に関する一般的な情報（時間の経過に伴う回答数の変化、接触チャネルおよび言語による配分）が含まれます。

   一般レポートの例：

   ![](assets/s_ncs_admin_survey_report_0.png)

* 回答の分類

   このレポートには、各質問に関する回答の分類が表示されます。This breakdown is only available for answers given to fields stored in **[!UICONTROL Question]** type containers. 選択コントロールに対してのみ有効です（例えば、テキストフィールドは分類されません）。

   ![](assets/s_ncs_admin_survey_report_2.png)

## 回答のエクスポート {#exporting-answers}

調査の回答は、後で処理するために、外部ファイルにエクスポートできます。それには、次の 2 つの方法があります。

1. レポートデータのエクスポート

   To export report data, click the **[!UICONTROL Export]** button and choose the export format.

   レポートデータのエクスポートについて詳しくは、[この節](../../reporting/using/about-reports-creation-in-campaign.md)を参照してください。

1. 回答のエクスポート

   To export answers, click the **[!UICONTROL Responses]** tab of the survey and right-click. 選択 **[!UICONTROL Export...]**.

   ![](assets/s_ncs_admin_survey_logs_export_menu.png)

   次に、エクスポートする情報およびストレージファイルを入力します。

   エクスポートウィザードで、出力ファイルのコンテンツおよび形式を設定できます。

   次のことが可能です。

   * 出力ファイルに列を追加し、（データベースに格納された）受信者の情報を復元する
   * エクスポートしたデータの形式を設定する
   * ファイルの情報のエンコード形式を選択する
   If the survey you want to export contains several **[!UICONTROL Multi-line text]** or **[!UICONTROL HTML text]** fields, it has to be exported in **[!UICONTROL XML]** format. To do this, select this format in the drop-down list of the **[!UICONTROL Output format]** field, as shown below:

   ![](assets/s_ncs_admin_survey_logs_export_xml.png)

   Click **[!UICONTROL Start]** to run the export.

   >[!NOTE]
   >
   >データのエクスポートおよびその設定のステージについて詳しくは、[この節](../../platform/using/generic-imports-and-exports.md)を参照してください。

## 収集されたデータの使用 {#using-the-collected-data}

オンライン調査で収集された情報は、ターゲティングワークフローのフレームワーク内で復元できます。これを行うには、ボックスを使用 **[!UICONTROL Survey responses]** します。

次の例では、少なくとも 2 人の子供を含む、オンライン調査で最高スコアを獲得した 5 人の受信者に特別に Web オファーを実行します。この回答の調査は、次のようになります。

![](assets/s_ncs_admin_survey_responses_wf_box_4.png)

In the targeting workflow, the **[!UICONTROL Survey responses]** will be configured as follows:

![](assets/s_ncs_admin_survey_responses_wf_box_1.png)

最初に、関連する調査を選択してから、ウィンドウの中央のセクションで、抽出するデータを選択します。この場合、5 つの最高スコアを復元するために分割ボックスで使用するので、少なくともスコア列を抽出する必要があります。

Indicate the filtering conditions for answers by clicking the **[!UICONTROL Edit query...]** link.

![](assets/s_ncs_admin_survey_responses_wf_box_2.png)

ターゲティングワークフローを開始します。このクエリは、8 人の受信者を復元します。

![](assets/s_ncs_admin_survey_responses_wf_box_5.png)

コレクションボックスのアウトバウンドトランジションを右クリックして、表示します。

![](assets/s_ncs_admin_survey_responses_wf_box_6.png)

次に、分割ボックスをワークフローに配置して、最高スコアの 5 人の受信者を復元します。

分割ボックスを編集して、次のように設定します。

* Start by selecting the adequate schema in the **[!UICONTROL General]** tab, then configure the sub-set:

   ![](assets/s_ncs_admin_survey_responses_wf_box_6b.png)

* タブに移動し、 **[!UICONTROL Sub-sets]** オプションを選択 **[!UICONTROL Limit the selected records]** して、リンクをクリックし **[!UICONTROL Edit...]** ます。

   ![](assets/s_ncs_admin_survey_responses_wf_box_7.png)

* このオプション **[!UICONTROL Keep only the first records after sorting]** を選択し、並べ替え列を選択します。 オプションをオン **[!UICONTROL Descending sort]** にします。

   ![](assets/s_ncs_admin_survey_responses_wf_box_8.png)

* Click the **[!UICONTROL Next]** button and limit the number of records to 5.

   ![](assets/s_ncs_admin_survey_responses_wf_box_9.png)

* Click **[!UICONTROL Finish]** then restart the workflow to approve targeting.

## データの標準化 {#standardizing-data}

エイリアスを使用して収集したデータに対して、Adobe Campaign で、標準化プロセスを設定できます。これにより、データベースに格納されたデータを標準化できます。これをおこなうには、関連情報を含む定義済みリストでエイリアスを定義します。

詳しくは、[このページ](../../platform/using/managing-enumerations.md#about-enumerations)を参照してください。
