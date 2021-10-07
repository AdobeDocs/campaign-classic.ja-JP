---
product: campaign
title: Linux での Adobe Campaign 7 への移行
description: Linux での Adobe Campaign 7 への移行
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
exl-id: 9dc0699c-0fbf-4f8e-81f7-8ca3d7e98798
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1890'
ht-degree: 1%

---

# Linux での Adobe Campaign 7 への移行{#migrating-in-linux-for-adobe-campaign-v}

![](../../assets/v7-only.svg)

## 一般的な手順 {#general-procedure}

Linux での移行手順は次のとおりです。

1. サービスの停止：[ サービス停止 ](#service-stop) を参照してください。
1. データベースを保存します。[ データベースと既存のインストールのバックアップ ](#back-up-the-database-and-the-existing-installation) を参照してください。
1. 以前のAdobe Campaignバージョンのパッケージをアンインストールします。[ 以前のバージョンのAdobe Campaignパッケージのアンインストール ](#uninstalling-adobe-campaign-previous-version-packages) を参照してください。
1. プラットフォームの移行：[Adobe Campaign v7 のデプロイ ](#deploying-adobe-campaign-v7) を参照してください。
1. サービスの再起動：[ サービスの再起動 ](#re-starting-services) を参照してください。

## サービス停止 {#service-stop}

まず、関係するすべてのマシン上のデータベースにアクセスできるすべてのプロセスを停止します。

1. **root** としてログインします。
1. リダイレクトモジュール（**webmdl** サービス）を使用するすべてのサーバーを停止する必要があります。 Apache の場合は、次のコマンドを実行します。

   ```
   /etc/init.d/apache2 stop
   ```

1. **root** として再度ログインします。
1. すべてのサーバーでAdobe Campaign以前のバージョンのサービスを停止します。

   ```
   /etc/init.d/nlserver6 stop
   ```

   バージョン 5.11 から移行する場合は、次のコマンドを実行します。

   ```
   /etc/init.d/nlserver5 stop
   ```

1. 各サーバーでAdobe Campaignサービスが停止していることを確認します。

   ```
   ps waux | grep nlserver
   ```

   アクティブなプロセスのリストと ID(PID) が表示されます。

1. 数分後も 1 つ以上のAdobe Campaignプロセスがアクティブまたはブロックされている場合は、それらを強制終了します。

   ```
   killall nlserver
   ```

1. 数分後もアクティブなプロセスがある場合は、次のコマンドを使用して、プロセスを強制的に閉じることができます。

   ```
   killall -9 nlserver
   ```

## データベースと既存のインストールのバックアップ {#back-up-the-database-and-the-existing-installation}

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5.11 からの移行 {#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. **neolane** としてログインし、次のコマンドを使用して **nl5** ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl5 nl5.back
   ```

   >[!IMPORTANT]
   >
   >予防策として、**nl5.back** フォルダーを zip ファイルにして、サーバー以外の安全な場所に保存することをお勧めします。

1. **config-`<instance name>`.xml** （**nl5.back** フォルダー内）を編集し、**mta**、**wfserver**、**stat** などを防ぎます。 サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart** を **_autoStart** に置き換えます（**neolane** と同じ）。

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
1. **neolane** としてログインし、次のコマンドを使用して **nl6** ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防策として、**nl6.back** フォルダーを zip ファイルにして、サーバー以外の安全な場所に保存することをお勧めします。

1. **config-`<instance name>`.xml** （**nl6.back** フォルダー内）を編集して、**mta**、**wfserver**、**stat** などを防ぎます。 サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart** を **_autoStart** に置き換えます (**Adobe Campaign** と同じ )。

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

### Adobe Campaign v6.1 からの移行 {#migrating-from-adobe-campaign-v6-1}

1. Adobe Campaignデータベースのバックアップを作成します。
1. **neolane** としてログインし、次のコマンドを使用して **nl6** ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防策として、**nl6.back** フォルダーを zip ファイルにして、サーバー以外の安全な場所に保存することをお勧めします。

## 以前のバージョンのAdobe Campaignパッケージのアンインストール {#uninstalling-adobe-campaign-previous-version-packages}

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5 パッケージのアンインストール {#uninstalling-adobe-campaign-v5-packages}

1. **root** としてログインします。
1. 次のコマンドを使用して、インストールされたAdobe Campaignパッケージを特定します。

   * **Debian** では、

      ```
      dpkg -l | grep nl
      ```

      インストールされているパッケージのリストが表示されます。

      ```
      ii  nlserver5                       5762                     nlserver5-5762
      ii  nlthirdparty5                   5660                     nlthirdparty5-5660
      ```

   * **Red Hat**:

      ```
      rpm -qa | grep nl
      ```

1. Adobe Campaign v5 パッケージをアンインストールします。

   * **Debian** では、

      ```
      dpkg --purge nlserver5 nlthirdparty5
      ```

   * **Red Hat**:

      ```
      rprm -ev nlserver5 nlthirdparty5
      ```

### Adobe Campaign v6 パッケージのアンインストール {#uninstalling-adobe-campaign-v6-packages}

この節では、Adobe Campaign v6.02 または v6.1 パッケージのアンインストール方法を示します。

1. **root** としてログインします。
1. 次のコマンドを使用して、インストールされたAdobe Campaignパッケージを特定します。

   * **Debian** では、

      ```
      dpkg -l | grep nl
      ```

      インストールされているパッケージのリストが表示されます。

      ```
      ii  nlserver6                       XXXX                     nlserver6-XXXX
      ii  nlthirdparty6                   XXXX                     nlthirdparty6-XXXX
      ```

   * **Red Hat**:

      ```
      rpm -qa | grep nl
      ```

1. Adobe Campaign v6 パッケージをアンインストールします。

   * **Debian** では、

      ```
      dpkg --purge nlserver6 nlthirdparty6
      ```

   * **Red Hat**:

      ```
      rprm -ev nlserver6 nlthirdparty6
      ```

## Adobe Campaign v7 のデプロイ {#deploying-adobe-campaign-v7}

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5.11 からの移行 {#migrating-from-adobe-campaign-v5_11-1}

Adobe Campaignのデプロイには、次の 2 つの段階があります。

* Adobe Campaign v7 パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで開始する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. 次のコマンドを使用して、最新のAdobe Campaign v7 パッケージをインストールします。

   * **Debian** では、

      ```
      dpkg -i nlserver6-XXXX-linux-2.6-intel.deb
      ```

   * **Red Hat**:

      ```
      rpm -Uvh nlserver6-XXXX-0.x86_64.rpm
      ```
   >[!IMPORTANT]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >v5.11 から移行する場合、Adobe Campaignはデフォルトで **/usr/local/neolane/nl6/** ディレクトリにインストールされます。
   >
   >パッケージがインストールされると、次のメッセージが表示されます。**&#39;WdbcTimeZone&#39;オプションがありません**。 これは正常です。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順でAdobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >Linux でのAdobe Campaignのインストール方法について詳しくは、[ この節 ](../../installation/using/installing-campaign-standard-packages.md) を参照してください。

1. **neolane** ユーザーと一致する **.bashrd** ファイルを変更します。 **neolane** としてログオンし、次のコマンドを実行します。

   ```
   su - neolane
   vim ~/.bashrc
   ```

   >[!NOTE]
   >
   >**neolane** としてログインすると、次のメッセージが表示されます。**nl5/env.sh :そのようなファイルやディレクトリはありません**。 これは正常です。

   ファイルの最後で、 **nl5/env.sh** を **nl6/env.sh** に置き換えます。

1. **root** としてログインし、次のコマンドを使用してインスタンスを準備します。

   ```
   /etc/init.d/nlserver6 start   
   Starting nlserver6: [  OK  ]
   ```

   ```
   /etc/init.d/nlserver6 stop
   Stopping nlserver6: [  OK  ]
   ```

   >[!NOTE]
   >
   >次のコマンドを使用して、Adobe Campaign v6 の内部ファイルシステムを作成できます。**conf** ディレクトリ（**config-default.xml** および **serverConf.xml** ファイルを含む）、**var** ディレクトリ。

1. **nl5.back** バックアップフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 **neolane** としてログインし、次のコマンドを実行します。

   >[!IMPORTANT]
   >
   >以下の最初のコマンドの場合は、**config-default.xml** ファイルをコピーしないでください。

   ```
   su - neolane
   
   cp nl5.back/conf/config-<instance name>.xml nl6/conf/
   cp nl5.back/customer.sh nl6/
   cp -r nl5.back/customers/* nl6/customers/
   cp -r nl5.back/var/* nl6/var/
   ```

1. Adobe Campaign v7 の **serverConf.xml** および **config-default.xml** ファイルで、Adobe Campaign v5 に対して行った特定の設定を適用します。 **serverConf.xml** ファイルの場合は、**nl5/conf/serverConf.xml.diff** ファイルを使用します。

   >[!NOTE]
   >
   >Adobe Campaign v5 からAdobe Campaign v7 に設定をレポートする場合は、物理ディレクトリへのパスがAdobe Campaign v5 ではなくAdobe Campaign v7 に続くことを確認してください。

1. 移行は一般的なインストールではないので、**trackinglogd** サービスを強制的に再起動する必要があります。 これをおこなうには、**nl6/conf/config-default.xml** ファイルを開き、**trackinglogd** サービスが有効になっていることを確認します（トラッキング/リダイレクトサーバー上でのみ）。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >**trackinglogd** サービスがトラッキングサーバーで開始されていない場合、トラッキング情報は転送されません。

1. 次のコマンドを使用して、Adobe Campaign v7 設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します（**neolane** という名前で）。

   ```
   su - neolane
   nlserver config -timezone:<time zone> -postupgrade -instance:<instance name>
   ```

   >[!IMPORTANT]
   >
   >アップグレード後に（**-timezone** オプションを使用して）参照として使用するタイムゾーンを指定する必要があります。 この場合、Europe/Paris タイムゾーン **-timezone を使用します。&quot;Europe/Paris&quot;**。

   >[!NOTE]
   >
   >ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションについて詳しくは、[ タイムゾーン ](../../migration/using/general-configurations.md#time-zones) の節を参照してください。

>[!IMPORTANT]
>
>まだAdobe Campaignサービスを開始しない：変更は、引き続き Apache でおこなう必要があります。

### Adobe Campaign v6.02 からの移行 {#migrating-from-adobe-campaign-v6_02-1}

Adobe Campaignのデプロイには、次の 2 つの段階があります。

* Adobe Campaign v7 パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで開始する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. 次のコマンドを使用して、最新のAdobe Campaign v7 パッケージをインストールします。

   * **Debian** では、

      ```
      dpkg -i nlserver6-XXXX-amd64_debX.deb
      ```

   * **Red Hat**:

      ```
      rpm -Uvh nlserver6-XXXX-x86_64_rhX.rpm
      ```
   >[!IMPORTANT]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >Adobe Campaign v7 は、デフォルトでAdobe Campaign v6.02 と同じディレクトリにインストールされます。**/usr/local/neolane/nl6/**.

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順でAdobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >Linux でのAdobe Campaignのインストール方法について詳しくは、[ この節 ](../../installation/using/installing-campaign-standard-packages.md) を参照してください。

1. 移行は一般的なインストールではないので、**trackinglogd** サービスを強制的に再起動する必要があります。 これをおこなうには、**nl6/conf/config-default.xml** ファイルを開き、**trackinglogd** サービスが有効になっていることを確認します（トラッキング/リダイレクトサーバー上でのみ）。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >**trackinglogd** サービスがトラッキングサーバーで開始されていない場合、トラッキング情報は転送されません。

1. **nl6.back** バックアップフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 **neolane** としてログインし、次のコマンドを実行します。

   ```
   su - neolane
   
   cp nl6.back/conf/config*.xml nl6/conf/
   cp nl6.back/customer.sh nl6/
   cp -r nl6.back/customers/* nl6/customers/
   cp -r nl6.back/var/* nl6/var/
   ```

1. 次のコマンドを使用して、Adobe Campaign v7 設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します（**neolane** という名前で）。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

   >[!NOTE]
   >
   >「マルチタイムゾーン」モードは、PostgreSQL データベースエンジンの v6.02 でのみ使用できました。 どのバージョンのデータベースエンジンを使用していても使用できるようになりました。 ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションについて詳しくは、[ タイムゾーン ](../../migration/using/general-configurations.md#time-zones) の節を参照してください。

### Adobe Campaign v6.1 からの移行 {#migrating-from-adobe-campaign-v6_1-1}

Adobe Campaignのデプロイには、次の 2 つの段階があります。

* Adobe Campaign v7 パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで開始する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. 次のコマンドを使用して、最新のAdobe Campaign v7 パッケージをインストールします。

   * **Debian** では、

      ```
      dpkg -i nlserver6-XXXX-amd64_debX.deb
      ```

   * **Red Hat**:

      ```
      rpm -Uvh nlserver6-XXXX-x86_64_rhX.rpm
      ```
   >[!IMPORTANT]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >Adobe Campaign v7 は、デフォルトで **/usr/local/neolane/nl6/** ディレクトリにインストールされます。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順でAdobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >Linux でのAdobe Campaignのインストール方法について詳しくは、[ この節 ](../../installation/using/installing-campaign-standard-packages.md) を参照してください。

1. **nl6.back** バックアップフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 **neolane** としてログインし、次のコマンドを実行します。

   ```
   su - neolane
   
   cp nl6.back/conf/config*.xml nl6/conf/
   cp nl6.back/customer.sh nl6/
   cp -r nl6.back/customers/* nl6/customers/
   cp -r nl6.back/var/* nl6/var/
   ```

1. 次のコマンドを使用して、Adobe Campaign v7 設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します（**neolane** という名前で）。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

## リダイレクトサーバーの移行 (Apache) {#migrating-the-redirection-server--apache-}

>[!NOTE]
>
>この節の説明は、Adobe Campaign v5.11 からの移行時にのみ当てはまります。

この段階で、Apache を停止する必要があります。 次を参照してください。[ サービス停止 ](#service-stop)。

1. **root** としてログインします。
1. Apache 環境変数を変更して、**nl6** ディレクトリにリンクします。

   * **Debian** では、

      ```
      vi /etc/apache2/envvars
      ```

   * **Red Hat**:

      ```
      vi /usr/local/apache2/bin/envvars
      ```

1. 次に、次のコマンドを実行します。

   * **Debian** では、

      **nlsrv.load** ファイルで、**nl5** を **nl6** に置き換えます。

      ```
      vi /etc/apache2/mods-available/nlsrv.load
      ```

      **nlsrv.conf** ファイルのリンクを削除し、新しく作成します。

      ```
      rm /etc/apache2/mods-available/nlsrv.conf 
      ln -s /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf /etc/apache2/
      mods-available/nlsrv.conf
      ```

   * **Red Hat**:

      **/usr/local/apache2/conf** ディレクトリに移動し、**http.conf** ファイルを編集して、次の行で **nl5** を **nl6** に置き換えます。

      **RHEL 7/Debian 8**:

      ```
      LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
      Include /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf
      ```

1. **alias.conf** ファイルに移動し、すべての **nl5** を **nl6** に置き換えます。 Debian でこれをおこなうには、次のコマンドを実行します。

   ```
   vi /etc/apache2/mods-available/alias.conf
   ```

## セキュリティゾーン {#security-zones}

v6.02 以前から移行する場合は、サービスを開始する前にセキュリティゾーンを設定する必要があります。 詳しくは、[ セキュリティ ](../../migration/using/general-configurations.md#security) を参照してください。

## サービスの再起動 {#re-starting-services}

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5.11 からの移行 {#migrating-from-adobe-campaign-v5_11-2}

**config-`<instance name>`.xml** ファイルで、**mta**、**wfserver**、**stat** などの自動起動を再開します。 サービス

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

  <mta autoStart="true" statServerAddress="localhost"/>
  <stat autoStart="true"/>
  <wfserver autoStart="true"/>
  <inMail autoStart="true"/>
  <sms autoStart="false"/>
</serverconf>
```

次の各サーバーで Apache とAdobe Campaignのサービスを開始します。

1. 追跡サーバーとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、不具合がなく、[ 一般設定 ](../../migration/using/general-configurations.md) セクションの推奨事項に従ってすべての動作を確認します。

### Adobe Campaign v6.02 からの移行 {#migrating-from-adobe-campaign-v6_02-2}

**config-`<instance name>`.xml** ファイルで、**mta**、**wfserver**、**stat** などの自動起動を再開します。 サービス

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

  <mta autoStart="true" statServerAddress="myStatServer"/>
  <stat autoStart="true"/>
  <wfserver autoStart="true"/>
  <inMail autoStart="true"/>
  <sms autoStart="false"/>
</serverconf>
```

次の各サーバーで Apache とAdobe Campaignのサービスを開始します。

1. 追跡サーバーとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

新しいインストールを完全にテストし、リグレスしていないことを確認し、[ 一般設定 ](../../migration/using/general-configurations.md) の節の推奨事項に従って、すべてが正しく動作していることを確認します。

### Adobe Campaign v6.1 からの移行 {#migrating-from-adobe-campaign-v6_1-2}

次の各サーバーで Apache とAdobe Campaignのサービスを開始します。

1. 追跡サーバーとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

新しいインストールを完全にテストし、リグレスしていないことを確認し、[ 一般設定 ](../../migration/using/general-configurations.md) の節の推奨事項に従って、すべてが正しく動作していることを確認します。

## Adobe Campaign v5 の削除とクレンジング {#deleting-and-cleansing-adobe-campaign-v5}

>[!NOTE]
>
>この節の説明は、Adobe Campaign v5.11 からの移行時にのみ当てはまります。

Adobe Campaign v5 のインストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールの完全なチェックを実行してもらう。
* ロールバックが必要ないことが確実である場合は、Adobe Campaign v5 をアンインストールしてください。

**nl5.back** ディレクトリを削除します。 **neolane** としてログインし、次のコマンドを実行します。

```
su - neolane
rm -rf nl5.back
```

サーバーを再起動します。
