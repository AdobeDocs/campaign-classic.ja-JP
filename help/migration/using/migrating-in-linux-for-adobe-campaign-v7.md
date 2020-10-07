---
title: Linux での Adobe Campaign 7 への移行
seo-title: Linux での Adobe Campaign 7 への移行
description: Linux での Adobe Campaign 7 への移行
seo-description: null
page-status-flag: never-activated
uuid: 47870ea4-b07b-4db7-8094-7a8b6f4b6936
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
discoiquuid: 8f6519e8-5c8d-4974-b193-a9f1cf78b3a3
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 1%

---


# Linux での Adobe Campaign 7 への移行{#migrating-in-linux-for-adobe-campaign-v}

## 一般的な手順 {#general-procedure}

Linuxでの移行手順は次のとおりです。

1. サービスの停止：「 [サービスの停止](#service-stop)」を参照してください。
1. データベースの保存：データベースと既存のインストールの [バックアップを参照してください](#back-up-the-database-and-the-existing-installation)。
1. 以前のAdobe Campaign版パッケージをアンインストールする：「Adobe Campaignの以前のバージョンのパッケージの [アンインストール](#uninstalling-adobe-campaign-previous-version-packages)」を参照してください。
1. プラットフォームの移行：adobe campaignv7の [導入を参照してください](#deploying-adobe-campaign-v7)。
1. 再開始サービス：詳しくは、「 [サービスの再開](#re-starting-services)」を参照してください。

## サービス停止 {#service-stop}

まず、関連するすべてのマシン上のデータベースにアクセスできるすべてのプロセスを停止します。

1. rootとしてログイン **します**。
1. リダイレクトモジュール(**webmdl** サービス)を使用するすべてのサーバーを停止する必要があります。 Apacheの場合は、次のコマンドを実行します。

   ```
   /etc/init.d/apache2 stop
   ```

1. 再度 **rootとしてログインします**。
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

   アクティブなプロセスのリストは、そのID(PID)と共に表示されます。

1. 数分後に1つ以上のAdobe Campaignプロセスがアクティブまたはブロックされたままの場合は、プロセスを強制終了します。

   ```
   killall nlserver
   ```

1. 数分後に一部のプロセスがアクティブなままの場合は、次のコマンドを使用して、プロセスを強制的に閉じることができます。

   ```
   killall -9 nlserver
   ```

## データベースと既存のインストールのバックアップ {#back-up-the-database-and-the-existing-installation}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5.11からの移行 {#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. neolaneとしてログインし **、次のコマンドを使用して** nl5 **** ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl5 nl5.back
   ```

   >[!IMPORTANT]
   >
   >予防策として、 **nl5.back** フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. mta **、`<instance name>`mta** 、wserver **、server** stat、 **stat、etcの各フォルダ内にあるconfig-**.xmlを編集して、mta ******** 、nl5.backフォルダ内にある。 サービスが自動的に開始されない。 例えば、autoStart **を** _autoStart **(** neolaneと置き換えます ****)。

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
1. neolaneとしてログインし **、次のコマンドを使用して** nl6 **** ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防策として、 **nl6.back** フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. mta **、`<instance name>`wfserver** 、 **server** 、stat、 **nl、.xmlを防ぐために、config-**.xml ********（nl6.backフォルダ内）を編集します。 サービスが自動的に開始されない。 例えば、autoStart **を** _autoStart **(** Adobe Campaignとして ****)に置き換えます。

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

### Adobe Campaignv6.1からの移行 {#migrating-from-adobe-campaign-v6-1}

1. Adobe Campaignデータベースのバックアップを作成します。
1. neolaneとしてログインし **、次のコマンドを使用して** nl6 **** ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防策として、 **nl6.back** フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

## Adobe Campaignの以前のバージョンのパッケージをアンインストールする {#uninstalling-adobe-campaign-previous-version-packages}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5パッケージのアンインストール {#uninstalling-adobe-campaign-v5-packages}

1. rootとしてログイン **します**。
1. 次のコマンドを使用して、インストールされるAdobe Campaignパッケージを識別します。

   * Debian **の場合**:

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

1. Adobe Campaignv5パッケージをアンインストールします。

   * Debian **の場合**:

      ```
      dpkg --purge nlserver5 nlthirdparty5
      ```

   * In **Red Hat**:

      ```
      rprm -ev nlserver5 nlthirdparty5
      ```

### Adobe Campaignv6パッケージのアンインストール {#uninstalling-adobe-campaign-v6-packages}

この節では、Adobe Campaignv6.02またはv6.1のパッケージをアンインストールする方法を示します。

1. rootとしてログイン **します**。
1. 次のコマンドを使用して、インストールされるAdobe Campaignパッケージを識別します。

   * Debian **の場合**:

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

1. Adobe Campaignv6パッケージをアンインストールします。

   * Debian **の場合**:

      ```
      dpkg --purge nlserver6 nlthirdparty6
      ```

   * In **Red Hat**:

      ```
      rprm -ev nlserver6 nlthirdparty6
      ```

## Deploying Adobe Campaign v7 {#deploying-adobe-campaign-v7}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5.11からの移行 {#migrating-from-adobe-campaign-v5_11-1}

Adobe Campaignのデプロイには、次の2つの段階があります。

* Adobe Campaignv7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後の手順：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順を適用します。

1. 次のコマンドを使用して、最新Adobe Campaignのv7パッケージをインストールします。

   * Debian **の場合**:

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
   >v5.11から移行する際、Adobe Campaignはデフォルトで/usr/local/neolane/nl6/ **ディレクトリにインストールされ** ます。
   >
   >パッケージがインストールされると、次のメッセージが表示されます。 **&#39;WdbcTimeZone&#39;オプションがありません**。 これは正常です。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順に従って、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでAdobe Campaignをインストールする方法の詳細は、 [この節を参照してください](../../installation/using/installing-campaign-standard-packages.md)。

1. Neolane **** ユーザーと一致する.bashrd **** ファイルを変更します。 neolaneとしてログオン **し** 、次のコマンドを実行します。

   ```
   su - neolane
   vim ~/.bashrc
   ```

   >[!NOTE]
   >
   >neolaneとしてログインすると ****、次のメッセージが表示されます。 **nl5/env.sh :該当するファイルまたはディレクトリはありません**。 これは正常です。

   ファイルの末尾で、nl5/env.sh **をnl6/env.sh** に置き換え **ます**。

1. **rootとしてログインし** 、次のコマンドを使用してインスタンスを準備します。

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
   >次の各コマンドを使用して、Adobe Campaignv6の内部ファイルシステムを作成できます。 **conf** ディレクトリ( **config-default.xmlファイルと** serverConf.xml **ファイルを含む)、** var **** ディレクトリ

1. nl5.back **** backupフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 neolaneとしてログインし **、次のコマンドを実行します** 。

   >[!IMPORTANT]
   >
   >以下の最初のコマンドでは、 **config-default.xmlファイルをコピーしないでください** 。

   ```
   su - neolane
   
   cp nl5.back/conf/config-<instance name>.xml nl6/conf/
   cp nl5.back/customer.sh nl6/
   cp -r nl5.back/customers/* nl6/customers/
   cp -r nl5.back/var/* nl6/var/
   ```

1. Adobe Campaignv7 **serverConf.xml** ファイルと **** config-default.xmlファイルで、Adobe Campaignv5に対して設定した特定の設定を適用します。 serverConf.xml **ファイルの場合は、nl5/conf/serverConf.xml.diff****** ()ファイルを使用します。

   >[!NOTE]
   >
   >Adobe Campaignv5からAdobe Campaignv7へのレポート設定では、物理ディレクトリへのパスがAdobe Campaignv5ではなくAdobe Campaignv7へのパスになっていることを確認します。

1. 移行は一般的なインストールではないので、 **trackinglogd** サービスを強制的に再起動する必要があります。 これを行うには、nl6/conf/config-default.xml **ファイルを開き、** trackinglog **** サービスがアクティブになっている（トラッキング/リダイレクトサーバー上でのみ）ことを確認します。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >トラッキングサーバーで **trackinglogd** サービスが開始されていない場合、トラッキング情報は転送されません。

1. 次のコマンドを使用して、Adobe Campaignv7の設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します( **neolane**)。

   ```
   su - neolane
   nlserver config -timezone:<time zone> -postupgrade -instance:<instance name>
   ```

   >[!IMPORTANT]
   >
   >アップグレード後の時点で( **-timezone** オプションを使用して)参照として使用するタイムゾーンを指定する必要があります。 この場合、ヨーロッパ/パリタイムゾーン **— タイムゾーンを使用しています。「Europe/Paris」**。

   >[!NOTE]
   >
   >ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションの詳細については、 [タイムゾーン](../../migration/using/general-configurations.md#time-zones) (Time zones)の節を参照してください。

>[!IMPORTANT]
>
>まだ開始Adobe Campaignサービスを使用しない：変更はApacheで行う必要があります。

### Adobe Campaignv6.02からの移行 {#migrating-from-adobe-campaign-v6_02-1}

Adobe Campaignのデプロイには、次の2つの段階があります。

* Adobe Campaignv7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後の手順：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順を適用します。

1. 次のコマンドを使用して、最新Adobe Campaignのv7パッケージをインストールします。

   * Debian **の場合**:

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
   >Adobe Campaignv7は、デフォルトでAdobe Campaignv6.02と同じディレクトリにインストールされます。 **/usr/local/neolane/nl6/**.

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順に従って、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでAdobe Campaignをインストールする方法の詳細は、 [この節を参照してください](../../installation/using/installing-campaign-standard-packages.md)。

1. 移行は一般的なインストールではないので、 **trackinglogd** サービスを強制的に再起動する必要があります。 これを行うには、nl6/conf/config-default.xml **ファイルを開き、** trackinglog **** サービスがアクティブになっている（トラッキング/リダイレクトサーバー上でのみ）ことを確認します。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >トラッキングサーバーで **trackinglogd** サービスが開始されていない場合、トラッキング情報は転送されません。

1. nl6. **back** backupフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 neolaneとしてログインし **、次のコマンドを実行します** 。

   ```
   su - neolane
   
   cp nl6.back/conf/config*.xml nl6/conf/
   cp nl6.back/customer.sh nl6/
   cp -r nl6.back/customers/* nl6/customers/
   cp -r nl6.back/var/* nl6/var/
   ```

1. 次のコマンドを使用して、Adobe Campaignv7の設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します( **neolane**)。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

   >[!NOTE]
   >
   >「マルチタイムゾーン」モードは、PostgreSQLデータベースエンジン用のv6.02でのみ使用可能でした。 どのバージョンのデータベースエンジンを使用していても使用できるようになりました。 ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションの詳細については、 [タイムゾーン](../../migration/using/general-configurations.md#time-zones) (Time zones)の節を参照してください。

### Adobe Campaignv6.1からの移行 {#migrating-from-adobe-campaign-v6_1-1}

Adobe Campaignのデプロイには、次の2つの段階があります。

* Adobe Campaignv7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後の手順：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順を適用します。

1. 次のコマンドを使用して、最新Adobe Campaignのv7パッケージをインストールします。

   * Debian **の場合**:

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
   >Adobe Campaignv7は、デフォルトで/usr/local/neolane/nl6/ **ディレクトリにインストールされ** ます。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順に従って、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでAdobe Campaignをインストールする方法の詳細は、 [この節を参照してください](../../installation/using/installing-campaign-standard-packages.md)。

1. nl6. **back** backupフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 neolaneとしてログインし **、次のコマンドを実行します** 。

   ```
   su - neolane
   
   cp nl6.back/conf/config*.xml nl6/conf/
   cp nl6.back/customer.sh nl6/
   cp -r nl6.back/customers/* nl6/customers/
   cp -r nl6.back/var/* nl6/var/
   ```

1. 次のコマンドを使用して、Adobe Campaignv7の設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します( **neolane**)。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

## リダイレクトサーバーを移行しています(Apache) {#migrating-the-redirection-server--apache-}

>[!NOTE]
>
>この節は、Adobe Campaignv5.11から移行する場合にのみ適用されます。

この段階で、Apacheを停止する必要があります。 参照先： [サービスの停止](#service-stop)。

1. rootとしてログイン **します**。
1. Apache環境変数を変更して、 **nl6** ディレクトリにリンクさせます。

   * Debian **の場合**:

      ```
      vi /etc/apache2/envvars
      ```

   * In **Red Hat**:

      ```
      vi /usr/local/apache2/bin/envvars
      ```

1. 次に、次のコマンドを実行します。

   * Debian **の場合**:

      nlsrv.load **ファイルで、** nl5 **を** nl6 **に置き換えます**。

      ```
      vi /etc/apache2/mods-available/nlsrv.load
      ```

      nlsrv.conf **** ファイルのリンクを削除し、新しいファイルを作成します。

      ```
      rm /etc/apache2/mods-available/nlsrv.conf 
      ln -s /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf /etc/apache2/
      mods-available/nlsrv.conf
      ```

   * In **Red Hat**:

      /usr/local/apache2/conf **ディレクトリに移動し、** http.conf **ファイルを編集し、** nl5 **nl6を次の行で置き換え****** ます。

      RHEL 7/ **Debian 8の場合**:

      ```
      LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
      Include /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf
      ```

1. alias.conf **ファイルに移動し、すべての** nl5 **を** nl6に置き換えます ****。 Debianでこれを行うには、次のコマンドを実行します。

   ```
   vi /etc/apache2/mods-available/alias.conf
   ```

## Security zones {#security-zones}

v6.02以前から移行する場合は、サービスを開始する前にセキュリティゾーンを構成する必要があります。 詳細については、「 [セキュリティ](../../migration/using/general-configurations.md#security)」を参照してください。

## サービスの再起動 {#re-starting-services}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5.11からの移行 {#migrating-from-adobe-campaign-v5_11-2}

config- **`<instance name>`.xml** ファイルで、 **mta** wfserver, **stat****** note, netupなどの自動起動を再開します。 サービス。

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

次の各サーバー上の開始ApacheおよびAdobe Campaignサービス：

1. トラッキングとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、 [一般設定の節の推奨事項に従って、回帰がないこと、すべての動作を確認してください](../../migration/using/general-configurations.md) 。

### Adobe Campaignv6.02からの移行 {#migrating-from-adobe-campaign-v6_02-2}

config- **`<instance name>`.xml** ファイルで、 **mta** wfserver, **stat****** note, netupなどの自動起動を再開します。 サービス。

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

次の各サーバー上の開始ApacheおよびAdobe Campaignサービス：

1. トラッキングとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

新しいインストールを完全にテストし、再帰しないこと、および [一般設定の節の推奨事項に従ってすべてが正しく動作していることを確認してください](../../migration/using/general-configurations.md) 。

### Adobe Campaignv6.1からの移行 {#migrating-from-adobe-campaign-v6_1-2}

次の各サーバー上の開始ApacheおよびAdobe Campaignサービス：

1. トラッキングとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

新しいインストールを完全にテストし、再帰しないこと、および [一般設定の節の推奨事項に従ってすべてが正しく動作していることを確認してください](../../migration/using/general-configurations.md) 。

## Adobe Campaignv5の削除とクレンジング {#deleting-and-cleansing-adobe-campaign-v5}

>[!NOTE]
>
>この節は、Adobe Campaignv5.11から移行する場合にのみ適用されます。

Adobe Campaignv5のインストールを削除およびクリーニングする前に、次の推奨事項を適用する必要があります。

* 新しいインストールの完全なチェックを実行するには、機能チームに依頼します。
* Adobe Campaignv5は、ロールバックが必要ないことが確実にわかった場合にのみアンインストールします。

nl5. **back** ディレクトリを削除します。 neolaneとしてログインし **、次のコマンドを実行します** 。

```
su - neolane
rm -rf nl5.back
```

サーバーの開始を再度行います。
