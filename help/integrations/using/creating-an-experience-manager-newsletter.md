---
title: Experience Manager ニュースレターの作成
seo-title: Experience Manager ニュースレターの作成
description: Experience Manager ニュースレターの作成
seo-description: null
page-status-flag: never-activated
uuid: 75cf4891-06a6-42d2-9b22-b4d93e0dc64a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
discoiquuid: 627ade78-96b3-4a6e-9ace-74610a3c8d1a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0745b9c9d72538b8573ad18ff4054ecf788905f2

---


# Experience Manager ニュースレターの作成{#creating-an-experience-manager-newsletter}

この統合を利用して、例えば、Adobe Experience Manager で作成したニュースレターを Adobe Campaign で E メールキャンペーンの一部として使用できます。

この統合を利用する方法の詳細な例については、この[詳細な手順ガイド](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/aem.html)を参照してください。

**Adobe Experience Manager から：**

1. From your AEM author instance, click the **Adobe Experience** logo in the upper left side of the page and select **[!UICONTROL Sites]**.

   ![](assets/aem_uc_1.png)

1. 選択 **[!UICONTROL Campaigns > Name of your brand (here We.Retail) > Master Area > Email campaigns]**.
1. Click the **[!UICONTROL Create]** button in the upper right side of the page then select **[!UICONTROL Page]**.

   ![](assets/aem_uc_2.png)

1. テンプレートを選 **[!UICONTROL Adobe Campaign Email (AC 6.1)]** 択し、ニュースレターに名前を付けます。
1. ページを作成したら、メニューにアクセスし **[!UICONTROL Page information]** てをクリックしま **[!UICONTROL Open Properties]**&#x200B;す。

   ![](assets/aem_uc_3.png)

1. タブで、2 **[!UICONTROL Cloud Services]** つ目のドロッ **[!UICONTROL Adobe Campaign]** プダウン **[!UICONTROL Cloud service configuration]** から「as」を選択し、Adobe Campaignインスタンスを選択します。

   ![](assets/aem_uc_4.png)

1. Adobe Campaign のパーソナライゼーションフィールドなどのコンポーネントを追加して E メールコンテンツを編集します。
1. 電子メールの準備が整ったら、メニューにアクセスし **[!UICONTROL Page information]** てをクリックしま **[!UICONTROL Start workflow]**&#x200B;す。

   ![](assets/aem_uc_5.png)

1. 最初のドロップダウンから、「ワークフローモデル」 **[!UICONTROL Publish to Adobe Campaign]** を選択し、をクリックしま **[!UICONTROL Start workflow]**&#x200B;す。

   ![](assets/aem_uc_6.png)

1. 次に、前の手順として、ワークフローを起動 **[!UICONTROL Approve for Campaign]** します。
1. ページの上部に免責事項が表示されます。Click **[!UICONTROL Complete]** to confirm the review and click **[!UICONTROL Ok]**.

   ![](assets/aem_uc_7.png)

1. もう一度クリ **[!UICONTROL Complete]** ックし、ド **[!UICONTROL Newsletter approval]** ロップダウ **[!UICONTROL Next Step]** ンでを選択します。

   ![](assets/aem_uc_8.png)

これでニュースレターが準備でき、Adobe Campaign で同期されました。

**Adobe Campaign から：**

1. タブで、「 **[!UICONTROL Campaigns]** 次へ」をクリッ **[!UICONTROL Deliveries]** クしま **[!UICONTROL Create]**&#x200B;す。

   ![](assets/aem_uc_9.png)

1. ドロップダウ **[!UICONTROL Delivery template]** ンで、テンプレートを選択 **[!UICONTROL Email delivery with AEM content (mailAEMContent)]** します。

   ![](assets/aem_uc_10.png)

1. Add a **[!UICONTROL Label]** to your delivery and click **[!UICONTROL Continue]**.
1. ボタンをクリッ **[!UICONTROL Synchronize]** クします。

   If this button does not appear in your interface, click the **[!UICONTROL Properties]** button and select the **[!UICONTROL Advanced]** tab. このフ **[!UICONTROL Content editing mode]** ィールドは、フィールド内のAEM **[!UICONTROL AEM]** インスタンスを使用してに設定する必要があ **[!UICONTROL AEM account]** ります。

   ![](assets/aem_uc_11.png)

1. 以前に Adobe Experience Manager で作成した配信を選択し、「**[!UICONTROL Ok]**」をクリックします。
1. Click the **[!UICONTROL Refresh content]** button as soon as some changes are made to your AEM delivery.

   ![](assets/aem_uc_12.png)

これで E メールをオーディエンスに送信する準備が整いました。
