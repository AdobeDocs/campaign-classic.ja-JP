---
product: campaign
title: 共有アセットを挿入
description: 共有アセットを挿入
feature: Asset Sharing
audience: integrations
content-type: reference
topic-tags: asset-sharing
exl-id: 30a94bce-6d96-4a6d-a62f-7451c822f0e3
TQID: 'https://experienceleague.adobe.com/5SrvIw1sYSNd4Hw1we554AfxDj3VgeTeqIOOzTTrWuY'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
    internal-label: Integrations
subfeature_v2:
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
    internal-label: Analytics integration
  - id: df0d6518-6f49-46e2-b46e-3bcc513f553f
    internal-label: Experience Manager integration
  - id: eb007b6d-6e57-46ab-9485-3f24d6102304
    internal-label: Experience Platform integration
  - id: b1fd1501-3105-4d6b-b4d4-9af53126df75
    internal-label: Target integration
  - id: 2e08b477-1993-5928-975d-5f4cabe8fbe0
    internal-label: Asset Sharing
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 100%
---
# 共有アセットを挿入{#inserting-a-shared-asset}

Adobe Experience Cloud から共有されるアセットは、メールやランディングページで次のように使用できます。

1. 新しいメールまたは新しいランディングページを作成します。

   Adobe Experience Manager Assets ライブラリのアセットを使用する場合は、[統合を設定](../../integrations/using/configuring-access-to-assets.md#integrating-with-aem-assets)したときに作成した配信テンプレートを使用します。

   この特定のテンプレートがない場合、配信の&#x200B;**プロパティ**&#x200B;で、「**[!UICONTROL コンテンツ編集モード]**」（「**[!UICONTROL 詳細]**」タブ）が「**DCE**」に設定され、AEM Assets リソースライブラリへのアクセスに使用する AEM 外部アカウントが入力されていることを確認してください。

1. 編集ウィンドウで、「画像を追加」オプションを選択します。

   * [標準編集モード](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/defining-the-email-content.html?lang=ja#adding-images){target="_blank"}を使用している場合、**[!UICONTROL 画像]**／**[!UICONTROL 共有アセットを選択]**&#x200B;を選択します。

     ![](assets/dam_insert_image_standard.png)

   * [詳細編集モード](../../web/using/about-campaign-html-editor.md)（DCE）を使用している場合、画像ブロックに移動し、コンテキストメニューから「**[!UICONTROL 共有アセットを選択]**」を選択します。

     ![](assets/dam_insert_image_dce.png)

     >[!NOTE]
     >
     >DCE を使用している場合、[Web にアクセス](../../platform/using/adobe-campaign-workspace.md#console-and-web-access)している Adobe Campaign から共有画像を挿入することはできません。

1. 表示される選択ウィンドウで画像を選択し、確定します。

   Adobe Campaign インスタンスの設定により、Adobe Experience Cloud ライブラリまたは AEM Assets ライブラリからの画像を使用できます。 [Assets へのアクセスの設定](../../integrations/using/configuring-access-to-assets.md)の節を参照してください。

   ![](assets/dam_shared_image_selection.png)

>[!NOTE]
>
>Adobe Target との統合を使用している場合、共有画像をデフォルト画像として使用できます。 [このページ](../../integrations/using/integrating-with-adobe-target.md)を参照してください。
