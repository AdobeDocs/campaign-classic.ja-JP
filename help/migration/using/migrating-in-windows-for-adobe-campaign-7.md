---
title: Windows での Adobe Campaign 7 への移行
seo-title: Windows での Adobe Campaign 7 への移行
description: Windows での Adobe Campaign 7 への移行
seo-description: null
page-status-flag: never-activated
uuid: 74464400-bdd4-42f8-bcbe-ace7095ae4e4
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
discoiquuid: f459dc07-b7db-4526-b428-852b51c9c00e
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 2%

---


# Windows での Adobe Campaign 7 への移行{#migrating-in-windows-for-adobe-campaign}

## 一般的な手順 {#general-procedure}

Windowsの場合の移行手順は次のとおりです。

1. サービスの停止：「 [サービスの停止](#service-stop)」を参照してください。
1. データベースのバックアップ：「データベースと現在のインストールの [バックアップ](#back-up-the-database-and-the-current-installation)」を参照してください。
1. プラットフォームの移行：adobe campaignv7の [導入を参照してください](#deploying-adobe-campaign-v7)。
1. リダイレクトサーバー(IIS)を移行する：リダイレクトサーバー(IIS)を [移行するを参照してください](#migrating-the-redirection-server--iis-)。
1. 再開始サービス：詳しくは、サービスの [再起動を参照してください](#re-starting-the-services)。
1. 以前のバージョンのAdobe Campaignを削除および削除する：「 [削除とクレンジングAdobe Campaignの前のバージョン](#deleting-and-cleansing-adobe-campaign-previous-version)」を参照してください。

## サービス停止 {#service-stop}

まず、関連するすべてのマシン上のデータベースにアクセスできるすべてのプロセスを停止します。

1. リダイレクトモジュール(**webmdl** サービス)を使用しているすべてのサーバーを停止する必要があります。 IISの場合は、次のコマンドを実行します。

   ```
   iisreset /stop
   ```

1. 次のコマンドを使用して、 **mta** モジュールとその子モジュール(**mtachild**)を停止する必要があります。

   ```
   nlserver stop mta@<instance name>
   nlserver stop mtachild@<instance name>
   ```

1. すべてのサーバーでAdobe Campaignサービスを停止します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   net stop nlserver6
   ```

   v5.11から移行する場合は、次のコマンドを実行します。

   ```
   net stop nlserver5
   ```

1. 各サーバーで、Adobe Campaignサービスが正しく停止していることを確認します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   tasklist /FI "IMAGENAME eq nlserver*"
   ```

   アクティブなプロセスのリストとID(PID)が表示されます。

   ```
   Image Name                     PID Session Name        Session#    Mem Usage
   ========================= ======== ================ =========== ============
   nlserver.exe                  3192 Console                    1     13,108 K
   ```

1. 数分後に1つ以上のAdobe Campaignプロセスがアクティブまたはブロックされたままの場合は、プロセスを強制終了します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   taskkill /IM nlserver* /T
   ```

1. 数分後に一部のプロセスがアクティブなままの場合は、次のコマンドを使用して、プロセスを強制的に閉じることができます。

   ```
   taskkill /F /IM nlserver* /T
   ```

## データベースと現在のインストールのバックアップ {#back-up-the-database-and-the-current-installation}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5.11からの移行 {#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. 次のコマンドを使用して、 **Neolane v5** ディレクトリのバックアップを作成します。

   ```
   ren "Neolane v5" "Neolane v5.back"
   ```

   >[!IMPORTANT]
   >
   >予防策として、 **Neolane v5.back** フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. Windowsサービス管理コンソールで、5.11アプリケーションサーバーサービスの自動スタートアップを無効にします。 次のコマンドも使用できます。

   ```
   sc config nlserver5 start= disabled
   ```

1. **config-`<instance name>`.xmlを編集します** ( **Neolane v5内)。 back** folder)を使用して、 **mta**、wfserver **、** stat ****&#x200B;などの サービスが自動的に開始されない。 例えば、autoStart **を** _autoStart ****&#x200B;に置き換えます。

   ```
   <?xml version='1.0'?>
   <serverconf>
     <shared>
       <dataStore hosts="myServer*" lang="en_US">
         <dataSource name="default">
           <dbcnx encrypted="1" login="myLogin" password="myPassword"  provider="postgresql" server="myServer"/>
         </dataSource>
       </dataStore>
     </shared>
   
     <mta _autoStart="true" statServerAddress="myStatServer"/>
     <stat _autoStart="true"/>
     <wfserver _autoStart="true"/>
     <inMail _autoStart="true"/>
     <sms _autoStart="false"/>
   </serverconf>
   ```

### Adobe Campaignv6.02からの移行 {#migrating-from-adobe-campaign-v6-02}

1. Adobe Campaignデータベースのバックアップを作成します。
1. 次のコマンドを使用して、 **Neolane v6** ディレクトリのバックアップを作成します。

   ```
   ren "Neolane v6" "Neolane v6.back"
   ```

   >[!IMPORTANT]
   >
   >予防策として、 **Neolane v6.back** フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. Windowsサービスマネージャーで、6.02アプリケーションサーバーの自動スタートアップを非アクティブにします。 次のコマンドも使用できます。

   ```
   sc config nlserver6 start= disabled
   ```

1. **Neolane v6で`<instance name>`config-****.xmlを編集します。 back** folder)を使用して、 **mta**、wfserver **、** stat ****&#x200B;などの サービスが自動的に開始されない。 例えば、autoStart **を** _autoStart ****&#x200B;に置き換えます。

   ```
   <?xml version='1.0'?>
   <serverconf>
     <shared>
       <dataStore hosts="myServer*" lang="en_US">
         <dataSource name="default">
           <dbcnx encrypted="1" login="myLogin" password="myPassword" provider="postgresql" server="myServer"/>
         </dataSource>
       </dataStore>
     </shared>
   
     <mta _autoStart="true" statServerAddress="myStatServer"/>
     <stat _autoStart="true"/>
     <wfserver _autoStart="true"/>
     <inMail _autoStart="true"/>
     <sms _autoStart="false"/>
   </serverconf>
   ```

### Adobe Campaignv6.1からの移行 {#migrating-from-adobe-campaign-v6-1}

1. Adobe Campaignデータベースのバックアップを作成します。
1. 次のコマンドを使用して、 **Adobe Campaignv6** ディレクトリのバックアップを作成します。

   ```
   ren "Adobe Campaign v6" "Adobe Campaign v6.back"
   ```

   >[!IMPORTANT]
   >
   >予防策として、 **Adobe Campaignv6.back** フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. Windowsサービス管理コンソールで、6.11アプリケーションサーバーサービスの自動スタートアップを無効にします。 次のコマンドも使用できます。

   ```
   sc config nlserver6 start= disabled
   ```

## Deploying Adobe Campaign v7 {#deploying-adobe-campaign-v7}

Adobe Campaignのデプロイには、次の2つの段階があります。

* ビルドv7のインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後の手順：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順を適用します。

1. setup.exeインストールファイルを実行して、最新Adobe Campaignのv7ビルドを **インストールします** 。 WindowsでのAdobe Campaignサーバーのインストールについて詳しくは、 [この節を参照してください](../../installation/using/installing-the-server.md)。

   ![](assets/migration_wizard_1_7.png)

   >[!NOTE]
   >
   >Adobe Campaignv7は、デフォルトでC:\Program Files\Adobe\Adobe Campaign v7 **** ディレクトリにインストールされます。

1. クライアントコンソールのインストールプログラムを使用可能にするには、 **setup-client-7.0.XXXX.exe** ファイルをAdobe Campaignのインストールディレクトリにコピーします。 **C:\Program Files\Adobe\Adobe Campaign v7\datakit\nl\eng\jsp**.

   >[!NOTE]
   >
   >WindowsでAdobe Campaignをインストールする方法の詳細については、 [この節を参照してください](../../installation/using/installing-the-server.md)。

1. 次のコマンドを使用して、最初に使用するインスタンスを開始します。

   ```
   net start nlserver6-v7
   net stop nlserver6-v7
   ```

   >[!NOTE]
   >
   >次の各コマンドでは、Adobe Campaignv7の内部ファイルシステムを作成できます。 **conf** ディレクトリ( **config-default.xml** ファイルと **serverConf.xmlファイルを使用)、** var **** ディレクトリなど

1. Neolane v5.back **、Neolane v6.back**、または **Adobe Campaignv6.backバックアップファイルを使用して、各インスタンスの設定ファイルとサブフォルダをコピー&amp;ペースト（上書き）します(** v6.backバックアップファイルは、この節の ****[](#back-up-the-database-and-the-current-installation)項を参照してください)。
1. 移行元のバージョンに応じて、次のコマンドを実行します。

   ```
   copy "Neolane v5.back"/conf/config-<instance name>.xml "Adobe Campaign v7"/conf/
   copy "Neolane v5.back"/customers/* "Adobe Campaign v7"/customers/
   copy "Neolane v5.back"/var/* "Adobe Campaign v7"/var/
   ```

   ```
   copy "Neolane v6.back"/conf/config-<instance name>.xml "Adobe Campaign v7"/conf/
   copy "Neolane v6.back"/customers/* "Adobe Campaign v7"/customers/
   copy "Neolane v6.back"/var/* "Adobe Campaign v7"/var/
   ```

   ```
   copy "Adobe Campaign v6.back"/conf/config-<instance name>.xml "Adobe Campaign v7"/conf/
   copy "Adobe Campaign v6.back"/customers/* "Adobe Campaign v7"/customers/
   copy "Adobe Campaign v6.back"/var/* "Adobe Campaign v7"/var/
   ```

   >[!IMPORTANT]
   >
   >上記の最初のコマンドでは、 **config-default.xmlファイルをコピーしないでください** 。

1. Adobe Campaignv7の **serverConf.xml** ファイルと **** config-default.xmlファイルに、Adobe Campaignの以前のバージョンで設定した固有の設定を適用します。 serverConf.xml **ファイルの場合は、Neolane v5/conf/serverConf.xml.diff** 、 **Neolane v6/conf/serverConf.xml diff**、または **Adobe Campaignv6/conf/serverConf.xml.diff****** .fileを使用します。

   >[!NOTE]
   >
   >Adobe Campaignの前のバージョンからAdobe Campaignv7へのレポート構成の場合は、物理ディレクトリへのパスがAdobe Campaignv7につながっている(Neolane v5、Neolane v6、Adobe Campaignv6ではない)ことを確認します。

1. 次のコマンドを使用して、Adobe Campaignv7の設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します。

   ```
   nlserver config -postupgrade -instance:<instance name>
   ```

>[!IMPORTANT]
>
>まだ開始Adobe Campaignサービスを使用しない：一部の変更は、IISで行う必要があります。

## リダイレクトサーバー(IIS)を移行しています {#migrating-the-redirection-server--iis-}

この段階で、IISサーバーを停止する必要があります。 「 [サービスの停止](#service-stop)」を参照してください。

1. インター **ネット情報サービス(IIS)マネージャ** コンソールを開きます。
1. Adobe Campaignの前のバージョンに使用するサイトのバインディング（リスンポート）を変更します。

   * 前のAdobe Campaignに使用するサイトを右クリックし、「連結を **[!UICONTROL 編集]**」を選択します。
   * リスンポートのタイプ(**[!UICONTROL http]** または **[!UICONTROL https]**)ごとに、適切な行を選択し、「 **[!UICONTROL 編集]**」をクリックします。
   * 別のポートを入力してください。 デフォルトでは、リスンポートはhttpの場合は80、httpsの場合は443です。 新しいポートが使用可能であることを確認します。

      ![](assets/_migration_iis_3_611.png)

      >[!NOTE]
      >
      >IISサーバーに高度な設定（共有ポートと異なるIPアドレス）とのAdobe Campaign用のWebサイトが複数ある場合は、管理者にお問い合わせください。

1. Adobe Campaignv7用の新しいWebサイトの作成：

   * [ **[!UICONTROL Sites]** ]フォルダを右クリックし、[ **[!UICONTROL Webサイト…]を選択します。]**.

      ![](assets/_migration_iis_4.png)

   * サイトの名前( **Adobe Campaignv7** など)を入力します。
   * Webサイトの基本ディレクトリへのアクセスパスは使用されませんが、 **[!UICONTROL 物理アクセスパス]** (Physical access path)フィールドを入力する必要があります。 既定のIISアクセスパスを入力してください： **C:\inetpub\wwwroot**.
   * 「 **[!UICONTROL Connect as...]** as」ボタンをクリックし、「 **[!UICONTROL Application user]** （アプリケーションユーザー）」オプションが選択されていることを確認します。
   * 「 **[!UICONTROL IPアドレス]** 」フィールドと「 **[!UICONTROL ポート]** 」フィールドはデフォルト値のままにできます。 その他の値を使用する場合は、IPアドレスやポートが使用可能であることを確認します。
   * [ **[!UICONTROL 開始Webサイトをすぐに表示]** ]ボックスをオンにします。

      ![](assets/_migration_iis_5_7.png)

1. **iis_neolane_setup.vbs** スクリプトを実行して、以前に作成した仮想ディレクトリでAdobe Campaignサーバーが使用するリソースを自動的に構成します。

   * このファイルは\tomcat-7\conf file **`[Adobe Campaign v7]`にあります。ここ****`[Adobe Campaign v7]`** で、はAdobe Campaignのインストールディレクトリへのアクセスパスです。 スクリプトを実行するコマンドは次のとおりです（管理者の場合）。

      ```
      cd C:\Program Files (x86)\Adobe Campaign\Adobe Campaign v7\tomcat-7\conf
      cscript iis_neolane_setup.vbs
      ```

   * 「 **[!UICONTROL OK]** 」をクリックして、スクリプトの実行を確認します。

      ![](assets/s_ncs_install_iis7_parameters_step2_7.png)

   * Adobe Campaignv7用に以前に作成したWebサイトの番号を入力し、「 **[!UICONTROL OK]**」をクリックします。

      ![](assets/s_ncs_install_iis7_parameters_step3_7.png)

   * 確認メッセージが表示されます。

      ![](assets/s_ncs_install_iis7_parameters_step7_7.png)

   * 「 **[!UICONTROL コンテンツの表示]** 」タブで、Webサイトの設定にAdobe Campaignリソースが正しく設定されていることを確認します。

      ![](assets/s_ncs_install_iis7_parameters_step6_7.png)

      >[!NOTE]
      >
      >ツリー構造が表示されない場合は、IISを再開始します。
      >
      >この節では、次のIIS構成手順を詳し [く説明します](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server)。

## Security zones {#security-zones}

v6.02以前から移行する場合は、サービスを開始する前にセキュリティゾーンを構成する必要があります。 詳細については、「 [セキュリティ](../../migration/using/general-configurations.md#security)」を参照してください。

## サービスの再起動 {#re-starting-the-services}

次の各サーバーでの開始IISとAdobe Campaignサービス：

1. トラッキングとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、 [一般設定の節の推奨事項に従って、回帰がないこと、すべての動作を確認してください](../../migration/using/general-configurations.md) 。

## 以前のバージョンのクレンジングAdobe Campaignの削除 {#deleting-and-cleansing-adobe-campaign-previous-version}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5 {#adobe-campaign-v5}

Adobe Campaignv5のインストールを削除およびクリーニングする前に、次の推奨事項を適用する必要があります。

* 新しいインストールの完全なチェックを実行するには、機能チームに依頼します。
* Adobe Campaignv5は、ロールバックが必要ないことが確実にわかった場合にのみアンインストールします。

1. IISでNeolane v5 **Webサイトを削除し、** Neolane v5 **** アプリケーションプールを削除します。
1. Neolane v5.back **フォルダーの名前をNeolane v5** に変更 **します**。
1. コンポーネントの追加削除ウィザードを使用してAdobe Campaignv5をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. 次のコマンドを使用して、 **nlserver5** Windowsサービスを削除します。

   ```
   sc delete nlserver5
   ```

1. サーバーの開始を再度行います。

### Adobe Campaign v6.02 {#adobe-campaign-v6-02}

Adobe Campaignv6.02のインストールを削除およびクリーニングする前に、次の推奨事項を適用する必要があります。

* 新しいインストールの完全なチェックを実行するには、機能チームに依頼します。
* Adobe Campaignv6.02は、ロールバックが必要ないことが確実にわかった場合にのみアンインストールします。

1. IISでNeolane v6 **Webサイトを削除し、** Neolane v6 **** アプリケーションプールを削除します。
1. Neolane v6.back **フォルダーの名前をNeolane v6** に変更 **します**。
1. Adobe Campaignv6.02をアンインストールするには、コンポーネントの追加削除ウィザードを使用します。

   ![](assets/migration_wizard_2.png)

1. サーバーの開始を再度行います。

### Adobe Campaign v6.1 {#adobe-campaign-v6-1}

Adobe Campaignv6のインストールを削除してクリーンアップする前に、次の推奨事項を適用する必要があります。

* 新しいインストールの完全なチェックを実行するには、機能チームに依頼します。
* Adobe Campaignv6は、ロールバックが必要ないことが確実にわかった場合にのみアンインストールします。

1. IISで、 **Adobe Campaignv6** Webサイトを削除し、 **Adobe Campaignv6** アプリケーションプールを削除します。
1. 「 **Adobe Campaignv6.back** 」フォルダの名前を「 **Adobe Campaignv6**」に変更します。
1. コンポーネントの追加削除ウィザードを使用してAdobe Campaignv6をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. サーバーの開始を再度行います。

