---
product: campaign
title: 標準デプロイメント
description: 標準デプロイメント
feature: Installation, Architecture, Deployment
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 4df126fa-4a6e-46a7-af6e-1e2e97f0072e
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 7%

---

# 標準デプロイメント{#standard-deployment}



この構成には、次の 3 台のコンピューターが必要です。

* LAN 内のエンドユーザー用アプリケーションサーバー（キャンペーンの準備、レポートなど）、
* ロードバランサーの背後にある DMZ 内の 2 つのフロントサーバー。

DMZ 内の 2 台のサーバーは、トラッキング、ミラーページおよび配信を処理し、高可用性のために冗長になります。

LAN 内のアプリケーションサーバーは、エンドユーザーにサービスを提供し、すべての繰り返しプロセス（ワークフローエンジン）を実行します。 したがって、フロントサーバーでピーク負荷に達した場合、アプリケーションユーザーは影響を受けません。

データベースサーバーは、これら 3 つとは別のコンピューターでホストできます。 それ以外の場合は、オペレーティングシステムがAdobe Campaign（Linux または Windows）でサポートされている限り、アプリケーションサーバーとデータベースサーバーは LAN 内で同じコンピューターを共有します。

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_001_ncs_install_standardconfig.png)

このタイプの設定では、多数の受信者（500,000 ～ 1,000,000 人）を処理できます。これは、データベースサーバー（および使用可能な帯域幅）が主な制限要因であるためです。

## 機能 {#features}

### メリット {#advantages}

* フェイルオーバー機能：一方のコンピュータでハードウェアの問題が発生した場合に、もう一方のコンピュータにプロセスを切り替える機能。
* ロードバランサーの背後にある両方のコンピューターに MTA とリダイレクト機能をデプロイできるので、全体的なパフォーマンスが向上します。 2 つのアクティブな MTA と十分な帯域幅を使用すると、1 時間あたり 100,000 件のメールの領域でブロードキャストレートを達成することが可能です。

## インストールと設定の手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 3 台のコンピューターすべてに JDK をインストールする。
* Web サーバー（IIS、Apache）を使用する場合
* 3 台のコンピュータ上のデータベース・サーバへのアクセス
* POP3 経由でアクセスできるバウンスメールボックス。
* 2 つの DNS エイリアスの作成：

   * 1 つ目はトラッキング用に公開され、VIP（virtual IP address）上のロードバランサーを指します。これは次に、2 つのフロントサーバーに配信されます。
   * 2 つ目は、コンソール経由でアクセスするために内部ユーザーに公開され、同じアプリケーションサーバーを指します。

* STMP （25）、DNS （53）、HTTP （80）、HTTPS （443）、SQL （Oracle用 1521、PostgreSQL 用 5432 など）を開くように設定されたファイアウォール ポート。 詳しくは、こちらを参照してください。 [データベースアクセス](../../installation/using/network-configuration.md#database-access).

### アプリケーションサーバーのインストール {#installing-the-application-server}

手順に従って、Adobe Campaign アプリケーションサーバーからデータベースを作成するスタンドアロンインスタンスをインストールします（手順 12）。 こちらを参照してください [インストールと設定（単一マシン）](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-).

コンピューターはトラッキングサーバーではないので、web サーバーとの統合を考慮しないでください。

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンス名： **デモ**
* DNS マスク： **console.campaign.net&#42;** （クライアントコンソール接続の場合とレポートの場合のみ）
* Language: English
* データベース： **campaign:demo@dbsrv**

### 2 つのフロントサーバーのインストール {#installing-the-two-frontal-servers}

インストールと構成の手順は、両方のコンピュータで同じです。

手順は、以下のとおりです。

1. Adobe Campaign サーバーをインストールします。

   詳しくは、次を参照してください [Linux での Campaign インストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) （Linux）と [Windows での Campaign インストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) （Windows）。

1. 次の項で説明する Web サーバー統合手順（IIS、Apache）に従います。

   * Linux 場合： [Linux 用 Web サーバーへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windows: [Windows 用 Web サーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)

1. を作成 **デモ** インスタンス。 それには、次の 2 つの方法があります。

   * コンソールを使用してインスタンスを作成します。

     ![](assets/install_create_new_connexion.png)

     詳しくは、次を参照してください [インスタンスの作成とログオン](../../installation/using/creating-an-instance-and-logging-on.md).

     または

   * コマンドラインを使用してインスタンスを作成します。

     ```
     nlserver config -addinstance:demo/tracking.campaign.net*
     ```

     詳しくは、次を参照してください [インスタンスの作成](../../installation/using/command-lines.md#creating-an-instance).

   インスタンスの名前は、アプリケーションサーバーの名前と同じです。

   を使用したサーバーへの接続 **nlserver web** モジュール （ミラーページ、購読解除）はロードバランサーの URL （tracking.campaign.net）から作成されます。

1. 変更： **内部** をアプリケーションサーバーと同じに変更します。

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. データベースをインスタンスにリンクします。

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. が含まれる **config-default.xml** および **config-demo.xml** ファイル、を有効にする **web**, **trackinglogd** および **mta** モジュール。

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. を編集する **serverConf.xml** ファイルに入力します。

   * mta モジュールの DNS 設定：

     ```
     <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
     ```

     >[!NOTE]
     >
     >この **nameServer** パラメーターは Windows でのみ使用されます。

     詳しくは、次を参照してください [配信設定](configure-delivery-settings.md).

   * リダイレクトパラメーターの冗長なトラッキングサーバー：

     ```
     <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
     <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
     ```

     詳しくは、次を参照してください [冗長トラッキング](configuring-campaign-server.md#redundant-tracking).

1. Web サイトを開始し、URL からリダイレクトをテストします。 [https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test).

   ブラウザーには、（ロードバランサーによってリダイレクトされた URL に応じて）次のメッセージが表示されます。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linux 場合： [Web サーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windows: [Web サーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaign サーバーを起動します。
1. Adobe Campaign コンソールで、を使用して接続します **admin** パスワードなしでログインし、配置ウィザードを起動します。

   詳しくは、次を参照してください [インスタンスのデプロイ](../../installation/using/deploying-an-instance.md).

   トラッキングモジュールの設定を除けば、設定はスタンドアロンインスタンスと同じです。

1. リダイレクトに使用される外部 URL （ロードバランサーの URL）と、2 つのフロントサーバーの内部 URL を入力します。

   詳しくは、次を参照してください [トラッキング設定](../../installation/using/deploying-an-instance.md#tracking-configuration).

   ![](assets/d_ncs_install_tracking2.png)

   >[!NOTE]
   >
   >前に作成した 2 つのトラッキングサーバーの既存のインスタンスを使用し、を使用します **内部** ログイン。
