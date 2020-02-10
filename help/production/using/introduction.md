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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# はじめに{#introduction}

ここでは、Adobe Campaign、クライアント側、サーバー側のアップグレードに適用される手順、および既存のインスタンスのUnicodeへの切り替えについて説明します。

>[!NOTE]
>
>ホストされるインスタンスの場合は、アドビ管理者と連携する必要があります。\
>オンプレミスインスタンスの場合は、アドビコンサルタントから支援を受けることができます。

アップグレードは、Adobe Campaignがインストールされているすべてのサーバーに適用する必要があります。

1. リダイレクトサーバーとトラッキングサーバー(Apache/IIS)を移行します。
1. パワーブースタ/クラスタサーバを移行します。
1. マーケティングサーバーを移行します。

Adobe Campaignは、サーバー側で実行されるいくつかのプロセスに基づいており、特に更新時に操作する必要があります。

* アプリケーションサーバー(nlserver Web)
* 配信サーバー(nlserver mta)
* リダイレクトサーバー(webmdl)

>[!NOTE]
>
>For more on the various Adobe Campaign processes, refer to [this section](../../installation/using/general-architecture.md#logical-application-layer).\
>パワーブースタまたはパワークラスタタイプのアーキテクチャを使用する場合は、すべてのパワーブースタ/クラスタサーバにこのプロセスを適用する必要があります。

新しいバージョンでデータベース構造の変更が必要な場合は、次の順序でサーバーを再起動することをお勧めします。

1. アプリケーションサーバー(nlserver Web)、
1. リダイレクトサーバ(webmdl)、
1. 配信サーバー(nlserver mta)。

