---
solution: Campaign Classic
product: campaign
title: ソースと宛先の使用を開始する
description: Adobe Experience Platformのソースと宛先についての詳細。
audience: integrations
content-type: reference
translation-type: tm+mt
source-git-commit: b4da54c122e75a175f6f586a05955b3dfed00c1e
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 1%

---


# ソースと宛先の使用を開始する{#rtcdp}

## ソースと宛先について

Adobe Experience Platformを使用すると、Campaign ClassicとAdobeのリアルタイム顧客データプラットフォーム(RTCDP)の間でデータを共有できます。 これにより、キャンペーンワークフロー内のAdobe Experience Platformオーディエンスをターゲットし、送信、開く、クリック数などのオーディエンスに関連するAdobeReal-time Customer Data Platformデータをに送信できます。

* **目的地**&#x200B;で、Adobe Experience PlatformからCampaign Classicにオーディエンスを取り込む。 これにより、マーケティングキャンペーンの既知および不明なデータをアクティブ化できます。
* **ソース**&#x200B;を使用して、Campaign Classicデータ（送信、開く、クリックなど）をAdobe Experience Platformにエクスポートします。 これにより、異なるソースから収集したデータを1か所に集め、得られた洞察を利用してより多くの作業を行うことができます。

>[!IMPORTANT]
>
>この統合を実行する際は、Adobe Campaign契約に従って、SFTPストレージの制限、データベースストレージの制限およびアクティブなプロファイルの制限に注意してください。

Adobeリアルタイム顧客データプラットフォーム、宛先、ソースの詳細については、次のページを参照してください。

* [アドビのリアルタイムカスタマーデータプラットフォーム（CDP）](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html)
* [Destinationsドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html)
* [ソースドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html)

## Campaign ClassicとAdobe Experience Platformの接続

Adobe Experience PlatformとCampaign Classicの間でデータを共有するには、まずAdobe Campaignを&#x200B;**宛先**&#x200B;として接続し、AWS S3またはAzure BLOBストレージの場所をAdobeエクスペリエンスプラットフォームの&#x200B;**Source**&#x200B;として接続する必要があります。

コネクタを設定したら、ワークフローを使用して、Campaign Classicへのデータのインポートまたはエクスポートを設定できます。

![](assets/rtcdp-schema.png)

これらの読み込みおよび書き出しプロセスの設定方法について詳しくは、次の節を参照してください。

* [Adobe Experience Platformセグメントをキャンペーンに取り込む](../../integrations/using/ingest-aep-data.md)
* [キャンペーンからAdobe Experience Platformへのデータのエクスポート](../../integrations/using/export-campaign-data.md)
