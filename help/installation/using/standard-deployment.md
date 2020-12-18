---
solution: Campaign Classic
product: campaign
title: 標準デプロイメント
description: 標準デプロイメント
audience: installation
content-type: reference
topic-tags: deployment-types-
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '832'
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

## インストールと設定の手順{#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 3台のコンピュータすべてのJDK
* Webサーバー(IIS、Apache)は、
* 3台のコンピュータすべてのデータベース・サーバへのアクセス、
* POP3経由でバウンスメールボックスにアクセス可能、
* 2つのDNSエイリアスの作成：

   * 最初に公開され、仮想IPアドレス(VIP)上のロードバランサーをトラッキングして指し示し、2つの正面サーバーに配布されます。
   * 2つ目は、内部ユーザーに対してコンソール経由でアクセスし、同じアプリケーションサーバーを指し示す形で表示されます。

* STMP (25)、DNS (53)、HTTP (80)、HTTPS (443)、SQL （1521 for PostgreSQLなど）を開くように設定されたファイアウォール ポート。 詳しくは、[データベースアクセス](../../installation/using/network-configuration.md#database-access)を参照してください。

### アプリケーションサーバーのインストール{#installing-the-application-server}

Adobe Campaignアプリケーションサーバーからデータベースの作成まで、スタンドアロンインスタンスをインストールする手順に従います（手順12）。 [インストールと設定（シングルマシン）](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-)を参照してください。

コンピューターはトラッキングサーバーではないので、Webサーバーとの統合を考慮しないでください。

次の例では、インスタンスのパラメーターを示します。

* インスタンスの名前：**demo**
* DNSマスク：**console.console.キャンペーン.net***（クライアントコンソール接続とレポートのみ）
* 言語：英語
* データベース：**キャンペーン:demo@dbsrv**

### 2台のフロントサーバーの設置{#installing-the-two-frontal-servers}

インストールと構成の手順は、両方のコンピューターで同じです。

手順は、以下のとおりです。

1. Adobe Campaignサーバーをインストールします。

   詳しくは、[Linuxでのキャンペーンインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md)(Linux)および[Windowsでのキャンペーンインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md)(Windows)を参照してください。

1. 次の節で説明するWebサーバー統合手順(IIS、Apache)に従います。

   * Linuxの場合：[Linux用のWebサーバーへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windowsの場合：[Windows用のWebサーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)

1. **demo**&#x200B;インスタンスを作成します。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、[インスタンスの作成と](../../installation/using/creating-an-instance-and-logging-on.md)へのログを参照してください。

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*
      ```

      詳しくは、[インスタンスの作成](../../installation/using/command-lines.md#creating-an-instance)を参照してください。
   インスタンスの名前は、アプリケーションサーバーの名前と同じです。

   **nlserver web**&#x200B;モジュール(ミラーページ、購読解除)を使用したサーバーへの接続は、ロードバランサー(tracking.キャンペーン.net)のURLから行われます。

1. **internal**&#x200B;をアプリケーションサーバーと同じに変更します。

   詳しくは、[内部識別子](../../installation/using/campaign-server-configuration.md#internal-identifier)を参照してください。

1. データベースをインスタンスにリンクする：

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. **config-default.xml**&#x200B;と&#x200B;**config-demo.xml**&#x200B;ファイルで、**web**、**trackinglogd**&#x200B;と&#x200B;**mta**&#x200B;モジュールを有効にします。

   詳しくは、[プロセスの有効化](../../installation/using/campaign-server-configuration.md#enabling-processes)を参照してください。

1. **serverConf.xml**&#x200B;ファイルを編集し、次の内容を入力します。

   * MTAモジュールのDNS設定：

      ```
      <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
      ```

      >[!NOTE]
      >
      >**nameServers**&#x200B;パラメーターはWindowsでのみ使用されます。

      詳しくは、[配信設定](../../installation/using/campaign-server-configuration.md#delivery-settings)を参照してください。

   * リダイレクトパラメーターの冗長なトラッキングサーバー：

      ```
      <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
      <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
      ```

      詳しくは、[冗長トラッキング](../../installation/using/configuring-campaign-server.md#redundant-tracking)を参照してください。

1. Webサイトを開始し、URLからのリダイレクトをテストします。[https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test).

   ブラウザーには、次のメッセージが表示されます（ロードバランサーによってリダイレクトされるURLに応じて異なります）。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合：[Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windowsの場合：[Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバーの開始。
1. Adobe Campaignコンソールで、パスワードを入力せずに&#x200B;**admin**&#x200B;ログインを使用して接続し、展開ウィザードを起動します。

   詳しくは、[インスタンスのデプロイ](../../installation/using/deploying-an-instance.md)を参照してください。

   設定は、トラッキングモジュールの設定とは別に、スタンドアロンインスタンスと同じです。

1. リダイレクトに使用する外部URL（ロードバランサーの外部URL）と、2つのフロントサーバーの内部URLを入力します。

   詳しくは、[トラッキングの設定](../../installation/using/deploying-an-instance.md#tracking-configuration)を参照してください。

   ![](assets/d_ncs_install_tracking2.png)

   >[!NOTE]
   >
   >以前に作成した2つのトラッキングサーバーの既存のインスタンスを使用し、**内部**&#x200B;ログインを使用します。

