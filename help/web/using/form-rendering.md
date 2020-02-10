---
title: フォームレンダリング
seo-title: フォームレンダリング
description: フォームレンダリング
seo-description: null
page-status-flag: never-activated
uuid: 714ce201-5535-4fde-b388-1605ac54edcb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: web-forms
discoiquuid: 669635bd-868b-4550-b075-6294ccb71297
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# フォームレンダリング{#form-rendering}

## フォームレンダリングテンプレートの選択 {#selecting-the-form-rendering-template}

フォーム設定により、ページ生成に使用するテンプレートを選択できます。To access them, click the **[!UICONTROL Settings]** button in the form detail toolbar, and select the **[!UICONTROL Rendering]** tab. デフォルトで、多数のテンプレート（スタイルシート）を使用できます。

![](assets/s_ncs_admin_survey_rendering_select.png)

エディターの下部のセクションで、選択したテンプレートのレンダリングを表示できます。

ズーム機能を使用すると、選択したテンプレートを編集できます。

![](assets/s_ncs_admin_survey_render_edit.png)

これらのテンプレートを修正または上書きできます。To do this, click the **[!UICONTROL Page layout...]** link and personalize the information.

![](assets/s_ncs_admin_survey_render_edit_param.png)

次の操作をおこなうことができます。

* ロゴとして使用する画像を変更し、サイズを適応させます。
* また、ユーザーがこのレンダリングテンプレートを選択する際にプレビュー画像にアクセスするためのパスを指定します。

The **[!UICONTROL Headers/Footers]** tab lets you change the information displayed in the headers and footers of each form page using this template.

![](assets/s_ncs_admin_survey_render_edit_header.png)

Each line of the **[!UICONTROL Page headers]** and **[!UICONTROL Page footers]** section corresponds to a line in the HTML page. Click **[!UICONTROL Add]** to create a new line.

Select an existing line and click the **[!UICONTROL Detail]** button to personalize it.

![](assets/s_ncs_admin_survey_render_edit_header_detail.png)

各タブで、行のコンテンツを変更したり、境界線を追加したり、フォント属性を変更したりできます。「**[!UICONTROL OK]**」をクリックして、これらの変更を確定します。

The **[!UICONTROL Position]** fields let you define the position of elements in the page header and footer.

![](assets/s_ncs_admin_survey_render_edit_header_position.png)

>[!NOTE]
>
>レンダリングテンプレートはノードに保存 **[!UICONTROL Administration > Configuration > Form rendering]** されます。\
>詳しくは、「フォームレンダリングのカスタマ [イズ」を参照してください](#customizing-form-rendering)

## フォームのレンダリングのカスタマイズ {#customizing-form-rendering}

### 要素のレイアウトの変更 {#changing-the-layout-of-elements}

フォームの各要素（入力フィールド、画像、ラジオボタンなど）について、スタイルシートをオーバーロードできます。

To do this, use the **[!UICONTROL Advanced]** tab.

![](assets/s_ncs_admin_survey_advanced_tab.png)

次のプロパティを定義できます。

* **[!UICONTROL Label position]**:詳しく [は、ラベルの位置の定義](../../web/using/defining-web-forms-layout.md#defining-the-position-of-labels)、
* **[!UICONTROL Label format]**:折り返し、または折り返しなし、
* **[!UICONTROL Number of cells]** :詳しく [は、ページ上でのフィールドの配置を参照してください](../../web/using/defining-web-forms-layout.md#positioning-the-fields-on-the-page)。
* **[!UICONTROL Horizontal alignment]** （左、右、中央揃え） **[!UICONTROL Vertical alignment]** と（高、低、中央）、
* **[!UICONTROL Width]** の領域：これは、パーセンテージ、またはem、ポイント、またはピクセル（デフォルト値）で表すことができます。
* Maximum **[!UICONTROL Length]**: Maximum number of characters allowed (for Text, Number and Password type controls),
* **[!UICONTROL Lines]**:タイプゾーンの **[!UICONTROL Multi-line text]** 行数、
* **[!UICONTROL Style inline]**:を使用すると、CSSスタイルシートに追加の設定をオーバーロードできます。 これらは、次の例のように、**;** 文字を使用して区切られます。

   ![](assets/s_ncs_admin_survey_advanced_tab_inline.png)

### ヘッダーとフッターの定義 {#defining-headers-and-footers}

フィールドは、ルートがページと同じ名前のツリー構造で並んでいます。フィールドを選択して、名前を修正します。

The title of the window must be entered in the **[!UICONTROL Page]** tab of the form property window. また、ページヘッダーとフッターにセットコンテンツを追加できます（この情報は、すべてのページに表示されます）。This content is entered in the matching sections of the **[!UICONTROL Texts]** tab, as shown below:

![](assets/s_ncs_admin_survey_titles_config.png)

### HTML ヘッダーへの要素の追加 {#adding-elements-to-html-header}

フォームページの HTML ヘッダーに挿入する追加の要素を入力できます。To do this, enter the elements in the **[!UICONTROL Header]** tab of the relevant page.

これにより、例えば、ページのタイトルバーに表示されるアイコンを参照できます。

![](assets/webform_header_page_tab.png)

## コントロール設定の定義 {#defining-control-settings}

ユーザーがフォームに入力する際に、形式または設定に応じて、特定のフィールドに対するチェックが自動的に実行されます。This lets you make certain fields mandatory (refer to [Defining mandatory fields](#defining-mandatory-fields)) or check the format of the data entered (refer to [Checking data format](#checking-data-format)). （アウトバウンドトランジションを有効にするリンクまたはボタンをクリックすることで）ページの承認中にチェックが実行されます。

### 必須フィールドの定義 {#defining-mandatory-fields}

特定のフィールドを必須にするには、フィールドの作成時にこのオプションを選択します。

![](assets/s_ncs_admin_survey_required_field.png)

フィールドに入力することなく、ユーザーがこのページを承認すると、次のメッセージが表示されます。

![](assets/s_ncs_admin_survey_required_default_msg.png)

このメッセージは、リンクをクリックしてパーソナライズで **[!UICONTROL Personalize this message]** きます。

![](assets/s_ncs_admin_survey_required_custom_msg.png)

フィールドに入力することなく、ユーザーがこのページを承認すると、次のメッセージが表示されます。

![](assets/s_ncs_admin_survey_required_custom_msg2.png)

### データ形式のチェック {#checking-data-format}

その値がデータベースの既存のフィールドに格納されるフォームのチェックの場合、ストレージフィールドのルールが適用されます。

その値が変数に格納されるフォームのチェックの場合、承認ルールは変数の形式によって異なります。

For example, if you create a **[!UICONTROL Number]** check to store the client number, as shown below:

![](assets/s_ncs_admin_survey_choose_format.png)

ユーザーは、フォームフィールドに整数を入力する必要があります。

## フィールドの条件付き表示の定義 {#defining-fields-conditional-display}

ユーザーが選択した値に基づいて表示されるページでのフィールドの表示を設定できます。これは、1 つのフィールドまたはフィールドグループ（コンテナでグループ化されている場合）に適用できます。

For each element of the page, the **[!UICONTROL Visibility]** section lets you define the display conditions.

![](assets/s_ncs_admin_survey_condition_edit.png)

条件は、データベースフィールドまたは変数の値が関係する可能性があります。

フィールドの選択ウィンドウで、次のデータから選択できます。

![](assets/s_ncs_admin_survey_condition_select.png)

* メインツリーには、フォームコンテキストのパラメーターが含まれます。デフォルトパラメーターは、識別子（受信者の暗号化された識別子に一致）、言語および接触チャネルです。

   詳しくは、この[ページ](../../web/using/defining-web-forms-properties.md#form-url-parameters)を参照してください。

* The **[!UICONTROL Recipients]** sub-tree contains the input fields inserted into the form and stored in the database.

   詳しくは、「データベースへのデ [ータの格納」を参照してください](../../web/using/web-forms-answers.md#storing-data-in-the-database)。

* The **[!UICONTROL Variables]** sub-tree contains the available variables for this form. 詳しくは、「ローカル変数へのデ [ータの格納」を参照してください](../../web/using/web-forms-answers.md#storing-data-in-a-local-variable)。

詳しくは、次の使用例を参照してください。選択し [た値に応じて異なるオプションを表示](../../web/using/use-cases--web-forms.md#displaying-different-options-depending-on-the-selected-values)。

You can also condition the display of form pages using the **[!UICONTROL Test]** object. 詳しくは、この[ページ](../../web/using/defining-web-forms-page-sequencing.md#conditional-page-display)を参照してください。

## 既存のフォームからの要素のインポート {#importing-elements-from-an-existing-form}

他の Web フォームからフィールドまたはコンテナをインポートできます。これにより、アドレスブロック、ニュースレターの購読エリアなど、フォームに挿入される再利用可能なブロックのライブラリを作成できます。

要素をフォームに挿入するには、次の手順に従います。

1. Edit the page which you want to insert one or more elements into, then click **[!UICONTROL Import an existing block]** in the toolbar.

   ![](assets/s_ncs_admin_survey_import_block.png)

1. インポートするフィールドを含む Web フォームを選択し、インポートするコンテナおよびフィールドを選択します。

   ![](assets/s_ncs_admin_survey_import_block_selection.png)

   >[!NOTE]
   >
   >The **[!UICONTROL Edit link]** icon to the right of the source form name lets you view the selected Web form.

1. Click **[!UICONTROL Ok]** to confirm insertion.

   ![](assets/s_ncs_admin_survey_import_block_rendering.png)

