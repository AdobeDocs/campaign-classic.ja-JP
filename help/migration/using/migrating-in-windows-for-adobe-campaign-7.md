---
solution: Campaign Classic
product: campaign
title: Windows での Adobe Campaign 7 への移行
description: Windows での Adobe Campaign 7 への移行
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 1%

---


# Windows での Adobe Campaign 7 への移行{#migrating-in-windows-for-adobe-campaign}

## 一般的な手順{#general-procedure}

Windowsの場合の移行手順は次のとおりです。

1. サービスの停止：[サービスの停止](#service-stop)を参照してください。
1. データベースのバックアップ：[データベースと現在のインストールのバックアップ](#back-up-the-database-and-the-current-installation)を参照してください。
1. プラットフォームの移行：[Adobe Campaignv7](#deploying-adobe-campaign-v7)の導入を参照してください。
1. リダイレクトサーバー(IIS)を移行する：[リダイレクトサーバー(IIS)](#migrating-the-redirection-server--iis-)を移行するを参照してください。
1. 再開始サービス：[サービスの再起動](#re-starting-the-services)を参照してください。
1. 以前のバージョンのAdobe Campaignを削除および削除する：[クレンジングAdobe Campaignの以前のバージョン](#deleting-and-cleansing-adobe-campaign-previous-version)の削除とバージョンを参照してください。

## サービス停止{#service-stop}

まず、関連するすべてのマシン上のデータベースにアクセスできるすべてのプロセスを停止します。

1. リダイレクトモジュール（**webmdl**&#x200B;サービス）を使用しているすべてのサーバーを停止する必要があります。 IISの場合は、次のコマンドを実行します。

   ```
   iisreset /stop
   ```

1. **mta**&#x200B;モジュールとその子モジュール(**mtachild**)は、次のコマンドを使用して停止する必要があります。

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

## データベースと現在のインストール{#back-up-the-database-and-the-current-installation}をバックアップします。

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5.11からの移行{#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. 次のコマンドを使用して、**Neolane v5**&#x200B;ディレクトリのバックアップを作成します。

   ```
   ren "Neolane v5" "Neolane v5.back"
   ```

   >[!IMPORTANT]
   >
   >予防策として、**Neolane v5.back**&#x200B;フォルダーをzipにして、サーバー以外の安全な場所に保存することをお勧めします。

1. Windowsサービス管理コンソールで、5.11アプリケーションサーバーサービスの自動スタートアップを無効にします。 次のコマンドも使用できます。

   ```
   sc config nlserver5 start= disabled
   ```

1. **config-`<instance name>`.xml**&#x200B;を編集します（**Neolane v5内）。 back**&#x200B;フォルダー)を使用して、**mta**、**wfserver**、**stat**&#x200B;などを防ぎます。 サービスが自動的に開始されない。 例えば、**autoStart**&#x200B;を&#x200B;**_autoStart**&#x200B;に置き換えます。

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

### Adobe Campaignv6.02からの移行{#migrating-from-adobe-campaign-v6-02}

1. Adobe Campaignデータベースのバックアップを作成します。
1. 次のコマンドを使用して、**Neolane v6**&#x200B;ディレクトリのバックアップを作成します。

   ```
   ren "Neolane v6" "Neolane v6.back"
   ```

   >[!IMPORTANT]
   >
   >予防策として、**Neolane v6.back**&#x200B;フォルダーをzipにして、サーバー以外の安全な場所に保存することをお勧めします。

1. Windowsサービスマネージャーで、6.02アプリケーションサーバーの自動スタートアップを非アクティブにします。 次のコマンドも使用できます。

   ```
   sc config nlserver6 start= disabled
   ```

1. **config-`<instance name>`.xml**&#x200B;を編集します（**Neolane v6内）。 back**&#x200B;フォルダー)を使用して、**mta**、**wfserver**、**stat**&#x200B;などを防ぎます。 サービスが自動的に開始されない。 例えば、**autoStart**&#x200B;を&#x200B;**_autoStart**&#x200B;に置き換えます。

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

### Adobe Campaignv6.1からの移行{#migrating-from-adobe-campaign-v6-1}

1. Adobe Campaignデータベースのバックアップを作成します。
1. 次のコマンドを使用して、**Adobe Campaignv6**&#x200B;ディレクトリのバックアップを作成します。

   ```
   ren "Adobe Campaign v6" "Adobe Campaign v6.back"
   ```

   >[!IMPORTANT]
   >
   >予防策として、**Adobe Campaignv6.back**&#x200B;フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. Windowsサービス管理コンソールで、6.11アプリケーションサーバーサービスの自動スタートアップを無効にします。 次のコマンドも使用できます。

   ```
   sc config nlserver6 start= disabled
   ```

## Adobe Campaignv7の導入{#deploying-adobe-campaign-v7}

Adobe Campaignのデプロイには、次の2つの段階があります。

* ビルドv7のインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後の手順：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順を適用します。

1. **setup.exe**&#x200B;インストールファイルを実行して、最新Adobe Campaignのv7ビルドをインストールします。 WindowsでのAdobe Campaignサーバーのインストールについて詳しくは、[](../../installation/using/installing-the-server.md)を参照してください。

   ![](assets/migration_wizard_1_7.png)

   >[!NOTE]
   >
   >Adobe Campaignv7は、デフォルトで&#x200B;**C:\Program Files\Adobe\Adobe Campaign v7**&#x200B;ディレクトリにインストールされます。

1. クライアントコンソールのインストールプログラムを使用可能にするには、**setup-client-7.0.XXXX.exe**&#x200B;ファイルをAdobe Campaignのインストールディレクトリにコピーします。**C:\Program Files\Adobe\Adobe Campaign v7\datakit\nl\eng\jsp**.

   >[!NOTE]
   >
   >WindowsでのAdobe Campaignのインストールについて詳しくは、[このセクション](../../installation/using/installing-the-server.md)を参照してください。

1. 次のコマンドを使用して、最初に使用するインスタンスを開始します。

   ```
   net start nlserver6-v7
   net stop nlserver6-v7
   ```

   >[!NOTE]
   >
   >次の各コマンドでは、Adobe Campaignv7の内部ファイルシステムを作成できます。**conf**&#x200B;ディレクトリ（**config-default.xml**&#x200B;ファイルと&#x200B;**serverConf.xml**&#x200B;ファイルを含む）、**var**&#x200B;ディレクトリなど。

1. **Neolane v5.back**、**Neolane v6.back**&#x200B;または&#x200B;**Adobe Campaignv6.back**&#x200B;バックアップファイルを使用して、各インスタンスの設定ファイルとサブフォルダーをコピー&amp;ペースト（上書き）します（移行元のバージョンによって異なります）。[](#back-up-the-database-and-the-current-installation)
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
   >上記の最初のコマンドでは、**config-default.xml**&#x200B;ファイルをコピーしないでください。

1. Adobe Campaignv7の&#x200B;**serverConf.xml**&#x200B;ファイルと&#x200B;**config-default.xml**&#x200B;ファイルに、Adobe Campaign前のバージョンでの設定に従って設定を適用します。 **serverConf.xml**&#x200B;ファイルには、**Neolane v5/conf/serverConf.xml.diff**、**Neolane v6/conf/serverConf.xml.diff**、または&#x200B;**Adobe Campaignv6/conf/serverConf.xml.diff**&#x200B;ファイルを使用します。

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

## リダイレクトサーバー(IIS)を移行中{#migrating-the-redirection-server--iis-}

この段階で、IISサーバーを停止する必要があります。 [サービスの停止](#service-stop)を参照してください。

1. **インターネット情報サービス(IIS)マネージャー**&#x200B;コンソールを開きます。
1. Adobe Campaignの前のバージョンに使用するサイトのバインディング（リスンポート）を変更します。

   * Adobe Campaign前のバージョンに使用するサイトを右クリックし、「**[!UICONTROL 連結を編集]**」を選択します。
   * リスンポートのタイプ（**[!UICONTROL http]**&#x200B;または&#x200B;**[!UICONTROL https]**）ごとに、適切な行を選択し、「**[!UICONTROL 編集]**」をクリックします。
   * 別のポートを入力してください。 デフォルトでは、リスンポートはhttpの場合は80、httpsの場合は443です。 新しいポートが使用可能であることを確認します。

      ![](assets/_migration_iis_3_611.png)

      >[!NOTE]
      >
      >IISサーバーに高度な設定（共有ポートと異なるIPアドレス）とのAdobe Campaign用のWebサイトが複数ある場合は、管理者にお問い合わせください。

1. Adobe Campaignv7用の新しいWebサイトの作成：

   * **[!UICONTROL サイト]**&#x200B;フォルダーを右クリックし、「**[!UICONTROL 追加Webサイト…」を選択します。]**。

      ![](assets/_migration_iis_4.png)

   * サイトの名前(例えば&#x200B;**Adobe Campaignv7**)を入力します。
   * Webサイトの基本ディレクトリへのアクセスパスは使用されませんが、**[!UICONTROL 物理アクセスパス]**&#x200B;フィールドを入力する必要があります。 既定のIISアクセスパスを入力してください：**C:\inetpub\wwwroot**.
   * [**[!UICONTROL 接続方法…]をクリックします。]**&#x200B;をボタンとして追加し、「**[!UICONTROL アプリケーションユーザー]**」オプションが選択されていることを確認します。
   * **[!UICONTROL IPアドレス]**&#x200B;フィールドと&#x200B;**[!UICONTROL ポート]**&#x200B;フィールドにはデフォルト値を入力しておきます。 その他の値を使用する場合は、IPアドレスやポートが使用可能であることを確認します。
   * **[!UICONTROL 開始ウェブサイトをすぐに]**&#x200B;チェックボックスをオンにします。

      ![](assets/_migration_iis_5_7.png)

1. **iis_neolane_setup.vbs**&#x200B;スクリプトを実行し、以前に作成した仮想ディレクトリでAdobe Campaignサーバーが使用するリソースを自動的に構成します。

   * このファイルは&#x200B;**`[Adobe Campaign v7]`\conf**&#x200B;ディレクトリにあります。**`[Adobe Campaign v7]`**&#x200B;は、Adobe Campaignのインストールディレクトリへのアクセスパスです。 スクリプトを実行するコマンドは次のとおりです（管理者の場合）。

      ```
      cd C:\Program Files (x86)\Adobe Campaign\Adobe Campaign v7\conf
      cscript iis_neolane_setup.vbs
      ```

   * 「**[!UICONTROL OK]**」をクリックして、スクリプトの実行を確定します。

      ![](assets/s_ncs_install_iis7_parameters_step2_7.png)

   * Adobe Campaignv7用に以前に作成したWebサイトの番号を入力し、「**[!UICONTROL OK]**」をクリックします。

      ![](assets/s_ncs_install_iis7_parameters_step3_7.png)

   * 確認メッセージが表示されます。

      ![](assets/s_ncs_install_iis7_parameters_step7_7.png)

   * 「**[!UICONTROL コンテンツの表示]**」タブで、Webサイトの設定がAdobe Campaignリソースと共に正しく設定されていることを確認します。

      ![](assets/s_ncs_install_iis7_parameters_step6_7.png)

      >[!NOTE]
      >
      >ツリー構造が表示されない場合は、IISを再開始します。
      >
      >次のIISの設定手順については、[このセクション](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server)で詳しく説明します。

## セキュリティゾーン{#security-zones}

v6.02以前から移行する場合は、サービスを開始する前にセキュリティゾーンを構成する必要があります。 詳しくは、[セキュリティ](../../migration/using/general-configurations.md#security)を参照してください。

## サービスの再開{#re-starting-the-services}

次の各サーバーでの開始IISとAdobe Campaignサービス：

1. トラッキングとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、回帰がないこと、および[一般的な設定](../../migration/using/general-configurations.md)セクションの推奨事項に従って動作することを確認してください。

## 以前のバージョン{#deleting-and-cleansing-adobe-campaign-previous-version}のクレンジングAdobe Campaignを削除しています

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5 {#adobe-campaign-v5}

Adobe Campaignv5のインストールを削除およびクリーニングする前に、次の推奨事項を適用する必要があります。

* 新しいインストールの完全なチェックを実行するには、機能チームに依頼します。
* Adobe Campaignv5は、ロールバックが必要ないことが確実にわかった場合にのみアンインストールします。

1. IISで、**Neolane v5** Webサイトを削除し、**Neolane v5**&#x200B;アプリケーションプールを削除します。
1. **Neolane v5.back**&#x200B;フォルダーの名前を&#x200B;**Neolane v5**&#x200B;に変更します。
1. コンポーネントの追加削除ウィザードを使用してAdobe Campaignv5をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. 次のコマンドを使用して、**nlserver5** Windowsサービスを削除します。

   ```
   sc delete nlserver5
   ```

1. サーバーの開始を再度行います。

### Adobe Campaign v6.02 {#adobe-campaign-v6-02}

Adobe Campaignv6.02のインストールを削除およびクリーニングする前に、次の推奨事項を適用する必要があります。

* 新しいインストールの完全なチェックを実行するには、機能チームに依頼します。
* Adobe Campaignv6.02は、ロールバックが必要ないことが確実にわかった場合にのみアンインストールします。

1. IISで、**Neolane v6** Webサイトを削除し、**Neolane v6**&#x200B;アプリケーションプールを削除します。
1. **Neolane v6.back**&#x200B;フォルダーの名前を&#x200B;**Neolane v6**&#x200B;に変更します。
1. Adobe Campaignv6.02をアンインストールするには、コンポーネントの追加削除ウィザードを使用します。

   ![](assets/migration_wizard_2.png)

1. サーバーの開始を再度行います。

### Adobe Campaign v6.1 {#adobe-campaign-v6-1}

Adobe Campaignv6のインストールを削除してクリーンアップする前に、次の推奨事項を適用する必要があります。

* 新しいインストールの完全なチェックを実行するには、機能チームに依頼します。
* Adobe Campaignv6は、ロールバックが必要ないことが確実にわかった場合にのみアンインストールします。

1. IISの場合は、**Adobe Campaignv6** Webサイトを削除し、**Adobe Campaignv6**&#x200B;アプリケーションプールを削除します。
1. **Adobe Campaignv6.back**&#x200B;フォルダーの名前を&#x200B;**Adobe Campaignv6**&#x200B;に変更します。
1. コンポーネントの追加削除ウィザードを使用してAdobe Campaignv6をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. サーバーの開始を再度行います。

