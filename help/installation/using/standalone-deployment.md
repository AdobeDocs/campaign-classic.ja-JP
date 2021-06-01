---
product: campaign
title: スタンドアロンデプロイメント
description: スタンドアロンデプロイメント
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 194366ab-fd9f-4431-9163-ae16c1f96db2
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 5%

---

# スタンドアロンデプロイメント{#standalone-deployment}

この設定には、同じコンピューター上のすべてのコンポーネントが含まれます。

* アプリケーションプロセス(web)
* 配信プロセス(mta)
* リダイレクトプロセス（追跡）
* ワークフロープロセスとスケジュール済みタスク(wfserver)
* バウンスメールプロセス(inMail)
* 統計プロセス(stat)。

プロセス間の全体的な通信は、次のスキーマに従って実行されます。

![](assets/s_900_ncs_install_standaloneconfig.png)

このタイプの設定は、例えば次のソフトウェアレイヤーを使用して、100,000人未満の受信者のリストを管理する場合に実行できます。

* Linux、
* Apache,
* PostgreSQL,
* Qmail.

ボリュームが増えると、このアーキテクチャのバリアントにより、データベース・サーバが別のコンピュータに移動し、パフォーマンスが向上します。

>[!NOTE]
>
>十分なリソースが存在する場合は、既存のデータベース・サーバも使用できます。

## 機能 {#features}

### メリット {#advantages}

* 完全なスタンドアロン構成と低い構成コスト（以下に示すオープンソースソフトウェアを使用する場合は課金対象ライセンスは不要）。
* インストールとネットワーク設定の簡素化。

### デメリット {#disadvantages}

* インシデントの場合の重要なコンピューター。
* メッセージをブロードキャストする際の帯域幅が制限されます（当社の経験では、1時間あたり数万件のメール）。
* ブロードキャスト時のアプリケーションの遅延の可能性。
* アプリケーションサーバーは、リダイレクションサーバーをホストするので、外部から（例えばDMZに配置されている間に）使用できる必要があります。

## インストールと設定の手順{#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* JDK,
* Webサーバー(IIS、Apache)
* データベース・サーバへのアクセス
* POP3を介してアクセス可能なバウンスメールボックス
* 2つのDNSエイリアスの作成：

   * 最初に公開されたのは、そのパブリックIP上のコンピュータを追跡し、指し示す目的で、
   * 2つ目のエイリアスは、コンソールにアクセスし、同じコンピュータを指すために、内部ユーザーに公開されます。

* SMTP(25)、DNS(53)、HTTP(80)、HTTPS(443)、SQL(1521)(Oracle用)、PostgreSQL（5432など）を開くように設定されたファイアウォール ポート。 詳しくは、[ネットワーク設定](../../installation/using/network-configuration.md)を参照してください。

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンスの名前：**demo**
* DNSマスク：**console.campaign.net***（クライアントコンソール接続およびレポートの場合のみ）
* データベース：**campaign:demo@dbsrv**

### インストールと構成（単一マシン） {#installing-and-configuring--single-machine-}

次の手順に従います。

1. Adobe Campaignサーバーのインストール手順に従います。**nlserver**&#x200B;パッケージ（Linuxの場合）または&#x200B;**setup.exe**（Windowsの場合）。

   詳しくは、 [LinuxでのCampaignのインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md)(Linux)および[WindowsでのCampaignのインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md)(Windows)を参照してください。

1. Adobe Campaignサーバーがインストールされたら、**nlserver web -tomcat**&#x200B;コマンドを使用してアプリケーションサーバー(web)を起動します（Webモジュールを使用すると、ポート8080でリッスンするスタンドアロンWebサーバーモードでTomcatを起動できます）。

   ```
   12:08:18 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   12:08:18 >   Starting Web server module (pid=28505, tid=-1225184768)...
   12:08:18 >   Tomcat started
   12:08:18 >   Server started
   ```

   >[!NOTE]
   >
   >Webモジュールを初めて実行すると、**config-default.xml**&#x200B;と&#x200B;**serverConf.xml**&#x200B;ファイルがインストールフォルダーの&#x200B;**conf**&#x200B;ディレクトリに作成されます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に記載されています。

   **Ctrl+C**&#x200B;を押して、サーバーを停止します。

   詳しくは、以下の節を参照してください。

   * Linuxの場合：[サーバの最初の起動](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server),
   * Windowsの場合：[サーバーの最初の起動](../../installation/using/installing-the-server.md#first-start-up-of-the-server)。

1. 次のコマンドを使用して、**内部**&#x200B;パスワードを変更します。

   ```
   nlserver config -internalpassword
   ```

   詳細については、[このセクション](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. 追跡用のDNSマスク（この場合は&#x200B;**tracking.campaign.net**）と、クライアントコンソール（この場合は&#x200B;**console.campaign.net**）へのアクセスを含む&#x200B;**demo**&#x200B;インスタンスを作成します。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、[インスタンスの作成と](../../installation/using/creating-an-instance-and-logging-on.md)へのログオンを参照してください。

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*,console.campaign.net*
      ```

      詳しくは、[インスタンスの作成](../../installation/using/command-lines.md#creating-an-instance)を参照してください。

1. **config-demo.xml**&#x200B;ファイル（前の手順で&#x200B;**config-default.xml**&#x200B;の隣に作成）を編集し、**mta**（配信）、**wfserver**（ワークフロー）、**inMail**（バウンス）とa10/>stat **（統計）プロセスが有効になっている。**&#x200B;次に、統計サーバーのアドレスを設定します。

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

   詳細については、[このセクション](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. **serverConf.xml**&#x200B;ファイルを編集して配信ドメインを指定し、MXタイプのDNSクエリに応答するためにMTAモジュールで使用されるDNSサーバーのIP（またはホスト）アドレスを指定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >**nameServers**&#x200B;パラメーターはWindowsでのみ使用されます。

   詳しくは、[Campaignサーバーの設定](../../installation/using/configuring-campaign-server.md)を参照してください。

1. クライアントコンソール設定プログラム(**setup-client-7.XX**、**YYYY.exe**（v7の場合）または&#x200B;**setup-client-6.XX**、**YYYY.exe**（v6.1の場合）を&#x200B;**/datakit/datakitにコピーします。nl/eng/jsp**&#x200B;フォルダー。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

1. 次の節で説明するWebサーバー統合手順(IIS、Apache)に従います。

   * Linuxの場合：[Linux用Webサーバーへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windowsの場合：[Windows用Webサーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)

1. Webサイトを開始し、URLを使用してリダイレクトをテストします。https://tracking.campaign.net/r/test.

   ブラウザーに次のメッセージが表示される必要があります。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="localhost"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linuxの場合：[Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windowsの場合：[Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバー(Windowsの場合は&#x200B;**net start nlserver6**、Linuxの場合は&#x200B;**/etc/init.d/nlserver6 start**)を起動し、もう一度&#x200B;**nlserver pdump**&#x200B;コマンドを実行して、有効なすべてのモジュールの有無を確認します。

   >[!NOTE]
   >
   >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）。**systemctl start nlserver**

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

1. URLを使用して&#x200B;**nlserver web**&#x200B;モジュールをテストします。https://console.campaign.net/nl/jsp/logon.jsp

   このURLを使用して、クライアント設定プログラムのダウンロードページにアクセスできます。

   アクセス制御ページに到達したら、**内部**&#x200B;ログインと関連するパスワードを入力します。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

   ![](assets/s_ncs_install_access_client.png)

1. （前のダウンロードページから、またはWindowsインストールの場合はサーバー上で直接起動した）Adobe Campaignクライアントコンソールを起動し、サーバー接続URLをhttps://console.campaign.netに設定して、**内部**&#x200B;ログインを使用して接続します。

   [このページ](../../installation/using/creating-an-instance-and-logging-on.md)と[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

   初めてログインすると、データベース作成ウィザードが表示されます。

   ![](assets/s_ncs_install_db_oracle_creation01.png)

   ウィザードの手順に従って、接続インスタンスに関連付けられたデータベースを作成します。

   詳しくは、[データベースの作成と設定](../../installation/using/creating-and-configuring-the-database.md)を参照してください。

   データベースを作成したら、ログオフします。

1. パスワードを入力せずに&#x200B;**admin**&#x200B;ログインを使用してクライアントコンソールに再度ログオンし、デプロイウィザード（ **[!UICONTROL ツール/詳細]**&#x200B;メニュー）を起動して、インスタンスの設定を完了します。

   詳しくは、[インスタンスのデプロイ](../../installation/using/deploying-an-instance.md)を参照してください。

   設定する主なパラメーターは次のとおりです。

   * Eメール配信：送信者と返信アドレス、およびバウンスメール用のエラーメールボックス。
   * トラッキング：リダイレクトに使用する外部URLと内部URLを入力し、「**トラッキングサーバーでの登録**」をクリックしてから、トラッキングサーバーの&#x200B;**demo**&#x200B;インスタンスで検証します。

      詳しくは、[トラッキング設定](../../installation/using/deploying-an-instance.md#tracking-configuration)を参照してください。

      ![](assets/s_ncs_install_deployment_wiz_09.png)

      Adobe Campaignサーバーはアプリケーションサーバーとリダイレクションサーバーの両方として使用されるので、トラッキングログと転送URLの収集に使用される内部URLは、Tomcat(https://localhost:8080)への直接内部接続です。

   * バウンス管理：バウンスメールを処理するパラメーターを入力します（**未処理のバウンスメール**&#x200B;セクションを考慮しないでください）。
   * アクセス元：レポート用の2つのURL（Webフォームとミラーページ）を指定します。

      ![](assets/d_ncs_install_web_url.png)
