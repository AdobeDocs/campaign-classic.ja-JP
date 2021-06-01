---
product: campaign
title: 標準デプロイメント
description: 標準デプロイメント
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 4df126fa-4a6e-46a7-af6e-1e2e97f0072e
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 7%

---

# 標準デプロイメント{#standard-deployment}

この構成では、次の3台のコンピュータが必要です。

* LAN内のアプリケーションサーバー（エンドユーザー向けのキャンペーンの準備、レポート作成など）
* ロードバランサーの後ろのDMZに2つの正面サーバー。

DMZの2台のサーバは、トラッキング、ミラーページ、配信を処理し、高可用性を実現するために冗長化されています。

LAN内のアプリケーションサーバーは、エンドユーザーに対してサービスを提供し、すべての繰り返しプロセス（ワークフローエンジン）を実行します。 したがって、フロントサーバーでピーク負荷に達した場合、アプリケーションユーザーは影響を受けません。

データベース・サーバは、これら3台とは別のコンピュータでホストできます。 オペレーティングシステムがAdobe Campaign（LinuxまたはWindows）でサポートされている限り、アプリケーションサーバーとデータベースサーバーがLAN内で同じコンピューターを共有することはありません。

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_001_ncs_install_standardconfig.png)

このタイプの設定では、データベースサーバー（および利用可能な帯域幅）が主な制限要因として、多数の受信者(500,000～1,000,000)を処理できます。

## 機能 {#features}

### メリット {#advantages}

* フェイルオーバー機能：ハードウェア上の問題が発生した場合に、プロセスを1台のコンピュータに切り替える機能。
* MTAとリダイレクト機能は、ロードバランサーの背後にある両方のコンピューターにデプロイできるので、全体的なパフォーマンスが向上します。 2つのアクティブなMTAと十分な帯域幅を備えた場合、1時間あたり100,000件のメールの地域でブロードキャストレートを達成できます。

## インストールと設定の手順{#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 3台のコンピュータすべてのJDK
* Webサーバー(IIS、Apache)は、両方のフロントで
* 3台のコンピュータすべてでデータベース・サーバにアクセス
* POP3を介してアクセス可能なバウンスメールボックス
* 2つのDNSエイリアスの作成：

   * 最初に公開されたのは、仮想IPアドレス(VIP)上のロードバランサーをトラッキングし、それを指し、2つのフロントサーバーに配布されるためです。
   * 2つ目は、コンソールを介してアクセスし、同じアプリケーションサーバーを指すために、内部ユーザーに公開されます。

* STMP(25)、DNS(53)、HTTP(80)、HTTPS(443)、SQL(1521)(Oracle用)、5432（PostgreSQL用）などを開くように設定されたファイアウォール ポート。 詳しくは、[データベースアクセス](../../installation/using/network-configuration.md#database-access)の節を参照してください。

### アプリケーションサーバー{#installing-the-application-server}のインストール

次の手順に従って、Adobe Campaignアプリケーションサーバーからデータベースの作成にスタンドアロンインスタンスをインストールします（手順12）。 [インストールと設定（シングルマシン）](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-)を参照してください。

コンピューターはトラッキングサーバーではないので、Webサーバーとの統合を考慮しないでください。

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンスの名前：**demo**
* DNSマスク：**console.campaign.net***（クライアントコンソール接続およびレポートの場合のみ）
* 言語：英語
* データベース：**campaign:demo@dbsrv**

### 2台のフロントサーバーの取り付け{#installing-the-two-frontal-servers}

インストールおよび設定手順は、両方のコンピュータで同じです。

手順は、以下のとおりです。

1. Adobe Campaignサーバーをインストールします。

   詳しくは、 [LinuxでのCampaignのインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md)(Linux)および[WindowsでのCampaignのインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md)(Windows)を参照してください。

1. 次の節で説明するWebサーバー統合手順(IIS、Apache)に従います。

   * Linuxの場合：[Linux用Webサーバーへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windowsの場合：[Windows用Webサーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)

1. **demo**&#x200B;インスタンスを作成します。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、[インスタンスの作成と](../../installation/using/creating-an-instance-and-logging-on.md)でのログオンを参照してください。

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*
      ```

      詳しくは、[インスタンスの作成](../../installation/using/command-lines.md#creating-an-instance)を参照してください。
   インスタンスの名前は、アプリケーションサーバーの名前と同じです。

   **nlserver web**&#x200B;モジュール（ミラーページ、購読解除）を使用したサーバーへの接続は、ロードバランサー(tracking.campaign.net)のURLから確立されます。

1. **内部**&#x200B;をアプリケーションサーバーと同じに変更します。

   詳細については、[このセクション](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. データベースをインスタンスにリンクします。

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. **config-default.xml**&#x200B;と&#x200B;**config-demo.xml**&#x200B;ファイルで、**web**、**trackinglogd**&#x200B;および&#x200B;**mta**&#x200B;モジュールを有効にします。

   詳細については、[このセクション](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. **serverConf.xml**&#x200B;ファイルを編集し、次の内容を設定します。

   * MTAモジュールのDNS設定：

      ```
      <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
      ```

      >[!NOTE]
      >
      >**nameServers**&#x200B;パラメーターはWindowsでのみ使用されます。

      詳しくは、[配信設定](configure-delivery-settings.md)を参照してください。

   * リダイレクトパラメーターの冗長なトラッキングサーバー：

      ```
      <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
      <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
      ```

      詳しくは、[冗長なトラッキング](configuring-campaign-server.md#redundant-tracking)を参照してください。

1. Webサイトを起動し、次のURLからリダイレクトをテストします。[https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test).

   ブラウザーには、次のメッセージが表示されます（ロードバランサーによってリダイレクトされたURLに応じて異なります）。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linuxの場合：[Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windowsの場合：[Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバーを起動します。
1. Adobe Campaignコンソールで、パスワードなしで&#x200B;**admin**&#x200B;ログインを使用して接続し、デプロイウィザードを起動します。

   詳しくは、[インスタンスのデプロイ](../../installation/using/deploying-an-instance.md)を参照してください。

   設定は、トラッキングモジュールの設定以外は、スタンドアロンインスタンスと同じです。

1. リダイレクトに使用する外部URL（ロードバランサーのURL）と、2つのフロントサーバーの内部URLを設定します。

   詳しくは、[トラッキング設定](../../installation/using/deploying-an-instance.md#tracking-configuration)を参照してください。

   ![](assets/d_ncs_install_tracking2.png)

   >[!NOTE]
   >
   >前に作成した2つのトラッキングサーバーの既存のインスタンスを使用し、**内部**&#x200B;ログインを使用します。
