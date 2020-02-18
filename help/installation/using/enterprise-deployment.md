---
title: エンタープライズでの導入
seo-title: エンタープライズでの導入
description: エンタープライズでの導入
seo-description: null
page-status-flag: never-activated
uuid: 2c2b5cef-86cb-4cb5-801a-ca6afeae90bb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: deployment-types-
discoiquuid: 066d0ac1-033c-467b-aa6c-43a97ecd8632
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 6b631f8456ad1f61cec1630334d76752f6af9866

---


# エンタープライズでの導入{#enterprise-deployment}

これは最も完全な設定です。 セキュリティと可用性を高めるため、標準的な設定に基づいて構築されています。

* 拡張性と可用性を実現する、HTTPまたはTCPロードバランサーの背後にある専用のリダイレクトサーバー
* スループットとフェイルオーバー機能（フォルト・トレランス）を向上させる2台のアプリケーション・サーバ。これらはLAN内で隔離されています。

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_901_ncs_install_enterpriseconfig.png)

このタイプの構成では、適切な帯域幅とチューニングにより、1時間あたりの予想スループットが100,000メールを超える可能性があります。

## 機能 {#features}

### メリット {#advantages}

* セキュリティの最適化：DMZ内のコンピュータには、外部に公開する必要のあるサーバのみがインストールされます。
* 高可用性により、次のことを容易に実現：外部から見えるコンピューターのみ、高可用性を考慮して管理する必要があります。

### 欠点 {#disadvantages}

ハードウェアと管理のコストが高くなります。

### 推奨機器 {#recommended-equipment}

* アプリケーションサーバー：2 GhzクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。
* リダイレクトサーバー：2 GhzクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。

>[!NOTE]
>
>既存のロードバランサーをリダイレクトサーバーへのトラフィックに再利用できます。

## インストールと設定の手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 両方のアプリケーションサーバーのJDK、
* Webサーバー(IIS、Apache)が両方のフロントで使用され、
* 両方のアプリケーションサーバー上のデータベースサーバーへのアクセス、
* POP3経由でバウンスメールボックスにアクセス可能、
* ロードバランサーに2つのDNSエイリアスを作成します。

   * 最初に公開され、仮想IPアドレス(VIP)上のロードバランサーを追跡し、それを指し示し、2つのフロントサーバーに配布します。
   * 2つ目は、コンソール経由でのアクセスと、仮想IPアドレス(VIP)上のロードバランサーを指す内部ユーザーに公開され、2つのアプリケーションサーバーに配布されます。

* STMP (25)、DNS (53)、HTTP (80)、HTTPS (443)、SQL （Oracleの場合は1521、PostgreSQLの場合は5432など）を開くように設定されたファイアウォールポート。 詳細は、「データベースアクセス」を参 [照してください](../../installation/using/network-configuration.md#database-access)。

>[!CAUTION]
>
>アプリケーションサーバーが1つのデータベースインスタンスを参照している場合、1つのインスタンスで標準パッケージを読み込んだ後は、パッケージに含まれるスキーマは別のインスタンスに読み込まれません。
>  
>アプリケーションサーバーが1つのデータベースインスタンスを参照している場合、1つのインスタンスでスキーマを変更した後は、そのスキーマは別のインスタンスに読み込まれません。
>
>これらの問題を回復するには、エラーが発生した2番目のインスタンスで「web@default」プロセスを再起動する必要があります。

### アプリケーションサーバーのインストールと設定1 {#installing-and-configuring-the-application-server-1}

次の例では、インスタンスのパラメーターを示します。

* インスタンスの名前：デモ
* DNSマスク：tracking.campaign.net*、console.campaign.net*（アプリケーションサーバーは、クライアントコンソールの接続とレポート、ミラーページおよび購読解除ページのURLを処理します）
* 言語：英語
* データベース：campaign:demo@dbsrv

最初のサーバーをインストールする手順は次のとおりです。

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

   * Linuxの場合：サ [ーバーの初回起動](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windowsの場合：サ [ーバーの初回起動](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

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

1. config- **demo.xml** （前のコマンドで作成し、config-default.xmlファイルの隣にある）を編集し、 **mta** (delivery)wffserver(delivery), **wfserver(workflow),mail** serverMailsMailsStatististics(enabled) **************** ,

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

1. serverConf.xml **ファイルを編集し** 、配信ドメインを指定し、MTAモジュールがMXタイプのDNSクエリに応答するために使用するDNSサーバーのIP（またはホスト）アドレスを指定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >nameServersパラ **メーターは** 、Windowsでのみ使用されます。

   For more on this, refer to [Campaign server configuration](../../installation/using/campaign-server-configuration.md).

1. クライアントコンソールプログラム(**setup-client-7.XX**, **YYYY.exe（v7の場合）またはsetup-client-6.XX** , **yyyy.exe(********** v6の場合)をコピーし、eng/jsp/jspの場合)をコピーします。

   この詳細については、以下の節を参照してください。

   * Linuxの場合：Linux用のク [ライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合：Windows向けの [クライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)。

1. Adobe Campaignサーバー(**net start nlserver6** (Windows)、 **/etc/init.d/nlserver6 start** (Linux))を起動し、もう一度コマンドnlserver pdump **(nlserver pdump** )を実行して、すべての有効なモジュールの存在を確認します。

   >[!NOTE]
   >
   >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）。 **systemctl start nlserver**


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

1. 次のURLを使用し **て、nlserver Web** moduleをテストします。https://console.campaign.net/nl/jsp/logon.jsp [](https://tracking.campaign.net/r/test).

   このURLを使用すると、クライアントセットアッププログラムのダウンロードページにアクセスできます。

   アクセス制御ペ **ージに到達したら** 、内部ログインと関連するパスワードを入力します。

   ![](assets/s_ncs_install_access_client.png)

   この詳細については、以下の節を参照してください。

   * Linuxの場合：Linux用のク [ライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合：Windows向け [クライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)

### アプリケーションサーバーのインストールと設定2 {#installing-and-configuring-the-application-server-2}

次の手順に従います。

1. Adobe Campaignサーバーをインストールします。
1. 作成したインスタンスのファイルをアプリケーションサーバー1にコピーします。

   アプリケーションサーバー1と同じインスタンス名を保持します。

1. 内部をアプリ **ケーション** ・サーバー1と同じに変更します。
1. データベースをインスタンスにリンクします。

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. config- **demo.xml** （前のコマンドで作成し、config-default.xmlファイルの隣にある）を編集し、 **mta** (delivery)wffserver(delivery), **wfserver(workflow),mail** serverMailsMailsStatististics(enabled) **************** ,

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

1. serverConf.xmlフ **ァイルを編集し** 、MTAモジュールのDNS設定を設定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >nameServersパ **ラメーターは** 、Windowsでのみ使用されます。

   For more on this, refer to [Campaign server configuration](../../installation/using/campaign-server-configuration.md).

1. Adobe Campaignサーバーを起動します。

   この詳細については、以下の節を参照してください。

   * Linuxの場合：サ [ーバーの初回起動](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windowsの場合：サ [ーバーの初回起動](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

### フロントサーバーのインストールと設定 {#installing-and-configuring-the-frontal-servers}

インストール手順と構成手順は、両方のコンピューターで同じです。

手順は、以下のとおりです。

1. Adobe Campaignサーバーのインストール、
1. 以下の節で説明するWebサーバー統合手順(IIS、Apache)に従います。

   * Linuxの場合：Linux [用のWebサーバへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)、
   * Windowsの場合：Windows [用のWebサーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)。

1. インスト **ール時に作成した** config-demo.xml **、** serverConf.xmlファイルをコピーします。 config-demo.xmlファイルで、 **kinglogdとmtaをアクティブにします。** mtaをアクティブにします。 **** mail **deactivate**, **wfserver** deactivate, stat ******** processes,
1. serverConf.xmlファ **イルを編集し** 、リダイレクトのパラメーターに冗長なトラッキングサーバーを設定します。

   ```
   <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
   <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
   ```

1. Webサイトを起動し、URLからのリダイレクトをテストします。https://tracking.campaign.net/r/test [](https://tracking.campaign.net/r/test)

   ブラウザーに次のメッセージが表示されます（ロードバランサーによってリダイレクトされるURLに応じて異なります）。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   この詳細については、以下の節を参照してください。

   * Linuxの場合：Webサ [ーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)、
   * Windowsの場合：Webサ [ーバーを起動し、設定をテストします](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)。

1. Adobe Campaignサーバーを起動します。

