---
title: Assets へのアクセスの設定
seo-title: Assets へのアクセスの設定
description: Assets へのアクセスの設定
seo-description: null
page-status-flag: never-activated
uuid: dc8c0016-92c8-41ab-98c6-d0fe0bfd6c41
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: asset-sharing
discoiquuid: df1b6ead-3471-404a-b43f-a68fb86cb14c
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0745b9c9d72538b8573ad18ff4054ecf788905f2

---


# Assets へのアクセスの設定{#configuring-access-to-assets}

この節では、Assets コアサービスまたは Adobe Experience Manager Assets ライブラリとの統合機能で使用するために必要な Adobe Campaign の設定手順を説明します。

>[!CAUTION]
>
>これらの統合は同時におこないます。次の情報をよく読んでから設定をおこなってください。

* **Experience Cloud Assets** との統合：この統合により、Adobe Experience Cloud ライブラリから画像を挿入できます。設定とライセンスモデルに応じて、このライブラリは Assets コアサービスまたは Assets On Demand になります。この統合は、Adobe Campaign に **[!UICONTROL Adobe Experience Cloud との統合]**&#x200B;組み込みパッケージをインストールすることによって設定する必要があります。
* **AEM Assets** との統合：この統合により、Adobe Experience Manager Assets ライブラリから画像を挿入できます。この統合は、Adobe Campaign に **[!UICONTROL AEM 統合]**&#x200B;組み込みパッケージをインストールすることによって設定する必要があります。

>[!NOTE]
>
>2 つのパッケージ（**[!UICONTROL AEM 統合]**&#x200B;および **[!UICONTROL Adobe Marketing Experience との統合]**）がインストールされている場合、Adobe Experience Cloud ライブラリで使用可能なアセットだけを使用できます。AEM Assets ライブラリのアセットにもアクセスするには、AEM Assets と Adobe Experience Cloud を同期する必要があります。AEM Assets 内のアセットも、Adobe Experience Cloud ライブラリで使用可能になります。AEM Assets と Adobe Experience Cloud の同期について詳しくは、[詳細ドキュメント](https://docs.adobe.com/docs/ja/aod/overview/collaborating/aem-assets-aod-sync.html)を参照してください。

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
>**[!UICONTROL Adobe Experience Cloud との統合]**&#x200B;パッケージも Adobe Campaign インスタンスにインストールされている場合、Adobe Experience Cloud ライブラリで使用可能なアセットだけを使用することができます。AEM Assets ライブラリのアセットにもアクセスするには、AEM Assets と Adobe Experience Cloud を同期する必要があります。AEM Assets 内のアセットも、Adobe Experience Cloud ライブラリで使用可能になります。その場合、特定の配信テンプレートを作成する必要はありません。AEM Assets と Adobe Experience Cloud 間の同期について詳しくは、[詳細ドキュメント](https://docs.adobe.com/docs/ja/aod/overview/collaborating/aem-assets-aod-sync.html)を参照してください。

