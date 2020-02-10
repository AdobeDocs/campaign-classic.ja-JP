---
title: スタンドアロンの展開
seo-title: スタンドアロンの展開
description: スタンドアロンの展開
seo-description: null
page-status-flag: never-activated
uuid: 48ce793e-cb9f-4102-898f-758512cb9bf2
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: deployment-types-
discoiquuid: 9834638f-a8bb-4969-9f8d-99b8d9fdb1ca
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 5f3ceab5ee82587d9f1829792bdabf2209f793cd

---


# スタンドアロンの展開{#standalone-deployment}

この設定には、同じコンピューター上のすべてのコンポーネントが含まれます。

* アプリケーションプロセス(Web)、
* 配信プロセス(mta)、
* リダイレクトプロセス（トラッキング）、
* ワークフロープロセスとスケジュールされたタスク(wfserver)、
* 直帰メールプロセス(inMail)、
* 統計プロセス(stat)。

プロセス間の全体的な通信は、次のスキーマに従って実行されます。

![](assets/s_900_ncs_install_standaloneconfig.png)

このタイプの設定は、100,000人未満の受信者のリストを管理する場合や、例えば次のソフトウェアレイヤーを使用する場合に実行できます。

* Linux、
* Apache、
* PostgreSQL,
* Qmail.

ボリュームが増えると、このアーキテクチャの一種により、パフォーマンスを向上させるためにデータベース・サーバが別のコンピュータに移動されます。

>[!NOTE]
>
>十分なリソースがある場合は、既存のデータベース・サーバも使用できます。

## 機能 {#features}

### メリット {#advantages}

* 完全なスタンドアロンおよび低い構成コスト（以下に示すオープンソースソフトウェアを使用する場合は、課金対象ライセンスは不要）。
* シンプルなインストールとネットワーク構成

### 欠点 {#disadvantages}

* 事故が発生した場合の重要なコンピュータ。
* メッセージをブロードキャストする際の帯域幅が限られている（当社の経験上、1時間あたり数万通のメール）。
* 放送時のアプリの遅延の可能性。
* アプリケーションサーバーは、リダイレクトサーバーをホストするので、外部から（例えばDMZ内にある間）利用可能である必要があります。

## インストールと設定の手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* JDK,
* Webサーバー(IIS、Apache)、
* データベース・サーバへのアクセス、
* POP3経由でバウンスメールボックスにアクセス可能、
* 2つのDNSエイリアスの作成：

   * 最初に公開され、その公開IP上のコンピュータを追跡し、指し示す。
   * コンソールにアクセスし、同じコンピュータを指すために、内部ユーザに公開される2番目のエイリアス。

* STMP (25)、DNS (53)、HTTP (80)、HTTPS (443)、SQL （Oracleの場合は1521、PostgreSQLの場合は5432など）を開くように設定されたファイアウォールポート。 詳細については、「ネットワークの設定」を参 [照してくださ](../../installation/using/network-configuration.md)い。

次の例では、インスタンスのパラメーターを示します。

* インスタンスの名前：デ **モ**
* DNSマスク： **console.campaign.net*** （クライアントコンソール接続およびレポートの場合のみ）
* データベース：キャンペ **ーン：demo@dbsrv**

### インストールと設定（シングルマシン） {#installing-and-configuring--single-machine-}

次の手順に従います。

1. Adobe Campaignサーバーのインストール手順に従います。Linuxの **nlserver** パッケージ、 **Windowsの** setup.exe。

   詳しくは、 [LinuxでのCampaignのインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) (Linux)およびWindowsでのCampaignのイ [ンストールの前提条件(Windows](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) )を参照してください。

1. Adobe Campaignサーバーがインストールされたら、 **nlserver web -tomcat** (Webモジュールを使用して、ポート8080でリッスンするスタンドアロンWebサーバーモードでTomcatを起動し、Tomcatが正しく起動することを確認します。

   ```
   12:08:18 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   12:08:18 >   Starting Web server module (pid=28505, tid=-1225184768)...
   12:08:18 >   Tomcat started
   12:08:18 >   Server started
   ```

   >[!NOTE]
   >
   >Webモジュールを初めて実行すると、 **config-default.xml** と **serverConf.xmlファイルがインストールフォルダーの** conf **** ディレクトリに作成されます。 serverConf.xmlで使用可能なすべてのパ **ラメーターを** 、この節に示 [します](../../installation/using/the-server-configuration-file.md)。

   Ctrl + cキ **ーを押して** 、サーバーを停止します。

   この詳細については、以下の節を参照してください。

   * Linuxの場合：サ [ーバの最初の起動](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)、
   * Windowsの場合：サ [ーバーの最初の起動](../../installation/using/installing-the-server.md#first-start-up-of-the-server)。

1. 次のコマンドを使 **用して** 、内部パスワードを変更します。

   ```
   nlserver config -internalpassword
   ```

   For more on this, refer to [Internal identifier](../../installation/using/campaign-server-configuration.md#internal-identifier).

1. 追跡用の **DNSマスク(この例では** tracking.campaign.net **)と、クライアントコンソール(この例では** console.campaign.net ****)へのアクセスを持つデモインスタンスを作成します。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、「インスタンスの作成とロ [グオン」を参照してください](../../installation/using/creating-an-instance-and-logging-on.md)。

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*,console.campaign.net*
      ```

      For more on this, refer to [Creating an instance](../../installation/using/command-lines.md#creating-an-instance).

1. (前の手順で **config-default.xml** )の隣に作成した **demo-config.xmlファイルを編集し、** mta ( **config-default.xml************** )を確認します。 次に、統計サーバーのアドレスを設定します。

   ```
   <?xml version='1.0'?>
   <serverconf>  
     <shared>    
       <!-- add lang="eng" to dataStore to force English for the instance -->    
       <dataStore hosts="tracking.campaign.net*,console.campaign.net*">      
         <mapping logical="*" physical="default"/>    
       </dataStore>  </shared>  
       <mta autoStart="true" statServerAddress="localhost"/>
       <wfserver autoStart="true"/>  
       <inMail autoStart="true"/>  
       <sms autoStart="false"/>  
       <listProtect autoStart="false"/>
   </serverconf>
   ```

   For more on this, refer to [Enabling processes](../../installation/using/campaign-server-configuration.md#enabling-processes).

1. serverConf.xml **ファイルを編集し** 、配信ドメインを指定し、MTAモジュールがMXタイプのDNSクエリに応答するために使用するDNSサーバーのIP（またはホスト）アドレスを指定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >nameServersパ **ラメーターは** 、Windowsでのみ使用されます。

   For more on this, refer to [Campaign server configuration](../../installation/using/campaign-server-configuration.md).

1. クライアントコンソールプログラム(**setup-client-7.XX**, **YYYY.exe（v7の場合）またはsetup-client-6.XX** , **yyyy.exe(********** v6の場合)をコピーし、eng/jsp/jspの場合)をコピーします。

   この詳細については、以下の節を参照してください。

   * Linuxの場合：Linux用のク [ライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合：Windows向け [クライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)

1. 以下の節で説明するWebサーバー統合手順(IIS、Apache)に従います。

   * Linuxの場合：Linux [用のWebサーバーへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windowsの場合：Windows [用Webサーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)

1. Webサイトを開始し、次のURLを使用してリダイレクトをテストします。https://tracking.campaign.net/r/test [](https://tracking.campaign.net/r/test).

   ブラウザーに次のメッセージを表示する必要があります。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="localhost"/>
   ```

   この詳細については、以下の節を参照してください。

   * Linuxの場合：Webサ [ーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windowsの場合：Webサ [ーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバー(**net start nlserver6** (Windows)、 **/etc/init.d/nlserver6 start** (Linux))を起動し、もう一度コマンドnlserver pdump **(nlserver pdump** )を実行して、すべての有効なモジュールの存在を確認します。

   ```
   12:09:54 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   syslogd@default (7611) - 9.2 MB
   stat@demo (5988) - 1.5 MB
   inMail@demo (7830) - 11.9 MB
   watchdog (27369) - 3.1 MB
   mta@demo (7831) - 15.6 MB
   wfserver@demo (7832) - 11.5 MB
   web@default (28671) - 40.5 MB
   ```

   また、このコマンドを使用すると、コンピューターにインストールされているAdobe Campaignサーバーのバージョンとビルド番号を知ることができます。

1. 次のURLを使用し **て、nlserver Web** moduleをテストします。https://console.campaign.net/nl/jsp/logon.jsp [](https://tracking.campaign.net/r/test)

   このURLを使用すると、クライアントセットアッププログラムのダウンロードページにアクセスできます。

   アクセス制御ペ **ージに到達したら** 、内部ログインと関連するパスワードを入力します。

   ![](assets/s_ncs_install_access_client.png)

   この詳細については、以下の節を参照してください。

   * Linuxの場合：Linux用のク [ライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合：Windows向け [クライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)

1. Adobe Campaignクライアントコンソールを起動し（前のダウンロードページから、またはWindowsインストールの場合はサーバー上で直接起動）、サーバー接続URLをhttps://console.campaign.net [に設定し](https://console.campaign.net) 、内部ログインを使用 **して** 接続します。

   詳しくは、イン [スタンスの作成とログオン](../../installation/using/creating-an-instance-and-logging-on.md) 、および内部識別 [子を参照してください](../../installation/using/campaign-server-configuration.md#internal-identifier)。

   初めてログインすると、データベース作成ウィザードが表示されます。

   ![](assets/s_ncs_install_db_oracle_creation01.png)

   ウィザードの手順に従って、接続インスタンスに関連付けられたデータベースを作成します。

   詳しくは、「データベースの作成と [設定」を参照してください](../../installation/using/creating-and-configuring-the-database.md)。

   データベースが作成されたら、ログオフします。

1. パスワードを指定せずに **admin** loginを使用してクライアントコンソールに再度ログオンし、デプロイメントウィザード(メニ **[!UICONTROL Tools > Advanced]** ュー)を起動してインスタンスの設定を完了します。

   詳しくは、「インスタンスのデプロイ」を [参照してください](../../installation/using/deploying-an-instance.md)。

   設定する主なパラメーターは次のとおりです。

   * 電子メール配信：バウンスメールの送信者と返信アドレス、およびエラーメールボックス。
   * 追跡：リダイレクトに使用する外部URLと内部URLを入力し、トラッキングサーバーの「 **Registration(s)** 」をクリックして、トラッキングサーバーのデモインスタンスで **** 検証します。

      For more on this, refer to [Tracking configuration](../../installation/using/deploying-an-instance.md#tracking-configuration).

      ![](assets/s_ncs_install_deployment_wiz_09.png)

      Adobe Campaignサーバーはアプリケーションサーバーとリダイレクトサーバーの両方で使用されるので、トラッキングログの収集とURLの転送に使用される内部URLは、Tomcat(https://localhost:8080)への直接内部接続です。

   * バウンス管理：バウンスメールを処理するパラメーターを入力します(「未処理のバウンスメ **ール** 」セクションは考慮しないでください)。
   * アクセス元：レポート用の2つのURL（Webフォームとミラーページ）を指定します。

      ![](assets/d_ncs_install_web_url.png)

