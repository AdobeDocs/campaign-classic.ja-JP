---
title: '"ユースケース：概要の作成"'
seo-title: '"ユースケース：概要の作成"'
description: '"ユースケース：概要の作成"'
seo-description: null
page-status-flag: never-activated
uuid: 404ae82b-2766-4802-8673-aaaa26868f46
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: web-applications
discoiquuid: a3834828-4d39-4699-b648-d399797b8ea7
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# ユースケース：概要の作成{#use-cases-creating-overviews}

次の例では、概要タイプの Web アプリケーションを作成して、データベースのすべての Web アプリケーションを表示します。次の要素を設定します。

* フォルダ上のフィルタ(フォ [ルダ上のフィルタの追加](#adding-a-filter-on-a-folder))、
* 新しいWebアプリケーションを作成するためのボタン( [新しいWebアプリケーションを設定するためのボタンの追加](#adding-a-button-to-configure-a-new-web-application))、
* 詳細表示をリスト内の各エントリに対して行う(詳 [細のリストへの追加](#adding-detail-to-a-list))、
* リンク編集ツールごとに1つのフィルター(リ [ンクエディターを使用したフィルターの作成](#creating-a-filter-using-a-link-editor))、
* 更新リンク(更新リン [クの作成を参照](#creating-a-refresh-link))。

![](assets/s_ncs_configuration_webapp_overview.png)

## 単一ページ Web アプリケーションの作成 {#creating-a-single-page-web-application}

1. Create a single **[!UICONTROL Page]** Web application and disable outbound transitions and transitions to the next page.

   ![](assets/s_ncs_configuration_webapp_create.png)

1. ページタイトルの変更

   このタイトルは、概要ヘッダーおよび Web アプリケーションの概要に表示されます。

1. In the Web application properties, modify the rendering of your application by selecting the **[!UICONTROL Single-page Web application]** template.

   ![](assets/s_ncs_configuration_webapp_rendering.png)

1. Webアプリケー **[!UICONTROL Page]** ションのアクティビティを開き、リストを開きま&#x200B;**[!UICONTROL Static element > List]**&#x200B;す()。
1. リストの **[!UICONTROL Data]** タブで、ドキュメントのタイプ、お **[!UICONTROL Web applications]** よび出力 **[!UICONTROL Label]** 列を **[!UICONTROL Creation date]** 選択 **[!UICONTROL Type of application]** します。
1. In the **[!UICONTROL Filter]** sub-tab, create the following filter as shown below in order to display Web applications only and exclude templates from your view.

   ![](assets/s_ncs_configuration_webapp_filter.png)

1. Close the configuration window of your page and click **[!UICONTROL Preview]**.

   データベースで使用可能な Web アプリケーションのリストが表示されます。

   ![](assets/s_ncs_configuration_webapp_preview.png)

## フォルダーのフィルターの追加 {#adding-a-filter-on-a-folder}

概要では、Adobe Campaign ツリーでの場所に応じてデータにアクセスすることを選択できます。これが、フォルダーのフィルターです。フォルダーのフィルターを概要に追加するには、次の手順に従います。

1. カーソルをウェブアプリケ **[!UICONTROL Page]** ーションのノードに置き、要素を追 **[!UICONTROL Select folder]** 加します(**[!UICONTROL Advanced controls > Select folder]**)。
1. 表示され **[!UICONTROL Storage]** るウィンドウで、リンクをクリック **[!UICONTROL Edit variables]** します。
1. ニーズに合わせて変数ラベルを変更します。
1. 値 **folder** で変数名を変更します。

   >[!NOTE]
   >
   >変数の名前は、フォルダーにリンクした要素の名前（スキーマで定義）に一致する必要があります（つまり、この場合は **folder**）。テーブルを参照する際に、この名前を再利用する必要があります。

1. 変数に **[!UICONTROL XML]** タイプを適用します。

   ![](assets/s_ncs_configuration_webapp_variable_xml.png)

1. インタラクションを **[!UICONTROL Refresh page]** 選択します。

   ![](assets/s_ncs_configuration_webapp_variable.png)

1. Place your cursor on your list, and in the **[!UICONTROL Advanced]** tab, reference the variable previously created in the **[!UICONTROL Folder filter XPath]** tab of the list. フォルダーリンクに関係している要素の名前（つまり **folder**）を使用する必要があります。

   ![](assets/s_ncs_configuration_webapp_variable002.png)

   >[!NOTE]
   >
   >この段階では、Web アプリケーションは、アプリケーションコンテキスト内にないので、フィルターは、フォルダーでテストできません。

## 新しい Web アプリケーションを設定するためのボタンの追加 {#adding-a-button-to-configure-a-new-web-application}

1. 要素にカーソルを置 **[!UICONTROL Page]** き、リンクを追加しま&#x200B;**[!UICONTROL Static elements > Link]**&#x200B;す()。
1. 概要のボタンに表示されるので、リンクラベルを修正します。

   この例では、ラベルは &quot;**New**&quot; です。

1. 「URL」フィールドに次のURLを挿入します。xtk://open/?schema=nms:webApp&amp;form=nms:newWebApp ****.

   >[!NOTE]
   >
   >**nms:webApp** は、Web アプリケーションスキーマと一致します。
   >
   >**nms:newWebApp** は、新しい Web アプリケーション作成ウィザードと一致します。

1. URL を同じウィンドウで表示することを選択します。
1. 画像フィールドにWebアプリケーションアイコンを追加します。/nms/img/webApp.png ****.

   This icon will appear on the **[!UICONTROL New]** button.

1. Enter **button** in the **[!UICONTROL Style]** field.

   This style is referred to in the **[!UICONTROL Single-page Web application]** template selected previously.

   ![](assets/s_ncs_configuration_webapp_link.png)

## リストへの詳細の追加 {#adding-detail-to-a-list}

概要でリストを設定する場合、リストの各エントリに関する追加の詳細を表示することを選択できます。

1. 前に作成したリスト要素にカーソルを置きます。
1. タブのド **[!UICONTROL General]** ロップダウンリスト **[!UICONTROL Columns and additional detail]** で表示モードを選択します。

   ![](assets/s_ncs_configuration_webapp_detail.png)

1. タブで、 **[!UICONTROL Data]** 列、および列を追 **[!UICONTROL Primary key]** 加し **[!UICONTROL Internal name]** 、各 **[!UICONTROL Description]** オプション **[!UICONTROL Hidden field]** を選択します。

   ![](assets/s_ncs_configuration_webapp_detail002.png)

   これで、この情報は、各エントリの詳細にのみ表示されます。

1. In the **[!UICONTROL Additional detail]** tab, add the following code:

   ```
   <div class="detailBox">
     <div class="actionBox">
       <span class="action"><img src="/xtk/img/fileEdit.png"/><a title="Open" class="linkAction" href="xtk://open/?schema=nms:webApp&form=nms:webApp&pk=
       <%=webApp.id%>">Open...</a></span>
       <% 
       if( webApp.@appType == 1 ) { //survey
       %>
       <span class="action"><img src="/xtk/img/report.png"/><a target="_blank" title="Reports" class="linkAction" href="/xtk/report.jssp?_context=selection&
         _schema=nms:webApp&_selection=<%=webApp.@id%>
         &__sessiontoken=<%=document.controller.getSessionToken()%>">Reports</a></span>
       <% 
       } 
       %>
     </div>
     <div>
       Internal name: <%= webApp.@internalName %>
     </div>
     <%
     if( webApp.desc != "" )
     {
     %>
     <div>
       Description: <%= webApp.desc %>
     </div>
     <% 
     } 
     %>
   </div>
   ```

>[!NOTE]
>
>JavaScript ライブラリは、サーバー上で更新するのに 5 分かかります。サーバーを再起動して、この遅延を待機するのを回避できます。

## リストのフィルターと更新 {#filtering-and-updating-the-list}

ここでは、特定のオペレーターによって作成された Web アプリケーションの概要を表示するフィルターを作成します。このフィルターは、リンクエディターで作成されます。オペレーターを選択したら、リストを更新してフィルターを適用します。これには、更新リンクを作成する必要があります。

これら 2 つの要素は、概要で視覚的にグループ化させるために、同じコンテナにグループ化されます。

1. カーソルを要素に合わせ、 **[!UICONTROL Page]** を選択します **[!UICONTROL Container > Standard]**。
1. 列数を &quot;**2**&quot; に設定し、リンクエディターおよびリンクがお互い隣になるようにします。

   ![](assets/s_ncs_configuration_webapp_container.png)

   要素のレイアウトについては、[この節](../../web/using/about-web-forms.md)を参照してください。

1. **dottedFilter** を適用します。

   This style is referred to in the **[!UICONTROL Single-page Web applicatio]** n template selected previously.

   ![](assets/s_ncs_configuration_webapp_container002.png)

### リンクエディターを使用したフィルターの作成 {#creating-a-filter-using-a-link-editor}

1. Place your cursor on the container created during the previous stage and insert a link editor via the **[!UICONTROL Advanced controls]** menu.
1. In the storage window which opens automatically, select the **[!UICONTROL Variables]** option, then click the **[!UICONTROL Edit variables]** link and create an XML variable for filtering data.

   ![](assets/s_ncs_configuration_webapp_variable003.png)

1. ラベルを修正します。

   It will appear next to the **[!UICONTROL Filter]** field in the overview.

1. アプリケーションスキーマとしてオペレーターテーブルを選択します。

   ![](assets/s_ncs_configuration_webapp_linkeditor.png)

1. Place your cursor on the list element and create a filter via the **[!UICONTROL Data > Filter]** tab:

   * **** 式：「作成者」リンクの外部キー
   * **演算子：**&#x200B;等しい
   * **** 値：変数（変数）
   * **** 次の場合に考慮します。&#39;$(var2/@id)&#39;!=&quot;
   ![](assets/s_ncs_configuration_webapp_filter002.png)

>[!CAUTION]
>
>Web アプリケーションユーザーは、情報にアクセスするための適切な Adobe Campaign 権限を持つ識別されたオペレーターである必要があります。このタイプの設定は、匿名 Web アプリケーションに対しては機能しません。

### 更新リンクの作成 {#creating-a-refresh-link}

1. Place the cursor on the container and insert a **[!UICONTROL Link]** via the **[!UICONTROL Static elements]** menu.
1. ラベルを修正します。
1. 選択 **[!UICONTROL Refresh data in a list]**.
1. 前に作成したリストを追加します。

   ![](assets/s_ncs_configuration_webapp_refreshlink.png)

1. フィールドに更新アイコンを追加 **[!UICONTROL Image]** します。**/xtk/img/refresh.png **.
1. 次に示すように、並べ替え矢印を使用して、Web アプリケーションの様々な要素を認識します。

   ![](assets/s_ncs_configuration_webapp_orderelements.png)

これで、Web アプリケーションが設定されました。You can click the **[!UICONTROL Preview]** tab to preview it.

![](assets/s_ncs_configuration_webapp_result.png)

