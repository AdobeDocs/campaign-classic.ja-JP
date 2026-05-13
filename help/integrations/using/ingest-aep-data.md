---
product: campaign
title: Adobe Experience Platform セグメントの Campaign への取り込み
description: Adobe Experience Platform のオーディエンスを Campaign Classic に取り込む方法について説明します
feature: Experience Platform Integration
audience: integrations
content-type: reference
exl-id: 6db8a653-b649-402c-8814-24826edadba7
TQID: https://experienceleague.adobe.com/gZ3arUya5UYcZckqtlDObZTA7laUmVttTDHxgOb97vE
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
subfeature_v2:
  - id: eb007b6d-6e57-46ab-9485-3f24d6102304
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 100%

---

# Adobe Experience Platform セグメントの Campaign への取り込み {#destinations}



Adobe Experience Platform オーディエンスを Campaign に取り込んでワークフローで使用するには、まず Adobe Campaign を Adobe Experience Platform の&#x200B;**宛先**&#x200B;として接続し、エクスポート対象のセグメントを設定する必要があります。

宛先が設定されると、データはストレージの場所にエクスポートされます。これを取り込むには、Campaign Classic に専用のワークフローを作成する必要があります。

## Adobe Campaign を宛先として接続する

Adobe Experience Platform で、Adobe Campaign との接続を設定するには、エクスポートしたセグメントに対してストレージの場所を選択します。 また、この手順では、エクスポートするセグメントを選択し、そこに含める追加の XDM フィールドを指定することもできます。

詳しくは、[宛先のドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign.html?lang=ja)を参照してください。

宛先の設定が完了すると、Adobe Experience Platform は指定したストレージの場所にタブ区切りの .txt または .csv ファイルを作成します。 この操作は、24 時間に 1 回実行されるようスケジュールされています。

セグメントを Campaign に取り込むための Campaign Classic ワークフローを設定できるようになりました。

## Campaign Classic でのインポートワークフローの作成

Campaign Classic を宛先として設定したら、Adobe Experience Platform がエクスポートしたファイルを読み込むための専用のワークフローを作成する必要があります。

これをおこなうには、**[!UICONTROL ファイル転送]**&#x200B;アクティビティを追加して設定する必要があります。 このアクティビティの設定方法について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/event-activities/file-transfer.html?lang=ja){target="_blank"}を参照してください。

![](assets/rtcdp-file-transfer.png)

その後、必要に応じてワークフローを構築できます（セグメントデータを使用してデータベースを更新する、チャネル間の配信をセグメントに送信するなど）。

例えば、以下のワークフローでは、ストレージの場所から毎日ファイルをダウンロードし、その後、セグメントデータを使用して Campaign データベースを更新します。

![](assets/rtcdp-workflow.png)
