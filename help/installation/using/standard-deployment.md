---
product: campaign
title: 標準デプロイメント
description: 標準デプロイメント
feature: Installation, Architecture, Deployment
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 4df126fa-4a6e-46a7-af6e-1e2e97f0072e
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 7%

---

# 標準デプロイメント{#standard-deployment}



この構成では、次の 3 台のコンピュータが必要です。

* エンドユーザー（キャンペーンの準備、レポート作成など）向けの LAN 内のアプリケーションサーバー
* ロードバランサーの後ろの DMZ に 2 つのフロントサーバー。

DMZ の 2 台のサーバーは、トラッキング、ミラーページ、配信を処理し、高可用性を実現するために冗長化されています。

LAN 内のアプリケーションサーバーは、エンドユーザーに対してサービスを提供し、すべての反復プロセス（ワークフローエンジン）を実行します。 したがって、フロントサーバーでピーク負荷に達した場合、アプリケーションユーザーは影響を受けません。

データベース・サーバは、これら 3 台とは別のコンピュータでホストできます。 オペレーティングシステムがAdobe Campaign（Linux または Windows）でサポートされている限り、アプリケーションサーバーとデータベースサーバーは LAN 内で同じコンピューターを共有します。

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_001_ncs_install_standardconfig.png)

このタイプの設定では、データベースサーバー（および利用可能な帯域幅）が主な制限要因として、多数の受信者 (500,000～1,000,000) を処理できます。

## 機能 {#features}

### メリット {#advantages}

* フェイルオーバー機能：ハードウェアの問題が発生した場合に、プロセスを 1 台のコンピュータに切り替える機能。
* MTA とリダイレクト機能はロードバランサーの背後にある両方のコンピューターにデプロイできるので、全体的なパフォーマンスが向上しました。 2 つのアクティブな MTA と十分な帯域幅を備えた場合、1 時間に 100,000 件のメールの領域でブロードキャストレートを達成できます。

## インストールおよび設定の手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 3 台のコンピュータすべてで JDK を使用する。
* Web サーバー (IIS、Apache) の両方のフロントで、
* 3 台のコンピュータすべてでデータベース・サーバにアクセスする
* POP3 経由でアクセス可能なバウンスメールボックス
* 2 つの DNS エイリアスの作成：

   * 最初の公開は、トラッキング用に公開され、仮想 IP アドレス (VIP) 上のロードバランサーを指し、その後、2 つのフロントサーバーに配布されます。
   * 2 つ目は、コンソールを介してアクセスし、同じアプリケーションサーバーを指すように、内部ユーザーに公開されます。

* STMP(25)、DNS(53)、HTTP(80)、HTTPS(443)、SQL(1521Oracle用、5432（PostgreSQL 用など）を開くように設定されたファイアウォール ポート。 詳しくは、を参照してください。 [データベースアクセス](../../installation/using/network-configuration.md#database-access).

### アプリケーションサーバーのインストール {#installing-the-application-server}

手順に従って、Adobe Campaignアプリケーションサーバーからデータベースの作成にスタンドアロンインスタンスをインストールします（手順 12）。 参照： [インストールと設定（シングルマシン）](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-).

コンピューターはトラッキングサーバーではないので、Web サーバーとの統合を考慮しないでください。

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンスの名前： **デモ**
* DNS マスク： **console.campaign.net&#42;** （クライアントコンソール接続およびレポートの場合のみ）
* 言語：英語
* データベース： **campaign:demo@dbsrv**

### 2 つのフロントサーバーのインストール {#installing-the-two-frontal-servers}

インストールおよび設定手順は、両方のコンピュータで同じです。

手順は、以下のとおりです。

1. Adobe Campaignサーバーをインストールします。

   詳しくは、 [Linux での Campaign のインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) (Linux) および [Windows での Campaign のインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) (Windows)。

1. 次の節で説明されている Web サーバー統合手順 (IIS、Apache) に従います。

   * Linux の場合： [Linux 用 Web サーバーへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windows の場合： [Windows 用 Web サーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)

1. を作成します。 **デモ** インスタンス。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

     ![](assets/install_create_new_connexion.png)

     詳しくは、 [インスタンスの作成とログオン](../../installation/using/creating-an-instance-and-logging-on.md).

     または

   * コマンドラインを使用してインスタンスを作成します。

     ```
     nlserver config -addinstance:demo/tracking.campaign.net*
     ```

     詳しくは、 [インスタンスの作成](../../installation/using/command-lines.md#creating-an-instance).

   インスタンスの名前は、アプリケーションサーバーの名前と同じです。

   を使用したサーバーへの接続 **nlserver web** モジュール（ミラーページ、購読解除）は、ロードバランサー (tracking.campaign.net) の URL から作成されます。

1. 次を変更： **内部** をアプリケーションサーバーと同じに設定します。

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. データベースをインスタンスにリンクします。

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. Adobe Analytics の **config-default.xml** および **config-demo.xml** ファイル、有効化 **web**, **trackinglogd** および **mta** モジュール。

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. を編集します。 **serverConf.xml** ファイルと入力：

   * MTA モジュールの DNS 設定：

     ```
     <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
     ```

     >[!NOTE]
     >
     >The **nameServers** パラメーターは、Windows でのみ使用されます。

     詳しくは、 [配信設定](configure-delivery-settings.md).

   * リダイレクトパラメーターの冗長なトラッキングサーバー：

     ```
     <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
     <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
     ```

     詳しくは、 [重複した追跡](configuring-campaign-server.md#redundant-tracking).

1. Web サイトを開始し、次の URL からリダイレクトをテストします。 [https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test).

   ブラウザーには、次のメッセージが表示されます（ロードバランサーによってリダイレクトされた URL に応じて異なります）。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linux の場合： [Web サーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windows の場合： [Web サーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバーを起動します。
1. Adobe Campaignコンソールで、 **admin** パスワードを使用せずにログインし、デプロイウィザードを起動します。

   詳しくは、 [インスタンスのデプロイ](../../installation/using/deploying-an-instance.md).

   設定は、トラッキングモジュールの設定以外は、スタンドアロンインスタンスと同じです。

1. リダイレクトに使用する外部 URL（ロードバランサーの URL）と、2 つのフロントサーバーの内部 URL を設定します。

   詳しくは、 [トラッキング設定](../../installation/using/deploying-an-instance.md#tracking-configuration).

   ![](assets/d_ncs_install_tracking2.png)

   >[!NOTE]
   >
   >ここでは、以前に作成した 2 つのトラッキングサーバーの既存のインスタンスを使用し、 **内部** ログインします。
