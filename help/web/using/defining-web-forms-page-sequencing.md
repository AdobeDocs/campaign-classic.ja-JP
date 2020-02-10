---
title: Web フォームページの順番の定義
seo-title: Web フォームページの順番の定義
description: Web フォームページの順番の定義
seo-description: null
page-status-flag: never-activated
uuid: 297fad62-d806-4bd8-9b8c-313c20344ab0
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: web-forms
discoiquuid: 85bf3244-6896-43e7-96b8-84c45c282fec
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c9c9d5f96856ce9e19571bad032d2bf04eaa60bd

---


# Web フォームページの順番の定義{#defining-web-forms-page-sequencing}

フォームには、1 つ以上のページを含めることができます。フォームは、ページとテスト、スクリプト実行およびページジャンプを記録するステージを並べることができるダイアグラムを使用して構築されます。ダイアグラム設定モードは、ワークフローの場合と同じです。

## 前のページと次のページについて {#about-previous-page-and-next-page}

For each page, you can delete the **[!UICONTROL Next]** or **[!UICONTROL Previous]** buttons. これを行うには、該当するページを選択し、オプションまたはを選 **[!UICONTROL Disable next page]** 択しま **[!UICONTROL Disallow returning to the previous page]** す。

![](assets/s_ncs_admin_survey_no_next_page.png)

これらのボタンをリンクに置き換えることができます。詳しくは、HTML [コンテンツの挿入を参照してくださ](../../web/using/static-elements-in-a-web-form.md#inserting-html-content)い。

## ジャンプの挿入 {#inserting-a-jump}

The **[!UICONTROL Jump]** object gives access to another page or another form when the user clicks **[!UICONTROL Next]**.

次のジャンプ先を設定できます。

* フォームの別のページ。To do this, select **[!UICONTROL Internal activity]** and then specify the desired page, as below:

   ![](assets/s_ncs_admin_jump_param1.png)

* 別のフォーム。To do this, select the **[!UICONTROL Explicit]** option and specify the destination form.

   ![](assets/s_ncs_admin_jump_param2.png)

* ジャンプ先は変数に格納できます。この場合、次に示すように、ドロップダウンリストから選択します。

   ![](assets/s_ncs_admin_jump_param3.png)

* The **[!UICONTROL Comment]** tab lets you enter information that will be visible by the operator when they click the object in the diagram.

   ![](assets/s_ncs_admin_survey_jump_comment.png)

## Example: accessing another form according to a parameter of the URL {#example--accessing-another-form-according-to-a-parameter-of-the-url}

次の例では、承認の際に URL のパラメーターによって指定された別のフォームを表示する Web フォームを設定します。それには、次の手順に従います。

1. Insert a jump at the end of a form: this replaces the **[!UICONTROL End]** box.

   ![](assets/s_ncs_admin_survey_jump_sample1.png)

1. フォームプロパティで、ローカル変数（**next**）に格納されたパラメーター（**next**）を追加します。ローカル変数は、ローカル変 [数へのデータの格納で詳しく説明します](../../web/using/web-forms-answers.md#storing-data-in-a-local-variable)。

   ![](assets/s_ncs_admin_survey_jump_sample2.png)

1. Edit the **[!UICONTROL Jump]** object, select the **[!UICONTROL Stored in a variable]** option and select the **next** variable from the drop-down box.

   ![](assets/s_ncs_admin_survey_jump_sample3.png)

1. 配信 URL には、次のような、宛先のフォームの内部名を含める必要があります。

   ```
   https://[myserver]/webForm/APP62?&next=APP22
   ```

   When the user clicks the **[!UICONTROL Approve]** button, form **APP22** is displayed.

## フォームの別のページへのリンクの挿入 {#inserting-a-link-to-another-page-of-the-form}

フォームの別のページへのリンクを挿入できます。To do this, add a **[!UICONTROL Link]** type static element to the page. For more on this, refer to [Inserting a link](../../web/using/static-elements-in-a-web-form.md#inserting-a-link).

## 条件付きページ表示 {#conditional-page-display}

### 回答に基づいて表示 {#display-based-on-responses}

The **[!UICONTROL Test]** box lets you condition the sequencing of pages in a form. テスト結果に応じた様々な分岐線を定義できますこれにより、ユーザーが提供する回答に応じて異なるページを表示できます。

例えば、既にオンラインで注文した顧客に異なるページを表示したり、10 を超える注文をした顧客に別のページを表示したりできます。To do this, in the first page of the form, insert a **[!UICONTROL Number]** type input field for the user to state how many orders they have placed.

![](assets/s_ncs_admin_survey_test_ex0.png)

この情報をデータベースのフィールドに格納するか、ローカル変数を使用できます。

>[!NOTE]
>
>ストレージ・モードの詳細は、「 [Response storage」フィールドに示されます](../../web/using/web-forms-answers.md#response-storage-fields)。

この例では、変数を使用します。

![](assets/s_ncs_admin_survey_test_ex1.png)

フォームのダイアグラムで、条件を定義するためにテストボックスを挿入します。各条件について、テストボックスの出力時に、新しい分岐が追加されます。

![](assets/s_ncs_admin_survey_test_ex2.png)

Select the **[!UICONTROL Activate the default branching]** option to add a transition for cases where none of the conditions is true. このオプションは、定義した条件によってすべての可能性がカバーされている場合は、不要です。

次に、例えば次のように、いずれかの条件が true である場合のページの順番を定義します。

![](assets/s_ncs_admin_survey_test_ex3.png)

### パラメーターに基づいて表示 {#display-based-on-parameters}

また、Web フォームの初期化パラメーターに応じて、またはデータベースに格納された値に応じて、ページの順番をパーソナライズできます。フォームURL [パラメーターを参照してくださ](../../web/using/defining-web-forms-properties.md#form-url-parameters)い。

## スクリプトの追加 {#adding-scripts}

The **[!UICONTROL Script]** object lets you enter a JavaScript script directly, for example to modify the value of a field, retrieve data from the database, or call an Adobe Campaign API.

## 終了ページのパーソナライズ {#personalizing-the-end-page}

終了ページをダイアグラム最後に配置する必要があります。The end page is displayed when the user clicks the **[!UICONTROL Approve]** button in the Web form.

To personalize this page, double-click **[!UICONTROL End]** and enter the content of the page in the central editor.

![](assets/s_ncs_admin_survey_end_page_edit.png)

* 既存の HTML コンテンツをコピー＆ペーストできます。これを行うには、をクリックし **[!UICONTROL Display source code]** てHTMLコードを挿入します。
* 外部 URL を使用できます。これをおこなうには、対応するオプションを選択し、表示するページの URL を入力します。

