---
product: campaign
title: Windows での Adobe Campaign 7 への移行
description: Windows での Adobe Campaign 7 への移行
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
exl-id: 3743d018-3316-4ce3-ae1c-25760aaf5785
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 1%

---

# Windows での Adobe Campaign 7 への移行{#migrating-in-windows-for-adobe-campaign}

![](../../assets/v7-only.svg)

## 一般的な手順 {#general-procedure}

Windows の場合、移行手順は次のとおりです。

1. サービスを停止：参照する [サービス停止](#service-stop).
1. データベースのバックアップ：参照する [データベースと現在のインストールのバックアップ](#back-up-the-database-and-the-current-installation).
1. プラットフォームの移行：参照する [Adobe Campaign v7 のデプロイ](#deploying-adobe-campaign-v7).
1. リダイレクションサーバー (IIS) を移行します。参照する [リダイレクトサーバー (IIS) の移行](#migrating-the-redirection-server--iis-).
1. サービスを再開します。参照する [サービスの再起動](#re-starting-the-services).
1. 以前のバージョンのAdobe Campaignを削除してクレンジング：参照する [以前のバージョンのAdobe Campaignの削除とクレンジング](#deleting-and-cleansing-adobe-campaign-previous-version).

## サービス停止 {#service-stop}

まず、関係するすべてのマシン上のデータベースにアクセスしているすべてのプロセスを停止します。

1. リダイレクトモジュールを使用するすべてのサーバー (**webmdl** サービス ) を停止する必要があります。 IIS の場合は、次のコマンドを実行します。

   ```
   iisreset /stop
   ```

1. この **mta** モジュールとその子モジュール (**mtachild**) は、次のコマンドを使用して停止する必要があります。

   ```
   nlserver stop mta@<instance name>
   nlserver stop mtachild@<instance name>
   ```

1. すべてのサーバーでAdobe Campaignサービスを停止します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   net stop nlserver6
   ```

   v5.11 から移行する場合は、次のコマンドを実行します。

   ```
   net stop nlserver5
   ```

1. 各サーバーで、Adobe Campaignサービスが正しく停止されていることを確認します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   tasklist /FI "IMAGENAME eq nlserver*"
   ```

   アクティブなプロセスのリストとその ID(PID) が表示されます。

   ```
   Image Name                     PID Session Name        Session#    Mem Usage
   ========================= ======== ================ =========== ============
   nlserver.exe                  3192 Console                    1     13,108 K
   ```

1. 数分後に 1 つ以上のAdobe Campaignプロセスがアクティブまたはブロックされたままの場合は、プロセスを強制終了します。 管理者権限でログインし、次のコマンドを実行します。

   ```
   taskkill /IM nlserver* /T
   ```

1. 数分後に一部のプロセスがアクティブなままの場合は、次のコマンドを使用して、プロセスを強制的に閉じることができます。

   ```
   taskkill /F /IM nlserver* /T
   ```

## データベースと現在のインストールのバックアップ {#back-up-the-database-and-the-current-installation}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5.11 からの移行 {#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. のバックアップを作成 **Neolane v5** 次のコマンドを使用するディレクトリ：

   ```
   ren "Neolane v5" "Neolane v5.back"
   ```

   >[!IMPORTANT]
   >
   >予防措置として、 **Neolane v5.back** フォルダーに保存し、サーバー以外の安全な場所に保存します。

1. Windows サービス管理コンソールで、5.11 アプリケーションサーバーサービスの自動起動を無効にします。 また、次のコマンドを使用することもできます。

   ```
   sc config nlserver5 start= disabled
   ```

1. を編集します。 **config-`<instance name>`.xml** ( **Neolane v5. 戻る** ) を使用して、 **mta**, **wfserver**, **stat**&#x200B;など サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart** と **_autoStart**.

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

### Adobe Campaign v6.02 からの移行 {#migrating-from-adobe-campaign-v6-02}

1. Adobe Campaignデータベースのバックアップを作成します。
1. のバックアップを作成 **Neolane v6** 次のコマンドを使用するディレクトリ：

   ```
   ren "Neolane v6" "Neolane v6.back"
   ```

   >[!IMPORTANT]
   >
   >予防措置として、 **Neolane v6.back** フォルダーに保存し、サーバー以外の安全な場所に保存します。

1. Windows サービスマネージャで、 6.02 アプリケーションサーバーの自動起動を無効にします。 また、次のコマンドを使用することもできます。

   ```
   sc config nlserver6 start= disabled
   ```

1. を編集します。 **config-`<instance name>`.xml** ( **Neolane v6. 戻る** ) を使用して、 **mta**, **wfserver**, **stat**&#x200B;など サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart** と **_autoStart**.

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

### Adobe Campaign v6.1 からの移行 {#migrating-from-adobe-campaign-v6-1}

1. Adobe Campaignデータベースのバックアップを作成します。
1. のバックアップを作成 **Adobe Campaign v6** 次のコマンドを使用するディレクトリ：

   ```
   ren "Adobe Campaign v6" "Adobe Campaign v6.back"
   ```

   >[!IMPORTANT]
   >
   >予防措置として、 **Adobe Campaign v6.back** フォルダーに保存し、サーバー以外の安全な場所に保存します。

1. Windows サービス管理コンソールで、6.11 アプリケーションサーバーサービスの自動起動を無効にします。 また、次のコマンドを使用することもできます。

   ```
   sc config nlserver6 start= disabled
   ```

## Adobe Campaign v7 のデプロイ {#deploying-adobe-campaign-v7}

Adobe Campaignのデプロイには、次の 2 つの段階があります。

* ビルド v7 のインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで開始する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. を実行して最新のAdobe Campaign v7 ビルドをインストールする **setup.exe** インストールファイル。 Windows でのAdobe Campaignサーバーのインストールについて詳しくは、 [この節](../../installation/using/installing-the-server.md).

   ![](assets/migration_wizard_1_7.png)

   >[!NOTE]
   >
   >Adobe Campaign v7 は、デフォルトで **C:\Program Files\Adobe\Adobe Campaign v7** ディレクトリ。

1. クライアントコンソールのインストールプログラムを使用可能にするには、 **setup-client-7.0.XXX.exe** ファイルをAdobe Campaignのインストールディレクトリに移動します。 **C:\Program Files\Adobe\Adobe Campaign v7\datakit\nl\eng\jsp**.

   >[!NOTE]
   >
   >Windows でのAdobe Campaignのインストールについて詳しくは、 [この節](../../installation/using/installing-the-server.md).

1. 次のコマンドを使用して、最初の使用用のインスタンスを起動します。

   ```
   net start nlserver6-v7
   net stop nlserver6-v7
   ```

   >[!NOTE]
   >
   >次のコマンドを使用して、Adobe Campaign v7 内部ファイルシステムを作成できます。 **conf** ディレクトリ ( **config-default.xml** および **serverConf.xml** ファイル ) **var** ディレクトリ等

1. を使用して、各インスタンスの設定ファイルとサブフォルダーをコピー&amp;ペースト（上書き）します。 **Neolane v5.back**, **Neolane v6.back** または **Adobe Campaign v6.back** バックアップファイル ( 移行元のバージョンに応じて異なります。詳しくは、 [この節](#back-up-the-database-and-the-current-installation)) をクリックします。
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
   >上記の最初のコマンドでは、 **config-default.xml** ファイル。

1. 内 **serverConf.xml** および **config-default.xml** Adobe Campaign v7 のファイルを使用する場合は、Adobe Campaignの以前のバージョンで使用していた特定の設定を適用します。 の **serverConf.xml** ファイルを使用する場合は、 **Neolane v5/conf/serverConf.xml.diff**, **Neolane v6/conf/serverConf.xml.diff** または **Adobe Campaign v6/conf/serverConf.xml.diff** ファイル。

   >[!NOTE]
   >
   >Adobe Campaignの以前のバージョンからAdobe Campaign v7 に設定をレポートする場合、物理ディレクトリへのパスがAdobe Campaign v7 になることを確認します (Neolane v5、Neolane v6 またはAdobe Campaign v6 にはならない )。

1. 次のコマンドを使用して、Adobe Campaign v7 設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します。

   ```
   nlserver config -postupgrade -instance:<instance name>
   ```

>[!IMPORTANT]
>
>まだAdobe Campaignサービスを開始しない：IIS でいくつかの変更を行う必要があります。

## リダイレクトサーバー (IIS) の移行 {#migrating-the-redirection-server--iis-}

この段階で、IIS サーバーを停止する必要があります。 参照： [サービス停止](#service-stop).

1. を開きます。 **インターネットインフォメーションサービス (IIS) マネージャ** コンソール。
1. Adobe Campaignの以前のバージョンで使用するサイトのバインディング（リッスンポート）を変更します。

   * Adobe Campaignの以前のバージョンで使用したサイトを右クリックし、「 」を選択します。 **[!UICONTROL バインドを編集]**.
   * リスンポートの各タイプ (**[!UICONTROL http]** および/または **[!UICONTROL https]**)、適切な行を選択して、 **[!UICONTROL 編集]**.
   * 別のポートを入力してください。 デフォルトでは、リスンポートは http の場合は 80、https の場合は 443 です。 新しいポートが使用可能であることを確認します。

      ![](assets/_migration_iis_3_611.png)

      >[!NOTE]
      >
      >IIS サーバーに、高度な設定（共有ポートと異なる IP アドレス）を持つAdobe Campaign用の Web サイトが複数含まれている場合は、管理者にお問い合わせください。

1. Adobe Campaign v7 用の新しい Web サイトの作成：

   * を右クリックします。 **[!UICONTROL サイト]** フォルダーと選択 **[!UICONTROL Web サイトの追加…]**.

      ![](assets/_migration_iis_4.png)

   * サイトの名前を入力します。 **Adobe Campaign v7** 例：
   * Web サイトの基本ディレクトリへのアクセスパスは使用されませんが、 **[!UICONTROL 物理アクセスパス]** フィールドに値を入力する必要があります。 デフォルトの IIS アクセスパスを入力： **C:\inetpub\wwwroot**.
   * 次をクリック： **[!UICONTROL 接続名…]** ボタンとして、 **[!UICONTROL アプリケーションユーザー]** 」オプションが選択されている。
   * デフォルト値を **[!UICONTROL IP アドレス]** および **[!UICONTROL ポート]** フィールド。 他の値を使用する場合は、IP アドレスまたはポート（あるいは両方）が使用可能であることを確認します。
   * 次を確認します。 **[!UICONTROL Web サイトをすぐに開始]** ボックス

      ![](assets/_migration_iis_5_7.png)

1. を実行します。 **iis_neolane_setup.vbs** 先ほど作成した仮想ディレクトリ上のAdobe Campaignサーバーで使用されるリソースを自動的に設定するスクリプト。

   * このファイルは、 **`[Adobe Campaign v7]`\conf** ディレクトリ。ここで、 **`[Adobe Campaign v7]`** は、Adobe Campaignインストールディレクトリへのアクセスパスです。 スクリプトを実行するコマンドは、次のとおりです（管理者向け）。

      ```
      cd C:\Program Files (x86)\Adobe Campaign\Adobe Campaign v7\conf
      cscript iis_neolane_setup.vbs
      ```

   * クリック **[!UICONTROL OK]** スクリプトの実行を確定します。

      ![](assets/s_ncs_install_iis7_parameters_step2_7.png)

   * Adobe Campaign v7 用に以前に作成した Web サイトの番号を入力し、 **[!UICONTROL OK]**.

      ![](assets/s_ncs_install_iis7_parameters_step3_7.png)

   * 次の確認メッセージが表示されます。

      ![](assets/s_ncs_install_iis7_parameters_step7_7.png)

   * 内 **[!UICONTROL コンテンツ表示]** 「 」タブで、Web サイトの設定がAdobe Campaignのリソースで正しく設定されていることを確認します。

      ![](assets/s_ncs_install_iis7_parameters_step6_7.png)

      >[!NOTE]
      >
      >ツリー構造が表示されない場合は、IIS を再起動します。
      >
      >次の IIS 設定手順について詳しくは、 [この節](../../installation/using/integration-into-a-web-server-for-windows.md#configuring-the-iis-web-server).

## セキュリティゾーン {#security-zones}

v6.02 以前から移行する場合は、サービスを開始する前にセキュリティゾーンを設定する必要があります。 詳しくは、 [セキュリティ](../../migration/using/general-configurations.md#security).

## サービスの再起動 {#re-starting-the-services}

次の各サーバーで IIS とAdobe Campaignサービスを起動します。

1. トラッキングおよびリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、不具合がなく、 [一般設定](../../migration/using/general-configurations.md) 」セクションに入力します。

## 以前のバージョンのAdobe Campaignの削除とクレンジング {#deleting-and-cleansing-adobe-campaign-previous-version}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5 {#adobe-campaign-v5}

Adobe Campaign v5 のインストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールの完全なチェックを実行してもらう。
* ロールバックが必要ないことが確実な場合にのみ、Adobe Campaign v5 をアンインストールします。

1. IIS で、 **Neolane v5** Web サイト、 **Neolane v5** アプリケーションプール。
1. 名前を変更 **Neolane v5.back** フォルダー名 **Neolane v5**.
1. コンポーネントの追加と削除ウィザードを使用してAdobe Campaign v5 をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. を削除します。 **nlserver5** 次のコマンドを使用する Windows サービス：

   ```
   sc delete nlserver5
   ```

1. サーバーを再起動します。

### Adobe Campaign v6.02 {#adobe-campaign-v6-02}

Adobe Campaign v6.02 のインストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールの完全なチェックを実行してもらう。
* ロールバックが必要ないことが確実な場合にのみ、Adobe Campaign v6.02 をアンインストールします。

1. IIS で、 **Neolane v6** Web サイト、 **Neolane v6** アプリケーションプール。
1. 名前を変更 **Neolane v6.back** フォルダー名 **Neolane v6**.
1. コンポーネントの追加と削除ウィザードを使用してAdobe Campaign v6.02 をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. サーバーを再起動します。

### Adobe Campaign v6.1 {#adobe-campaign-v6-1}

Adobe Campaign v6 のインストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールの完全なチェックを実行してもらう。
* ロールバックが必要ないことが確実な場合にのみ、Adobe Campaign v6 をアンインストールします。

1. IIS で、 **Adobe Campaign v6** Web サイト、 **Adobe Campaign v6** アプリケーションプール。
1. 名前を変更 **Adobe Campaign v6.back** フォルダー名 **Adobe Campaign v6**.
1. コンポーネントの追加と削除ウィザードを使用してAdobe Campaign v6 をアンインストールします。

   ![](assets/migration_wizard_2.png)

1. サーバーを再起動します。
