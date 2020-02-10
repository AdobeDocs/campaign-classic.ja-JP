---
title: LinuxでのAdobe Campaign v7への移行
seo-title: LinuxでのAdobe Campaign v7への移行
description: LinuxでのAdobe Campaign v7への移行
seo-description: null
page-status-flag: never-activated
uuid: 47870ea4-b07b-4db7-8094-7a8b6f4b6936
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
discoiquuid: 8f6519e8-5c8d-4974-b193-a9f1cf78b3a3
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# LinuxでのAdobe Campaign v7への移行{#migrating-in-linux-for-adobe-campaign-v}

## 一般的な手順 {#general-procedure}

Linuxでの移行手順は次のとおりです。

1. サービスの停止：「サー [ビス停止](#service-stop)、
1. データベースの保存：詳しく [は、データベースと既存のインストールのバックアップ](#back-up-the-database-and-the-existing-installation)、
1. 以前のAdobe Campaignバージョンパッケージのアンインストール：「Adobe Campaign以 [前のバージョンのパッケージのアンインストール](#uninstalling-adobe-campaign-previous-version-packages)、
1. プラットフォームの移行：詳しくは、 [Adobe Campaign v7の導入](#deploying-adobe-campaign-v7)、
1. サービスの再開：詳しくは、サ [ービスの再起動を参照してください](#re-starting-services)。

## サービス停止 {#service-stop}

まず、関連するすべてのマシン上のデータベースにアクセスできるすべてのプロセスを停止します。

1. rootとしてログイ **ンします**。
1. リダイレクトモジュール(**webmdl** サービス)を使用するサーバーはすべて停止する必要があります。 Apacheの場合は、次のコマンドを実行します。

   ```
   /etc/init.d/apache2 stop
   ```

1. 再び **rootとしてログインします**。
1. すべてのサーバーでAdobe Campaignの以前のバージョンのサービスを停止します。

   ```
   /etc/init.d/nlserver6 stop
   ```

   v5.11から移行する場合は、次のコマンドを実行します。

   ```
   /etc/init.d/nlserver5 stop
   ```

1. 各サーバーでAdobe Campaignサービスが停止していることを確認します。

   ```
   ps waux | grep nlserver
   ```

   アクティブなプロセスのリストが、そのID(PID)と共に表示されます。

1. 1つ以上のAdobe Campaignプロセスが、数分後もアクティブであるかブロックされている場合は、それらを強制終了します。

   ```
   killall nlserver
   ```

1. 数分後も一部のプロセスがアクティブなままの場合は、次のコマンドを使用して、プロセスを強制的に閉じることができます。

   ```
   killall -9 nlserver
   ```

## データベースと既存のインストールのバックアップ {#back-up-the-database-and-the-existing-installation}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5.11からの移行 {#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. neolaneとしてログ **インし** 、次のコマンドを使用して **nl5** ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl5 nl5.back
   ```

   >[!CAUTION]
   >
   >予防策として、 **nl5.backフォルダーを圧縮し** 、サーバー以外の安全な場所に保存することをお勧めします。

1. mta **,`<instance name>`server** fstat **,** stat ************ etc サービスが自動的に開始されない。 例えば、autoStartを **** _autoStart **(** neolaneとして **)に置き換えます**。

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

### Adobe Campaign v6.02からの移行 {#migrating-from-adobe-campaign-v6-02}

1. Adobe Campaignデータベースのバックアップを作成します。
1. neolaneとしてログ **インし** 、次のコマンドを使用して **nl6** ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!CAUTION]
   >
   >予防策として、 **nl6.backフォルダーを圧縮し** 、サーバー以外の安全な場所に保存することをお勧めします。

1. **config-`<instance name>`.xmlを(** nl6.backフォルダ内の)編集します。これは、mta **、** wserver **stat、********** stat、etcという名前です。 サービスが自動的に開始されない。 例えば、autoStartを **** _autoStart **(** Adobe Campaignと同じ ****)に置き換えます。

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

### Adobe Campaign v6.1からの移行 {#migrating-from-adobe-campaign-v6-1}

1. Adobe Campaignデータベースのバックアップを作成します。
1. neolaneとしてログ **インし** 、次のコマンドを使用して **nl6** ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!CAUTION]
   >
   >予防策として、 **nl6.backフォルダーを圧縮し** 、サーバー以外の安全な場所に保存することをお勧めします。

## Adobe Campaignの以前のバージョンのパッケージをアンインストールする {#uninstalling-adobe-campaign-previous-version-packages}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5パッケージのアンインストール {#uninstalling-adobe-campaign-v5-packages}

1. rootとしてログイ **ンします**。
1. 次のコマンドを使用して、インストールされたAdobe Campaignパッケージを特定します。

   * Debian **の場**&#x200B;合：

      ```
      dpkg -l | grep nl
      ```

      インストール済みパッケージのリストが表示されます。

      ```
      ii  nlserver5                       5762                     nlserver5-5762
      ii  nlthirdparty5                   5660                     nlthirdparty5-5660
      ```

   * In **Red Hat**:

      ```
      rpm -qa | grep nl
      ```

1. Adobe Campaign v5パッケージをアンインストールします。

   * Debian **の場**&#x200B;合：

      ```
      dpkg --purge nlserver5 nlthirdparty5
      ```

   * In **Red Hat**:

      ```
      rprm -ev nlserver5 nlthirdparty5
      ```

### Adobe Campaign v6パッケージのアンインストール {#uninstalling-adobe-campaign-v6-packages}

この節では、Adobe Campaign v6.02またはv6.1パッケージをアンインストールする方法を示します。

1. rootとしてログイ **ンします**。
1. 次のコマンドを使用して、インストールされたAdobe Campaignパッケージを特定します。

   * Debian **の場**&#x200B;合：

      ```
      dpkg -l | grep nl
      ```

      インストール済みパッケージのリストが表示されます。

      ```
      ii  nlserver6                       XXXX                     nlserver6-XXXX
      ii  nlthirdparty6                   XXXX                     nlthirdparty6-XXXX
      ```

   * In **Red Hat**:

      ```
      rpm -qa | grep nl
      ```

1. Adobe Campaign v6パッケージをアンインストールします。

   * Debian **の場**&#x200B;合：

      ```
      dpkg --purge nlserver6 nlthirdparty6
      ```

   * In **Red Hat**:

      ```
      rprm -ev nlserver6 nlthirdparty6
      ```

## Deploying Adobe Campaign v7 {#deploying-adobe-campaign-v7}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5.11からの移行 {#migrating-from-adobe-campaign-v5_11-1}

Adobe Campaignの展開には、次の2つの段階があります。

* Adobe Campaign v7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignを導入するには、次の手順を適用します。

1. 次のコマンドを使用して、最新のAdobe Campaign v7パッケージをインストールします。

   * Debian **の場**&#x200B;合：

      ```
      dpkg -i nlserver6-v7-XXXX-linux-2.6-intel.deb
      ```

   * In **Red Hat**:

      ```
      rpm -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
      ```
   >[!CAUTION]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >v5.11から移行する場合、Adobe Campaignはデフォルトで/usr/local/neolane/nl6/ **ディレクトリにインストー** ルされます。
   >
   >パッケージがインストールされると、次のメッセージが表示されます。&#39; **WdbcTimeZone&#39;オプションがありません**。 これは正常です。

1. クライアントコンソールインストールプログラムを使用可能にするには、Adobe Campaignインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでのAdobe Campaignのインストール方法について詳しくは、この節を参照し [てください](../../installation/using/installing-campaign-standard-packages.md)。

1. Neolaneユーザーと **一致する.bashrd** ファイルを変 **更します** 。 neolaneとしてログオン **し** 、次のコマンドを実行します。

   ```
   su - neolane
   vim ~/.bashrc
   ```

   >[!NOTE]
   >
   >neolaneとしてログインすると ****、次のメッセージが表示されます。 **nl5/env.sh :該当するファイルまたはディレクトリはありません**。 これは正常です。

   ファイルの末尾で、nl5/env.shをnl6/env.shに置き **換え** ま **す**。

1. 次のコマンドを使用し **て** 、rootとしてログインし、インスタンスを準備します。

   ```
   /etc/init.d/nlserver6-v7 start   
   Starting nlserver6-v7: [  OK  ]
   ```

   ```
   /etc/init.d/nlserver6-v7 stop
   Stopping nlserver6-v7: [  OK  ]
   ```

   >[!NOTE]
   >
   >次の各コマンドを使用して、Adobe Campaign v6内部ファイルシステムを作成できます。 **conf** ディレクトリ( **config-default.xmlファイルと** serverConf.xmlファイル、 **var****** formed directoryを含む)

1. nl5.back **** backupフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 neolaneとしてログイン **し** 、次のコマンドを実行します。

   >[!CAUTION]
   >
   >次の最初のコマンドでは、 **config-default.xmlファイルをコピーしないでください** 。

   ```
   su - neolane
   
   cp nl5.back/conf/config-<instance name>.xml nl6/conf/
   cp nl5.back/customer.sh nl6/
   cp -r nl5.back/customers/* nl6/customers/
   cp -r nl5.back/var/* nl6/var/
   ```

1. Adobe Campaign v7 **serverConf.xml** 、 **** config-default.xmlファイルで、Adobe Campaign v5に対して設定した特定の設定を適用します。 serverConf.xmlフ **ァイルの場合は** 、nl5/conf/serverConf.xml.diffフ **ァイルを使用します** 。

   >[!NOTE]
   >
   >Adobe Campaign v5からAdobe Campaign v7に設定をレポートする場合は、物理ディレクトリへのパスがAdobe Campaign v5につながっているのではなく、Adobe Campaign v7につながっていることを確認します。

1. 移行は一般的なインストールではないので、trackinglogdサービスを強制的に再起動する必要が **あります** 。 これを行うには、nl6/conf/config-default.xml **** fileを開き、 **trackinglogd** サービスが有効になっている（トラッキング/リダイレクトサーバー上でのみ）ことを確認します。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!CAUTION]
   >
   >トラッキング **ログ** サービスがトラッキングサーバーで開始されていない場合、トラッキング情報は転送されません。

1. 次のコマンドを使用して、Adobe Campaign v7の設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して（neolaneとして）アップグレード後のプロセス **を開始します**。

   ```
   su - neolane
   nlserver config -timezone:<time zone> -postupgrade -instance:<instance name>
   ```

   >[!CAUTION]
   >
   >アップグレード後に参照として使用するタイムゾーンを指定する必要があります( **-timezone** オプションを使用)。 この場合、ヨーロッパ/パリのタイムゾーンを使用し **ています。「ヨーロッパ/パリ」**。

   >[!NOTE]
   >
   >ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションの詳細については、タイムゾーンの節を [参照してくださ](../../migration/using/general-configurations.md#time-zones) い。

>[!CAUTION]
>
>まだAdobe Campaignサービスを開始しない：変更はApacheで行う必要があります。

### Adobe Campaign v6.02からの移行 {#migrating-from-adobe-campaign-v6_02-1}

Adobe Campaignの展開には、次の2つの段階があります。

* Adobe Campaign v7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignを導入するには、次の手順を適用します。

1. 次のコマンドを使用して、最新のAdobe Campaign v7パッケージをインストールします。

   * Debian **の場**&#x200B;合：

      ```
      dpkg -i nlserver6-v7-XXXX-amd64_debX.deb
      ```

   * In **Red Hat**:

      ```
      rpm -Uvh nlserver6-v7-XXXX-x86_64_rhX.rpm
      ```
   >[!CAUTION]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >Adobe Campaign v7は、デフォルトでAdobe Campaign v6.02と同じディレクトリにインストールされます。 **/usr/local/neolane/nl6/**.

1. クライアントコンソールインストールプログラムを使用可能にするには、Adobe Campaignインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでのAdobe Campaignのインストール方法について詳しくは、この節を参照し [てください](../../installation/using/installing-campaign-standard-packages.md)。

1. 移行は一般的なインストールではないので、trackinglogdサービスを強制的に再起動する必要が **あります** 。 これを行うには、nl6/conf/config-default.xml **** fileを開き、 **trackinglogd** サービスが有効になっている（トラッキング/リダイレクトサーバー上でのみ）ことを確認します。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!CAUTION]
   >
   >トラッキング **ログ** サービスがトラッキングサーバーで開始されていない場合、トラッキング情報は転送されません。

1. nl6.back **** backupフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 neolaneとしてログイン **し** 、次のコマンドを実行します。

   ```
   su - neolane
   
   cp nl6.back/conf/config*.xml nl6/conf/
   cp nl6.back/customer.sh nl6/
   cp -r nl6.back/customers/* nl6/customers/
   cp -r nl6.back/var/* nl6/var/
   ```

1. 次のコマンドを使用して、Adobe Campaign v7の設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して（neolaneとして）アップグレード後のプロセス **を開始します**。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

   >[!NOTE]
   >
   >「マルチタイムゾーン」モードは、PostgreSQLデータベースエンジン用にv6.02でのみ使用可能でした。 どのバージョンのデータベースエンジンが使用されていても使用できるようになりました。 ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションの詳細については、タイムゾーンの節を [参照してくださ](../../migration/using/general-configurations.md#time-zones) い。

### Adobe Campaign v6.1からの移行 {#migrating-from-adobe-campaign-v6_1-1}

Adobe Campaignの展開には、次の2つの段階があります。

* Adobe Campaign v7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignを導入するには、次の手順を適用します。

1. 次のコマンドを使用して、最新のAdobe Campaign v7パッケージをインストールします。

   * Debian **の場**&#x200B;合：

      ```
      dpkg -i nlserver6-v7-XXXX-amd64_debX.deb
      ```

   * In **Red Hat**:

      ```
      rpm -Uvh nlserver6-v7-XXXX-x86_64_rhX.rpm
      ```
   >[!CAUTION]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >Adobe Campaign v7は、デフォルトで/usr/local/neolane/nl6/ **ディレクトリにインストールさ** れます。

1. クライアントコンソールインストールプログラムを使用可能にするには、Adobe Campaignインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでのAdobe Campaignのインストール方法について詳しくは、この節を参照し [てください](../../installation/using/installing-campaign-standard-packages.md)。

1. nl6.back **** backupフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 neolaneとしてログイン **し** 、次のコマンドを実行します。

   ```
   su - neolane
   
   cp nl6.back/conf/config*.xml nl6/conf/
   cp nl6.back/customer.sh nl6/
   cp -r nl6.back/customers/* nl6/customers/
   cp -r nl6.back/var/* nl6/var/
   ```

1. 次のコマンドを使用して、Adobe Campaign v7の設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して（neolaneとして）アップグレード後のプロセス **を開始します**。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

## リダイレクトサーバー(Apache)の移行 {#migrating-the-redirection-server--apache-}

>[!NOTE]
>
>この節は、Adobe Campaign v5.11から移行する場合にのみ適用されます。

この段階で、Apacheを停止する必要があります。 参照先：サー [ビス停止](#service-stop)。

1. rootとしてログイ **ンします**。
1. Apache環境変数を変更して、 **nl6** ディレクトリにリンクします。

   * Debian **の場**&#x200B;合：

      ```
      vi /etc/apache2/envvars
      ```

   * In **Red Hat**:

      ```
      vi /usr/local/apache2/bin/envvars
      ```

1. 次に、次のコマンドを実行します。

   * Debian **の場**&#x200B;合：

      nlsrv.load **ファイルで、** nl5 **を** nl6に置き換え **ます**。

      ```
      vi /etc/apache2/mods-available/nlsrv.load
      ```

      nlsrv.confファイルのリ **ンクを削除し** 、新しいリンクを作成します。

      ```
      rm /etc/apache2/mods-available/nlsrv.conf 
      ln -s /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf /etc/apache2/
      mods-available/nlsrv.conf
      ```

   * In **Red Hat**:

      /usr/local/apache2/conf **ディレクトリに移動し、** http.confファイルを編集して、 **nl5** nl6 ******** を次の行に置き換えます。

      RHEL 6 **/Debian 7の場合**:

      ```
      LoadModule requesthandler22_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
      Include /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf
      ```

      RHEL 7 **/Debian 8では**:

      ```
      LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
      Include /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf
      ```

1. alias.confファ **イルに移動し** 、すべての **nl5** を **nl6に置き換えます**。 Debianでこれを行うには、次のコマンドを実行します。

   ```
   vi /etc/apache2/mods-available/alias.conf
   ```

## Security zones {#security-zones}

v6.02以前から移行する場合は、サービスを開始する前にセキュリティゾーンを設定する必要があります。 詳細については、「セキュリティ」を参照し [てくださ](../../migration/using/general-configurations.md#security)い。

## サービスの再開 {#re-starting-services}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaign v5.11からの移行 {#migrating-from-adobe-campaign-v5_11-2}

config- **.xmlファイル`<instance name>`で、** mta **wfserver**, **stat,** stat, etcの自動起動を再開 ****&#x200B;します。 サービス。

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

次の各サーバーでApacheおよびAdobe Campaignサービスを開始します。

1. トラッキングとリダイレクトサーバー。
1. ミッドソーシングサーバー。
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、回帰がないこと、および「一般設定」セクションの推奨事項に従ってすべての動作を確認 [します](../../migration/using/general-configurations.md) 。

### Adobe Campaign v6.02からの移行 {#migrating-from-adobe-campaign-v6_02-2}

config- **.xmlファイル`<instance name>`で、** mta **wfserver**, **stat,** stat, etcの自動起動を再開 ****&#x200B;します。 サービス。

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

次の各サーバーでApacheおよびAdobe Campaignサービスを開始します。

1. トラッキングとリダイレクトサーバー。
1. ミッドソーシングサーバー。
1. マーケティングサーバー。

新しいインストールを完全にテストし、再生されないことを確認し、「一般設定」セクションの推奨事項に従って、すべてが正しく動作していることを [確認します](../../migration/using/general-configurations.md) 。

### Adobe Campaign v6.1からの移行 {#migrating-from-adobe-campaign-v6_1-2}

次の各サーバーでApacheおよびAdobe Campaignサービスを開始します。

1. トラッキングとリダイレクトサーバー。
1. ミッドソーシングサーバー。
1. マーケティングサーバー。

新しいインストールを完全にテストし、再生されないことを確認し、「一般設定」セクションの推奨事項に従って、すべてが正しく動作していることを [確認します](../../migration/using/general-configurations.md) 。

## Adobe Campaign v5の削除とクレンジング {#deleting-and-cleansing-adobe-campaign-v5}

>[!NOTE]
>
>この節は、Adobe Campaign v5.11から移行する場合にのみ適用されます。

Adobe Campaign v5のインストールを削除してクリーンアップする前に、次の推奨事項を適用する必要があります。

* 新しいインストールの完全なチェックを実行する機能チームを招待します。
* Adobe Campaign v5は、ロールバックが必要ないことが確実な場合にのみアンインストールします。

nl5.back **ディレクトリを削除します** 。 neolaneとしてログイン **し** 、次のコマンドを実行します。

```
su - neolane
rm -rf nl5.back
```

サーバーを再起動します。
