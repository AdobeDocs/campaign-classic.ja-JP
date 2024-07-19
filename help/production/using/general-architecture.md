---
product: campaign
title: 一般的なアーキテクチャ
description: 一般的なアーキテクチャ
feature: Monitoring, Architecture
audience: production
content-type: reference
topic-tags: introduction
exl-id: 3bfb5448-6996-4080-bf9a-434f1207637e
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---

# 一般的なアーキテクチャ{#general-architecture}



## 最小アーキテクチャ {#minimum-architecture}

最小限の設定では、Adobe Campaignは次の環境で動作します。

* Adobe Campaign アプリケーションサーバー
* データベース。

  ![](assets/formation_exploitation.png)

次の図は、最小アーキテクチャのコンテキストに関連するトラフィックが次のみであることを示しています。

1. インターネット経由のAdobe Campaign サーバーへの HTTP プロトコルトラフィック。
1. インターネットを介したAdobe Campaign サーバーとの間の SMTP プロトコルトラフィック。

## 分散アーキテクチャ {#distributed-architecture}

Adobe Campaignは、複数のマシンに分割できる複数のモジュールで構成されています。 この動作モードには、次のようないくつかの利点があります。

* ロード・バランシング
* モジュールの冗長性の設定
* 複数のサービスプロバイダーに分類されたアーキテクチャの構築（提供されるサービスのセグメント化）。

![](assets/architecturerepartie.png)

複数のマシンにモジュールを配布することで、優れた柔軟性の利用と適応性の向上が可能になります。

>[!NOTE]
>
>様々なアーキテクチャについて詳しくは、[ この節 ](../../installation/using/general-architecture.md) を参照してください。

## 開いているポートのリスト {#list-of-open-ports}

| ポート番号 | 関係するAdobe Campaign モジュールまたはアプリケーション | 設定可能 |
|---|---|---|
| 443/tcp または 80/tcp | Web サーバー（Apache/IIS） | はい |
| 6666/udp （ローカル） | Adobe Campaign:Syslogd | はい |
| 8005/tcp （ローカル） | Adobe Campaign:web モジュール | はい |
| 8080/tcp | Adobe Campaign:web モジュール（tomcat） | はい |
| 7777 | 統計サーバー（統計サーバー） | はい |
