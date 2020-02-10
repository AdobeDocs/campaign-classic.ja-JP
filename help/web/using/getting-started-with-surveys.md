---
title: 調査の概要
seo-title: 調査の概要
description: 調査の概要
seo-description: null
page-status-flag: never-activated
uuid: 62ca684c-94a7-465a-9536-75e8a96b1c0e
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: online-surveys
discoiquuid: 2df82006-dcc3-4b07-bc36-b646b1c27aaa
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# 調査の概要{#getting-started-with-surveys}

ここでは、次のテンプレートを使用して、簡単な調査を作成するための主な手順について要約しています。

![](assets/s_ncs_admin_survey_result.png)

手順は次のとおりです。

1. [手順 1 - 調査の作成](#step-1---creating-a-survey),
1. [手順 2 - テンプレートの選択](#step-2---selecting-the-template),
1. [手順 3 - 調査の構築](#step-3---building-the-survey),
1. [手順 4 - ページコンテンツの作成](#step-4---creating-the-page-content),
1. [手順 5 - 調査データの格納](#step-5---storing-the-survey-data-),
1. [手順 6 - ページのパブリッシュ](#step-6---publishing-the-pages),
1. [手順 7 - オンライン調査の共有](#step-7---sharing-your-online-survey).

## 手順 1 - 調査の作成 {#step-1---creating-a-survey}

新しい調査を作成するには、「または」タブに移動し **[!UICONTROL Campaigns]** てメ **[!UICONTROL Profiles and targets]** ニューをクリック **[!UICONTROL Web Applications]** します。 Click the **[!UICONTROL Create]** button above the list of forms.

![](assets/s_ncs_admin_survey_create.png)

## 手順 2 - テンプレートの選択 {#step-2---selecting-the-template}

調査テンプレートを選択し、調査に名前を付けます。この名前はエンドユーザーには表示されませんが、Adobe Campaign内で調査を識別できます。 Click **[!UICONTROL Save]** to add the survey to the list of Web applications.

![](assets/s_ncs_admin_survey_wz_00.png)

## 手順 3 - 調査の構築 {#step-3---building-the-survey}

調査は、ダイアグラムで構築されます。ダイアグラムには、コンテンツが作成されるページ、データがプリロードおよび保存される手順およびテストフェーズの各要素が配置されます。また、スクリプトおよびクエリも挿入できます。

To build the chart, click the **[!UICONTROL Edit]** form of the survey.

調査には、**少なくとも**、ページ、ストレージボックス、終了ページの 3 つのコンポーネントが含まれている必要があります。

* To create a page, select the **[!UICONTROL Page]** object in the left-hand section of the editor and deposit it in the middle section, as shown below:

   ![](assets/s_ncs_admin_survey_new_page.png)

* Next, select the **[!UICONTROL Storage]** object and place it on the output transition of the page.
* Finally, select the **[!UICONTROL End]** object and place it on the end of the output transition of the storage box to obtain the following diagram:

   ![](assets/s_ncs_admin_survey_end.png)

## 手順 4 - ページコンテンツの作成 {#step-4---creating-the-page-content}

In the following example, we are using a **[!UICONTROL Page (v5 compatibility)]** type page. This type of page is accessed via the advanced menu of the **[!UICONTROL Edit]** tab.

![](assets/s_ncs_admin_survey_pagev5.png)

* 入力フィールドの追加

   To create the content of the page, you must edit it: to do this, double-click the **[!UICONTROL Page]** object. ツールバーの最初のアイコンをクリックし、フィールド作成ウィザードを開きます。To create an entry field for the user name to be stored in the matching field of the recipient&#39;s profile, select **[!UICONTROL Edit a recipient]**.

   ![](assets/s_ncs_admin_survey_add_field_menu.png)

   Click the **[!UICONTROL Next]** button to select the field for data storage in the database. この場合、「姓」フィールドです。

   ![](assets/s_ncs_admin_survey_choose_field.png)

   Click **[!UICONTROL Finish]** to confirm field creation.

   デフォルトでは、既にデータベースに存在するフィールドに情報が格納されると、そのフィールドは、選択したフィールドの名前になります（つまり、この例では「姓」）。このラベルは、次に示すように修正できます。

   ![](assets/s_ncs_admin_survey_change_label.png)

   次に、ユーザーのアカウント番号用の入力フィールドを作成します。操作を繰り返して、「アカウント番号」フィールドを選択します。

   同じ手順を実行して、ユーザーが E メールアドレスを入力するためのフィールドを追加します。

* To create a question, right-click the last element in the tree, and select **[!UICONTROL Containers > Question]** , or click the **[!UICONTROL Containers]** icon and select **[!UICONTROL Question]**.

   ![](assets/s_ncs_admin_survey_add_qu.png)

   質問のラベルを入力し、回答フィールドを質問のサブブランチとして挿入します。これを行うには、回答フィールドを作成する際に、質問にリンクされたノードを選択する必要があります。 次に示すよ **[!UICONTROL drop-down listx]** うに、ア **[!UICONTROL Selection controls]** イコンを使用するか、右クリックしてを追加します。

   ![](assets/s_ncs_admin_survey_add_list.png)

   ストレージスペースを選択します。列挙フィールドを選択し、値を自動的に取得します（この場合、E メール形式）。

   ![](assets/s_ncs_admin_survey_add_itz_list.png)

   タブで、リ **[!UICONTROL General]** ンクをクリックし **[!UICONTROL Initialize the list of values from the database]** ます。値のテーブルは自動的に入力されます。

   ![](assets/s_ncs_admin_survey_add_value.png)

   Click **[!UICONTROL OK]** to close the editor, and **[!UICONTROL Save]** to save changes.

   >[!NOTE]
   >
   >For each field or question, you can adapt the page layout to suit your needs, thanks to the options in the **[!UICONTROL Advanced]** tab. 調査画面のレイアウトについて詳しくは、[この節](../../web/using/about-web-forms.md)を参照してください。

   In the detail screen, click the **[!UICONTROL Preview]** tab to view the rendering of the survey you have just created.

   ![](assets/s_ncs_admin_survey_preview.png)

## 手順 5 - 調査データの格納 {#step-5---storing-the-survey-data-}

ストレージボックスを使用すると、ユーザーの回答をデータベースに保存できます。既にデータベースにあるプロファイルを識別するために、紐付けキーを選択する必要があります。

これをおこなうには、ボックスを編集して、データを格納する際に紐付けキーとして使用するフィールドを選択します。

次の例では、保存（確認）を実行する際に、フォームに入力したのと同じアカウント番号のプロファイルがデータベースに保存されている場合、そのプロファイルが更新されます。プロファイルが存在しない場合は、作成されます。

![](assets/s_ncs_admin_survey_save_edit.png)

Click **[!UICONTROL OK]** to confirm, then click **[!UICONTROL Save]** to save the survey

## 手順 6 - ページのパブリッシュ {#step-6---publishing-the-pages}

ユーザーが HTML ページにアクセスできるようにするには、アプリケーションを使用可能にする必要があります。編集中の状態から本番にしなければなりません。調査を本番に移行するには、パブリッシュする必要があります。これには、以下の手順に従います。

* Click the **[!UICONTROL Publish]** button located above the survey dashboard.
* Click **[!UICONTROL Start]** to launch publication and close the wizard.

   ![](assets/s_ncs_admin_survey_start_publ.png)

   調査のステータスが&#x200B;**オンライン**&#x200B;に変わります。

   ![](assets/survey_published.png)

## 手順 7 - オンライン調査の共有{#step-7---sharing-your-online-survey}

本番に移行された調査はサーバーでアクセスでき、配信可能となります。調査にアクセスするための URL は、ダッシュボードに表示されます。

![](assets/survey_url_from_dashboard.png)

調査を配信するには、例えば、ターゲット母集団へのアクセスリンクを含むメッセージを送信したり、調査のアクセス URL を Web ページに配置したりできます。

その後、レポートおよびログを使用して、ユーザーの回答を監視できます。[回答のトラッキング](../../web/using/publish--track-and-use-collected-data.md#response-tracking)を参照してください。

>[!CAUTION]
>
>パブリック URL には、調査の内部名が含まれます。内部名を修正すると、URL は自動的に更新されます。すべての調査へのリンクも、更新する必要があります。
>
>フォームへのリンクを含む配信が、既に送信されている場合、このリンクは機能しなくなります。

