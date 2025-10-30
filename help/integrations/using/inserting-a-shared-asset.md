---
product: campaign
title: 共有アセットを挿入
description: 共有アセットを挿入
feature: Asset Sharing
audience: integrations
content-type: reference
topic-tags: asset-sharing
exl-id: 30a94bce-6d96-4a6d-a62f-7451c822f0e3
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: ht
source-wordcount: '233'
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

   Adobe Campaign インスタンスの設定により、Adobe Experience Cloud ライブラリまたは AEM Assets ライブラリからの画像を使用できます。[Assets へのアクセスの設定](../../integrations/using/configuring-access-to-assets.md)の節を参照してください。

   ![](assets/dam_shared_image_selection.png)

>[!NOTE]
>
>Adobe Target との統合を使用している場合、共有画像をデフォルト画像として使用できます。[このページ](../../integrations/using/integrating-with-adobe-target.md)を参照してください。
