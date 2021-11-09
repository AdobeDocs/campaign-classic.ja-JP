---
product: campaign
title: スタンドアロンデプロイメント
description: スタンドアロンデプロイメント
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 194366ab-fd9f-4431-9163-ae16c1f96db2
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 5%

---

# スタンドアロンデプロイメント{#standalone-deployment}

![](../../assets/v7-only.svg)

この構成には、同じコンピュータ上のすべてのコンポーネントが含まれます。

* アプリケーションプロセス (web)
* 配信プロセス (mta)
* リダイレクトプロセス（トラッキング）
* ワークフロープロセスとスケジュール済みタスク (wfserver)
* バウンスメールプロセス (inMail)
* 統計プロセス (stat)。

プロセス間の全体的な通信は、次のスキーマに従って実行されます。

![](assets/s_900_ncs_install_standaloneconfig.png)

このタイプの設定は、例えば次のソフトウェアレイヤーを使用して、100,000 人未満の受信者のリストを管理する場合に実行できます。

* Linux、
* Apache,
* PostgreSQL,
* Qmail.

ボリュームが増えると、このアーキテクチャのバリアントによって、データベース・サーバが別のコンピュータに移動し、パフォーマンスが向上します。

>[!NOTE]
>
>十分なリソースがある場合は、既存のデータベースサーバも使用できます。

## 機能 {#features}

### メリット {#advantages}

* 完全なスタンドアロンおよび低い構成コスト（以下に示すオープンソースソフトウェアを使用する場合は課金ライセンスは不要）。
* インストールとネットワーク設定を簡素化。

### デメリット {#disadvantages}

* インシデントが発生した場合の重要なコンピューター。
* メッセージをブロードキャストする際の帯域幅が制限されています（当社の経験では、1 時間あたり数万件のメールが送信されています）。
* ブロードキャスト時のアプリケーションの遅延の可能性。
* アプリケーションサーバーは、リダイレクションサーバーをホストするので、外部から（DMZ に配置されている間など）使用できる必要があります。

## インストールおよび設定手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* JDK,
* Web サーバー (IIS、Apache)
* データベース・サーバへのアクセス
* POP3 経由でアクセス可能なバウンスメールボックス
* 2 つの DNS エイリアスの作成：

   * 最初の公開は、そのパブリック IP 上のコンピュータを追跡し、指し示す目的で一般に公開されます。
   * 2 つ目のエイリアスは、コンソールにアクセスし、同じコンピュータを指すように、内部ユーザーに公開されます。

* SMTP(25)、DNS(53)、HTTP(80)、HTTPS(443)、SQL(1521Oracle用、5432（PostgreSQL 用など）を開くように設定されたファイアウォール ポート。 詳しくは、 [ネットワーク設定](../../installation/using/network-configuration.md).

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンスの名前： **デモ**
* DNS マスク： **console.campaign.net*** （クライアントコンソール接続およびレポートの場合のみ）
* データベース： **campaign:demo@dbsrv**

### インストールと設定（シングルマシン） {#installing-and-configuring--single-machine-}

次の手順に従います。

1. Adobe Campaignサーバーのインストール手順に従います。 **nlserver** Linux または **setup.exe** （Windows の場合）

   詳しくは、 [Linux での Campaign のインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) (Linux) および [Windows での Campaign のインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) (Windows)。

1. Adobe Campaignサーバーがインストールされたら、コマンドを使用してアプリケーションサーバー (Web) を起動します。 **nlserver web -tomcat** （Web モジュールを使用すると、Tomcat をスタンドアロンの Web サーバーモードで起動し、ポート 8080 でリッスンします）。また、Tomcat が正しく起動することを確認できます。

   ```
   12:08:18 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   12:08:18 >   Starting Web server module (pid=28505, tid=-1225184768)...
   12:08:18 >   Tomcat started
   12:08:18 >   Server started
   ```

   >[!NOTE]
   >
   >Web モジュールを初めて実行すると、 **config-default.xml** および **serverConf.xml** ファイルを **conf** インストールフォルダーの下のディレクトリ。 次の **serverConf.xml** を [セクション](../../installation/using/the-server-configuration-file.md).

   押す **Ctrl+C** をクリックして、サーバーを停止します。

   詳しくは、以下の節を参照してください。

   * Linux の場合： [サーバーの最初の起動](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server),
   * Windows の場合： [サーバーの最初の起動](../../installation/using/installing-the-server.md#first-start-up-of-the-server).

1. を **内部** 次のコマンドを使用したパスワード：

   ```
   nlserver config -internalpassword
   ```

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. を作成します。 **デモ** 追跡用の DNS マスクを持つインスタンス ( この場合、 **tracking.campaign.net**) にアクセスし、クライアントコンソール ( この場合は **console.campaign.net**) をクリックします。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、 [インスタンスの作成とログオン](../../installation/using/creating-an-instance-and-logging-on.md).

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*,console.campaign.net*
      ```

      詳しくは、 [インスタンスの作成](../../installation/using/command-lines.md#creating-an-instance).

1. を編集します。 **config-demo.xml** ファイル ( 前の手順で **config-default.xml**) をクリックし、 **mta** （配信） **wfserver** （ワークフロー）、 **inMail** （バウンスメール）および **stat** （統計）プロセスが有効になっている。 次に、統計サーバーのアドレスを設定します。

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

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. を編集します。 **serverConf.xml** ファイルを作成して配信ドメインを指定した後、MTA モジュールが MX タイプの DNS クエリに応答するために使用する DNS サーバーの IP（またはホスト）アドレスを指定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >この **nameServers** パラメーターは、Windows でのみ使用されます。

   詳しくは、 [Campaign サーバーの設定](../../installation/using/configuring-campaign-server.md).

1. クライアントコンソールセットアッププログラム (**setup-client-7.XX**, **YYYY.exe** v7 または **setup-client-6.XX**, **YYYY.exe** （v6.1 の場合） **/datakit/nl/eng/jsp** フォルダー。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

1. 次の節で説明されている Web サーバー統合手順 (IIS、Apache) に従います。

   * Linux の場合： [Linux 用 Web サーバーへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windows の場合： [Windows 用 Web サーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)

1. Web サイトを開始し、次の URL を使用してリダイレクトをテストします。https://tracking.campaign.net/r/test.

   ブラウザーには、次のメッセージが表示される必要があります。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="localhost"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linux の場合： [Web サーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windows の場合： [Web サーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバーを起動します (**net start nlserver6** Windows の場合、 **/etc/init.d/nlserver6 start** （Linux の場合）、コマンドを実行します。 **nlserver pdump** もう一度有効なモジュールがすべて存在するかどうかを確認します。

   >[!NOTE]
   >
   >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl start nlserver**

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

1. をテストします。 **nlserver web** URL を使用するモジュール：https://console.campaign.net/nl/jsp/logon.jsp

   この URL を使用して、クライアントセットアッププログラムのダウンロードページにアクセスできます。

   次を入力します。 **内部** ログインと関連するパスワード（アクセス制御ページにアクセスする際に使用） [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

   ![](assets/s_ncs_install_access_client.png)

1. ( 以前のダウンロードページから、または Windows インストールの場合はサーバー上で直接起動したAdobe Campaignクライアントコンソールを起動し、サーバー接続 URL をhttps://console.campaign.netに設定し、 **内部** ログインします。

   参照： [このページ](../../installation/using/creating-an-instance-and-logging-on.md) および [この節](../../installation/using/configuring-campaign-server.md#internal-identifier).

   初めてログインすると、データベース作成ウィザードが表示されます。

   ![](assets/s_ncs_install_db_oracle_creation01.png)

   ウィザードの手順に従い、接続インスタンスに関連付けられたデータベースを作成します。

   詳しくは、 [データベースの作成と設定](../../installation/using/creating-and-configuring-the-database.md).

   データベースが作成されたら、ログオフします。

1. を使用してクライアントコンソールに再度ログオンします。 **admin** パスワードを指定せずにログインし、デプロイウィザードを起動します ( **[!UICONTROL ツール/詳細]** メニュー ) をクリックして、インスタンスの設定を完了します。

   詳しくは、 [インスタンスのデプロイ](../../installation/using/deploying-an-instance.md).

   設定する主なパラメーターは次のとおりです。

   * E メール配信：送信者と返信のアドレスおよびバウンスメール用のエラーメールボックス。
   * トラッキング：リダイレクトに使用する外部 URL と内部 URL を入力し、 **トラッキングサーバーへの登録** その後、 **デモ** トラッキングサーバーのインスタンス。

      詳しくは、 [トラッキング設定](../../installation/using/deploying-an-instance.md#tracking-configuration).

      ![](assets/s_ncs_install_deployment_wiz_09.png)

      Adobe Campaignサーバーはアプリケーションサーバーとリダイレクトサーバーの両方で使用されるので、トラッキングログの収集と URL の転送に使用される内部 URL は、Tomcat(https://localhost:8080) への直接内部接続です。

   * バウンス管理：バウンスメールを処理するパラメーターを入力します ( **未処理のバウンスメール** を参照 )。
   * アクセス元：レポート、Web フォーム、ミラーページの 2 つの URL を指定します。

      ![](assets/d_ncs_install_web_url.png)
