---
title: スタンドアロンデプロイメント
seo-title: スタンドアロンデプロイメント
description: スタンドアロンデプロイメント
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
source-git-commit: f8d36b9fca9624500c5273eb73a1702f077dd60c
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 2%

---


# スタンドアロンデプロイメント{#standalone-deployment}

この設定には、同じコンピューター上のすべてのコンポーネントが含まれます。

* application process (web)、
* 配信プロセス(mta)、
* リダイレクトプロセス（追跡）、
* ワークフロープロセスとスケジュール済みタスク(wfserver)、
* バウンスメールプロセス(inMail)、
* 統計プロセス(stat)。

プロセス間の全体的な通信は、以下のスキーマに従って行われます。

![](assets/s_900_ncs_install_standaloneconfig.png)

このタイプの設定は、100,000個未満の受信者と、例えば次のリストレイヤーを使用して管理する場合に実行できます。

* Linux、
* Apache,
* PostgreSQL,
* Qmail.

ボリュームが増えると、このアーキテクチャの一種によって、パフォーマンスを向上させるために、データベース・サーバが別のコンピュータに移動されます。

>[!NOTE]
>
>十分なリソースがある場合は、既存のデータベース・サーバも使用できます。

## 機能 {#features}

### メリット {#advantages}

* 完全なスタンドアロンと低い構成コスト（以下に示すオープンソースソフトウェアを使用する場合は、課金対象ライセンスは不要）。
* インストールとネットワークの構成をシンプル化。

### デメリット {#disadvantages}

* 事故が発生した場合に重要なコンピューター。
* メッセージをブロードキャストする際の帯域幅が限られている（当社の経験上、1時間あたり数万通のメール）。
* 放送時のアプリの遅延の可能性。
* アプリケーションサーバーは、リダイレクトサーバーをホストするので、外部（例えばDMZ内にある間）から使用できる必要があります。

## インストールと設定の手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* JDK,
* Webサーバー(IIS、Apache)、
* データベース・サーバへのアクセス、
* POP3経由でバウンスメールボックスにアクセス可能、
* 2つのDNSエイリアスの作成：

   * 最初に公開され、そのパブリックIP上のコンピュータを追跡し、指し示す。
   * 2つ目のエイリアスは、コンソールアクセスと同じコンピューターのポインティングのために、内部ユーザーに公開されます。

* SMTP (25)、DNS (53)、HTTP (80)、HTTPS (443)、SQL （Oracleの場合は1521、PostgreSQLの場合は5432など）を開くように設定されたファイアウォール ポート。 詳細については、「 [ネットワーク設定](../../installation/using/network-configuration.md)」を参照してください。

次の例では、インスタンスのパラメーターを示します。

* インスタンスの名前： **デモ**
* DNSマスク： **console.キャンペーン.net*** （クライアントコンソール接続およびレポートの場合のみ）
* データベース： **キャンペーン:demo@dbsrv**

### インストールと設定（シングルマシン） {#installing-and-configuring--single-machine-}

次の手順に従います。

1. Adobe Campaignサーバーのインストール手順に従います。 **Linuxではnlserver** パッケージ、Windowsでは **setup.exe** 。

   詳しくは、「Linuxでのキャンペーンインストールの [前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) (Linux)」および「Windowsでのキャンペーンインストールの [前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) (Windows)」を参照してください。

1. Adobe Campaignサーバーがインストールされたら、次のコマンドを使用して **nlserver web -tomcat** （Webモジュール）を開始し、Tomcat開始を正しく開始できるようにします。

   ```
   12:08:18 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   12:08:18 >   Starting Web server module (pid=28505, tid=-1225184768)...
   12:08:18 >   Tomcat started
   12:08:18 >   Server started
   ```

   >[!NOTE]
   >
   >Webモジュールを初めて実行すると、 **config-default.xml** ファイルと **serverConf.xmlファイルがインストールフォルダーの** conf **** ディレクトリに作成されます。 serverConf.xmlで使用可能なすべてのパラメ **ーターをこの** 節に示します [](../../installation/using/the-server-configuration-file.md)。

   サーバーを停止するには、 **Ctrl + C** (C)キーを押します。

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合： [サーバの最初の開始アップ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)、
   * Windowsの場合： [サーバーの最初の開始アップ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)。

1. 次のコマンドを使用して **内部パスワードを変更します** 。

   ```
   nlserver config -internalpassword
   ```

   For more on this, refer to [Internal identifier](../../installation/using/campaign-server-configuration.md#internal-identifier).

1. 追跡用のDNSマスク(この場合は **tracking.** キャンペーン.net **)と、クライアントコンソール(この場合は** console.キャンペーン.net ****)へのアクセスを持つデモインスタンスを作成します。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、「インスタンスの [作成とログオン」を参照してください](../../installation/using/creating-an-instance-and-logging-on.md)。

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*,console.campaign.net*
      ```

      For more on this, refer to [Creating an instance](../../installation/using/command-lines.md#creating-an-instance).

1. config-demo.xml **ファイル（config-default.xmlの次の手順で作成）を編集し、** mta **(配信)(** mta) **(wfserverWorkflow)（ワークフロー）、** バウンスmail ************ () 次に、統計サーバーのアドレスを設定します。

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

1. serverConf.xml **** ファイルを編集し、配信ドメインを指定してから、MTAクエリがMXタイプのDNSモジュールに応答するために使用するDNSサーバーのIP（またはホスト）アドレスを指定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >nameServers **パラメーターは** 、Windowsでのみ使用されます。

   For more on this, refer to [Campaign server configuration](../../installation/using/campaign-server-configuration.md).

1. クライアントコンソールプログラム(**setup-client-7.XX**、YYYY **.exe（v7の場合）または** setup-client-6.YYYY **.exe(** YYYYの場合).exe ******** v6.exe(akeng/jsp)をコピーし、eng/jspフォルダーを作成します。

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合： [Linux用クライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合： [Windows向けクライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)

1. 次の節で説明するWebサーバー統合手順(IIS、Apache)に従います。

   * For Linux: [Integration into a Web server for Linux](../../installation/using/integration-into-a-web-server-for-linux.md)
   * For Windows: [Integration into a Web server for Windows](../../installation/using/integration-into-a-web-server-for-windows.md)

1. Webサイトを開始し、URLを使用してリダイレクトをテストします。https://tracking.campaign.net/r/test

   ブラウザーに次のメッセージを表示する必要があります。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="localhost"/>
   ```

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合： [Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windowsの場合： [Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバー(Windowsでは&#x200B;**net開始nlserver6** 、Linuxでは **/etc/init.d/nlserver6開始** )に開始し、もう一度コマンド **** nlserver pdumpを実行して、有効なすべてのモジュールの存在を確認します。

   >[!NOTE]
   >
   >20.1からは、（Linuxの場合は）次のコマンドを使用することをお勧めします。 **systemctl開始nlserver**

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

   また、このコマンドを使用すると、コンピューターにインストールされているAdobe Campaignサーバーのバージョンとビルド番号を確認できます。

1. URLを使用して **nlserver web** moduleをテストします。https://console.campaign.net/nl/jsp/logon.jsp

   このURLを使用すると、クライアントセットアッププログラムのダウンロードページにアクセスできます。

   アクセス制御ページに到達したら、 **内部ログイン** 、および関連するパスワードを入力します。

   ![](assets/s_ncs_install_access_client.png)

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合： [Linux用クライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合： [Windows向けクライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)

1. Adobe Campaignクライアントコンソールを開始（前のダウンロードページから、またはWindowsインストールの場合はサーバー上で直接起動）するには、サーバー接続URLをhttps://console.campaign.netに設定し、 **内部** ログインを使用して接続します。

   詳しくは、インスタンスの [作成およびログオン](../../installation/using/creating-an-instance-and-logging-on.md) / [内部識別子を参照してください](../../installation/using/campaign-server-configuration.md#internal-identifier)。

   初めてログインすると、データベース作成ウィザードが表示されます。

   ![](assets/s_ncs_install_db_oracle_creation01.png)

   ウィザードの手順に従って、接続インスタンスに関連付けられたデータベースを作成します。

   For more on this, refer to [Creating and configuring the database](../../installation/using/creating-and-configuring-the-database.md).

   データベースが作成されたら、ログオフします。

1. パスワードを使用せずに **admin** loginを使用し、デプロイメントウィザード( **[!UICONTROL ツール/詳細]** メニュー)を開始してクライアントコンソールに再度ログオンし、インスタンスの設定を完了します。

   For more on this, refer to [Deploying an instance](../../installation/using/deploying-an-instance.md).

   設定する主なパラメーターは次のとおりです。

   * 電子メール配信:バウンスメールの送信者と返信アドレス、およびエラーメールボックス。
   * 追跡：リダイレクトに使用する外部URLと内部URLを入力し、トラッキングサーバーの **登録をクリックし** てから、トラッキングサーバーの **デモ** インスタンスで検証します。

      For more on this, refer to [Tracking configuration](../../installation/using/deploying-an-instance.md#tracking-configuration).

      ![](assets/s_ncs_install_deployment_wiz_09.png)

      Adobe Campaignサーバーはアプリケーションサーバーとリダイレクトサーバーの両方として使用されるので、トラッキングログの収集とURLの転送に使用される内部URLは、Tomcat(https://localhost:8080)への直接の内部接続です。

   * バウンス管理：直帰メールを処理するパラメータを入力します(「未処理の直帰メール **** 」セクションを考慮しないでください)。
   * アクセス元：レポート、Web フォーム、ミラーページの2つのURLを指定します。

      ![](assets/d_ncs_install_web_url.png)

