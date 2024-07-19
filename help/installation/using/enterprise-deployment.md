---
product: campaign
title: 企業へのデプロイメント
description: 企業へのデプロイメント
feature: Installation, Architecture, Deployment
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 38c14010-203a-47ab-b23d-6f431dab9a88
source-git-commit: 1be1528d657537786c430ea9c8bdb3aad58ba20d
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 7%

---

# 企業へのデプロイメント{#enterprise-deployment}



これは最も完全な設定です。 セキュリティと可用性を向上させるために、次のような標準設定に基づいて構築されています。

* スケーラビリティと可用性を確保するために、HTTP または TCP ロードバランサーの背後にある専用のリダイレクトサーバー。
* スループットとフェイルオーバー機能（フォルト・トレランス）を向上させるために 2 台のアプリケーション・サーバが LAN 内で分離されています。

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_901_ncs_install_enterpriseconfig.png)

このタイプの設定では、適切な帯域幅とチューニングにより、予想されるスループットが 1 時間あたり 100,000 通を超える場合があります。

## 機能 {#features}

### メリット {#advantages}

* セキュリティの最適化：外部に公開する必要があるサーバーのみが、DMZ 内のコンピューターにインストールされます。
* 高可用性の確保が容易：外部から見えるコンピューターのみを、高可用性を念頭に置いて管理する必要があります。

### デメリット {#disadvantages}

ハードウェアおよび管理コストの増加。

### 推奨機器 {#recommended-equipment}

* アプリケーションサーバー：2 Ghz クアッドコア CPU、4 GB RAM、ソフトウェア RAID 1 80 GB SATA ハードドライブ。
* リダイレクトサーバ：2 Ghz クアッドコア CPU、4 GB RAM、ソフトウェア RAID 1 80 GB SATA ハードドライブ。

>[!NOTE]
>
>リダイレクトサーバーへのトラフィックに既存のロードバランサーを再利用できます。

## インストールと設定の手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 両方のアプリケーションサーバーの JDK
* Web サーバー（IIS、Apache）を使用する場合
* 両方のアプリケーション・サーバ上のデータベース・サーバへのアクセス
* POP3 経由でアクセスできるバウンスメールボックス。
* ロードバランサー上に 2 つの DNS エイリアスを作成します。

   * 1 つ目はトラッキング用に公開され、VIP（virtual IP address）上のロードバランサーを指します。これは次に、2 つのフロントサーバーに配信されます。
   * 2 つ目は、コンソール経由でアクセスするために内部ユーザーに公開され、バーチャル IP アドレス（VIP）上のロードバランサーを指し、2 つのアプリケーションサーバーに配布されます。

* STMP （25）、DNS （53）、HTTP （80）、HTTPS （443）、SQL （Oracle用 1521、PostgreSQL 用 5432 など）を開くように設定されたファイアウォール ポート。 詳しくは、[ データベースアクセス ](../../installation/using/network-configuration.md#database-access) の節を参照してください。

>[!CAUTION]
>
>アプリケーションサーバーが 1 つのデータベースインスタンスを指している場合、1 つのインスタンスで標準パッケージを読み込むと、パッケージに含まれるスキーマがもう 1 つのインスタンスで読み込まれません。
>  
>アプリケーションサーバーが 1 つのデータベースインスタンスを指している場合、1 つのインスタンスでスキーマを変更した後、もう 1 つのインスタンスでスキーマが読み込まれません。
>
>これらの問題を解決するには、エラーが発生した 2 番目のインスタンスで「web@default」プロセスを再起動する必要があります。

### アプリケーションサーバーのインストールと設定 1 {#installing-and-configuring-the-application-server-1}

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンスの名前：demo
* DNS マスク：tracking.campaign.net&#42;、console.campaign.net&#42; （クライアントコンソール接続およびレポート用の URL と、ミラーページおよび購読解除ページ用の URL は、アプリケーションサーバーで処理されます）
* Language: English
* データベース：campaign:demo@dbsrv

最初のサーバーをインストールする手順は次のとおりです。

1. Adobe Campaign サーバーのインストール手順に従います。Linux の場合は **nlserver** パッケージ、Windows の場合は **setup.exe** です。

   詳しくは、[Linux](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) での Campaign インストールの前提条件（Linux）および [Windows](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) での Campaign インストールの前提条件（Windows）を参照してください。

1. Adobe Campaign サーバーをインストールしたら、コマンド **nlserver web -tomcat** を使用してアプリケーションサーバー（web）を起動し（この Web モジュールを使用すると、ポート 8080 をリッスンするスタンドアロン Web サーバーモードで Tomcat を起動できます）、Tomcat が正しく起動することを確認します。

   ```sql
   12:08:18 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   12:08:18 >   Starting Web server module (pid=28505, tid=-1225184768)...
   12:08:18 >   Tomcat started
   12:08:18 >   Server started
   ```


   >[!NOTE]
   >
   >Web モジュールを初めて実行すると、インストールフォルダーの下の **conf** ディレクトリに **config-default.xml** ファイルと **serverConf.xml** ファイルが作成されます。 **serverConf.xml** で使用可能なすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に一覧表示されます。

   **Ctrl+C** キーを押して、サーバーを停止します。

   詳しくは、以下の節を参照してください。

   * Linux の場合：[ サーバーの最初の起動 ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windows の場合：[ サーバーの最初の起動 ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

1. **internal** パスワードを次のコマンドを使用して変更します。

   ```
   nlserver config -internalpassword
   ```

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. トラッキング用の DNS マスク（この場合は **tracking.campaign.net**）とクライアントコンソールへのアクセス（この場合は **console.campaign.net**）を使用して **demo** インスタンスを作成します。 それには、次の 2 つの方法があります。

   * コンソールを使用してインスタンスを作成します。

     ![](assets/install_create_new_connexion.png)

     詳しくは、[ インスタンスの作成とログオン ](../../installation/using/creating-an-instance-and-logging-on.md) を参照してください。

     または

   * コマンドラインを使用してインスタンスを作成します。

     ```
     nlserver config -addinstance:demo/tracking.campaign.net*,console.campaign.net*
     ```

     詳しくは、[ インスタンスの作成 ](../../installation/using/command-lines.md#creating-an-instance) を参照してください。

1. **config-demo.xml** ファイル（前のコマンドで作成され、**config-default.xml** ファイルの隣にある）を編集して、**mta** （配信）、**wfserver** （ワークフロー）、**inMail** （リバウンドメール）、**stat** （統計）の各プロセスが有効になっていることを確認し、**app** 統計サーバーのアドレスを設定します。

   ```xml
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

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. **serverConf.xml** ファイルを編集して配信ドメインを指定し、MTA モジュールが MX タイプの DNS クエリに応答するために使用する DNS サーバーの IP （またはホスト）アドレスを指定します。

   ```xml
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >**nameServers** パラメーターは、Windows でのみ使用されます。

   詳しくは、[Campaign サーバー設定 ](../../installation/using/configuring-campaign-server.md) を参照してください。

1. クライアントコンソールのセットアッププログラム **setup-client-7.XX**, **YYYY.exe** を **/datakit/nl/eng/jsp** フォルダーにコピーします。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

1. Adobe Campaign サーバー（Windows の場合は **net start nlserver6**、Linux の場合は **/etc/init.d/nlserver6 start**）を起動し、もう一度 **nlserver pdump** コマンドを実行して、有効なすべてのモジュールが存在するかどうかを確認します。

   >[!NOTE]
   >
   >20.1 以降では、次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl start nlserver**


   ```sql
   12:09:54 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   syslogd@default (7611) - 9.2 MB
   stat@demo (5988) - 1.5 MB
   inMail@demo (7830) - 11.9 MB
   watchdog (27369) - 3.1 MB
   mta@demo (7831) - 15.6 MB
   wfserver@demo (7832) - 11.5 MB
   web@default (28671) - 40.5 MB
   ```

   また、このコマンドを使用すると、コンピューターにインストールされているAdobe Campaign サーバーのバージョンとビルド番号を把握することもできます。

1. 次の URL を使用して **nlserver web** モジュールをテストします：[https://console.campaign.net/nl/jsp/logon.jsp](https://tracking.campaign.net/r/test)。

   この URL から、クライアント設定プログラムのダウンロードページにアクセスできます。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

   アクセス制御ページに到達したら、**内部** ログインと、関連するパスワードを入力します。

   ![](assets/s_ncs_install_access_client.png)

### アプリケーションサーバーのインストールと設定 2 {#installing-and-configuring-the-application-server-2}

次の手順に従います。

1. Adobe Campaign サーバーをインストールします。
1. 作成したインスタンスのファイルをアプリケーションサーバー 1 にコピーします。

   アプリケーションサーバー 1 と同じインスタンス名にします。

1. **internal** をアプリケーションサーバー 1 と同じに変更します。
1. データベースをインスタンスにリンクします。

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. **config-demo.xml** ファイル（前のコマンドで作成され、**config-default.xml** ファイルの隣にある）を編集して、**mta** （配信）、**wfserver** （ワークフロー）、**inMail** （リバウンドメール）、**stat** （統計）の各プロセスが有効になっていることを確認し、**app** 統計サーバーのアドレスを設定します。

   ```xml
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

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. **serverConf.xml** ファイルを編集し、MTA モジュールの DNS 設定を入力します。

   ```xml
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >**nameServers** パラメーターは Windows でのみ使用されます。

   詳しくは、[Campaign サーバー設定 ](../../installation/using/configuring-campaign-server.md) を参照してください。

1. Adobe Campaign サーバーを起動します。

   詳しくは、以下の節を参照してください。

   * Linux の場合：[ サーバーの最初の起動 ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windows の場合：[ サーバーの最初の起動 ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

### フロントサーバーのインストールと設定 {#installing-and-configuring-the-frontal-servers}

インストールと構成の手順は、両方のコンピューターで同じです。

手順は、以下のとおりです。

1. Adobe Campaign サーバーをインストールします。
1. 次の節で説明されている web サーバー統合手順（IIS、Apache）に従います。

   * Linux の場合：[Linux 用の web サーバーへの統合 ](../../installation/using/integration-into-a-web-server-for-linux.md)、
   * Windows の場合：[Windows の Web サーバーへの統合 ](../../installation/using/integration-into-a-web-server-for-windows.md)。

1. インストール時に作成した **config-demo.xml** および **serverConf.xml** ファイルをコピーします。 **config-demo.xml** ファイル内で **trackinglogd** プロセスをアクティベートし、**mta**、**inmail**、**wfserver** および **stat** プロセスをアクティベート解除します。
1. **serverConf.xml** ファイルを編集し、リダイレクトのパラメーターに冗長なトラッキングサーバーを入力します。

   ```xml
   <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
   <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
   ```

1. Web サイトを開始して、次の URL からリダイレクトをテストしてください：[https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test)

   ブラウザーには、（ロードバランサーによってリダイレクトされた URL に応じて）次のメッセージが表示されます。

   ```xml
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```xml
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linux の場合：[Web サーバーの起動と設定のテスト ](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)、
   * Windows の場合：[Web サーバーの起動と設定のテスト ](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)。

1. Adobe Campaign サーバーを起動します。
