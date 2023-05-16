---
product: campaign
title: はじめに
description: はじめに
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 3e39a0d2-ff7e-4233-82bb-2b360f696a33
source-git-commit: 6dc6aeb5adeb82d527b39a05ee70a9926205ea0b
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 3%

---

# はじめに{#introduction}



この節では、Adobe Campaign、クライアント側、サーバー側のアップグレードに適用する手順と、既存のインスタンスの Unicode への切り替えについて説明します。

>[!NOTE]
>
>Hosted/Managed Services インスタンスの場合は、Adobe管理者と連携する必要があります。\
>オンプレミスインスタンスの場合は、Adobeコンサルタントからサポートを受けることができます。

Adobe Campaignがインストールされているすべてのサーバーにアップグレードを適用する必要があります。

1. リダイレクトとトラッキングサーバー (Apache/IIS) を移行します。
1. パワーブースター/クラスターサーバーを移行します。
1. マーケティングサーバーを移行します。

Adobe Campaignは、サーバー側で実行されるいくつかのプロセスに基づいています。特に、更新時には、次のプロセスを操作する必要があります。

* アプリケーションサーバー（nlserver web）
* 配信サーバー (nlserver mta)
* リダイレクトサーバー (webmdl)

>[!CAUTION]
>
>クライアントコンソールは、サーバーインスタンスと同じビルド上にある必要があります。

>[!NOTE]
>
>様々なAdobe Campaignプロセスについて詳しくは、 [この節](../../installation/using/general-architecture.md#logical-application-layer).\
>パワーブースターまたはパワークラスタータイプのアーキテクチャを使用する場合は、このプロセスをすべてのパワーブースター/クラスターサーバーに適用する必要があります。

新しいバージョンでデータベース構造の変更が必要な場合は、次の順序でサーバーを再起動することをお勧めします。

1. アプリケーションサーバー (nlserver Web)
1. リダイレクトサーバー (webmdl)
1. 配信サーバー (nlserver mta)。
