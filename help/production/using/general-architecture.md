---
solution: Campaign Classic
product: campaign
title: 一般的なアーキテクチャ
description: 一般的なアーキテクチャ
audience: production
content-type: reference
topic-tags: introduction
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 4%

---


# 一般的なアーキテクチャ{#general-architecture}

## 最小アーキテクチャ{#minimum-architecture}

最小の設定では、Adobe Campaignは次の機能を使用します。

* adobe campaignアプリケーションサーバー、
* データベース。

   ![](assets/formation_exploitation.png)

次の図は、最小のアーキテクチャのコンテキストに関係するトラフィックは次のみであることを示しています。

1. インターネット経由でAdobe Campaignサーバに送信されるHTTPプロトコルトラフィック、
1. SMTPプロトコルは、インターネット経由でAdobe Campaignサーバーとの間でトラフィックを受け渡します。

## 分散アーキテクチャ {#distributed-architecture}

Adobe Campaignは複数のモジュールで構成され、複数のマシンで分類できます。 このオペレーティングモードには、次のような利点があります。

* ロードバランシング、
* モジュールの冗長性の設定、
* 複数のサービスプロバイダーにわたって分類された建築（提供されるサービスのセグメント化）の構築。

![](assets/architecturerepartie.png)

複数のマシンにわたるモジュールの配布により、使用の柔軟性が高まり、適応性が向上します。

>[!NOTE]
>
>様々なアーキテクチャの詳細については、[この](../../installation/using/general-architecture.md)を参照してください。

## オープン・ポートのリスト{#list-of-open-ports}

| ポート番号 | 関連するAdobe Campaignモジュールまたはアプリケーション | 設定可能 |
|---|---|---|
| 443/tcpまたは80/tcp | Webサーバー(Apache/IIS) | はい |
| 6666/udp（ローカル） | Adobe Campaign:Syslogd | はい |
| 8005/tcp （ローカル） | Adobe Campaign:ウェブモジュール | はい |
| 8080/tcp | Adobe Campaign:webモジュール(tomcat) | はい |
| 7777 | 統計サーバ（statサーバ） | はい |

