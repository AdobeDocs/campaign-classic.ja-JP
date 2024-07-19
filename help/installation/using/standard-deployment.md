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

* STMP （25）、DNS （53）、HTTP （80）、HTTPS （443）、SQL （Oracle用 1521、PostgreSQL 用 5432 など）を開くように設定されたファイアウォール ポート。 詳しくは、[ データベースアクセス ](../../installation/using/network-configuration.md#database-access) の節を参照してください。

### アプリケーションサーバーのインストール {#installing-the-application-server}

手順に従って、Adobe Campaign アプリケーションサーバーからデータベースを作成するスタンドアロンインスタンスをインストールします（手順 12）。 [ インストールと設定（単一マシン） ](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-) を参照してください。

コンピューターはトラッキングサーバーではないので、web サーバーとの統合を考慮しないでください。

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンスの名前：**demo**
* DNS マスク：**console.campaign.net&#42;** （クライアントコンソール接続およびレポートの場合のみ）
* Language: English
* データベース：**campaign:demo@dbsrv**

### 2 つのフロントサーバーのインストール {#installing-the-two-frontal-servers}

インストールと構成の手順は、両方のコンピュータで同じです。

手順は、以下のとおりです。

1. Adobe Campaign サーバーをインストールします。

   詳しくは、[Linux](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) での Campaign インストールの前提条件（Linux）および [Windows](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) での Campaign インストールの前提条件（Windows）を参照してください。

1. 次の項で説明する Web サーバー統合手順（IIS、Apache）に従います。

   * Linux の場合：[Linux 用の web サーバーへの統合 ](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windows の場合：[Windows の Web サーバーへの統合 ](../../installation/using/integration-into-a-web-server-for-windows.md)

1. **demo** インスタンスを作成します。 それには、次の 2 つの方法があります。

   * コンソールを使用してインスタンスを作成します。

     ![](assets/install_create_new_connexion.png)

     詳しくは、[ インスタンスの作成とログオン ](../../installation/using/creating-an-instance-and-logging-on.md) を参照してください。

     または

   * コマンドラインを使用してインスタンスを作成します。

     ```
     nlserver config -addinstance:demo/tracking.campaign.net*
     ```

     詳しくは、[ インスタンスの作成 ](../../installation/using/command-lines.md#creating-an-instance) を参照してください。

   インスタンスの名前は、アプリケーションサーバーの名前と同じです。

   **nlserver web** モジュール（ミラーページ、購読解除）を持つサーバーへの接続は、ロードバランサーの URL （tracking.campaign.net）から行われます。

1. **internal** をアプリケーションサーバーと同じに変更します。

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. データベースをインスタンスにリンクします。

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. **config-default.xml** および **config-demo.xml** ファイルで、**web**、**trackinglogd** および **mta** モジュールを有効にします。

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. **serverConf.xml** ファイルを編集し、次の情報を入力します。

   * mta モジュールの DNS 設定：

     ```
     <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
     ```

     >[!NOTE]
     >
     >**nameServers** パラメーターは Windows でのみ使用されます。

     詳しくは、[ 配信設定 ](configure-delivery-settings.md) を参照してください。

   * リダイレクトパラメーターの冗長なトラッキングサーバー：

     ```
     <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
     <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
     ```

     詳しくは、[ 冗長トラッキング ](configuring-campaign-server.md#redundant-tracking) を参照してください。

1. Web サイトを起動して、URL [https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test) からリダイレクトをテストします。

   ブラウザーには、（ロードバランサーによってリダイレクトされた URL に応じて）次のメッセージが表示されます。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linux の場合：[Web サーバーの起動と設定のテスト ](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windows の場合：[Web サーバーの起動と設定のテスト ](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaign サーバーを起動します。
1. Adobe Campaign コンソールで、パスワードなしで **admin** ログインを使用して接続し、デプロイメントウィザードを起動します。

   詳しくは、[ インスタンスのデプロイ ](../../installation/using/deploying-an-instance.md) を参照してください。

   トラッキングモジュールの設定を除けば、設定はスタンドアロンインスタンスと同じです。

1. リダイレクトに使用される外部 URL （ロードバランサーの URL）と、2 つのフロントサーバーの内部 URL を入力します。

   詳しくは、[ トラッキング設定 ](../../installation/using/deploying-an-instance.md#tracking-configuration) を参照してください。

   ![](assets/d_ncs_install_tracking2.png)

   >[!NOTE]
   >
   >以前に作成した 2 つのトラッキングサーバーの既存のインスタンスを使用し、**internal** ログインを使用します。
