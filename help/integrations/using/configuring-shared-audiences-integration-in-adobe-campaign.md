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
translation-type: tm+mt
source-git-commit: d567cb7dbc55d9c124d1cc83b7a5a9e2dfb5ab61
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 67%

---


# Adobe Campaign での共有オーディエンスの統合の設定{#configuring-shared-audiences-integration-in-adobe-campaign}

この依頼を送信すると、アドビによって統合のプロビジョニングが進められます。また、お客様には設定を完了させるための詳細情報が届きます。

1. [手順 1：Adobe Campaign での外部アカウントの設定または確認](#step-1--configure-or-check-the-external-accounts-in-adobe-campaign)
1. [手順 2：データソースの設定](#step-2--configure-the-data-source)
1. [手順 3：キャンペーントラッキングサーバーの設定](#step-3--configure-campaign-tracking-server)
1. [手順 4：訪問者 ID サービスの設定](#step-4--configure-the-visitor-id-service)

>[!IMPORTANT]
>
>demdexドメインを使用し、インポート外部アカウントに **ftp-out.demdex.com** 、エクスポート外部アカウントに **** ftp-in.demdex.comの構文に従う場合は、それに従って導入を適応させ、Amazonシンプルストレージサービス(S3)コネクタに移動してデータのインポートまたはエクスポートを行う必要があります。 AmazonS3で外部アカウントを設定する方法の詳細については、この [節を参照してください](../../integrations/using/configuring-shared-audiences-integration-in-adobe-campaign.md#step-1--configure-or-check-the-external-accounts-in-adobe-campaign)。

## 手順 1：Adobe Campaign での外部アカウントの設定または確認 {#step-1--configure-or-check-the-external-accounts-in-adobe-campaign}

まず、次の手順に従って、Adobe Campaign で外部アカウントの設定または確認をおこなう必要があります。

1. 「**[!UICONTROL エクスプローラー]**」アイコンをクリックします。
1. **[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;に移動します。通常、この SFTP アカウントはアドビによって設定されており、お客様には必要な情報が伝えられています。

   * **[!UICONTROL importSharedAudience]**:オーディエンスの読み込み専用のアカウント。
   * **[!UICONTROL exportSharedAudience]**:オーディエンスの書き出し専用アカウント。

   ![](assets/aam_config_1.png)

1. 「 **[!UICONTROL Export」オーディエンスを選択して、「Adobe Marketing Cloud]** 外部アカウントに」を選択します。

1. 「 **[!UICONTROL Type]** 」ドロップダウンから、 **[!UICONTROL AWS S3を選択します]**。

1. 次の詳細を入力します。

   * **[!UICONTROL AWS S3 Account Server]** URL（サーバーのURL）は、次のように入力する必要があります。

      ```
      <S3bucket name>.s3.amazonaws.com/<s3object path>
      ```

   * **[!UICONTROL AWSアクセスキーID]** AWSアクセスキーIDの場所を知るには、この [ページを参照してください](https://docs.aws.amazon.com/ja_jp/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys) 。

   * **[!UICONTROL AWSへの秘密アクセスキーAWS]**&#x200B;への秘密アクセスキーの場所を知るには、この [ページを参照してください](https://aws.amazon.com/jp/blogs/security/wheres-my-secret-access-key/)。

   * **[!UICONTROL AWSリージョン]** AWSリージョンの詳細については、この [ページを参照してください](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/)。
   ![](assets/aam_config_2.png)

1. 前の手順の詳細に従って、 **[!UICONTROL 「]** 保存 **[!UICONTROL 」をクリックし、Adobe Marketing Cloud]** 外部アカウントからインポートオーディエンスを設定します。

これで外部アカウントが設定されました。

## 手順 2：データソースの設定 {#step-2--configure-the-data-source}

**受信者 - 訪問者 ID** は Audience Manager 内で作成されます。これは、訪問者 ID にデフォルトで設定されている標準のデータソースです。Campaign から作成されたセグメントは、このデータソースの一部になります。

**[!UICONTROL 受信者 - 訪問者 ID]** データソースを設定するには：

1. **[!UICONTROL エクスプローラー]**&#x200B;ノードから、**[!UICONTROL 管理／プラットフォーム／AMC データソース]**&#x200B;を選択します。
1. 「**[!UICONTROL 受信者 - 訪問者 ID]**」を選択します。
1. アドビから提供された&#x200B;**[!UICONTROL データソース ID]** と **[!UICONTROL AAM 宛先 ID]** を入力します。

   ![](assets/aam_config_3.png)

## 手順 3：キャンペーントラッキングサーバーの設定 {#step-3--configure-campaign-tracking-server}

People コアサービスまたは Audience Manager との統合を設定する場合は、Campaign トラッキングサーバーも設定する必要があります。

Campaign トラッキングサーバーがドメインに登録されていることを確認する必要があります（CNAME）。ドメイン名のデリゲーションについて詳しくは、[この記事](https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html)を参照してください。

## 手順 4：訪問者 ID サービスの設定 {#step-4--configure-the-visitor-id-service}

訪問者 ID サービスを Web のプロパティや Web サイトで設定したことがない場合は、次の[ドキュメント](https://docs.adobe.com/content/help/ja-JP/id-service/using/implementation/setup-aam-analytics.html)を参照してサービスの設定方法を確認するか、次の[ビデオ](https://helpx.adobe.com/marketing-cloud/how-to/email-marketing.html#step-two)をご覧ください。

設定とプロビジョニングが完了し、統合を使用してオーディエンスまたはセグメントをインポートおよびエクスポートできるようになりました。
