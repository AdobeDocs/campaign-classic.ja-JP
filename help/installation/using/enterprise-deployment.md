---
product: campaign
title: 企業へのデプロイメント
description: 企業へのデプロイメント
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 38c14010-203a-47ab-b23d-6f431dab9a88
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 7%

---

# 企業へのデプロイメント{#enterprise-deployment}

これは最も完全な設定です。 セキュリティと可用性を高めるため、標準構成に基づいて構築されます。

* 拡張性と可用性を実現する、HTTPまたはTCPロードバランサーの背後にある専用のリダイレクトサーバー
* 2台のアプリケーション・サーバを使用して、スループットとフェイルオーバー機能（フォルト・トレランス）を向上させ、LAN内で分離します。

サーバーとプロセス間の一般的な通信は、次のスキーマに従って実行されます。

![](assets/s_901_ncs_install_enterpriseconfig.png)

このタイプの設定では、適切な帯域幅と調整により、1時間あたりの予想スループットが100,000件を超える可能性があります。

## 機能 {#features}

### メリット {#advantages}

* セキュリティの最適化：DMZのコンピュータには、外部に公開する必要のあるサーバのみがインストールされます。
* 高可用性により、次のことが容易に実現：外部から見えるコンピュータだけを、高可用性を考慮して管理する必要があります。

### デメリット {#disadvantages}

ハードウェアと管理コストの増加

### 推奨機器{#recommended-equipment}

* アプリケーションサーバー：2 GhzクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。
* リダイレクトサーバー：2 GhzクアッドコアCPU、4 GB RAM、ソフトウェアRAID 1 80 GB SATAハードドライブ。

>[!NOTE]
>
>既存のロードバランサーをリダイレクションサーバーへのトラフィックに再利用できます。

## インストールと設定の手順{#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* 両方のアプリケーションサーバーのJDK
* Webサーバー(IIS、Apache)は、両方のフロントで
* 両方のアプリケーション・サーバ上のデータベース・サーバへのアクセス
* POP3を介してアクセス可能なバウンスメールボックス
* ロードバランサーでの2つのDNSエイリアスの作成：

   * 最初に公開されたのは、仮想IPアドレス(VIP)上のロードバランサーをトラッキングし、それを指し、2つのフロントサーバーに配布されるためです。
   * 2つ目は、コンソールを介してアクセスし、仮想IPアドレス(VIP)上のロードバランサーを指し、2つのアプリケーションサーバーに配布される内部ユーザーに公開されます。

* STMP(25)、DNS(53)、HTTP(80)、HTTPS(443)、SQL(1521)(Oracle用)、5432（PostgreSQL用）などを開くように設定されたファイアウォール ポート。 詳しくは、[データベースアクセス](../../installation/using/network-configuration.md#database-access)の節を参照してください。

>[!CAUTION]
>
>アプリケーションサーバーが単一のデータベースインスタンスを指す場合、1つのインスタンスで標準パッケージをインポートした後、パッケージに含まれるスキーマは他のインスタンスに読み込まれません。
>  
>アプリケーションサーバーが単一のデータベースインスタンスを指している場合、1つのインスタンスでスキーマを変更した後、そのスキーマは他のインスタンスに読み込まれません。
>
>これらの問題を回復するには、エラーが発生した2番目のインスタンスで「web@default」プロセスを再起動する必要があります。

### アプリケーションサーバー1のインストールと設定{#installing-and-configuring-the-application-server-1}

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンスの名前：デモ
* DNSマスク：tracking.campaign.net*、console.campaign.net*（アプリケーションサーバーは、クライアントコンソールの接続とレポート、ミラーページと購読解除ページのURLを処理します）
* 言語：英語
* データベース：campaign:demo@dbsrv

最初のサーバーをインストールする手順は次のとおりです。

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

   * Linuxの場合：[サーバーの最初の起動](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windowsの場合：[サーバーの最初の起動](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

1. 次のコマンドを使用して、**内部**&#x200B;パスワードを変更します。

   ```
   nlserver config -internalpassword
   ```

   詳細については、[このセクション](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. 追跡用のDNSマスク（この場合は&#x200B;**tracking.campaign.net**）と、クライアントコンソール（この場合は&#x200B;**console.campaign.net**）へのアクセスを含む&#x200B;**demo**&#x200B;インスタンスを作成します。 それには、次の 2 つの方法があります。

   * コンソールからインスタンスを作成します。

      ![](assets/install_create_new_connexion.png)

      詳しくは、[インスタンスの作成と](../../installation/using/creating-an-instance-and-logging-on.md)でのログオンを参照してください。

      または

   * コマンドラインを使用してインスタンスを作成します。

      ```
      nlserver config -addinstance:demo/tracking.campaign.net*,console.campaign.net*
      ```

      詳しくは、[インスタンスの作成](../../installation/using/command-lines.md#creating-an-instance)を参照してください。

1. **config-demo.xml**&#x200B;ファイル（前のコマンドで作成し、**config-default.xml**&#x200B;ファイルの隣にある）を編集し、**mta**（配信）、**wfserver**（ワークフロー）、**inMail**&#x200B;を確認します。メール)と&#x200B;**stat**（統計）プロセスが有効になっている場合は、**app**&#x200B;統計サーバーのアドレスを設定します。

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

1. URLを使用して&#x200B;**nlserver web**&#x200B;モジュールをテストします。[https://console.campaign.net/nl/jsp/logon.jsp](https://tracking.campaign.net/r/test).

   このURLを使用して、クライアント設定プログラムのダウンロードページにアクセスできます。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

   アクセス制御ページに到達したら、**内部**&#x200B;ログインと関連するパスワードを入力します。

   ![](assets/s_ncs_install_access_client.png)

### アプリケーションサーバー2のインストールと設定{#installing-and-configuring-the-application-server-2}

次の手順に従います。

1. Adobe Campaignサーバーをインストールします。
1. 作成したインスタンスのファイルをアプリケーションサーバー1にコピーします。

   アプリケーションサーバー1と同じインスタンス名を保持します。

1. **内部**&#x200B;をアプリケーションサーバー1と同じに変更します。
1. データベースをインスタンスにリンクします。

   ```
   nlserver config -setdblogin:PostgreSQL:campaign:demo@dbsrv -instance:demo
   ```

1. **config-demo.xml**&#x200B;ファイル（前のコマンドで作成し、**config-default.xml**&#x200B;ファイルの隣にある）を編集し、**mta**（配信）、**wfserver**（ワークフロー）、**inMail**&#x200B;を確認します。メール)と&#x200B;**stat**（統計）プロセスが有効になっている場合は、**app**&#x200B;統計サーバーのアドレスを設定します。

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

   詳細については、[このセクション](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

1. **serverConf.xml**&#x200B;ファイルを編集し、MTAモジュールのDNS設定を設定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >**nameServers**&#x200B;パラメーターはWindowsでのみ使用されます。

   詳しくは、[Campaignサーバーの設定](../../installation/using/configuring-campaign-server.md)を参照してください。

1. Adobe Campaignサーバーを起動します。

   詳しくは、以下の節を参照してください。

   * Linuxの場合：[サーバーの最初の起動](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server)
   * Windowsの場合：[サーバーの最初の起動](../../installation/using/installing-the-server.md#first-start-up-of-the-server)

### フロントサーバのインストールと設定{#installing-and-configuring-the-frontal-servers}

インストール手順と構成手順は、両方のコンピュータで同じです。

手順は、以下のとおりです。

1. Adobe Campaignサーバーをインストールします。
1. 次の節で説明されているWebサーバー統合手順(IIS、Apache)に従います。

   * Linuxの場合：[Linux用のWebサーバーへの統合](../../installation/using/integration-into-a-web-server-for-linux.md),
   * Windowsの場合：[Windows用のWebサーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)。

1. インストール時に作成した&#x200B;**config-demo.xml**&#x200B;と&#x200B;**serverConf.xml**&#x200B;ファイルをコピーします。 **config-demo.xml**&#x200B;ファイルで、**trackinglogd**&#x200B;プロセスを有効にし、**mta**、**inmail**、**wfserver**&#x200B;および&#x200B;**stat**&#x200B;プロセスを無効にします。
1. **serverConf.xml**&#x200B;ファイルを編集し、リダイレクトのパラメーターに冗長なトラッキングサーバーを設定します。

   ```
   <spareServer enabledIf="$(hostname)!='front_srv1'" id="1" url="https://front_srv1:8080"/>
   <spareServer enabledIf="$(hostname)!='front_srv2'" id="2" url="https://front_srv2:8080"/>
   ```

1. Webサイトを起動し、次のURLからリダイレクトをテストします。[https://tracking.campaign.net/r/test](https://tracking.campaign.net/r/test)

   ブラウザーには、次のメッセージが表示されます（ロードバランサーによってリダイレクトされたURLに応じて異なります）。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv1"/>
   ```

   または

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="front_srv2"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linuxの場合：[Webサーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windowsの場合：[Webサーバーを起動し、設定をテストします。](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaignサーバーを起動します。
