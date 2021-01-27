---
solution: Campaign Classic
product: campaign
title: 企業へのデプロイメント
description: 企業へのデプロイメント
audience: installation
content-type: reference
topic-tags: deployment-types-
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '1263'
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

### デメリット{#disadvantages}

ハードウェアと管理のコストが高くなります。

### 推奨機器{#recommended-equipment}

* アプリケーションサーバー：2 GHZクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。
* リダイレクトサーバー：2 GHZクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。

>[!NOTE]
>
>既存のロードバランサーをリダイレクトサーバーへのトラフィックに再利用できます。

## インストールと設定の手順{#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 両方のアプリケーションサーバーのJDK、
* Webサーバー(IIS、Apache)は、
* 両方のアプリケーションサーバー上のデータベースサーバーへのアクセス、
* POP3経由でバウンスメールボックスにアクセス可能、
* ロードバランサーに2つのDNSエイリアスを作成します。

   * 最初に公開され、仮想IPアドレス(VIP)上のロードバランサーをトラッキングして指し示し、2つの正面サーバーに配布されます。
   * 2つ目は、内部ユーザーに対してコンソール経由でアクセスし、仮想IPアドレス(VIP)上のロードバランサーを指し示し、2つのアプリケーションサーバーに配布されます。

* STMP (25)、DNS (53)、HTTP (80)、HTTPS (443)、SQL （1521 for PostgreSQLなど）を開くように設定されたファイアウォール ポート。 詳しくは、[データベースアクセス](../../installation/using/network-configuration.md#database-access)を参照してください。

>[!CAUTION]
>
>アプリケーションサーバーが単一のデータベースインスタンスを指す場合、1つのインスタンスで標準パッケージを読み込んだ後は、パッケージに含まれるスキーマは別のインスタンスに読み込まれません。
>  
>アプリケーションサーバーが1つのデータベースインスタンスを参照している場合、1つのインスタンスでスキーマを変更した後は、そのスキーマは別のインスタンスに読み込まれません。
>
>これらの問題を回復するには、エラーが発生した2番目のインスタンスで「web@default」プロセスを再起動する必要があります。

### アプリケーションサーバー1のインストールと設定{#installing-and-configuring-the-application-server-1}

次の例では、インスタンスのパラメーターを示します。

* インスタンスの名前：デモ
* DNSマスク：tracking.キャンペーン.net*、console.キャンペーン.net*(アプリケーションサーバーは、クライアントコンソールの接続とレポート、およびミラーページと購読解除ページのURLを処理します)
* 言語：英語
* データベース：キャンペーン:demo@dbsrv

最初のサーバーをインストールする手順は次のとおりです。

1. Adobe Campaignサーバーのインストール手順に従います。Linuxの場合は&#x200B;**nlserver**&#x200B;パッケージ、Windowsの場合は&#x200B;**setup.exe**。

   詳しくは、[Linuxでのキャンペーンインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md)(Linux)および[Windowsでのキャンペーンインストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md)(Windows)を参照してください。

1. Adobe Campaign・サーバーがインストールされたら、**nlserver web -tomcat**&#x200B;コマンドを使用してアプリケーション・サーバー(web)を開始します(Webモジュールを使用すると、ポート8080で待機するスタンドアロンWebサーバー・モードでTomcatを開始できます)。

   ```
   12:08:18 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   12:08:18 >   Starting Web server module (pid=28505, tid=-1225184768)...
   12:08:18 >   Tomcat started
   12:08:18 >   Server started
   ```


   >[!NOTE]
   >
   >Webモジュールを初めて実行すると、インストールフォルダーの&#x200B;**conf**&#x200B;ディレクトリに&#x200B;**config-default.xml**&#x200B;ファイルと&#x200B;**serverConf.xml**&#x200B;ファイルが作成されます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

   **Ctrl + C**&#x200B;キーを押して、サーバーを停止します。

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合：[サーバの最初の開始アップ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windowsの場合：[サーバの最初の開始アップ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

1. **内部**&#x200B;パスワードを変更するには、次のコマンドを使用します。

   ```
   nlserver config -internalpassword
   ```

   詳しくは、[内部識別子](../../installation/using/campaign-server-configuration.md#internal-identifier)を参照してください。

1. 追跡用のDNSマスクを使用して&#x200B;**demo**&#x200B;インスタンスを作成し(この場合、**tracking.キャンペーン.net**)、クライアントコンソール(この場合、**console.キャンペーン.net**)にアクセスします。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、[インスタンスの作成と](../../installation/using/creating-an-instance-and-logging-on.md)へのログを参照してください。

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*,console.campaign.net*
      ```

      詳しくは、[インスタンスの作成](../../installation/using/command-lines.md#creating-an-instance)を参照してください。

1. **config-demo.xml**&#x200B;ファイル（前のコマンドで作成し、**config-default.xml**&#x200B;ファイルの横に配置）を編集し、**mta** (配信)、**wfserver** (workflow)、**inMail**&#x200B;リバウンドメール)と&#x200B;**stat** （統計）プロセスが有効になっている場合は、**app**&#x200B;統計サーバーのアドレスを設定します。

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

   詳しくは、[プロセスの有効化](../../installation/using/campaign-server-configuration.md#enabling-processes)を参照してください。

1. **serverConf.xml**&#x200B;ファイルを編集し、配信ドメインを指定して、MTAモジュールがMX型DNSクエリに応答するために使用するDNSサーバーのIP（またはホスト）アドレスを指定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >**nameServers**&#x200B;パラメーターは、Windowsでのみ使用されます。

   詳しくは、[キャンペーンサーバーの設定](../../installation/using/campaign-server-configuration.md)を参照してください。

1. クライアントコンソールのセットアッププログラム(**setup-client-7.XX**、**YYYY.exe** for v7、**setup-client-6.XX**、**YYYY.exe** for v6.1)を&#x200B;**/datakitにコピーします。/nl/eng/jsp**&#x200B;フォルダー

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合：[Linux用のクライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合：[Windowsのクライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)。

1. Adobe Campaignサーバー(Windowsでは&#x200B;**net開始nlserver6**、Linuxでは&#x200B;**/etc/init.d/nlserver6開始**)を開始し、**nlserver pdump**&#x200B;コマンドをもう一度実行して、有効なすべてのモジュールの存在を確認します。

   >[!NOTE]
   >
   >20.1からは、（Linuxの場合は）次のコマンドを使用することをお勧めします。**systemctl開始nlserver**


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

1. URLを使用して&#x200B;**nlserver web**&#x200B;モジュールをテストします。[https://console.campaign.net/nl/jsp/logon.jsp](https://tracking.campaign.net/r/test).

   このURLを使用すると、クライアントセットアッププログラムのダウンロードページにアクセスできます。

   アクセス制御ページに到達したら、**内部**&#x200B;ログインと関連するパスワードを入力します。

   ![](assets/s_ncs_install_access_client.png)

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合：[Linux用のクライアントコンソールの可用性](../../installation/using/client-console-availability-for-linux.md)
   * Windowsの場合：[Windowsでのクライアントコンソールの可用性](../../installation/using/client-console-availability-for-windows.md)

### アプリケーションサーバー2のインストールと設定{#installing-and-configuring-the-application-server-2}

次の手順に従います。

1. Adobe Campaignサーバーをインストールします。
1. 作成したインスタンスのファイルをアプリケーションサーバー1にコピーします。

   アプリケーションサーバー1と同じインスタンス名を保持します。

1. **internal**&#x200B;をアプリケーションサーバー1と同じに変更します。
1. データベースをインスタンスにリンクする：

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. **config-demo.xml**&#x200B;ファイル（前のコマンドで作成し、**config-default.xml**&#x200B;ファイルの横に配置）を編集し、**mta** (配信)、**wfserver** (workflow)、**inMail**&#x200B;リバウンドメール)と&#x200B;**stat** （統計）プロセスが有効になっている場合は、**app**&#x200B;統計サーバーのアドレスを設定します。

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

   詳しくは、[プロセスの有効化](../../installation/using/campaign-server-configuration.md#enabling-processes)を参照してください。

1. **serverConf.xml**&#x200B;ファイルを編集し、MTAモジュールのDNS設定を設定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >**nameServers**&#x200B;パラメーターはWindowsでのみ使用されます。

   詳しくは、[キャンペーンサーバーの設定](../../installation/using/campaign-server-configuration.md)を参照してください。

1. Adobe Campaignサーバーの開始。

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合：[サーバの最初の開始アップ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windowsの場合：[サーバの最初の開始アップ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

### フロントサーバーのインストールと設定{#installing-and-configuring-the-frontal-servers}

インストール手順と構成手順は、両方のコンピューターで同一です。

手順は、以下のとおりです。

1. Adobe Campaignサーバーをインストールします。
1. 以下の項で説明されているウェブサーバー統合手順(IIS、Apache)に従います。

   * Linuxの場合：[Linux用のWebサーバへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)、
   * Windowsの場合：[Windows](../../installation/using/integration-into-a-web-server-for-windows.md)用のWebサーバーへの統合。

1. インストール時に作成した&#x200B;**config-demo.xml**&#x200B;ファイルと&#x200B;**serverConf.xml**&#x200B;ファイルをコピーします。 **config-demo.xml**&#x200B;ファイルで、**trackinglogd**&#x200B;プロセスをアクティブにし、**mta**、**inmail**、**wfserver**、**stat**&#x200B;プロセスを非アクティブにします。
1. **serverConf.xml**&#x200B;ファイルを編集し、リダイレクトのパラメーターに冗長なトラッキングサーバーを設定します。

   ```
   <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
   <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
   ```

1. Webサイトを開始し、URLからのリダイレクトをテストします。[https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test)

   ブラウザーには、次のメッセージが表示されます（ロードバランサーによってリダイレクトされるURLに応じて異なります）。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   この点について詳しくは、以下の節を参照してください。

   * Linuxの場合：[Webサーバーを起動し、設定](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)をテストする、
   * Windowsの場合：[Webサーバーを起動し、設定](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)をテストします。

1. Adobe Campaignサーバーの開始。

