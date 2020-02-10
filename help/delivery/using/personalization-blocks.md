---
title: パーソナライゼーションブロック
seo-title: パーソナライゼーションブロック
description: パーソナライゼーションブロック
seo-description: null
page-status-flag: never-activated
uuid: f9867f8d-f6ce-4a5f-b6b4-fd8056d28576
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: personalizing-deliveries
discoiquuid: e68d1435-70e6-479e-a347-9ff9f9f11b92
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# パーソナライゼーションブロック{#personalization-blocks}

パーソナライゼーションブロックは動的なもので、パーソナライズされています。そこには、配信に挿入できる特定のレンダリングが格納されています。例えば、ロゴ、挨拶メッセージまたはミラーページへのリンクを追加できます。詳しくは、パーソ [ナライゼーションブロックの挿入を参照してくださ](#inserting-personalization-blocks)い。

>[!NOTE]
>
>パーソナライゼーションブロックは、からも利用できま **[!UICONTROL Digital Content Editor (DCE)]** す。 詳しくは、[このページ](../../web/using/editing-content.md#inserting-a-personalization-block)を参照してください。

パーソナライゼーションブロックは、Adobe Campaignエク **[!UICONTROL Resources > Campaign Management > Personalization blocks]** スプローラーのノードを介してアクセスします。 デフォルトでは複数のブロックを使用できます( [標準搭載のパーソナライゼーションブロックを参照](#out-of-the-box-personalization-blocks))。

新しいブロックを定義して、配信のパーソナライゼーションを最適化することもできます。詳しくは、「カスタムパーソナライゼーションブ [ロックの定義」を参照してくださ](#defining-custom-personalization-blocks)い。

## パーソナライゼーションブロックの挿入 {#inserting-personalization-blocks}

パーソナライゼーションブロックをメッセージに挿入するには、以下の手順に従います。

1. In the content editor of the delivery wizard, click the personalized field icon and select the **[!UICONTROL Include]** menu.
1. Select a personalization block from the list (the list displays the 10 last used blocks), or click the **[!UICONTROL Other...]** menu to access the full list.

   ![](assets/s_ncs_user_personalized_block01.png)

1. このメ **[!UICONTROL Other...]** ニューを使用すると、すべての既製パーソナライゼーションブロックとカスタムパーソナライゼーションブロックにアクセスできます( [Out-of-the-personalization blocks](#out-of-the-box-personalization-blocks) および [Defining custom personalization blocks](#defining-custom-personalization-blocks)を参照)。

   ![](assets/s_ncs_user_personalized_block02.png)

1. パーソナライゼーションブロックがスクリプトとして挿入されます。パーソナライゼーションが生成されると、受信者プロファイルに自動的に適応されます。

   ![](assets/s_ncs_user_personalized_block03.png)

1. Click the **[!UICONTROL Preview]** tab and select a recipient to view the personalization.

   ![](assets/s_ncs_user_personalized_block04.png)

配信コンテンツには、パーソナライゼーションブロックのソースコードを含めることができます。これを行うには、選択時に **[!UICONTROL Include the HTML source code of the block]** を選択します。

![](assets/s_ncs_user_personalized_block05.png)

HTML ソースコードが配信コンテンツに挿入されます。For example, the **[!UICONTROL Greetings]** personalization bloc displays as below:

![](assets/s_ncs_user_personalized_block06.png)

## パーソナライゼーションブロックの例 {#personalization-blocks-example}

この例では、パーソナライゼーションブロックを使用して、受信者によるミラーページの表示、ソーシャルネットワークでのニュースレターの共有、今後の配信の購読解除が可能な E メールを作成します。

そのためには、次のパーソナライゼーションブロックを挿入する必要があります。

* **[!UICONTROL Link to mirror page]** .
* **[!UICONTROL Social network sharing links]** .
* **[!UICONTROL Unsubscription link]** .

>[!NOTE]
>
>ミラーページの生成の詳細については、「ミラーページの [生成」を参照してください](../../delivery/using/sending-messages.md#generating-the-mirror-page)。

1. 新しい配信を作成するか、E メールタイプの既存の配信を開きます。
1. In the delivery wizard, click **[!UICONTROL Subject]** to edit the subject of the message and enter a subject.
1. メッセージ本文にパーソナライゼーションブロックを挿入します。To do this, click in the message content, click the personalized field icon and select the **[!UICONTROL Include]** menu.
1. 挿入する最初のブロックを選択します。上記の手順を繰り返して他の 2 つのブロックも挿入します。

   ![](assets/s_ncs_user_personalized_block_example.png)

1. Click the **[!UICONTROL Preview]** tab to view the personalization result. 受信者に応じたメッセージを確認するには、受信者を選択する必要があります。

   ![](assets/s_ncs_user_personalized_block_example2.png)

1. ブロックコンテンツが適切に表示されていることを確認します。

## 標準パーソナライゼーションブロック {#out-of-the-box-personalization-blocks}

デフォルトでは、メッセージコンテンツのパーソナライゼーションに役立つパーソナライゼーションブロックのリストが使用可能になっています。

>[!NOTE]
>
>パーソナライゼーションブロックのリストは、お使いのインスタンスにインストールされているモジュールやオプションによって異なります。

![](assets/s_ncs_user_personalized_block_list.png)

* **[!UICONTROL Greetings]** :受信者の名前を含む挨拶を挿入します。 例：「こんにちは、ジョン・ドウ。」
* **[!UICONTROL Insert logo]** :インスタンスの設定時に定義された、あらかじめ用意されているロゴを挿入します。
* **[!UICONTROL Powered by Adobe Campaign]** :「Powered by Adobe Campaign」ロゴを挿入します。
* **[!UICONTROL Mirror page URL]** :ミラーページのURLを挿入し、配信デザイナーがリンクを確認できるようにします。

   >[!NOTE]
   >
   >ミラーページの生成の詳細については、「ミラーページの [生成」を参照してください](../../delivery/using/sending-messages.md#generating-the-mirror-page)。

* **[!UICONTROL Link to mirror page]** :ミラーページへのリンクを挿入します。このメッセージを正しく表示できない場合は、ここをクリックしてください。
* **[!UICONTROL Unsubscription link]** :すべての配信（ブラックリスト）からの登録解除を可能にするリンクを挿入します。
* **[!UICONTROL Formatting function for proper nouns]** :javascript関数を **[!UICONTROL toSmartCase]** 生成します。この関数は、各単語の最初の文字を大文字に変更します。 This block must be inserted in the source code of the delivery, into **`<script>...</script>`** tags.

   次の例では、この関数を使用して、「My header」という要素を「My new header」という名前で各単語の大文字に置き換えています。

   ```
   <h1 id="sample">My header</h1>
   <script><%@ include view='toSmartCase'%>;
   document.getElementById("sample").innerHTML = toSmartCase("My new header");
   </script>
   ```

   ![](assets/s_ncs_user_personalized_block_uppercasefunction.png)

* **[!UICONTROL Registration page URL]** :購読URLを挿入します(サービスと購読 [についてを参照](../../delivery/using/about-services-and-subscriptions.md))。
* **[!UICONTROL Registration link]** :購読リンクを挿入します。 」は、インスタンスの設定時に定義されています。
* **[!UICONTROL Registration link (with referrer)]** :訪問者と配信を識別できるように、購読リンクを挿入します。 このリンクは、インスタンスの設定時に定義されたものです。

   >[!NOTE]
   >
   >このブロックは、訪問者をターゲットとする配信でのみ使用できます。

* **[!UICONTROL Registration confirmation]** :購読を確認するリンクを挿入します。
* **[!UICONTROL Social network sharing links]** :受信者が電子メールクライアント、Facebook、Twitter、Google +およびLinkedInとミラーページコンテンツへのリンクを共有できるボタンを挿入します(クチコミマーケティ [ングを参照：友人に転送する](../../delivery/using/viral-and-social-marketing.md#viral-marketing--forward-to-a-friend))。
* **[!UICONTROL Style of content emails]** および **[!UICONTROL Notification style]** :事前に定義されたHTMLスタイルで電子メールをフォーマットするコードを生成します。 These blocks must be inserted in the source code of the delivery, in the **[!UICONTROL ...]** section, into **`<style>...</style>`** tags.
* **[!UICONTROL Offer acceptance URL in unitary mode]** :インタラクションオファーをに設定できるURLを挿入します( **[!UICONTROL Accepted]** この節 [を参照](../../interaction/using/offer-analysis-report.md))。

## カスタムパーソナライゼーションブロックの定義 {#defining-custom-personalization-blocks}

You can define new personalization fields to be inserted from the personalized field icon via the **[!UICONTROL Include...]** menu. それらのフィールドは、パーソナライゼーションブロック内に定義されます。

パーソナライゼーションブロックを作成するには、エクスプローラーを開き、次の手順に従います。

1. ノードをクリッ **[!UICONTROL Resources > Campaign Management > Personalization blocks]** クします。
1. Right-click the list of blocks and select **[!UICONTROL New]** .
1. 次のように、パーソナライゼーションブロックの設定に入力します。

   ![](assets/s_ncs_user_personalized_block.png)

   * ブロックのラベルを入力します。このラベルは、パーソナライゼーションフィールドの挿入ウィンドウに表示されます。
   * パーソナラ **[!UICONTROL Visible in the customization menus]** イゼーションフィールド挿入アイコンからこのブロックにアクセスできるようにする場合に選択します。
   * 必要に応じて、HTML形式の電 **[!UICONTROL The content of the personalization block depends upon the format]** 子メールとテキスト形式の電子メールに対して2つの異なるブロックを定義する場合に選択します。

      このエディターの下部のセクションに、HTML コンテンツとテキストコンテンツを定義するためのタブが合わせて 2 つ表示されます。

      ![](assets/s_ncs_user_personalized_block_b.png)

   * Enter the content (in HTML, text, JavaScript, etc.) of the personalization block(s) and click **[!UICONTROL Save]** .
