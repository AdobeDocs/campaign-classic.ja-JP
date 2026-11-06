---
product: campaign
title: Campaignの更新について
description: Campaignの更新について
feature: Monitoring, Upgrade
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 3e39a0d2-ff7e-4233-82bb-2b360f696a33
TQID: 'https://experienceleague.adobe.com/L6Ais2NSt-Z29b7Jgz25a6uYInel9V-Hb5kv0u6oSLo'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: c03a11ff-bdf9-4e5b-b279-f468b4293464
    internal-label: Performance Monitoring
  - id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
    internal-label: Monitoring guidelines
  - id: eff19c99-440a-4318-b319-444edc4d8d8f
    internal-label: Upgrade
source-git-commit: 81e68b8bf551312dafc4a53ac4edc0f073cc5131
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%
---
# Campaignの更新について{#introduction}



この節では、Adobe Campaign、クライアントサイドおよびサーバーサイドのアップグレードに適用される手順を示し、既存のインスタンスのUnicodeへの切り替えについて説明します。

>[!NOTE]
>
>ホスト/マネージドサービスインスタンスの場合は、Adobe管理者と調整する必要があります。\
>オンプレミスインスタンスの場合は、Adobe Consultantsの支援を受けることができます。

アップグレードは、Adobe Campaignがインストールされているすべてのサーバーに適用する必要があります。

1. リダイレクトおよびトラッキングサーバー（Apache/IIS）を移行します。
1. Power Booster/Cluster サーバーを移行します。
1. マーケティングサーバーの移行。

Adobe Campaignは、アップデート時に操作する必要があるサーバーサイドで実行される複数のプロセスに基づいています。特に、次の点に注意してください。

* アプリケーションサーバー（nlserver web）
* 配信サーバー（nlserver mta）
* リダイレクトサーバー（webmdl）

>[!CAUTION]
>
>クライアントコンソールは、サーバーインスタンスと同じビルド上にある必要があります。

>[!NOTE]
>
>さまざまなAdobe Campaign プロセスについて詳しくは、[この節](../../installation/using/general-architecture.md#logical-application-layer)を参照してください。\
>Power BoosterまたはPower Cluster タイプのアーキテクチャを使用する場合は、このプロセスをすべてのPower Booster/Cluster サーバーに適用する必要があります。

新しいバージョンでデータベース構造が変更された場合は、次の順序でサーバーを再起動することをお勧めします。

1. アプリケーションサーバー（nlserver web）,
1. リダイレクトサーバー（webmdl）,
1. 配信サーバー（nlserver mta）:
