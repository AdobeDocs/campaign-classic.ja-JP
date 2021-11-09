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

1. サービスを停止：参照 [サービス停止](#service-stop).
1. データベースを保存します。参照 [データベースと既存のインストールのバックアップ](#back-up-the-database-and-the-existing-installation).
1. 以前のAdobe Campaignバージョンのパッケージをアンインストールします。参照 [Adobe Campaign以前のバージョンパッケージのアンインストール](#uninstalling-adobe-campaign-previous-version-packages).
1. プラットフォームの移行：参照する [Adobe Campaign v7 のデプロイ](#deploying-adobe-campaign-v7).
1. サービスを再開します。参照する [サービスの再起動](#re-starting-services).

## サービス停止 {#service-stop}

まず、関係するすべてのマシン上のデータベースにアクセスしているすべてのプロセスを停止します。

1. ログイン名 **root**.
1. リダイレクトモジュールを使用するすべてのサーバー (**webmdl** サービス ) を停止する必要があります。 Apache の場合は、次のコマンドを実行します。

   ```
   /etc/init.d/apache2 stop
   ```

1. 再度ログイン **root**.
1. すべてのサーバーでAdobe Campaignの以前のバージョンのサービスを停止します。

   ```
   /etc/init.d/nlserver6 stop
   ```

   v5.11 から移行する場合は、次のコマンドを実行します。

   ```
   /etc/init.d/nlserver5 stop
   ```

1. 各サーバーでAdobe Campaignサービスが停止していることを確認します。

   ```
   ps waux | grep nlserver
   ```

   アクティブなプロセスのリストとその ID(PID) が表示されます。

1. 数分後に 1 つ以上のAdobe Campaignプロセスがアクティブまたはブロックされたままの場合は、プロセスを強制終了します。

   ```
   killall nlserver
   ```

1. 数分後に一部のプロセスがアクティブなままの場合は、次のコマンドを使用して、プロセスを強制的に閉じることができます。

   ```
   killall -9 nlserver
   ```

## データベースと既存のインストールのバックアップ {#back-up-the-database-and-the-existing-installation}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5.11 からの移行 {#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. ログイン名 **ネオラン** そして、 **nl5** 次のコマンドを使用するディレクトリ：

   ```
   su - neolane
   mv nl5 nl5.back
   ```

   >[!IMPORTANT]
   >
   >予防措置として、 **nl5.back** フォルダーに保存し、サーバー以外の安全な場所に保存します。

1. を編集します。 **config-`<instance name>`.xml** ( **nl5.back** フォルダ )、 **mta**, **wfserver**, **stat** など サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart** と **_autoStart** ( **ネオラン**) をクリックします。

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
1. ログイン名 **ネオラン** そして、 **nl6** 次のコマンドを使用するディレクトリ：

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防措置として、 **nl6.back** フォルダーに保存し、サーバー以外の安全な場所に保存します。

1. を編集します。 **config-`<instance name>`.xml** ( **nl6.back** ) を使用して、 **mta**, **wfserver**, **stat**&#x200B;など サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart** と **_autoStart** ( **Adobe Campaign**) をクリックします。

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
1. ログイン名 **ネオラン** そして、 **nl6** 次のコマンドを使用するディレクトリ：

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防措置として、 **nl6.back** フォルダーに保存し、サーバー以外の安全な場所に保存します。

## Adobe Campaign以前のバージョンパッケージのアンインストール {#uninstalling-adobe-campaign-previous-version-packages}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5 パッケージのアンインストール {#uninstalling-adobe-campaign-v5-packages}

1. ログイン名 **root**.
1. 次のコマンドを使用して、インストールされているAdobe Campaignパッケージを特定します。

   * In **Debian**:

      ```
      dpkg -l | grep nl
      ```

      インストールされているパッケージの一覧が表示されます。

      ```
      ii  nlserver5                       5762                     nlserver5-5762
      ii  nlthirdparty5                   5660                     nlthirdparty5-5660
      ```

   * In **Red Hat**:

      ```
      rpm -qa | grep nl
      ```

1. Adobe Campaign v5 パッケージをアンインストールします。

   * In **Debian**:

      ```
      dpkg --purge nlserver5 nlthirdparty5
      ```

   * In **Red Hat**:

      ```
      rprm -ev nlserver5 nlthirdparty5
      ```

### Adobe Campaign v6 パッケージのアンインストール {#uninstalling-adobe-campaign-v6-packages}

この節では、Adobe Campaign v6.02 または v6.1 パッケージのアンインストール方法を示します。

1. ログイン名 **root**.
1. 次のコマンドを使用して、インストールされているAdobe Campaignパッケージを特定します。

   * In **Debian**:

      ```
      dpkg -l | grep nl
      ```

      インストールされているパッケージの一覧が表示されます。

      ```
      ii  nlserver6                       XXXX                     nlserver6-XXXX
      ii  nlthirdparty6                   XXXX                     nlthirdparty6-XXXX
      ```

   * In **Red Hat**:

      ```
      rpm -qa | grep nl
      ```

1. Adobe Campaign v6 パッケージをアンインストールします。

   * In **Debian**:

      ```
      dpkg --purge nlserver6 nlthirdparty6
      ```

   * In **Red Hat**:

      ```
      rprm -ev nlserver6 nlthirdparty6
      ```

## Adobe Campaign v7 のデプロイ {#deploying-adobe-campaign-v7}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5.11 からの移行 {#migrating-from-adobe-campaign-v5_11-1}

Adobe Campaignのデプロイには、次の 2 つの段階があります。

* Adobe Campaign v7 パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで開始する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. 次のコマンドを使用して、最新のAdobe Campaign v7 パッケージをインストールします。

   * In **Debian**:

      ```
      dpkg -i nlserver6-XXXX-linux-2.6-intel.deb
      ```

   * In **Red Hat**:

      ```
      rpm -Uvh nlserver6-XXXX-0.x86_64.rpm
      ```
   >[!IMPORTANT]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >v5.11 から移行する際、Adobe Campaignは **/usr/local/neolane/nl6/** デフォルトではディレクトリです。
   >
   >パッケージがインストールされると、次のメッセージが表示されます。 **「WdbcTimeZone」オプションがありません**. これは正常です。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順で、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >Linux でのAdobe Campaignのインストール方法について詳しくは、 [この節](../../installation/using/installing-campaign-standard-packages.md).

1. を変更します。 **.bashrd** ファイル **ネオラン** ユーザー。 ログオン名 **ネオラン** 次のコマンドを実行します。

   ```
   su - neolane
   vim ~/.bashrc
   ```

   >[!NOTE]
   >
   >ログイン時に **ネオラン**&#x200B;に設定すると、次のメッセージが表示されます。 **nl5/env.sh :そのようなファイルまたはディレクトリはありません**. これは正常です。

   ファイルの最後で、 **nl5/env.sh** と **nl6/env.sh**.

1. ログイン名 **root** 次のコマンドを使用して、インスタンスを準備します。

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
   >次のコマンドを使用して、Adobe Campaign v6 内部ファイルシステムを作成できます。 **conf** ディレクトリ ( **config-default.xml** および **serverConf.xml** ファイル ) **var** ディレクトリ。

1. 次に移動： **nl5.back** バックアップフォルダーを作成し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 ログイン名 **ネオラン** 次のコマンドを実行します。

   >[!IMPORTANT]
   >
   >以下の最初のコマンドでは、 **config-default.xml** ファイル。

   ```
   su - neolane
   
   cp nl5.back/conf/config-<instance name>.xml nl6/conf/
   cp nl5.back/customer.sh nl6/
   cp -r nl5.back/customers/* nl6/customers/
   cp -r nl5.back/var/* nl6/var/
   ```

1. Adobe Campaign v7 **serverConf.xml** および **config-default.xml** ファイルを使用する場合は、Adobe Campaign v5 に対して行った特定の設定を適用します。 の **serverConf.xml** ファイルを使用する場合は、 **nl5/conf/serverConf.xml.diff** ファイル。

   >[!NOTE]
   >
   >Adobe Campaign v5 からAdobe Campaign v7 への設定をレポートする場合、物理ディレクトリへのパスがAdobe Campaign v5 にはならず、Adobe Campaign v7 に続くことを確認します。

1. 移行は一般的なインストールではないので、 **trackinglogd** サービス。 これをおこなうには、 **nl6/conf/config-default.xml** ファイルを作成し、 **trackinglogd** サービスが有効化されている（トラッキング/リダイレクトサーバー上のみ）:

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >この **trackinglogd** サービスがトラッキングサーバーで開始されていないので、トラッキング情報は転送されません。

1. 次のコマンドを使用して、Adobe Campaign v7 設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します ( **ネオラン**):

   ```
   su - neolane
   nlserver config -timezone:<time zone> -postupgrade -instance:<instance name>
   ```

   >[!IMPORTANT]
   >
   >アップグレード後に ( **-timezone** オプション )。 この場合、ヨーロッパ/パリタイムゾーンを使用しています **-timezone:&quot;ヨーロッパ/パリ&quot;**.

   >[!NOTE]
   >
   >ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションについて詳しくは、 [タイムゾーン](../../migration/using/general-configurations.md#time-zones) 」セクションに入力します。

>[!IMPORTANT]
>
>まだAdobe Campaignサービスを開始しない：変更は Apache で行う必要があります。

### Adobe Campaign v6.02 からの移行 {#migrating-from-adobe-campaign-v6_02-1}

Adobe Campaignのデプロイには、次の 2 つの段階があります。

* Adobe Campaign v7 パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで開始する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. 次のコマンドを使用して、最新のAdobe Campaign v7 パッケージをインストールします。

   * In **Debian**:

      ```
      dpkg -i nlserver6-XXXX-amd64_debX.deb
      ```

   * In **Red Hat**:

      ```
      rpm -Uvh nlserver6-XXXX-x86_64_rhX.rpm
      ```
   >[!IMPORTANT]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >Adobe Campaign v7 は、デフォルトでAdobe Campaign v6.02 と同じディレクトリにインストールされます。 **/usr/local/neolane/nl6/**.

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順で、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >Linux でのAdobe Campaignのインストール方法について詳しくは、 [この節](../../installation/using/installing-campaign-standard-packages.md).

1. 移行は一般的なインストールではないので、 **trackinglogd** サービス。 これをおこなうには、 **nl6/conf/config-default.xml** ファイルを作成し、 **trackinglogd** サービスが有効化されている（トラッキング/リダイレクトサーバー上のみ）:

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >この **trackinglogd** サービスがトラッキングサーバーで開始されていないので、トラッキング情報は転送されません。

1. 次に移動： **nl6.back** バックアップフォルダーを作成し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 ログイン名 **ネオラン** 次のコマンドを実行します。

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

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します ( **ネオラン**):

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

   >[!NOTE]
   >
   >「マルチタイムゾーン」モードは、PostgreSQL データベースエンジンの v6.02 でのみ使用可能でした。 どのバージョンのデータベースエンジンが使用されていても使用できるようになりました。 ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションについて詳しくは、 [タイムゾーン](../../migration/using/general-configurations.md#time-zones) 」セクションに入力します。

### Adobe Campaign v6.1 からの移行 {#migrating-from-adobe-campaign-v6_1-1}

Adobe Campaignのデプロイには、次の 2 つの段階があります。

* Adobe Campaign v7 パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで開始する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. 次のコマンドを使用して、最新のAdobe Campaign v7 パッケージをインストールします。

   * In **Debian**:

      ```
      dpkg -i nlserver6-XXXX-amd64_debX.deb
      ```

   * In **Red Hat**:

      ```
      rpm -Uvh nlserver6-XXXX-x86_64_rhX.rpm
      ```
   >[!IMPORTANT]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >Adobe Campaign v7 が **/usr/local/neolane/nl6/** デフォルトではディレクトリです。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順で、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >Linux でのAdobe Campaignのインストール方法について詳しくは、 [この節](../../installation/using/installing-campaign-standard-packages.md).

1. 次に移動： **nl6.back** バックアップフォルダーを作成し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 ログイン名 **ネオラン** 次のコマンドを実行します。

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

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します ( **ネオラン**):

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

## リダイレクトサーバー (Apache) の移行 {#migrating-the-redirection-server--apache-}

>[!NOTE]
>
>この節の説明は、Adobe Campaign v5.11 からの移行時にのみ当てはまります。

この段階で、Apache を停止する必要があります。 次を参照してください。 [サービス停止](#service-stop).

1. ログイン名 **root**.
1. Apache 環境変数を変更して、 **nl6** ディレクトリ。

   * In **Debian**:

      ```
      vi /etc/apache2/envvars
      ```

   * In **Red Hat**:

      ```
      vi /usr/local/apache2/bin/envvars
      ```

1. 次のコマンドを実行します。

   * In **Debian**:

      内 **nlsrv.load** ファイル、置換 **nl5** と **nl6**.

      ```
      vi /etc/apache2/mods-available/nlsrv.load
      ```

      リンクの削除 **nlsrv.conf** ファイルを作成し、新しいファイルを作成します。

      ```
      rm /etc/apache2/mods-available/nlsrv.conf 
      ln -s /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf /etc/apache2/
      mods-available/nlsrv.conf
      ```

   * In **Red Hat**:

      次に移動： **/usr/local/apache2/conf** ディレクトリ、 **http.conf** ファイルと置換 **nl5** と **nl6** を次の行に示します。

      In **RHEL 7/Debian 8**:

      ```
      LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
      Include /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf
      ```

1. 次に移動： **alias.conf** ファイルとすべてを置換 **nl5** と **nl6**. これを Debian でおこなうには、次のコマンドを実行します。

   ```
   vi /etc/apache2/mods-available/alias.conf
   ```

## セキュリティゾーン {#security-zones}

v6.02 以前から移行する場合は、サービスを開始する前にセキュリティゾーンを設定する必要があります。 詳しくは、 [セキュリティ](../../migration/using/general-configurations.md#security).

## サービスの再起動 {#re-starting-services}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5.11 からの移行 {#migrating-from-adobe-campaign-v5_11-2}

内 **config-`<instance name>`.xml** ファイル，自動起動の再開 **mta**, **wfserver**, **stat**&#x200B;など サービス。

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

1. トラッキングおよびリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、不具合がなく、 [一般設定](../../migration/using/general-configurations.md) 」セクションに入力します。

### Adobe Campaign v6.02 からの移行 {#migrating-from-adobe-campaign-v6_02-2}

内 **config-`<instance name>`.xml** ファイル，自動起動の再開 **mta**, **wfserver**, **stat**&#x200B;など サービス。

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

1. トラッキングおよびリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

新しいインストールを完全にテストし、再処理されないことを確認し、 [一般設定](../../migration/using/general-configurations.md) 」セクションに入力します。

### Adobe Campaign v6.1 からの移行 {#migrating-from-adobe-campaign-v6_1-2}

次の各サーバーで Apache とAdobe Campaignのサービスを開始します。

1. トラッキングおよびリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

新しいインストールを完全にテストし、再処理されないことを確認し、 [一般設定](../../migration/using/general-configurations.md) 」セクションに入力します。

## Adobe Campaign v5 の削除とクレンジング {#deleting-and-cleansing-adobe-campaign-v5}

>[!NOTE]
>
>この節の説明は、Adobe Campaign v5.11 からの移行時にのみ当てはまります。

Adobe Campaign v5 のインストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールの完全なチェックを実行してもらう。
* ロールバックが必要ないことが確実な場合にのみ、Adobe Campaign v5 をアンインストールします。

を削除します。 **nl5.back** ディレクトリ。 ログイン名 **ネオラン** 次のコマンドを実行します。

```
su - neolane
rm -rf nl5.back
```

サーバーを再起動します。
