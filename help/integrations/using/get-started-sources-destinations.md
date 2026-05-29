---
product: campaign
title: ソースと宛先の基本を学ぶ
description: Adobe Experience Platform のソースと宛先について学ぶ
feature: Experience Platform Integration
audience: integrations
content-type: reference
exl-id: 8cee52c7-ea56-4701-8ebb-eb18afffea51
TQID: https://experienceleague.adobe.com/xPpBR6NrQ315FIw1beLnw4c0gyLzEoYWzIXDljDg9H4
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
subfeature_v2:
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
  - id: df0d6518-6f49-46e2-b46e-3bcc513f553f
  - id: eb007b6d-6e57-46ab-9485-3f24d6102304
  - id: b1fd1501-3105-4d6b-b4d4-9af53126df75
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 313
ht-degree: 100%

---

# ソースと宛先の操作 {#rtcdp}



## ソースと宛先について

Adobe Experience Platform を使用すると、Campaign Classic とアドビのリアルタイム顧客データプラットフォーム（RTCDP）の間でデータを共有できます。 これにより、Campaign ワークフローで Adobe Experience Platform オーディエンスをターゲットに設定し、オーディエンスに関連するデータ（送信数、開封数、クリック数など）をアドビのリアルタイム顧客データプラットフォームへと送信できます。

* **宛先**&#x200B;で、Adobe Experience Platform のオーディエンスを Campaign Classic に取り込みます。 これにより、マーケティングキャンペーンで既知のデータや不明なデータを活用することができます。
* **ソース**&#x200B;で、Campaign Classic のデータ（送信数、開封数、クリック数など）を Adobe Experience Platform にエクスポートします。 これにより、異なるソースから収集したデータを 1 か所に集め、得られたインサイトを利用してより多くのことを実行できます。

>[!IMPORTANT]
>
>この統合を使用する際は、Adobe Campaign の契約条件が定める SFTP ストレージ、データベースストレージ、アクティブプロファイルの制限に注意してください。

アドビのリアルタイム顧客データプラットフォーム、宛先、ソースについて詳しくは、次のページを参照してください。

* [アドビのリアルタイム顧客データプラットフォーム](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=ja)
* [宛先に関するドキュメント](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=ja)
* [ソースに関するドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ja)

## Campaign Classic と Adobe Experience Platform の接続

Adobe Experience Platform と Campaign Classic の間でデータを共有するには、まず Adobe Campaign を&#x200B;**宛先**&#x200B;として接続し、AWS S3 または Azure Blob ストレージの場所を Adobe Experience Platform の&#x200B;**ソース**&#x200B;として接続する必要があります。

コネクタを設定したら、ワークフローを使用して、Campaign Classic へのデータのインポートまたはエクスポートを設定できます。

![](assets/rtcdp-schema.png)

これらのインポートおよびエクスポートプロセスの設定方法について詳しくは、次の節を参照してください。

* [Adobe Experience Platform セグメントの Campaign への取り込み](../../integrations/using/ingest-aep-data.md)
* [Campaign から Adobe Experience Platform へのデータのエクスポート](../../integrations/using/export-campaign-data.md)
