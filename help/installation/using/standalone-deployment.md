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

この構成には、同じコンピューター上のすべてのコンポーネントが含まれます。

* アプリケーションプロセス (web)
* 配信プロセス (mta)
* リダイレクトプロセス（追跡）
* ワークフロープロセスとスケジュール済みタスク (wfserver)
* バウンスメールプロセス (inMail)
* 統計プロセス (stat)

プロセス間の全体的な通信は、次のスキーマに従って実行されます。

![](assets/s_900_ncs_install_standaloneconfig.png)

このタイプの設定は、100,000 人未満の受信者のリストを管理し、例えば次のソフトウェアレイヤーを使用して管理する場合に実行できます。

* Linux、
* Apache,
* PostgreSQL,
* Qmail.

ボリュームが増えると、このアーキテクチャの一部がデータベース・サーバを別のコンピュータに移動し、パフォーマンスが向上します。

>[!NOTE]
>
>十分なリソースがある場合は、既存のデータベース・サーバも使用できます。

## 機能 {#features}

### メリット {#advantages}

* 完全なスタンドアロン構成および低い構成コスト（以下に示すオープンソースソフトウェアを使用する場合は課金ライセンスは不要）。
* インストールとネットワーク設定を簡素化。

### デメリット {#disadvantages}

* インシデントが発生した場合の重要なコンピューター。
* メッセージを放送する際の帯域幅が制限されます（当社の経験では、1 時間あたり数万件のメール）。
* ブロードキャスト時のアプリケーションの遅延の可能性。
* アプリケーションサーバーは、リダイレクトサーバーをホストするので、外部から（DMZ などに配置されている間に）使用できる必要があります。

## インストールおよび設定手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* JDK,
* Web サーバー (IIS、Apache)
* データベース・サーバへのアクセス
* POP3 を介してアクセス可能なバウンスメールボックス
* 2 つの DNS エイリアスの作成：

   * 最初に、そのパブリック IP 上のコンピュータを追跡し、指し示すために一般に公開される。
   * 2 つ目のエイリアスは、コンソールにアクセスし、同じコンピューターを指すために内部ユーザーに公開されます。

* SMTP(25)、DNS(53)、HTTP(80)、HTTPS(443)、SQL(1521)、Oracle用、PostgreSQL 用などを開くように設定されたファイアウォール ポート。 詳しくは、[ ネットワーク設定 ](../../installation/using/network-configuration.md) を参照してください。

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンスの名前：**demo**
* DNS マスク：**console.campaign.net***（クライアントコンソール接続およびレポートの場合のみ）
* データベース：**campaign:demo@dbsrv**

### インストールと設定（シングルマシン） {#installing-and-configuring--single-machine-}

次の手順に従います。

1. Adobe Campaignサーバーのインストール手順に従います。**nlserver** パッケージ（Linux の場合）または **setup.exe**（Windows の場合）。

   詳しくは、[Linux での Campaign のインストールの前提条件 ](../../installation/using/prerequisites-of-campaign-installation-in-linux.md)(Linux) および [Windows での Campaign のインストールの前提条件 ](../../installation/using/prerequisites-of-campaign-installation-in-windows.md)(Windows) を参照してください。

1. Adobe Campaignサーバーがインストールされたら、**nlserver web -tomcat** コマンドを使用してアプリケーションサーバー (web) を起動します (Web モジュールを使用すると、ポート 8080 をリッスンするスタンドアロン Web サーバーモードで Tomcat を起動し、Tomcat が正しく起動します。

   ```
   12:08:18 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   12:08:18 >   Starting Web server module (pid=28505, tid=-1225184768)...
   12:08:18 >   Tomcat started
   12:08:18 >   Server started
   ```

   >[!NOTE]
   >
   >Web モジュールを初めて実行すると、**config-default.xml** と **serverConf.xml** ファイルがインストールフォルダーの **conf** ディレクトリに作成されます。 **serverConf.xml** で使用できるすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に記載されています。

   **Ctrl+C** を押して、サーバーを停止します。

   詳しくは、以下の節を参照してください。

   * Linux の場合：[ サーバの最初の起動 ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server),
   * Windows の場合：[ サーバーの最初の起動 ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)。

1. **内部** パスワードを次のコマンドで変更します。

   ```
   nlserver config -internalpassword
   ```

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. 追跡用の DNS マスク（この場合は **tracking.campaign.net**）と、クライアントコンソール（この場合は **console.campaign.net**）へのアクセスを含む **demo** インスタンスを作成します。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、[ インスタンスの作成と ](../../installation/using/creating-an-instance-and-logging-on.md) へのログオンを参照してください。

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*,console.campaign.net*
      ```

      詳しくは、[ インスタンスの作成 ](../../installation/using/command-lines.md#creating-an-instance) を参照してください。

1. **config-demo.xml** ファイル（前の手順で **config-default.xml** の隣に作成）を編集し、**mta**（配信）、**wfserver**（ワークフロー）、**inMail**（バウンス）と a10/>stat **（統計）プロセスが有効になっている。**&#x200B;次に、統計サーバーのアドレスを設定します。

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

1. **serverConf.xml** ファイルを編集して配信ドメインを指定し、MTA モジュールが MX タイプの DNS クエリに応答するために使用する DNS サーバーの IP（またはホスト）アドレスを指定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >**nameServers** パラメーターは、Windows でのみ使用されます。

   詳しくは、[Campaign サーバーの設定 ](../../installation/using/configuring-campaign-server.md) を参照してください。

1. クライアントコンソール設定プログラム (**setup-client-7.XX**、**YYYY.exe**（v7 の場合）または **setup-client-6.XX**、**YYYY.exe**（v6.1 の場合）を &lt;a8/datakit/nl/eng/jsp **フォルダー。**[詳細情報](../../installation/using/client-console-availability-for-windows.md)。

1. 次の節で説明する Web サーバー統合手順 (IIS、Apache) に従います。

   * Linux の場合：[Linux 用 Web サーバーへの統合 ](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windows の場合：[Windows 用 Web サーバーへの統合 ](../../installation/using/integration-into-a-web-server-for-windows.md)

1. Web サイトを起動し、次の URL を使用してリダイレクトをテストします。https://tracking.campaign.net/r/test

   ブラウザーには、次のメッセージが表示される必要があります。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="localhost"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linux の場合：[Web サーバーの起動と設定のテスト ](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windows の場合：[Web サーバーの起動と設定のテスト ](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバー (Windows では **net start nlserver6**、Linux では **/etc/init.d/nlserver6 start**) を起動し、**nlserver pdump** コマンドをもう一度実行して、有効なすべてのモジュールの有無を確認します。

   >[!NOTE]
   >
   >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl start nlserver**

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

   また、このコマンドを使用すると、コンピューターにインストールされているAdobe Campaignサーバーのバージョンとビルド番号を把握できます。

1. URL を使用して **nlserver web** モジュールをテストします。https://console.campaign.net/nl/jsp/logon.jsp

   この URL を使用して、クライアントセットアッププログラムのダウンロードページにアクセスできます。

   アクセス制御ページに到達したら、**内部** ログインと関連するパスワードを入力します。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

   ![](assets/s_ncs_install_access_client.png)

1. ( 前のダウンロードページから、または Windows インストールの場合はサーバー上で直接起動したAdobe Campaignクライアントコンソールを起動し、サーバー接続 URL をhttps://console.campaign.netに設定して、**内部** ログインを使用して接続します。

   [ このページ ](../../installation/using/creating-an-instance-and-logging-on.md) と [ この節 ](../../installation/using/configuring-campaign-server.md#internal-identifier) を参照してください。

   初めてログインすると、データベース作成ウィザードが表示されます。

   ![](assets/s_ncs_install_db_oracle_creation01.png)

   ウィザードの手順に従い、接続インスタンスに関連付けられたデータベースを作成します。

   詳しくは、[ データベースの作成と設定 ](../../installation/using/creating-and-configuring-the-database.md) を参照してください。

   データベースを作成したら、ログオフします。

1. パスワードを入力せずに **admin** ログインを使用してクライアントコンソールに再度ログオンし、デプロイウィザード（ **[!UICONTROL ツール/詳細]** メニュー）を起動して、インスタンスの設定を完了します。

   詳しくは、[ インスタンスのデプロイ ](../../installation/using/deploying-an-instance.md) を参照してください。

   設定する主なパラメーターは次のとおりです。

   * E メール配信：送信者と返信アドレス、およびバウンスメール用のエラーメールボックス。
   * トラッキング：リダイレクトに使用する外部 URL と内部 URL を入力し、「**トラッキングサーバーの登録**」をクリックしてから、トラッキングサーバーの **demo** インスタンスで検証します。

      詳しくは、[ トラッキング設定 ](../../installation/using/deploying-an-instance.md#tracking-configuration) を参照してください。

      ![](assets/s_ncs_install_deployment_wiz_09.png)

      Adobe Campaignサーバーはアプリケーションサーバーとリダイレクトサーバーの両方として使用されるので、トラッキングログと転送 URL の収集に使用される内部 URL は、Tomcat(https://localhost:8080) への直接内部接続です。

   * バウンス管理：バウンスメールを処理するパラメーターを入力します（**未処理のバウンスメール** セクションを考慮しないでください）。
   * アクセス元：レポート用の 2 つの URL、Web フォーム、ミラーページを指定します。

      ![](assets/d_ncs_install_web_url.png)
