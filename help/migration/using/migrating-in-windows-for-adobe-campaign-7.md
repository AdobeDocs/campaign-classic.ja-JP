---
product: campaign
title: Windows での Adobe Campaign 7 への移行
description: Windows での Adobe Campaign 7 への移行
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
exl-id: 3743d018-3316-4ce3-ae1c-25760aaf5785
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 1%

---

# Windows での Adobe Campaign 7 への移行{#migrating-in-windows-for-adobe-campaign}

## 一般的な手順{#general-procedure}

Windowsの場合、移行手順は次のとおりです。

1. サービスの停止：[サービス停止](#service-stop)を参照してください。
1. データベースのバックアップ：[データベースと現在のインストールのバックアップ](#back-up-the-database-and-the-current-installation)を参照してください。
1. プラットフォームの移行：[Adobe Campaign v7のデプロイ](#deploying-adobe-campaign-v7)を参照してください。
1. リダイレクションサーバー(IIS)を移行します。[リダイレクションサーバー(IIS)](#migrating-the-redirection-server--iis-)の移行を参照してください。
1. サービスの再起動：[サービスの再起動](#re-starting-the-services)を参照してください。
1. 以前のバージョンのAdobe Campaignを削除してクレンジングする：[Adobe Campaignの以前のバージョンの削除とクレンジング](#deleting-and-cleansing-adobe-campaign-previous-version)を参照してください。

## サービス停止{#service-stop}

まず、関係するすべてのマシン上のデータベースにアクセスできるすべてのプロセスを停止します。

1. リダイレクトモジュール（**webmdl**&#x200B;サービス）を使用するすべてのサーバーを停止する必要があります。 IISの場合は、次のコマンドを実行します。

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

1. 各サーバーで、Adobe Campaignサービスが正しく停止されていることを確認します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   tasklist /FI "IMAGENAME eq nlserver*"
   ```

   アクティブなプロセスとそのID(PID)のリストが表示されます。

   ```
   Image Name                     PID Session Name        Session#    Mem Usage
   ========================= ======== ================ =========== ============
   nlserver.exe                  3192 Console                    1     13,108 K
   ```

1. 数分後に1つ以上のAdobe Campaignプロセスがアクティブまたはブロックされたままの場合は、それらを強制終了します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   taskkill /IM nlserver* /T
   ```

1. 数分後に一部のプロセスがアクティブなままの場合は、次のコマンドを使用してプロセスを強制的に閉じることができます。

   ```
   taskkill /F /IM nlserver* /T
   ```

## データベースと現在のインストール{#back-up-the-database-and-the-current-installation}をバックアップします。

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5.11からの移行{#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. 次のコマンドを使用して、**Neolane v5**&#x200B;ディレクトリのバックアップを作成します。

   ```
   ren "Neolane v5" "Neolane v5.back"
   ```

   >[!IMPORTANT]
   >
   >予防措置として、**Neolane v5.back**&#x200B;フォルダーをzipファイルにして、サーバー以外の安全な場所に保存することをお勧めします。

1. Windowsサービス管理コンソールで、5.11アプリケーションサーバーサービスの自動起動を無効にします。 次のコマンドも使用できます。

   ```
   sc config nlserver5 start= disabled
   ```

1. **config-`<instance name>`.xml**&#x200B;を編集します（**Neolane v5内）。**&#x200B;フォルダーに戻る)をクリックして、**mta**、**wfserver**、**stat**&#x200B;などを防ぎます。 サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart**&#x200B;を&#x200B;**_autoStart**&#x200B;に置き換えます。

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

### Adobe Campaign v6.02からの移行{#migrating-from-adobe-campaign-v6-02}

1. Adobe Campaignデータベースのバックアップを作成します。
1. 次のコマンドを使用して、**Neolane v6**&#x200B;ディレクトリのバックアップを作成します。

   ```
   ren "Neolane v6" "Neolane v6.back"
   ```

   >[!IMPORTANT]
   >
   >予防措置として、**Neolane v6.back**&#x200B;フォルダーをzipにして、サーバー以外の安全な場所に保存することをお勧めします。

1. Windowsサービスマネージャーで、6.02アプリケーションサーバーの自動起動を無効にします。 次のコマンドも使用できます。

   ```
   sc config nlserver6 start= disabled
   ```

1. **config-`<instance name>`.xml**（**Neolane v6内）を編集します。**&#x200B;フォルダーに戻る)をクリックして、**mta**、**wfserver**、**stat**&#x200B;などを防ぎます。 サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart**&#x200B;を&#x200B;**_autoStart**&#x200B;に置き換えます。

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

### Adobe Campaign v6.1からの移行{#migrating-from-adobe-campaign-v6-1}

1. Adobe Campaignデータベースのバックアップを作成します。
1. 次のコマンドを使用して、**Adobe Campaign v6**&#x200B;ディレクトリのバックアップを作成します。

   ```
   ren "Adobe Campaign v6" "Adobe Campaign v6.back"
   ```

   >[!IMPORTANT]
   >
   >予防措置として、**Adobe Campaign v6.back**&#x200B;フォルダーをzip形式で圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. Windowsサービス管理コンソールで、6.11アプリケーションサーバーサービスの自動起動を無効にします。 次のコマンドも使用できます。

   ```
   sc config nlserver6 start= disabled
   ```

## Adobe Campaign v7 {#deploying-adobe-campaign-v7}のデプロイ

Adobe Campaignのデプロイには、次の2つの段階があります。

* ビルドv7のインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. **setup.exe**&#x200B;インストールファイルを実行して、最新のAdobe Campaign v7ビルドをインストールします。 WindowsでのAdobe Campaignサーバーのインストールについて詳しくは、[この節](../../installation/using/installing-the-server.md)を参照してください。

   ![](assets/migration_wizard_1_7.png)

   >[!NOTE]
   >
   >Adobe Campaign v7は、デフォルトで&#x200B;**C:\Program Files\Adobe\Adobe Campaign v7**&#x200B;ディレクトリにインストールされます。

1. クライアントコンソールのインストールプログラムを使用可能にするには、**setup-client-7.0.XXXX.exe**&#x200B;ファイルをAdobe Campaignのインストールディレクトリにコピーします。**C:\Program Files\Adobe\Adobe Campaign v7\datakit\nl\eng\jsp**.

   >[!NOTE]
   >
   >WindowsでのAdobe Campaignのインストールについて詳しくは、[この節](../../installation/using/installing-the-server.md)を参照してください。

1. 次のコマンドを使用して、最初の使用用のインスタンスを起動します。

   ```
   net start nlserver6-v7
   net stop nlserver6-v7
   ```

   >[!NOTE]
   >
   >次のコマンドを使用して、Adobe Campaign v7の内部ファイルシステムを作成できます。**conf**&#x200B;ディレクトリ（**config-default.xml**&#x200B;および&#x200B;**serverConf.xml**&#x200B;ファイルを含む）、**var**&#x200B;ディレクトリなど。

1. **Neolane v5.back**、**Neolane v6.back**&#x200B;または&#x200B;**Adobe Campaign v6.back**&#x200B;バックアップファイルを使用して、各インスタンスの設定ファイルとサブフォルダーをコピー&amp;ペースト（上書き）します（移行元のバージョンに応じて異なります）。[](#back-up-the-database-and-the-current-installation)
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

1. Adobe Campaign v7の&#x200B;**serverConf.xml**&#x200B;ファイルと&#x200B;**config-default.xml**&#x200B;ファイルで、Adobe Campaignの以前のバージョンでの設定を適用します。 **serverConf.xml**&#x200B;ファイルの場合は、**Neolane v5/conf/serverConf.xml.diff**、**Neolane v6/conf/serverConf.xml.diff**、または&#x200B;**Adobe Campaign v6/conf/serverConf.xml.diff**&#x200B;ファイルを使用します。

   >[!NOTE]
   >
   >Adobe Campaignの以前のバージョンからAdobe Campaign v7に設定をレポートする場合、物理ディレクトリへのパスがAdobe Campaign v7につながっている(Neolane v5、Neolane v6またはAdobe Campaign v6にはならない)ことを確認します。

1. 次のコマンドを使用して、Adobe Campaign v7設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します。

   ```
   nlserver config -postupgrade -instance:<instance name>
   ```

>[!IMPORTANT]
>
>まだAdobe Campaignサービスを開始しない：IISでいくつかの変更を行う必要があります。

## リダイレクションサーバー(IIS) {#migrating-the-redirection-server--iis-}を移行中

この段階で、IISサーバーを停止する必要があります。 [サービス停止](#service-stop)を参照してください。

1. **インターネットインフォメーションサービス(IIS)マネージャー**&#x200B;コンソールを開きます。
1. Adobe Campaignの以前のバージョンで使用するサイトのバインディング（リッスンポート）を変更します。

   * Adobe Campaignの以前のバージョンに使用するサイトを右クリックし、「**[!UICONTROL バインディングを編集]**」を選択します。
   * リスンポートの各タイプ（**[!UICONTROL http]**&#x200B;や&#x200B;**[!UICONTROL https]**）に対して、適切な行を選択し、「**[!UICONTROL 編集]**」をクリックします。
   * 別のポートを入力してください。 デフォルトでは、リスンポートはhttpの場合は80、httpsの場合は443です。 新しいポートが使用可能であることを確認します。

      ![](assets/_migration_iis_3_611.png)

      >[!NOTE]
      >
      >IISサーバーに、高度な設定（共有ポートと異なるIPアドレス）を持つAdobe Campaign用のWebサイトが複数含まれている場合は、管理者に問い合わせてください。

1. Adobe Campaign v7用の新しいWebサイトの作成：

   * **[!UICONTROL Sites]**&#x200B;フォルダーを右クリックし、「**[!UICONTROL Webサイトを追加…」を選択します。]**&#x200B;と入力します。

      ![](assets/_migration_iis_4.png)

   * 例えば、サイトの名前を&#x200B;**Adobe Campaign v7**&#x200B;と入力します。
   * Webサイトの基本ディレクトリへのアクセスパスは使用されませんが、**[!UICONTROL 物理アクセスパス]**&#x200B;フィールドに入力する必要があります。 デフォルトのIISアクセスパスを入力：**C:\inetpub\wwwroot**.
   * 「**[!UICONTROL 接続…」をクリックします。]**&#x200B;をボタンとして追加し、「**[!UICONTROL アプリケーションユーザー]**」オプションが選択されていることを確認します。
   * **[!UICONTROL IPアドレス]**&#x200B;フィールドと&#x200B;**[!UICONTROL ポート]**&#x200B;フィールドにはデフォルト値を残すことができます。 他の値を使用する場合は、IPアドレスやポートが使用可能であることを確認します。
   * 「**[!UICONTROL すぐにWebサイトを開始]**」ボックスをオンにします。

      ![](assets/_migration_iis_5_7.png)

1. **iis_neolane_setup.vbs**&#x200B;スクリプトを実行して、以前に作成した仮想ディレクトリ上のAdobe Campaignサーバーで使用されるリソースを自動的に設定します。

   * このファイルは、**`[Adobe Campaign v7]`\conf**&#x200B;ディレクトリにあります。ここで&#x200B;**`[Adobe Campaign v7]`**&#x200B;は、Adobe Campaignインストールディレクトリへのアクセスパスです。 スクリプトを実行するコマンドは次のとおりです（管理者向け）。

      ```
      cd C:\Program Files (x86)\Adobe Campaign\Adobe Campaign v7\conf
      cscript iis_neolane_setup.vbs
      ```

   * 「**[!UICONTROL OK]**」をクリックして、スクリプトの実行を確定します。

      ![](assets/s_ncs_install_iis7_parameters_step2_7.png)

   * Adobe Campaign v7用に以前に作成したWebサイトの番号を入力し、「**[!UICONTROL OK]**」をクリックします。

      ![](assets/s_ncs_install_iis7_parameters_step3_7.png)

   * 次の確認メッセージが表示されます。

      ![](assets/s_ncs_install_iis7_parameters_step7_7.png)

   * 「**[!UICONTROL コンテンツビュー]**」タブで、Webサイトの設定がAdobe Campaignのリソースで正しく設定されていることを確認します。

      ![](assets/s_ncs_install_iis7_parameters_step6_7.png)

      >[!NOTE]
      >
      >ツリー構造が表示されない場合は、IISを再起動します。
      >
      >次のIISの設定手順については、[この節](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server)で詳しく説明します。

## セキュリティゾーン{#security-zones}

v6.02以前から移行する場合は、サービスを開始する前にセキュリティゾーンを設定する必要があります。 詳しくは、[セキュリティ](../../migration/using/general-configurations.md#security)を参照してください。

## サービス{#re-starting-the-services}を再開しています

次の各サーバーでIISおよびAdobe Campaignサービスを開始します。

1. 追跡サーバーとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、リグレッションがなく、[一般設定](../../migration/using/general-configurations.md)セクションのすべての推奨事項に従ってすべてが動作することを確認します。

## Adobe Campaignの以前のバージョン{#deleting-and-cleansing-adobe-campaign-previous-version}の削除とクレンジング

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5 {#adobe-campaign-v5}

Adobe Campaign v5のインストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールの完全なチェックを実行してもらう。
* ロールバックが必要ないことが確実である場合は、Adobe Campaign v5をアンインストールする必要があります。

1. IISで、**Neolane v5** Webサイトを削除し、**Neolane v5**&#x200B;アプリケーションプールを削除します。
1. **Neolane v5.back**&#x200B;フォルダーの名前を&#x200B;**Neolane v5**&#x200B;に変更します。
1. コンポーネントの追加と削除ウィザードを使用してAdobe Campaign v5をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. 次のコマンドを使用して、**nlserver5** Windowsサービスを削除します。

   ```
   sc delete nlserver5
   ```

1. サーバーを再起動します。

### Adobe Campaign v6.02 {#adobe-campaign-v6-02}

Adobe Campaign v6.02のインストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールの完全なチェックを実行してもらう。
* ロールバックが必要ないことが確実な場合にのみ、Adobe Campaign v6.02をアンインストールします。

1. IISで、**Neolane v6** Webサイトを削除し、**Neolane v6**&#x200B;アプリケーションプールを削除します。
1. **Neolane v6.back**&#x200B;フォルダーの名前を&#x200B;**Neolane v6**&#x200B;に変更します。
1. コンポーネントの追加と削除ウィザードを使用してAdobe Campaign v6.02をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. サーバーを再起動します。

### Adobe Campaign v6.1 {#adobe-campaign-v6-1}

Adobe Campaign v6のインストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールの完全なチェックを実行してもらう。
* ロールバックが必要ないことが確実である場合は、Adobe Campaign v6をアンインストールする必要があります。

1. IISで、**Adobe Campaign v6** Webサイトを削除し、**Adobe Campaign v6**&#x200B;アプリケーションプールを削除します。
1. **Adobe Campaign v6.back**&#x200B;フォルダーの名前を&#x200B;**Adobe Campaign v6**&#x200B;に変更します。
1. コンポーネントの追加と削除ウィザードを使用してAdobe Campaign v6をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. サーバーを再起動します。
