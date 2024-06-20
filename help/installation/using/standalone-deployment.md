---
product: campaign
title: スタンドアロンデプロイメント
description: スタンドアロンデプロイメント
feature: Installation, Architecture, Deployment
audience: installation
content-type: reference
topic-tags: deployment-types-
exl-id: 194366ab-fd9f-4431-9163-ae16c1f96db2
source-git-commit: 1be1528d657537786c430ea9c8bdb3aad58ba20d
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 5%

---

# スタンドアロンデプロイメント{#standalone-deployment}



この構成には、同じコンピューター上のすべてのコンポーネントが含まれます。

* アプリケーションプロセス（web）、
* 配信プロセス（mta）、
* リダイレクトプロセス（トラッキング）、
* ワークフロープロセスおよびスケジュールされたタスク（wfserver）
* バウンスメールプロセス（inMail）、
* 統計プロセス（stat）。

プロセス間の全体的な通信は、次のスキーマに従って実行されます。

![](assets/s_900_ncs_install_standaloneconfig.png)

このタイプの設定は、例えば、次のようなソフトウェアレイヤーを使用して、10 万人未満の受信者のリストを管理する場合に実行できます。

* Linux、
* Apache、
* PostgreSQL、
* Qmail。

ボリュームが増加すると、このアーキテクチャの変形によってデータベース・サーバが別のコンピュータに移動され、パフォーマンスが向上します。

>[!NOTE]
>
>十分なリソースがある場合は、既存のデータベースサーバーも使用できます。

## 機能 {#features}

### メリット {#advantages}

* 完全なスタンドアロン型で設定コストが低い（以下に示すオープンソースソフトウェアを使用する場合、課金対象のライセンスは不要）。
* インストールとネットワーク設定を簡素化しました。

### デメリット {#disadvantages}

* インシデント発生時の重要なコンピュータ。
* メッセージをブロードキャストする際の帯域幅が制限される（当社の経験では、1 時間あたり数万通のメール）。
* ブロードキャスト時にアプリケーションの速度が低下する可能性がある。
* アプリケーションサーバーはリダイレクトサーバーをホストするので、外部（DMZ 内など）から使用可能である必要があります。

## インストールと設定の手順 {#installation-and-configuration-steps}

### 前提条件 {#prerequisites}

* JDK、
* Web サーバー（IIS、Apache）、
* データベースサーバーへのアクセス、
* POP3 経由でアクセスできるバウンスメールボックス。
* 2 つの DNS エイリアスの作成：

   * 1 つ目は、トラッキング用に公開され、パブリック IP 上のコンピューターを指します。
   * 2 つ目のエイリアスは、コンソールアクセス用に内部ユーザーに公開され、同じコンピューターを指します。

* SMTP （25）、DNS （53）、HTTP （80）、HTTPS （443）、SQL （Oracle用 1521、PostgreSQL 用 5432 など）を開くように設定されたファイアウォール ポート。 詳しくは、を参照してください。 [ネットワーク設定](../../installation/using/network-configuration.md).

次の例では、インスタンスのパラメーターは次のとおりです。

* インスタンス名： **デモ**
* DNS マスク： **console.campaign.net&#42;** （クライアントコンソール接続の場合とレポートの場合のみ）
* データベース： **campaign:demo@dbsrv**

### インストールと設定（単一マシン） {#installing-and-configuring--single-machine-}

次の手順に従います。

1. Adobe Campaign サーバーのインストール手順に従います。 **nlserver** linux のパッケージ、または **setup.exe** Windows の場合。

   詳しくは、次を参照してください [Linux での Campaign インストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-linux.md) （Linux）と [Windows での Campaign インストールの前提条件](../../installation/using/prerequisites-of-campaign-installation-in-windows.md) （Windows）。

1. Adobe Campaign サーバーをインストールしたら、コマンドを使用してアプリケーションサーバー（web）を起動します **nlserver web -tomcat** （この Web モジュールを使用すると、ポート 8080 をリッスンするスタンドアロン Web サーバーモードで Tomcat を起動し、Tomcat が正しく起動することを確認できます）。

   ```sql
   12:08:18 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   12:08:18 >   Starting Web server module (pid=28505, tid=-1225184768)...
   12:08:18 >   Tomcat started
   12:08:18 >   Server started
   ```

   >[!NOTE]
   >
   >Web モジュールが初めて実行されるときに、が作成されます。 **config-default.xml** および **serverConf.xml** 内のファイル **conf** インストールフォルダーの下のディレクトリ。 で使用できるすべてのパラメーター **serverConf.xml** の一覧はこちら [セクション](../../installation/using/the-server-configuration-file.md).

   押す **Ctrl+C** サーバーを停止します。

   詳しくは、以下の節を参照してください。

   * Linux 場合： [サーバーの初回起動](../../installation/using/installing-packages-with-linux.md#first-start-up-of-the-server),
   * Windows: [サーバーの初回起動](../../installation/using/installing-the-server.md#first-start-up-of-the-server).

1. 変更： **内部** 次のコマンドを使用してパスワードを設定します。

   ```
   nlserver config -internalpassword
   ```

   詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

1. を作成 **デモ** トラッキング用の DNS マスクを持つインスタンス（この場合は **tracking.campaign.net**）を選択し、クライアントコンソール（この場合は、 **console.campaign.net**）に設定します。 それには、次の 2 つの方法があります。

   * コンソールを使用してインスタンスを作成します。

     ![](assets/install_create_new_connexion.png)

     詳しくは、次を参照してください [インスタンスの作成とログオン](../../installation/using/creating-an-instance-and-logging-on.md).

     または

   * コマンドラインを使用してインスタンスを作成します。

     ```
     nlserver config -addinstance:demo/tracking.campaign.net*,console.campaign.net*
     ```

     詳しくは、次を参照してください [インスタンスの作成](../../installation/using/command-lines.md#creating-an-instance).

1. を編集する **config-demo.xml** ファイル（次の前の手順で作成） **config-default.xml**）を選択し、必ず **mta** （配信）、 **wfserver** （ワークフロー）、 **inMail** （バウンスメール）と **統計** （統計）プロセスが有効になっています。 次に、統計サーバーのアドレスを設定します。

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

1. を編集する **serverConf.xml** をファイルに入力して配信ドメインを指定し、MTA モジュールが MX タイプの DNS クエリに応答するために使用する DNS サーバーの IP （またはホスト）アドレスを指定します。

   ```
   <dnsConfig localDomain="campaign.com" nameServers="192.0.0.1, 192.0.0.2"/>
   ```

   >[!NOTE]
   >
   >この **nameServer** パラメーターは Windows でのみ使用されます。

   詳しくは、次を参照してください [Campaign サーバーの設定](../../installation/using/configuring-campaign-server.md).

1. クライアントコンソール設定プログラムをコピーします **setup-client-7.XXX.exe** に **/datakit/nl/eng/jsp** フォルダー。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

1. 次の項で説明する Web サーバー統合手順（IIS、Apache）に従います。

   * Linux 場合： [Linux 用 Web サーバーへの統合](../../installation/using/integration-into-a-web-server-for-linux.md)
   * Windows: [Windows 用 Web サーバーへの統合](../../installation/using/integration-into-a-web-server-for-windows.md)

1. Web サイトを開始し、URL https://tracking.campaign.net/r/testを使用してリダイレクトをテストします。

   ブラウザーには、次のメッセージが表示されます。

   ```
   <redir status="OK" date="AAAA/MM/JJ HH:MM:SS" build="XXXX" host="tracking.campaign.net" localHost="localhost"/>
   ```

   詳しくは、以下の節を参照してください。

   * Linux 場合： [Web サーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-linux.md#launching-the-web-server-and-testing-the-configuration)
   * Windows: [Web サーバーの起動と設定のテスト](../../installation/using/integration-into-a-web-server-for-windows.md#launching-the-web-server-and-testing-the-configuration)

1. Adobe Campaign サーバーを起動します（）。**net start nlserver6** windows の場合、 **/etc/init.d/nlserver6 開始** （Linux の場合）を実行し、コマンドを実行します。 **nlserver pdump** もう一度、有効なすべてのモジュールが存在するかどうかを確認します。

   >[!NOTE]
   >
   >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl start nlserver**

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

1. のテスト **nlserver web** 次の URL を使用したモジュール：https://console.campaign.net/nl/jsp/logon.jsp

   この URL から、クライアント設定プログラムのダウンロードページにアクセスできます。

   を入力 **内部** アクセス制御ページに到達したときのログインと関連するパスワード。 [詳細情報](../../installation/using/client-console-availability-for-windows.md)。

   ![](assets/s_ncs_install_access_client.png)

1. （前のダウンロードページから、または Windows インストールの場合はサーバー上で直接起動した）Adobe Campaign クライアントコンソールを起動し、サーバー接続 URL をhttps://console.campaign.netに設定してから、を使用して接続します。 **内部** ログイン。

   こちらを参照してください [このページ](../../installation/using/creating-an-instance-and-logging-on.md) および [この節](../../installation/using/configuring-campaign-server.md#internal-identifier).

   データベース作成ウィザードは、初めてログインすると表示されます。

   ![](assets/s_ncs_install_db_oracle_creation01.png)

   ウィザードの手順に従って、接続インスタンスに関連付けられたデータベースを作成します。

   詳しくは、次を参照してください [データベースの作成と設定](../../installation/using/creating-and-configuring-the-database.md).

   データベースを作成したら、ログオフします。

1. を使用して、クライアントコンソールに再度ログオンします。 **admin** パスワードを使用せずにログインし、デプロイメントウィザード（ **[!UICONTROL ツール /詳細]** メニュー）を選択して、インスタンスの設定を完了します。

   詳しくは、次を参照してください [インスタンスのデプロイ](../../installation/using/deploying-an-instance.md).

   設定する主なパラメーターは次のとおりです。

   * メール配信：送信者と返信アドレス、バウンスメールのエラーメールボックス。
   * トラッキング：リダイレクトに使用する外部 URL と内部 URL を入力し、クリックします **トラッキングサーバーの登録** で検証します **デモ** トラッキングサーバーのインスタンス。

     詳しくは、次を参照してください [トラッキング設定](../../installation/using/deploying-an-instance.md#tracking-configuration).

     ![](assets/s_ncs_install_deployment_wiz_09.png)

     Adobe Campaign サーバーはアプリケーションサーバーとリダイレクトサーバーの両方で使用されるため、トラッキングログや転送 URL の収集に使用される内部 URL は、Tomcat への直接の内部接続（https://localhost:8080）です。

   * バウンス管理：バウンスメールを処理するためのパラメーターを入力します（ **未処理のバウンスメール** この節を考慮に入れます）。
   * アクセス元：レポート、web フォーム、ミラーページの 2 つの URL を指定します。

     ![](assets/d_ncs_install_web_url.png)
