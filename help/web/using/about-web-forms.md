---
title: Web フォームについて
seo-title: Web フォームについて
description: Web フォームについて
seo-description: null
page-status-flag: never-activated
uuid: 1d129af4-008b-4f6a-9094-b2edd6c1eee1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: web-forms
discoiquuid: 3b8e4691-fcbc-48ef-b529-11c9a9a9d788
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# Web フォームについて{#about-web-forms}

Adobe Campaign には、Web フォームを定義して公開するためのグラフィカルなモジュールが統合されており、入力および選択フィールドを含むページを作成して、データベースからのデータを含めることができます。これにより、ユーザーがアクセスして情報を表示または入力できる Web ページをデザインおよび投稿できます。

この章では、Web フォームの作成と管理、フィールドとページの管理方法、およびストレージとモードの保存について詳しく説明します。

>[!CAUTION]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

## Web フォームを作成する手順 {#steps-for-creating-a-web-form}

ここでは、Adobe Campaign の **webForm** タイプをデザインするのに必要な手順と、利用可能なオプションおよび設定について説明します。Adobe Campaign を使用して、作成した Web フォームをユーザーが利用できるようにし、回答を収集してデータベースにアーカイブします。

>[!CAUTION]
>
>WebアプリケーションおよびWebフォームを設定する場合は、最低900ピクセルの垂直解像度が必要です(例：1600 x 900)。

Web forms are accessed via the Web Applications menu of the **Campaigns** tab. Adobe Campaignツリーでは、ノードの下にグループ化され **[!UICONTROL Resources > Online > Web Applications]** ます。

To create a Web form, click the **[!UICONTROL Create]** button above the list of Web applications.

![](assets/webapp_create_new.png)

Web フォームテンプレートを選択します（デフォルトは **[!UICONTROL newWebForm]**）。

![](assets/s_ncs_admin_survey_select_template.png)

これにより、フォームのダッシュボードが表示されます。

![](assets/webapp_empty_dashboard.png)

The **[!UICONTROL Edit]** tab lets you create your content.

![](assets/webapp_edit_tab.png)

Web フォームの設定とコンテンツを定義するには、次の手順に従います。

* 最初に、必要なページを作成し、入力フィールド、ドロップダウンリスト、HTML コンテンツなどをチェックします。

   この手順は、以下で詳しく説明します。

* ページの順番を定義し、表示を調節します。

   この手順の詳細は、「Webフォーム [ページの順序付けの定義」で説明します](../../web/using/defining-web-forms-page-sequencing.md)。

* 必要に応じて、コンテンツを翻訳します。

   この手順は、Webフォームの [翻訳で詳しく説明します](../../web/using/translating-a-web-form.md)。

## Web フォームの設計について {#about-web-forms-designing}

フォームのページは、入力ゾーン（テキスト）、選択フィールド（リスト、チェックボックスなど）および静的要素（画像、HTLM コンテンツなど）を定義および設定できる、専用のエディターで作成されます。They can be grouped into containers and their layout altered to suit your needs (for more on this, refer to [Creating containers](../../web/using/defining-web-forms-layout.md#creating-containers)).

以降の節では、フォーム画面のコンテンツとレイアウトの定義方法について説明します。

* [Web フォームへのフィールドの追加](../../web/using/adding-fields-to-a-web-form.md),
* [HTML コンテンツの挿入](../../web/using/static-elements-in-a-web-form.md#inserting-html-content),
* [Web フォームの静的要素](../../web/using/static-elements-in-a-web-form.md),
* [Web フォームレイアウトの定義](../../web/using/defining-web-forms-layout.md).

>[!NOTE]
>
>* During page design, you can view the final rendering in the **[!UICONTROL Preview]** tab. 変更を表示するには、最初にフォームを保存します。Any errors are displayed in the **[!UICONTROL Log]** tab.
>* ページの表示と情報ストレージが適切な順序でおこなわれることを確認するには、Web フォームのデバッグモードを有効にします。To do this, go to the **[!UICONTROL Preview]** sub-tab and check the **[!UICONTROL Enable debug mode]** box: all collected information and possible execution errors will be displayed at the bottom of each page.
>



### ツールバーのアイコンの使用 {#using-the-icons-in-the-toolbar}

ツールバーのアイコンまたは右クリックを使用して入力ゾーンを挿入することもできます。

![](assets/s_ncs_admin_webform_add_selection.png)

この場合、まず追加するフィールドのタイプを選択してから、回答ストレージモードを選択します。

![](assets/s_ncs_admin_webform_select_storage.png)

「**[!UICONTROL Ok]**」をクリックして、選択を承認します。

![](assets/s_ncs_admin_webform_confirm_storage.png)

