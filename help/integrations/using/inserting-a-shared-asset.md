---
title: 共有アセットを挿入
seo-title: 共有アセットを挿入
description: 共有アセットを挿入
seo-description: null
page-status-flag: never-activated
uuid: ab661bfd-d0a3-4b5c-ba52-4c76c834d584
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: asset-sharing
discoiquuid: 3d01cc7e-5685-4101-bf4b-ef5f6e52b3c9
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0745b9c9d72538b8573ad18ff4054ecf788905f2

---


# 共有アセットを挿入{#inserting-a-shared-asset}

Adobe Experience Cloud から共有されるアセットは、E メールやランディングページで次のように使用できます。

1. 新しい E メールまたは新しいランディングページを作成します。

   Adobe Experience Manager Assets ライブラリのアセットを使用する場合は、[統合を設定](../../integrations/using/configuring-access-to-assets.md#integrating-with-aem-assets)したときに作成した配信テンプレートを使用します。

   If you do not have this specific template, make sure that in the delivery **Properties**, the **[!UICONTROL Content editing mode]** (**[!UICONTROL Advanced]** tab) is set to **DCE** and that the AEM external account that you want to use for accessing your AEM Assets resource library is provided.

1. 編集ウィンドウで、「画像を追加」オプションを選択します。

   * 標準編集モードを使用し [ている場合は](../../delivery/using/defining-the-email-content.md#adding-images)、/を選 **[!UICONTROL Image]** 択しま **[!UICONTROL Select a shared asset]**&#x200B;す。

      ![](assets/dam_insert_image_standard.png)

   * If you are using the [advanced editing mode](../../web/using/about-campaign-html-editor.md) (DCE), go to an image block, then via the contextual menu, select **[!UICONTROL Select a shared asset]**.

      ![](assets/dam_insert_image_dce.png)

      >[!NOTE]
      >
      >DCE を使用している場合、[Web にアクセス](../../platform/using/adobe-campaign-workspace.md#console-and-web-access)している Adobe Campaign から共有画像を挿入することはできません。

1. 表示される選択ウィンドウで画像を選択し、確定します。

   Adobe Campaign インスタンスの設定により、Adobe Experience Cloud ライブラリまたは AEM Assets ライブラリからの画像を使用できます。「アセットへのア [クセスの設定](../../integrations/using/configuring-access-to-assets.md) 」を参照。

   ![](assets/dam_shared_image_selection.png)

>[!NOTE]
>
>Adobe Target との統合を使用している場合、共有画像をデフォルト画像として使用できます。[このページ](../../integrations/using/integrating-with-adobe-target.md)を参照してください。

