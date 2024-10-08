---
product: campaign
title: Microsoft Windows プラットフォームのAdobe Campaign v7 への移行
description: Microsoft Windows プラットフォームをAdobe Campaign v7 に移行する方法を説明します
feature: Upgrade
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
hide: true
hidefromtoc: true
exl-id: 3743d018-3316-4ce3-ae1c-25760aaf5785
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# Microsoft Windows プラットフォームから Campaign v7 への移行{#migrating-in-windows-for-adobe-campaign}



Microsoft Windows 環境の場合、移行手順は次のとおりです。

1. すべてのサービスを停止します [ 詳細情報 ](#service-stop)。
1. データベースのバックアップ - [ 詳細情報 ](#back-up-the-database)。
1. プラットフォームの移行 – [ 詳細情報 ](#deploying-adobe-campaign-v7)。
1. リダイレクトサーバー（IIS）の移行 – [ 詳細情報 ](#migrating-the-redirection-server--iis-)。
1. サービスの再起動 – [ 詳細情報 ](#re-starting-the-services)。
1. 以前のAdobe Campaign バージョンを削除して消去する – [ 詳細情報 ](#deleting-and-cleansing-adobe-campaign-previous-version)。

## サービス停止 {#service-stop}

まず、関係するすべてのマシン上のデータベースにアクセスできるすべてのプロセスを停止します。

1. リダイレクトモジュール（**webmdl** サービス）を使用するすべてのサーバーを停止する必要があります。 IIS の場合、次のコマンドを実行します。

   ```
   iisreset /stop
   ```

1. **mta** モジュールとその子モジュール（**mtachild**）は、次のコマンドを使用して停止する必要があります。

   ```
   nlserver stop mta@<instance name>
   nlserver stop mtachild@<instance name>
   ```

1. すべてのサーバーでAdobe Campaign サービスを停止します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   net stop nlserver6
   ```

<!--

   If you are migrating from v5.11, run the following command:

   ```
   net stop nlserver5
   ```

-->

1. 各サーバーで、Adobe Campaign サービスが正しく停止していることを確認します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   tasklist /FI "IMAGENAME eq nlserver*"
   ```

   アクティブなプロセスのリストとその ID （PID）が表示されます。

   ```
   Image Name                     PID Session Name        Session#    Mem Usage
   ========================= ======== ================ =========== ============
   nlserver.exe                  3192 Console                    1     13,108 K
   ```

1. 1 つ以上のAdobe Campaign プロセスがまだアクティブであるかブロックされている場合は、数分後に強制終了します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   taskkill /IM nlserver* /T
   ```

1. 数分後もアクティブなプロセスがある場合は、次のコマンドを使用して強制的に閉じることができます。

   ```
   taskkill /F /IM nlserver* /T
   ```

## Campaign データベースのバックアップ {#back-up-the-database}

次に、Adobe Campaign v6.1 のバックアップ手順を示します。

<!--

### For Adobe Campaign v5.11 {#migrating-from-adobe-campaign-v5-11}

1. Make a backup of the Adobe Campaign database.
1. Make a backup of the **Neolane v5** directory using the following command:

   ```
   ren "Neolane v5" "Neolane v5.back"
   ```

   >[!IMPORTANT]
   >
   >As a precaution, we recommend that you zip the **Neolane v5.back** folder and save it elsewhere in a safe location other than the server.

1. In the windows service management console, disable the automatic startup of the 5.11 application server service. You can also use the following command:

   ```
   sc config nlserver5 start= disabled
   ```

1. Edit the **config-`<instance name>`.xml** (in the **Neolane v5. back** folder) to prevent the **mta**, **wfserver**, **stat**, etc. services from starting automatically. For instance, replace **autoStart** with **_autoStart**.

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

-->

<!--
### For Adobe Campaign v6.02 {#migrating-from-adobe-campaign-v6-02}

1. Make a backup of the Adobe Campaign database.
1. Make a backup of the **Neolane v6** directory using the following command:

   ```
   ren "Neolane v6" "Neolane v6.back"
   ```

   >[!IMPORTANT]
   >
   >As a precaution, we recommend that you zip the **Neolane v6.back** folder and save it elsewhere in a safe location other than the server.

1. In the Windows service manager, deactivate the 6.02 application server automatic startup. You can also use the following command:

   ```
   sc config nlserver6 start= disabled
   ```

1. Edit the **config-`<instance name>`.xml** (in the **Neolane v6. back** folder) to prevent the **mta**, **wfserver**, **stat**, etc. services from starting automatically. For instance, replace **autoStart** with **_autoStart**.

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

-->

1. Adobe Campaign データベースのバックアップを作成します。
1. 次のコマンドを使用して、**Adobe Campaign v6** ディレクトリのバックアップを作成します。

   ```
   ren "Adobe Campaign v6" "Adobe Campaign v6.back"
   ```

   >[!IMPORTANT]
   >
   >予防措置として、**Adobe Campaign v6.back** フォルダーを zip 形式で圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. Windows サービス管理コンソールで、6.11 アプリケーションサーバーサービスの自動スタートアップを無効にします。 次のコマンドも使用できます。

   ```
   sc config nlserver6 start= disabled
   ```

## Adobe Campaign v7 のデプロイ {#deploying-adobe-campaign-v7}

Adobe Campaignのデプロイには、次の 2 つの段階があります。

* ビルド v7 をインストールしています：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで開始する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. **setup.exe** インストールファイルを実行して、最新のAdobe Campaign v7 ビルドをインストールします。 Windows へのAdobe Campaign サーバーのインストールについて詳しくは、[ この節 ](../../installation/using/installing-the-server.md) を参照してください。

   ![](assets/migration_wizard_1_7.png)

   >[!NOTE]
   >
   >Adobe Campaign v7 は、デフォルトで **C:\Program Files\Adobe\Adobe Campaign v7** ディレクトリにインストールされます。

1. クライアントコンソールのインストールプログラムを使用可能にするには、**setup-client-7.0.XXXX.exe** ファイルをAdobe Campaignのインストールディレクトリ （**C:\Program Files\Adobe\Adobe Campaign v7\datakit\nl\eng\jsp** にコピーします。

   >[!NOTE]
   >
   >Windows へのAdobe Campaignのインストールについて詳しくは、[ この節 ](../../installation/using/installing-the-server.md) を参照してください。

1. 次のコマンドを使用して、インスタンスを初めて使用するために起動します。

   ```
   net start nlserver6-v7
   net stop nlserver6-v7
   ```

   >[!NOTE]
   >
   >これらのコマンドを使用すると、Adobe Campaign v7 の内部ファイルシステムである **conf** ディレクトリ（**config-default.xml** および **serverConf.xml** ファイルを含む）、**var** ディレクトリなどを作成できます。

1. **Neolane v5.back**、{Neolane v6.back **または** 4}Adobe Campaign v6.back **のバックアップファイルを使用して、各インスタンスの設定ファイルとサブフォルダーをコピーして貼り付け（上書き）します（移行元のバージョンによって異なります。[ この節 ](#back-up-the-database-and-the-current-installation) を参照してください）。**
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
   >上記の最初のコマンドについては、**config-default.xml** ファイルをコピーしないでください。

1. Adobe Campaign v7 の **serverConf.xml** および **config-default.xml** ファイルで、Adobe Campaignの以前のバージョンで行った特定の設定を適用します。 **serverConf.xml** ファイルには、**Neolane v5/conf/serverConf.xml.diff**、**Neolane v6/conf/serverConf.xml.diff** または **Adobe Campaign v6/conf/serverConf.xml.diff** ファイルを使用します。

   >[!NOTE]
   >
   >Adobe Campaignの旧バージョンからAdobe Campaign v7 に設定をレポートする場合は、物理ディレクトリへのパスがAdobe Campaign v7 （Neolane v5、Neolane v6 またはAdobe Campaign v6 ではなく）につながっていることを確認してください。

1. 次のコマンドを使用して、Adobe Campaign v7 設定をリロードします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します。

   ```
   nlserver config -postupgrade -instance:<instance name>
   ```

>[!IMPORTANT]
>
>Adobe Campaign サービスはまだ開始しないでください。IIS で一部の変更を行う必要があります。

## リダイレクトサーバーの移行 {#migrating-the-redirection-server--iis-}

この段階で、IIS サーバーを停止する必要があります。 [ サービス停止 ](#service-stop) を参照してください。

1. **インターネット インフォメーション サービス （IIS） マネージャ** コンソールを開きます。
1. Adobe Campaignの以前のバージョンで使用されていたサイトのバインディング（リッスンポート）を変更します。

   * Adobe Campaignの以前のバージョンで使用されているサイトを右クリックし、「**[!UICONTROL 連結を編集]**」を選択します。
   * 各タイプのリッスンポート（**[!UICONTROL http]** や **[!UICONTROL https]**）に対して、適切な行を選択し **[!UICONTROL 編集]** をクリックします。
   * 別のポートを入力してください。 デフォルトでは、リッスンポートは http の場合は 80、https の場合は 443 です。 新しいポートが使用可能であることを確認します。

     ![](assets/_migration_iis_3_611.png)

     >[!NOTE]
     >
     >IIS サーバーに、高度な設定を持つAdobe Campaign用の複数の web サイト（共有ポートと異なる IP アドレス）が含まれている場合は、管理者にお問い合わせください。

1. Adobe Campaign v7 の新しい web サイトを作成します。

   * **[!UICONTROL Sites]** フォルダーを右クリックし、「**[!UICONTROL Web サイトを追加…]**」を選択します。

     ![](assets/_migration_iis_4.png)

   * サイトの名前（**Adobe Campaign v7** など）を入力します。
   * Web サイトの基本ディレクトリへのアクセスパスは使用されませんが、「**[!UICONTROL 物理アクセスパス]**」フィールドに入力する必要があります。 既定の IIS アクセス パスを入力してください：**C:\inetpub\wwwroot**。
   * **[!UICONTROL 別名で接続…]** ボタンをクリックし、「**[!UICONTROL アプリケーションユーザー]**」オプションが選択されていることを確認します。
   * デフォルト値は「**[!UICONTROL IP アドレス]**」フィールドと「**[!UICONTROL ポート]**」フィールドのままにすることができます。 他の値を使用する場合は、IP アドレスやポートが使用可能であることを確認してください。
   * 「**[!UICONTROL Web サイトをすぐに開始]** ボックスをオンにします。

     ![](assets/_migration_iis_5_7.png)

1. **iis_neolane_setup.vbs** スクリプトを実行して、以前に作成した仮想ディレクトリ上でAdobe Campaign サーバが使用するリソースを自動的に構成します。

   * このファイルは **`[Adobe Campaign v7]`\conf** ディレクトリにあります。**`[Adobe Campaign v7]`** は、Adobe Campaign インストールディレクトリへのアクセスパスです。 スクリプトを実行するコマンドを次に示します（管理者向け）。

     ```
     cd C:\Program Files (x86)\Adobe Campaign\Adobe Campaign v7\conf
     cscript iis_neolane_setup.vbs
     ```

   * 「**[!UICONTROL OK]**」をクリックして、スクリプトの実行を確定します。

     ![](assets/s_ncs_install_iis7_parameters_step2_7.png)

   * 以前にAdobe Campaign v7 用に作成した web サイトの数を入力して、「**[!UICONTROL OK]**」をクリックします。

     ![](assets/s_ncs_install_iis7_parameters_step3_7.png)

   * 確認メッセージが表示されます。

     ![](assets/s_ncs_install_iis7_parameters_step7_7.png)

   * 「**[!UICONTROL コンテンツビュー]**」タブで、web サイト設定がAdobe Campaign リソースで正しく設定されていることを確認します。

     ![](assets/s_ncs_install_iis7_parameters_step6_7.png)

     >[!NOTE]
     >
     >ツリー構造が表示されない場合は、IIS を再起動します。
     >
     >次の IIS 設定手順について詳しくは、[ この節 ](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server) を参照してください。

<!--
## Security zones {#security-zones}

If you are migrating from v6.02 or earlier, you must configure your security zones before starting services. [Learn more](../../migration/using/general-configurations.md#security)
-->

## サービスの再起動 {#re-starting-the-services}

次の各サーバで IIS およびAdobe Campaign サービスを開始します。

1. トラッキングサーバーとリダイレクトサーバー。
1. ミッドソーシングサーバー。
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、リグレッションがなく、すべてが機能することを確認します。

## 以前のバージョンを削除 {#deleting-and-cleansing-adobe-campaign-previous-version}

次に、Adobe Campaign v6.1 を削除する手順を示します。

<!--

### For Adobe Campaign v5 {#adobe-campaign-v5}

Before you delete and cleanse the Adobe Campaign v5 installation, you must apply the following recommendations:

* Get the functional teams to run a full check of the new installation.
* Only uninstall Adobe Campaign v5 once you are certain that no rollback is necessary.

1. In IIS, delete the **Neolane v5** website, then the **Neolane v5** application pool. 
1. Rename the **Neolane v5.back** folder as **Neolane v5**.
1. Uninstall Adobe Campaign v5 using the Add/remove components assistant. 

   ![](assets/migration_wizard_2.png)

1. Delete the **nlserver5** Windows service using the following command:

   ```
   sc delete nlserver5
   ```

1. Re-start the server.

### For Adobe Campaign v6.02 {#adobe-campaign-v6-02}

Before you delete and cleanse the Adobe Campaign v6.02 installation, you must apply the following recommendations:

* Get the functional teams to run a full check of the new installation.
* Only uninstall Adobe Campaign v6.02 once you are certain that no rollback is necessary.

1. In IIS, delete the **Neolane v6** website, then the **Neolane v6** application pool. 
1. Rename the **Neolane v6.back** folder as **Neolane v6**.
1. Uninstall Adobe Campaign v6.02 using the Add/remove components assistant. 

   ![](assets/migration_wizard_2.png)

1. Re-start the server.

-->

Adobe Campaign v6 インストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールのフルチェックを実行してもらいます。
* ロールバックが必要ないことが確実な場合にのみ、Adobe Campaign v6 をアンインストールします。

1. IIS で、**Adobe Campaign v6** web サイトを削除してから、**Adobe Campaign v6** アプリケーション プールを削除します。
1. **Adobe Campaign v6.back** フォルダーの名前を **Adobe Campaign v6** に変更します。
1. コンポーネントの追加と削除ウィザードを使用して、Adobe Campaign v6 をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. サーバーを再起動します。
