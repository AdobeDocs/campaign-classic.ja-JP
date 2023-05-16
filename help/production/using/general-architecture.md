---
product: campaign
title: 一般的なアーキテクチャ
description: 一般的なアーキテクチャ
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: production
content-type: reference
topic-tags: introduction
exl-id: 3bfb5448-6996-4080-bf9a-434f1207637e
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 4%

---

# 一般的なアーキテクチャ{#general-architecture}



## 最小アーキテクチャ {#minimum-architecture}

最小限の設定では、Adobe Campaignは次の機能を使用して動作します。

* Adobe Campaignアプリケーションサーバー
* データベース。

   ![](assets/formation_exploitation.png)

次の図は、最小アーキテクチャのコンテキストで関係するトラフィックは次のみであることを示しています。

1. インターネットを介したAdobe Campaignサーバーへの HTTP プロトコルトラフィック
1. インターネット経由でAdobe Campaignサーバーとの間で送信される SMTP プロトコルトラフィック。

## 分散アーキテクチャ {#distributed-architecture}

Adobe Campaignは、複数のモジュールで構成され、複数のマシンに分類できます。 この動作モードには、次のような利点があります。

* 負荷分散
* モジュールの冗長性の設定
* 複数のサービスプロバイダー（提供されるサービスのセグメント化）にわたって分類されたアーキテクチャの構築。

![](assets/architecturerepartie.png)

複数のマシンにわたるモジュールの配布により、使用の柔軟性が高く、適応性が向上します。

>[!NOTE]
>
>様々なアーキテクチャについて詳しくは、 [この節](../../installation/using/general-architecture.md).

## オープンポートのリスト {#list-of-open-ports}

| ポート番号 | 関係するAdobe Campaignモジュールまたはアプリケーション | 設定可能 |
|---|---|---|
| 443/tcp または 80/tcp | Web サーバー (Apache/IIS) | はい |
| 6666/udp （ローカル） | Adobe Campaign:Syslogd | はい |
| 8005/tcp （ローカル） | Adobe Campaign:web モジュール | はい |
| 8080/tcp | Adobe Campaign:web モジュール (tomcat) | はい |
| 7777 | 統計サーバ（統計サーバ） | はい |
