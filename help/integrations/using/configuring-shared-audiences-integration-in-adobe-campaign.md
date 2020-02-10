---
title: Adobe Campaign での共有オーディエンスの統合の設定
seo-title: Adobe Campaign での共有オーディエンスの統合の設定
description: Adobe Campaign での共有オーディエンスの統合の設定
seo-description: null
page-status-flag: never-activated
uuid: 6ed137e4-027f-4eb0-a0b5-4beb7deef51f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: audience-sharing
discoiquuid: 4443b0ca-80c6-467d-a4df-50864aae8496
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 6ae45cbd87fc0152fc654202e03501fc8d2abd06

---


# Adobe Campaign での共有オーディエンスの統合の設定{#configuring-shared-audiences-integration-in-adobe-campaign}

この依頼を送信すると、アドビによって統合のプロビジョニングが進められます。また、お客様には設定を完了させるための詳細情報が届きます。

1. [手順1:Adobe Campaignで外部アカウントを設定または確認する](#step-1--configure-or-check-the-external-accounts-in-adobe-campaign)
1. [手順2:データソースの設定](#step-2--configure-the-data-source)
1. [手順3:キャンペーントラッキングサーバーの設定](#step-3--configure-campaign-tracking-server)
1. [手順4:訪問者IDサービスの設定](#step-4--configure-the-visitor-id-service)

## Step 1: Configure or check the external accounts in Adobe Campaign {#step-1--configure-or-check-the-external-accounts-in-adobe-campaign}

まず、次の手順に従って、Adobe Campaign で外部アカウントの設定または確認をおこなう必要があります。

1. アイコンをクリッ **[!UICONTROL Explorer]** クします。
1. 移動 **[!UICONTROL Administration > Platform > External accounts]**. 通常、この SFTP アカウントはアドビによって設定されており、お客様には必要な情報が伝えられています。

   * **[!UICONTROL importSharedAudience]** :オーディエンスのインポート専用のSFTPアカウント。
   * **[!UICONTROL exportSharedAudience]** :オーディエンスの書き出し専用のSFTPアカウント。
   ![](assets/aam_config_1.png)

1. Fill in the **[!UICONTROL Server]** field: **ftp-out.demdex.com** domain for the import external account and **ftp-in.demdex.com** domain for the export external account.

   Campaign からのエクスポートは Audience Manager または People コアサービスへのインポートであることを覚えておいてください。

   >[!NOTE]
   >
   >S3を使用している場合は、次の構文を **[!UICONTROL AWS S3 Account Server]** 入力します。\
   `<S3bucket name>.s3.amazonaws.com/<s3object path>`\
   For more information on how to configure your S3 account, refer to this [page](../../platform/using/external-accounts.md#amazon-simple-storage-service--s3--external-account).

   ![](assets/aam_config_2.png)

1. アドビが提供 **[!UICONTROL Account]** するお **[!UICONTROL Password]** よびを追加します。

これで外部アカウントが設定されました。

## Step 2: Configure the Data Source {#step-2--configure-the-data-source}

**受信者 - 訪問者 ID** は Audience Manager 内で作成されます。これは、訪問者 ID にデフォルトで設定されている標準のデータソースです。Campaign から作成されたセグメントは、このデータソースの一部になります。

To configure the **[!UICONTROL Recipient - Visitor ID]** data source:

1. ノードから、 **[!UICONTROL Explorer]** を選択します **[!UICONTROL Administration > Platform > AMC Data sources]**。
1. 選択 **[!UICONTROL Recipient - Visitor ID]**.
1. アドビから提供さ **[!UICONTROL Data Source ID]** れたおよ **[!UICONTROL AAM Destination ID]** びを入力します。

   ![](assets/aam_config_3.png)

## Step 3: Configure Campaign Tracking server {#step-3--configure-campaign-tracking-server}

People コアサービスまたは Audience Manager との統合を設定する場合は、Campaign トラッキングサーバーも設定する必要があります。

Campaign トラッキングサーバーがドメインに登録されていることを確認する必要があります（CNAME）。ドメイン名のデリゲーションについて詳しくは、[この記事](https://helpx.adobe.com/campaign/kb/domain-name-delegation.html)を参照してください。

## Step 4: Configure the Visitor ID Service {#step-4--configure-the-visitor-id-service}

訪問者 ID サービスを Web のプロパティや Web サイトで設定したことがない場合は、次の[ドキュメント](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-aam-analytics.html)を参照してサービスの設定方法を確認するか、次の[ビデオ](https://helpx.adobe.com/marketing-cloud/how-to/email-marketing.html#step-two)をご覧ください。

設定とプロビジョニングが完了し、統合を使用してオーディエンスまたはセグメントをインポートおよびエクスポートできるようになりました。
