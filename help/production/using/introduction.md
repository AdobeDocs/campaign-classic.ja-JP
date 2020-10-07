---
title: はじめに
seo-title: はじめに
description: はじめに
seo-description: null
page-status-flag: never-activated
uuid: 4192a74e-1d4f-4784-80e3-53aaefa9141e
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
discoiquuid: 772992bf-588f-42bd-a72a-986a88815264
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---


# はじめに{#introduction}

この節では、アップグレードAdobe Campaign、クライアント側およびサーバー側に適用される手順、および既存のインスタンスのUnicodeへの切り替えについて説明します。

>[!NOTE]
>
>ホストインスタンスの場合は、Adobe管理者と連携する必要があります。\
>オンプレミスインスタンスの場合、Adobeコンサルタントから支援を受けることができます。

Adobe Campaignがインストールされているすべてのサーバーにアップグレードを適用する必要があります。

1. リダイレクトサーバーとトラッキングサーバー(Apache/IIS)を移行します。
1. パワー・ブースタ/クラスタ・サーバを移行します。
1. マーケティングサーバーを移行します。

Adobe Campaignは、サーバー側で実行されるいくつかのプロセスに基づいています。特に、アップデートの間に操作する必要があります。

* アプリケーションサーバー(nlserver Web)
* 配信サーバー(nlserver mta)
* リダイレクトサーバー(webmdl)

>[!NOTE]
>
>For more on the various Adobe Campaign processes, refer to [this section](../../installation/using/general-architecture.md#logical-application-layer).\
>パワー・ブースタまたはパワー・クラスタ・タイプ・アーキテクチャを使用する場合は、このプロセスをすべてのパワー・ブースタ/クラスタ・サーバに適用する必要があります。

新しいバージョンでデータベース構造の変更が必要な場合は、次の順序でサーバーを再起動することをお勧めします。

1. アプリケーションサーバー(nlserver Web)、
1. リダイレクトサーバー(webmdl)、
1. 配信サーバー(nlserver mta)。

