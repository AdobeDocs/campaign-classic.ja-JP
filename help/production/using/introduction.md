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
source-wordcount: '193'
ht-degree: 1%

---

# はじめに{#introduction}



この節では、Adobe Campaign、クライアント側およびサーバー側をアップグレードするために適用する手順を示し、既存のインスタンスの Unicode への切り替えについて説明します。

>[!NOTE]
>
>ホスト/マネージドサービスインスタンスの場合は、Adobe管理者と調整する必要があります。\
>オンプレミスインスタンスの場合は、Adobeコンサルタントからサポートを受けることができます。

アップグレードは、Adobe Campaignがインストールされているすべてのサーバーに適用する必要があります。

1. リダイレクトサーバーとトラッキングサーバー（Apache/IIS）を移行します。
1. パワーブースター/クラスターサーバーを移行します。
1. マーケティングサーバーを移行します。

Adobe Campaignは、サーバー側で実行されるいくつかのプロセスに基づいています。これらのプロセスは、特に更新時に操作する必要があります。

* アプリケーションサーバー（nlserver web）
* 配信サーバー（nlserver mta）
* リダイレクトサーバー（webmdl）

>[!CAUTION]
>
>クライアントコンソールは、サーバーインスタンスと同じビルドになっている必要があります。

>[!NOTE]
>
>様々なAdobe Campaign プロセスについて詳しくは、[&#x200B; この節 &#x200B;](../../installation/using/general-architecture.md#logical-application-layer) を参照してください。\
>パワーブースターまたはパワークラスタータイプのアーキテクチャを使用する場合、このプロセスをすべてのパワーブースター/クラスターサーバーに適用する必要があります。

新しいバージョンでデータベース構造の変更が必要な場合は、次の順序でサーバーを再起動することをお勧めします。

1. アプリケーションサーバー（nlserver web）
1. リダイレクトサーバー（webmdl）
1. 配信サーバー（nlserver mta）。
