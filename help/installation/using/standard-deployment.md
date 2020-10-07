---
title: 標準デプロイメント
seo-title: 標準デプロイメント
description: 標準デプロイメント
seo-description: null
page-status-flag: never-activated
uuid: e2f9c4d9-4b36-4899-9954-493135597057
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: deployment-types-
discoiquuid: d714b759-cc08-4656-876c-9820d5c56216
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---


# 標準デプロイメント{#standard-deployment}

この構成では、3台のコンピューターが必要です。

* LAN内のエンドユーザ向けのアプリケーションサーバ(キャンペーン、レポートなどの作成)、
* ロードバランサーの背後のDMZにある2台の正面サーバー。

DMZ内の2台のサーバは、トラッキング、ミラーページ、配信を処理し、高可用性を実現するために冗長化されています。

LAN内のアプリケーションサーバーは、エンドユーザーに対してサービスを提供し、すべての繰り返しプロセス(ワークフローエンジン)を実行します。 したがって、前頭サーバーでピーク負荷に達した場合、アプリケーションユーザーは影響を受けません。

データベース・サーバは、これら3台とは別のコンピュータにホストできます。 オペレーティングシステムがAdobe Campaign（LinuxまたはWindows）でサポートされている限り、アプリケーションサーバーとデータベースサーバーはLAN内で同じコンピューターを共有します。

サーバとプロセス間の一般的な通信は、次のスキーマに従って行われます。

![](assets/s_001_ncs_install_standardconfig.png)

このタイプの設定では、データベースサーバ（および使用可能な帯域幅）が主な制限要因となるので、大量の受信者(500,000 ～ 1,000,000)を処理できます。

## 機能 {#features}

### メリット {#advantages}

* フェイルオーバー機能：他方のコンピューターでハードウェアに問題が発生した場合に、プロセスを一方のコンピューターに切り替える機能。
* MTAとリダイレクト機能はロードバランサーの背後にある両方のコンピューターに展開できるので、全体的なパフォーマンスが向上します。 2つのアクティブなMTAと十分な帯域幅がある場合、1時間あたり100,000件のメールの領域でブロードキャストレートを達成できます。

## インストールと設定の手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 3台のコンピュータすべてのJDK
* Webサーバー(IIS、Apache)は、
* 3台のコンピュータすべてのデータベース・サーバへのアクセス、
* POP3経由でバウンスメールボックスにアクセス可能、
* 2つのDNSエイリアスの作成：

   * 最初に公開され、仮想IPアドレス(VIP)上のロードバランサーをトラッキングして指し示し、2つの正面サーバーに配布されます。
   * 2つ目は、内部ユーザーに対してコンソール経由でアクセスし、同じアプリケーションサーバーを指し示す形で表示されます。

* STMP (25)、DNS (53)、HTTP (80)、HTTPS (443)、SQL （Oracleの場合は1521、PostgreSQLの場合は5432など）を開くように設定されたファイアウォール ポート。 詳細は、「 [データベースアクセス](../../installation/using/network-configuration.md#database-access)」を参照してください。

### アプリケーションサーバーのインストール {#installing-the-application-server}

Adobe Campaignアプリケーションサーバーからデータベースの作成まで、スタンドアロンインスタンスをインストールする手順に従います（手順12）。 『 [インストールと設定（シングルマシン）』を参照してください](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-)。

コンピューターはトラッキングサーバーではないので、Webサーバーとの統合を考慮しないでください。

次の例では、インスタンスのパラメーターを示します。

* インスタンスの名前： **デモ**
* DNSマスク： **console.キャンペーン.net*** （クライアントコンソール接続およびレポートの場合のみ）
* 言語：英語
* データベース： **キャンペーン:demo@dbsrv**

### 2台のフロントサーバーのインストール {#installing-the-two-frontal-servers}

インストールと構成の手順は、両方のコンピューターで同じです。

手順は、以下のとおりです。

1. Adobe Campaignサーバーをインストールします。

   詳しくは、「Linuxでのキャンペーンインストールの [前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) (Linux)」および「Windowsでのキャンペーンインストールの [前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) (Windows)」を参照してください。

1. 次の節で説明するWebサーバー統合手順(IIS、Apache)に従います。

   * For Linux: [Integration into a Web server for Linux](../../installation/using/integration-into-a-web-server-for-linux.md)
   * For Windows: [Integration into a Web server for Windows](../../installation/using/integration-into-a-web-server-for-windows.md)

1. デ **モインスタンスを作成します** 。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、「インスタンスの [作成とログオン」を参照してください](../../installation/using/creating-an-instance-and-logging-on.md)。

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*
      ```

      For more on this, refer to [Creating an instance](../../installation/using/command-lines.md#creating-an-instance).
   インスタンスの名前は、アプリケーションサーバーの名前と同じです。

   nlserver web **ミラーページ(購読解除ー、キャンペーン)を使用してサーバーに接続する場合、ロードバランサー(tracking.** server.net)のURLから接続します。

1. 内 **部をアプリケーションサーバーと同じ** に変更します。

   For more on this, refer to [Internal identifier](../../installation/using/campaign-server-configuration.md#internal-identifier).

1. データベースをインスタンスにリンクする：

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. config-default.xml **ファイルとconfig-demo.xml** ファイルで、 **web** 、 **loggd、およびtrackingtaモジュールを有効にし********** ます。

   For more on this, refer to [Enabling processes](../../installation/using/campaign-server-configuration.md#enabling-processes).

1. serverConf.xml **ファイルを編集し** 、次の内容を入力します。

   * MTAモジュールのDNS設定：

      ```
      <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
      ```

      >[!NOTE]
      >
      >nameServers **パラメーターは** 、Windowsでのみ使用されます。

      For more on this, refer to [Delivery settings](../../installation/using/campaign-server-configuration.md#delivery-settings).

   * リダイレクトパラメーターの冗長なトラッキングサーバー：

      ```
      <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
      <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
      ```

      For more on this, refer to [Redundant tracking](../../installation/using/configuring-campaign-server.md#redundant-tracking).

1. Webサイトを開始し、URLからのリダイレクトをテストします。 [https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test).

   ブラウザーには、次のメッセージが表示されます（ロードバランサーによってリダイレクトされるURLに応じて異なります）。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合： [Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windowsの場合： [Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバーの開始。
1. Adobe Campaignコンソールで、パスワードを入力しないで **admin** loginを使用して接続し、デプロイメントウィザードを起動します。

   For more on this, refer to [Deploying an instance](../../installation/using/deploying-an-instance.md).

   設定は、トラッキングモジュールの設定とは別に、スタンドアロンインスタンスと同じです。

1. リダイレクトに使用する外部URL（ロードバランサーの外部URL）と、2つのフロントサーバーの内部URLを入力します。

   For more on this, refer to [Tracking configuration](../../installation/using/deploying-an-instance.md#tracking-configuration).

   ![](assets/d_ncs_install_tracking2.png)

   >[!NOTE]
   >
   >前の手順で作成した2つのトラッキングサーバーの既存のインスタンスを使用し、 **内部ログインを使用します** 。

