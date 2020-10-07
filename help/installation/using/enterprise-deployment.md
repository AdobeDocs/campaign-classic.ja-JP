---
title: 企業へのデプロイメント
seo-title: 企業へのデプロイメント
description: 企業へのデプロイメント
seo-description: null
page-status-flag: never-activated
uuid: 2c2b5cef-86cb-4cb5-801a-ca6afeae90bb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: deployment-types-
discoiquuid: 066d0ac1-033c-467b-aa6c-43a97ecd8632
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 2%

---


# 企業へのデプロイメント{#enterprise-deployment}

これは最も完全な設定です。 セキュリティと可用性を高めるため、標準的な設定に基づいて構築されています。

* 拡張性と可用性を確保するため、HTTPまたはTCPロードバランサーの背後に専用のリダイレクトサーバー
* スループットとフェイルオーバー機能（フォルトトレランス）を向上させる2台のアプリケーションサーバ。LAN内で孤立しています。

サーバとプロセス間の一般的な通信は、次のスキーマに従って行われます。

![](assets/s_901_ncs_install_enterpriseconfig.png)

このタイプの設定では、適切な帯域幅と調整により、1時間に100,000個のメールを予想されるスループットを超えることがあります。

## 機能 {#features}

### メリット {#advantages}

* セキュリティの最適化：DMZ内のコンピュータには、外部に公開する必要のあるサーバーのみがインストールされます。
* 高可用性により、次の項目を容易に実現：外部から見えるコンピュータだけを、高可用性を考慮して管理する必要があります。

### デメリット {#disadvantages}

ハードウェアと管理のコストが高くなります。

### 推奨される機器 {#recommended-equipment}

* アプリケーションサーバー：2 GHZクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。
* リダイレクトサーバー：2 GHZクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。

>[!NOTE]
>
>既存のロードバランサーをリダイレクトサーバーへのトラフィックに再利用できます。

## インストールと設定の手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 両方のアプリケーションサーバーのJDK、
* Webサーバー(IIS、Apache)は、
* 両方のアプリケーションサーバー上のデータベースサーバーへのアクセス、
* POP3経由でバウンスメールボックスにアクセス可能、
* ロードバランサーに2つのDNSエイリアスを作成します。

   * 最初に公開され、仮想IPアドレス(VIP)上のロードバランサーをトラッキングして指し示し、2つの正面サーバーに配布されます。
   * 2つ目は、内部ユーザーに対してコンソール経由でアクセスし、仮想IPアドレス(VIP)上のロードバランサーを指し示し、2つのアプリケーションサーバーに配布されます。

* STMP (25)、DNS (53)、HTTP (80)、HTTPS (443)、SQL （Oracleの場合は1521、PostgreSQLの場合は5432など）を開くように設定されたファイアウォール ポート。 詳細は、「 [データベースアクセス](../../installation/using/network-configuration.md#database-access)」を参照してください。

>[!CAUTION]
>
>アプリケーションサーバーが単一のデータベースインスタンスを指す場合、1つのインスタンスで標準パッケージを読み込んだ後は、パッケージに含まれるスキーマは別のインスタンスに読み込まれません。
>  
>アプリケーションサーバーが1つのデータベースインスタンスを参照している場合、1つのインスタンスでスキーマを変更した後は、そのスキーマは別のインスタンスに読み込まれません。
>
>これらの問題を回復するには、エラーが発生した2番目のインスタンスで「web@default」プロセスを再起動する必要があります。

### アプリケーションサーバーのインストールと設定1 {#installing-and-configuring-the-application-server-1}

次の例では、インスタンスのパラメーターを示します。

* インスタンスの名前：デモ
* DNSマスク：tracking.キャンペーン.net*、console.キャンペーン.net*(アプリケーションサーバーは、クライアントコンソールの接続とレポート、およびミラーページと購読解除ページのURLを処理します)
* 言語：英語
* データベース：キャンペーン:demo@dbsrv

最初のサーバーをインストールする手順は次のとおりです。

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

   * Linuxの場合： [サーバーの最初の開始アップ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windowsの場合： [サーバーの最初の開始アップ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

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

1. config **-demo.xml** ファイル（前のコマンドで作成し、config-default.xmlファイルの横にあります）を編集し、 **mta(配信、wfserver** 、wfserver、workflow、mailMail **、mailStat、****************** statingStats)を確認します。

   ```
   <?xml version='1.0'?>
   <serverconf>  
     <shared>    
       <!-- add lang="eng" to dataStore to force English for the instance -->    
       <dataStore hosts="tracking.campaign.net*,console.campaign.net*">      
         <mapping logical="*" physical="default"/>    
       </dataStore>  </shared>  
       <mta autoStart="true" statServerAddress="app">
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

1. クライアントコンソールプログラム(**setup-client-7.XX**、YYYY **.exe（v7の場合）または** setup-client-6.YYYY **.exe(** YYYYの場合).exe v6. ******** exe(akeng/jsp)をコピーし、eng/jspフォルダーを作成します。

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合： [Linux用クライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合： [Windows用のクライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)。

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

1. URLを使用して **nlserver web** moduleをテストします。 [https://console.campaign.net/nl/jsp/logon.jsp](https://tracking.campaign.net/r/test).

   このURLを使用すると、クライアントセットアッププログラムのダウンロードページにアクセスできます。

   アクセス制御ページに到達したら、 **内部ログイン** 、および関連するパスワードを入力します。

   ![](assets/s_ncs_install_access_client.png)

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合： [Linux用クライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合： [Windows向けクライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)

### アプリケーションサーバーのインストールと設定2 {#installing-and-configuring-the-application-server-2}

次の手順に従います。

1. Adobe Campaignサーバーをインストールします。
1. 作成したインスタンスのファイルをアプリケーションサーバー1にコピーします。

   アプリケーションサーバー1と同じインスタンス名を保持します。

1. 内 **部をアプリケーションサーバー** 1と同じに変更します。
1. データベースをインスタンスにリンクする：

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. config **-demo.xml** ファイル（前のコマンドで作成し、config-default.xmlファイルの横にあります）を編集し、 **mta(配信、wfserver** 、wfserver、workflow、mailMail **、mailStat、****************** statingStats)を確認します。

   ```
   <?xml version='1.0'?>
   <serverconf>  
     <shared>    
       <!-- add lang="eng" to dataStore to force English for the instance -->    
       <dataStore hosts="tracking.campaign.net*,console.campaign.net*">      
         <mapping logical="*" physical="default"/>    
       </dataStore>  </shared>  
       <mta autoStart="true" statServerAddress="app">
       <wfserver autoStart="true"/>  
       <inMail autoStart="true"/>  
       <sms autoStart="false"/>  
       <listProtect autoStart="false"/>
   </serverconf>
   ```

   For more on this, refer to [Enabling processes](../../installation/using/campaign-server-configuration.md#enabling-processes).

1. serverConf.xml **** ファイルを編集し、MTAモジュールのDNS設定を設定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >nameServers **パラメーターは** 、Windowsでのみ使用されます。

   For more on this, refer to [Campaign server configuration](../../installation/using/campaign-server-configuration.md).

1. Adobe Campaignサーバーの開始。

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合： [サーバーの最初の開始アップ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windowsの場合： [サーバーの最初の開始アップ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

### フロントサーバーのインストールと設定 {#installing-and-configuring-the-frontal-servers}

インストール手順と構成手順は、両方のコンピューターで同一です。

手順は、以下のとおりです。

1. Adobe Campaignサーバーをインストールします。
1. 以下の項で説明されているウェブサーバー統合手順(IIS、Apache)に従います。

   * For Linux: [Integration into a Web server for Linux](../../installation/using/integration-into-a-web-server-for-linux.md),
   * For Windows: [Integration into a Web server for Windows](../../installation/using/integration-into-a-web-server-for-windows.md).

1. インストール時に作成した **config-demo.xml** ファイルと **** serverConf.xmlファイルをコピーします。 config- **config.xml** ファイルで、trackinglogdプロセスをアクティブにし、mtaを非アクティブにします。mta **mail、inmail、server、statの各プロセスをアクティブにします。** config-logd **************** プロセスをアクティブにし、mtaを非アクティブにします。
1. serverConf.xml **** ファイルを編集し、リダイレクトのパラメーターに冗長なトラッキングサーバーを設定します。

   ```
   <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
   <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
   ```

1. Webサイトを開始し、URLからのリダイレクトをテストします。 [https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test)

   ブラウザーには、次のメッセージが表示されます（ロードバランサーによってリダイレクトされるURLに応じて異なります）。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合： [Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)、
   * Windowsの場合： [Webサーバーを起動し、設定をテストします](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)。

1. Adobe Campaignサーバーの開始。

