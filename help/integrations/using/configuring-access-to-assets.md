---
product: campaign
title: Assets へのアクセスの設定
description: Assets へのアクセスの設定
audience: integrations
content-type: reference
topic-tags: asset-sharing
exl-id: f3897a40-b080-47e5-9e31-4d861c1bacd5
source-git-commit: eb630b29dba8cc34046e2f14e9ed6ba8c017ea5d
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 86%

---

# Assets へのアクセスの設定{#configuring-access-to-assets}

この節では、Adobe Campaignで、AssetsコアサービスまたはAdobe Experience Manager Assets(AEM Assets)ライブラリとの統合機能を使用するために必要な設定手順について説明します。

>[!CAUTION]
>
>これらの統合は同時におこないます。次の情報をよく読んでから設定をおこなってください。

* **Experience Cloud Assets** との統合：この統合により、Adobe Experience Cloud ライブラリから画像を挿入できます。この統合は、Adobe Campaign に **[!UICONTROL Adobe Experience Cloud との統合]**&#x200B;組み込みパッケージをインストールすることによって設定する必要があります。
* **AEM Assets**&#x200B;との統合：この統合により、Adobe Experience Manager Assetsライブラリから画像を挿入できます。 この統合は、Adobe Campaign に **[!UICONTROL AEM 統合]**&#x200B;組み込みパッケージをインストールすることによって設定する必要があります。この統合は、Adobe Experience Manager 6.5では使用できなくなりました。

>[!NOTE]
>
>2 つのパッケージ（**[!UICONTROL AEM 統合]**&#x200B;および **[!UICONTROL Adobe Marketing Experience との統合]**）がインストールされている場合、Adobe Experience Cloud ライブラリで使用可能なアセットだけを使用できます。

## Experience Cloud Assets との統合 {#integrating-with-experience-cloud-assets}

Adobe Campaign と Experience Cloud Assets 間の統合を使用するには、次が必要です。

* Adobe Experience Cloud 組織
* Adobe IMS 認証モードが有効であること

Adobe Campaign と Adobe Experience Cloud の間の接続を有効化するには、IMS（Adobe ID 接続サービス）を介して接続を設定します。この設定について詳しくは、[Adobe ID を使用して接続](../../integrations/using/about-adobe-id.md)ドキュメントで説明しています。設定時には以下をおこないます。

* **[!UICONTROL Adobe Experience Cloud との統合]**&#x200B;パッケージのインストール
* Adobe Experience Cloud 外部アカウントの設定

>[!NOTE]
>
>この統合に関連する機能は、IMS から Adobe ID を使用して接続するユーザーだけが使用できます。

## AEM Assets との統合 {#integrating-with-aem-assets}


>[!CAUTION]
>
>この機能は、Adobe Experience Manager 6.5以降では廃止されています。 [詳細](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/deprecated-removed-features.html?lang=en#removed-features)

AEM Assets と Adobe Campaign を統合するには、まず Adobe Experience Manager と Adobe Campaign 間の統合を設定する必要があります。この設定には、主に次のことが必要になります。

* **[!UICONTROL AEM 統合]**&#x200B;組み込みパッケージのインストール
* Adobe Experience Manager に特有の外部アカウントの設定

Adobe Campaign と Adobe Experience Manager を統合する方法については、[詳細ドキュメント](../../integrations/using/about-adobe-experience-manager.md)を参照してください。

この統合を設定した後は、AEM Assets ライブラリを使用する新しい配信テンプレートを Adobe Campaign で設定できます。これをおこなうには、以下の手順に従います。

1. 新しい配信テンプレートを作成するか、既存の配信テンプレートを複製します。配信テンプレートについて詳しくは、[このページ](../../delivery/using/about-templates.md)を参照してください。
1. このテンプレートの&#x200B;**プロパティ**&#x200B;を編集します。
1. 「**[!UICONTROL 詳細設定]**」タブで、「**[!UICONTROL コンテンツ編集モード]**」を「**DCE**」に設定します。
1. AEM Assets ライブラリへのアクセスに使用する必要がある外部の **[!UICONTROL AEM アカウント]**&#x200B;を選択します。

   ![](assets/dam_aem_assets1.png)

このテンプレートに基づいて配信コンテンツに画像を挿入する場合、「**[!UICONTROL 共有アセットを選択]**」オプションを使用して AEM Assets ライブラリの画像を参照できます。詳しくは、[この節](../../integrations/using/inserting-a-shared-asset.md)を参照してください。

>[!NOTE]
>
>**[!UICONTROL Adobe Experience Cloud との統合]**&#x200B;パッケージも Adobe Campaign インスタンスにインストールされている場合、Adobe Experience Cloud ライブラリで使用可能なアセットだけを使用することができます。AEM Assets ライブラリのアセットにもアクセスするには、AEM Assets と Adobe Experience Cloud を同期する必要があります。AEM Assets 内のアセットも、Adobe Experience Cloud ライブラリで使用可能になります。その場合、特定の配信テンプレートを作成する必要はありません。AEM Assets と Adobe Experience Cloud 間の同期について詳しくは、[詳細ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/configure-assets-cc-integration.html?lang=ja#integration)を参照してください。
