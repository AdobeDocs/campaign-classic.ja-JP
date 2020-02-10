---
title: 一般的なアーキテクチャ
seo-title: 一般的なアーキテクチャ
description: 一般的なアーキテクチャ
seo-description: null
page-status-flag: never-activated
uuid: a565a10c-cbef-455a-aa1d-9be9cd207c7a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: introduction
discoiquuid: f4879774-afe5-4556-ab60-9297cabbca2c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# 一般的なアーキテクチャ{#general-architecture}

## 最小アーキテクチャ {#minimum-architecture}

最小限の設定では、Adobe Campaignは次の機能を使用します。

* adobe Campaignアプリケーションサーバー、
* データベース。

   ![](assets/formation_exploitation.png)

次の図は、最小アーキテクチャのコンテキストに関連するトラフィックは次のみであることを示しています。

1. インターネット経由でAdobe Campaignサーバーに送信されるHTTPプロトコルトラフィック、
1. インターネット経由でのAdobe Campaignサーバーとの間のSMTPプロトコルトラフィック。

## 分散アーキテクチャ {#distributed-architecture}

Adobe Campaignは複数のモジュールで構成され、複数のマシンで分類できます。 このオペレーティングモードには、次のような利点があります。

* ロードバランシング、
* モジュールの冗長性の設定、
* 複数のサービスプロバイダーにわたって分類されたアーキテクチャの構築（提供されるサービスのセグメント化）。

![](assets/architecturerepartie.png)

複数のマシンにモジュールを分散させることで、使用の柔軟性と適応性が向上します。

>[!NOTE]
>
>For more on the various architectures, refer to [this section](../../installation/using/general-architecture.md).

## オープン・ポートのリスト {#list-of-open-ports}

| ポート番号 | 関連するAdobe Campaignモジュールまたはアプリケーション | 設定可能 |
|---|---|---|
| 443/tcpまたは80/tcp | Webサーバー(Apache/IIS) | はい |
| 6666/udp（ローカル） | Adobe Campaign:Syslogd | はい |
| 8005/tcp （ローカル） | Adobe Campaign:ウェブモジュール | はい |
| 8080/tcp | Adobe Campaign:Webモジュール(tomcat) | はい |
| 7777 | 統計サーバ（statサーバ） | はい |

