---
solution: Campaign Classic
product: campaign
title: Adobe Experience Platformセグメントをキャンペーンに取り込む
description: Adobe Experience PlatformオーディエンスをCampaign Classicに取り込む方法を学びます。
audience: integrations
content-type: reference
translation-type: tm+mt
source-git-commit: 9b3254c16eed784846db87d27f9f5de009dafdc3
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Adobe Experience Platformセグメントをキャンペーンに取り込む{#destinations}

Adobe Experience Platformをキャンペーンに取り込んでワークフローで使用するには、まずAdobe CampaignをAdobe Experience Platform **宛先**&#x200B;として接続し、エクスポートするセグメントを使用して設定する必要があります。

宛先が設定されると、データはストレージの場所にエクスポートされ、取り込むために、Campaign Classicに専用のワークフローを構築する必要があります。

## Adobe Campaignを宛先として接続

Adobe Experience Platformで、Adobe Campaignとの接続を設定するには、書き出したセグメントのストレージの場所を選択します。 また、この手順では、エクスポートするセグメントを選択し、追加のXDMフィールドを指定して含めることもできます。

詳しくは、[宛先ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign.html)を参照してください。

宛先の設定が完了すると、Adobe Experience Platformは指定したストレージーの場所にタブ区切りの.txtまたは.csvファイルを作成します。 この操作は、24時間に1回スケジュールされて実行されます。

セグメントをキャンペーンに取り込むCampaign Classicワークフローを設定できるようになりました。

## Campaign Classicでのインポートワークフローの作成

Campaign Classicを宛先として設定したら、Adobe Experience Platformが書き出したファイルを読み込むための専用のワークフローを構築する必要があります。

これを行うには、**[!UICONTROL ファイル転送]**&#x200B;アクティビティを追加して設定する必要があります。 このアクティビティの設定方法について詳しくは、[この](../../workflow/using/file-transfer.md)セクションを参照してください。

![](assets/rtcdp-file-transfer.png)

その後、必要に応じてワークフローを構築できます(セグメントデータを使用してデータベースを更新し、チャネル間の配信をセグメントに送信するなど)。

例えば、以下のワークフローでは、ストレージーの場所から毎日ファイルをダウンロードし、その後、セグメントデータを使用してキャンペーンデータベースを更新します。

![](assets/rtcdp-workflow.png)
