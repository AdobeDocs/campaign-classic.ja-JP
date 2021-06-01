---
product: campaign
title: 一般的なアーキテクチャ
description: 一般的なアーキテクチャ
audience: production
content-type: reference
topic-tags: introduction
exl-id: 3bfb5448-6996-4080-bf9a-434f1207637e
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 4%

---

# 一般的なアーキテクチャ{#general-architecture}

## 最小アーキテクチャ{#minimum-architecture}

最小限の設定では、Adobe Campaignは次の操作をおこないます。

* Adobe Campaignアプリケーションサーバー
* データベース。

   ![](assets/formation_exploitation.png)

次の図は、最小アーキテクチャのコンテキストに関係するトラフィックは次のみであることを示しています。

1. インターネットを介したAdobe CampaignサーバーへのHTTPプロトコルトラフィック
1. インターネットを介したAdobe Campaignサーバーとの間のSMTPプロトコルトラフィック。

## 分散アーキテクチャ {#distributed-architecture}

Adobe Campaignは複数のモジュールで構成され、複数のマシンに分類できます。 この動作モードには、次のような利点があります。

* 負荷分散
* モジュールの冗長性の設定
* 複数のサービスプロバイダーに分類されたアーキテクチャの構築（提供されるサービスのセグメント化）。

![](assets/architecturerepartie.png)

複数のマシンにわたるモジュールの配布により、使用の柔軟性が高く、適応性が向上します。

>[!NOTE]
>
>様々なアーキテクチャについて詳しくは、[この節](../../installation/using/general-architecture.md)を参照してください。

## オープン・ポートのリスト{#list-of-open-ports}

| ポート番号 | 対象となるAdobe Campaignモジュールまたはアプリケーション | 設定可能 |
|---|---|---|
| 443/tcpまたは80/tcp | Webサーバー(Apache/IIS) | はい |
| 6666/udp （ローカル） | Adobe Campaign:Syslogd | はい |
| 8005/tcp （ローカル） | Adobe Campaign:webモジュール | はい |
| 8080/tcp | Adobe Campaign:webモジュール(tomcat) | はい |
| 7777 | 統計サーバ（統計サーバ） | はい |
