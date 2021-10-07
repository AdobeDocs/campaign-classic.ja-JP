---
product: campaign
title: 企業へのデプロイメント
description: 企業へのデプロイメント
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 38c14010-203a-47ab-b23d-6f431dab9a88
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 7%

---

# 企業へのデプロイメント{#enterprise-deployment}

![](../../assets/v7-only.svg)

これは最も完全な設定です。 標準構成に基づいて構築され、セキュリティと可用性が向上します。

* 拡張性と可用性を実現する、HTTP または TCP ロードバランサーの背後にある専用のリダイレクトサーバー
* 2 台のアプリケーションサーバを使用して、スループットとフェイルオーバー機能（フォールトトレランス）を向上させ、LAN 内で分離

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_901_ncs_install_enterpriseconfig.png)

このタイプの設定では、適切な帯域幅と調整により、1 時間あたりの予想スループットが 100,000 件を超える場合があります。

## 機能 {#features}

### メリット {#advantages}

* セキュリティの最適化：DMZ のコンピュータには、外部に公開する必要のあるサーバのみがインストールされます。
* 高可用性により、次のことを容易に実現：外部から見えるコンピュータだけを、高可用性を考慮して管理する必要があります。

### デメリット {#disadvantages}

ハードウェアと管理コストの増加

### 推奨機器 {#recommended-equipment}

* アプリケーションサーバー：2 Ghz クアッドコア CPU、4 GB RAM、ソフトウェア RAID 1 80 GB SATA ハードドライブ。
* リダイレクトサーバー：2 Ghz クアッドコア CPU、4 GB RAM、ソフトウェア RAID 1 80 GB SATA ハードドライブ。

>[!NOTE]
>
>既存のロードバランサーをリダイレクトサーバーへのトラフィックに再利用することができます。

## インストールおよび設定手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 両方のアプリケーションサーバーの JDK
* Web サーバー (IIS、Apache)
* 両方のアプリケーション・サーバ上のデータベース・サーバへのアクセス
* POP3 を介してアクセス可能なバウンスメールボックス
* ロードバランサーでの 2 つの DNS エイリアスの作成：

   * 最初に、仮想 IP アドレス (VIP) 上のロードバランサーを追跡して指し示すために公開され、2 つのフロントサーバーに配布されます。
   * 2 つ目は、コンソールを介してアクセスし、仮想 IP アドレス (VIP) のロードバランサーを指すように内部ユーザーに公開され、2 つのアプリケーションサーバーに配布されます。

* STMP(25)、DNS(53)、HTTP(80)、HTTPS(443)、SQL(1521)、Oracle用、PostgreSQL 用、5432 などを開くように設定されたファイアウォール ポート。 詳しくは、[ データベースアクセス ](../../installation/using/network-configuration.md#database-access) を参照してください。

>[!CAUTION]
>
>アプリケーションサーバーが単一のデータベースインスタンスを指している場合、1 つのインスタンスで標準パッケージをインポートした後、パッケージに含まれるスキーマは他のインスタンスに読み込まれません。
>  
>アプリケーションサーバーが単一のデータベースインスタンスを指している場合、1 つのインスタンスでスキーマを変更した後、そのスキーマは他のインスタンスに読み込まれません。
>
>これらの問題を回復するには、エラーが発生した 2 番目のインスタンスで「web@default」プロセスを再起動する必要があります。

### アプリケーションサーバー 1 のインストールと設定 {#installing-and-configuring-the-application-server-1}

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンスの名前：デモ
* DNS マスク：tracking.campaign.net*、console.campaign.net* （アプリケーションサーバーは、クライアントコンソールの接続とレポート、およびミラーページと購読解除ページの URL を処理します）
* 言語：英語
* データベース：campaign:demo@dbsrv

最初のサーバーをインストールする手順は次のとおりです。

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

   * Linux の場合：[ サーバーの最初の起動 ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windows の場合：[ サーバーの最初の起動 ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

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

1. **config-demo.xml** ファイルを編集し（前のコマンドで作成し、**config-default.xml** ファイルの隣にあります）、**mta**（配信）、**wfserver**（ワークフロー）、&lt;arebound8/>inMail **メール ) と** stat **（統計）プロセスが有効になっている場合は、** app **統計サーバーのアドレスを設定します。**

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

1. URL を使用して **nlserver web** モジュールをテストします。[https://console.campaign.net/nl/jsp/logon.jsp](https://tracking.campaign.net/r/test).

   この URL を使用して、クライアントセットアッププログラムのダウンロードページにアクセスできます。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

   アクセス制御ページに到達したら、**内部** ログインと関連するパスワードを入力します。

   ![](assets/s_ncs_install_access_client.png)

### アプリケーションサーバーのインストールと設定 2 {#installing-and-configuring-the-application-server-2}

次の手順に従います。

1. Adobe Campaignサーバーをインストールします。
1. 作成したインスタンスのファイルをアプリケーションサーバー 1 にコピーします。

   アプリケーションサーバー 1 と同じインスタンス名を保持します。

1. **内部** を、アプリケーションサーバー 1 と同じに変更します。
1. データベースをインスタンスにリンクします。

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. **config-demo.xml** ファイルを編集し（前のコマンドで作成し、**config-default.xml** ファイルの隣にあります）、**mta**（配信）、**wfserver**（ワークフロー）、&lt;arebound8/>inMail **メール ) と** stat **（統計）プロセスが有効になっている場合は、** app **統計サーバーのアドレスを設定します。**

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

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. **serverConf.xml** ファイルを編集し、MTA モジュールの DNS 設定を設定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >**nameServers** パラメーターは、Windows でのみ使用されます。

   詳しくは、[Campaign サーバーの設定 ](../../installation/using/configuring-campaign-server.md) を参照してください。

1. Adobe Campaignサーバーを起動します。

   詳しくは、以下の節を参照してください。

   * Linux の場合：[ サーバーの最初の起動 ](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windows の場合：[ サーバーの最初の起動 ](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

### フロントサーバーのインストールと設定 {#installing-and-configuring-the-frontal-servers}

インストール手順と設定手順は、両方のコンピュータで同じです。

手順は、以下のとおりです。

1. Adobe Campaignサーバーをインストールします。
1. 次の節で説明する Web サーバー統合手順 (IIS、Apache) に従います。

   * Linux の場合：[Linux の Web サーバーへの統合 ](../../installation/using/integration-into-a-web-server-for-linux.md),
   * Windows の場合：[Windows 用の Web サーバーへの統合 ](../../installation/using/integration-into-a-web-server-for-windows.md)。

1. インストール時に作成した **config-demo.xml** と **serverConf.xml** ファイルをコピーします。 **config-demo.xml** ファイルで、**trackinglogd** プロセスをアクティブにし、**mta**、**inmail**、**wfserver** および **stat** プロセスを非アクティブにします。
1. **serverConf.xml** ファイルを編集し、リダイレクトのパラメーターに冗長なトラッキングサーバーを設定します。

   ```
   <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
   <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
   ```

1. Web サイトを起動し、次の URL からリダイレクトをテストします。[https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test)

   ブラウザーには、次のメッセージが表示されます（ロードバランサーによってリダイレクトされた URL に応じて異なります）。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linux の場合：[Web サーバーの起動と設定のテスト ](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windows の場合：[Web サーバーを起動し、設定をテストします。](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバーを起動します。
