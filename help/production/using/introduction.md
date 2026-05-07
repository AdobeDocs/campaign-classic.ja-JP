---
product: campaign
title: はじめに
description: はじめに
feature: Monitoring, Upgrade
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 3e39a0d2-ff7e-4233-82bb-2b360f696a33
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# はじめに{#introduction}



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
