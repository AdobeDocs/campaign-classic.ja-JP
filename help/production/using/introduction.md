---
solution: Campaign Classic
product: campaign
title: はじめに
description: はじめに
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
translation-type: tm+mt
source-git-commit: 5b35d2ffdd0f591e2fe31dc98a54be9ea0c0c18d
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 1%

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

>[!CAUTION]
>
>クライアントコンソールは、サーバーインスタンスと同じビルド上にある必要があります。

>[!NOTE]
>
>様々なAdobe Campaignプロセスについての詳細は、[このセクション](../../installation/using/general-architecture.md#logical-application-layer)を参照してください。\
>パワー・ブースタまたはパワー・クラスタ・タイプ・アーキテクチャを使用する場合は、このプロセスをすべてのパワー・ブースタ/クラスタ・サーバに適用する必要があります。

新しいバージョンでデータベース構造の変更が必要な場合は、次の順序でサーバーを再起動することをお勧めします。

1. アプリケーションサーバー(nlserver Web)、
1. リダイレクトサーバー(webmdl)、
1. 配信サーバー(nlserver mta)。

