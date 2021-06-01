---
product: campaign
title: はじめに
description: はじめに
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 3e39a0d2-ff7e-4233-82bb-2b360f696a33
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 3%

---

# はじめに{#introduction}

この節では、Adobe Campaign、クライアント側、サーバー側のアップグレードに適用する手順と、既存のインスタンスのUnicodeへの切り替えについて説明します。

>[!NOTE]
>
>ホストされているインスタンスの場合は、Adobe管理者と連携する必要があります。\
>オンプレミスインスタンスの場合、Adobeコンサルタントからサポートを受けることができます。

アップグレードは、Adobe Campaignがインストールされているすべてのサーバーに適用する必要があります。

1. リダイレクトサーバーとトラッキングサーバー(Apache/IIS)を移行します。
1. パワーブースター/クラスターサーバーを移行します。
1. マーケティングサーバーを移行します。

Adobe Campaignは、サーバー側で実行されるいくつかのプロセスに基づいています。特に、更新時には、次のようにを操作する必要があります。

* アプリケーションサーバー（nlserver web）
* 配信サーバー(nlserver mta)
* リダイレクトサーバー(webmdl)

>[!CAUTION]
>
>クライアントコンソールは、サーバーインスタンスと同じビルド上にある必要があります。

>[!NOTE]
>
>様々なAdobe Campaignプロセスについて詳しくは、[この節](../../installation/using/general-architecture.md#logical-application-layer)を参照してください。\
>パワーブースターまたはパワークラスタータイプのアーキテクチャを使用する場合は、このプロセスをすべてのパワーブースター/クラスターサーバーに適用する必要があります。

新しいバージョンでデータベース構造の変更が必要な場合は、次の順序でサーバーを再起動することをお勧めします。

1. アプリケーションサーバー(nlserver web)
1. リダイレクションサーバー(webmdl)
1. 配信サーバー(nlserver mta)。
