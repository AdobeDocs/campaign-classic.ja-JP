---
solution: Campaign Classic
product: campaign
title: Linux での Adobe Campaign 7 への移行
description: Linux での Adobe Campaign 7 への移行
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '1890'
ht-degree: 1%

---


# Linux での Adobe Campaign 7 への移行{#migrating-in-linux-for-adobe-campaign-v}

## 一般的な手順{#general-procedure}

Linuxでの移行手順は次のとおりです。

1. サービスの停止：[サービスの停止](#service-stop)を参照してください。
1. データベースの保存：[データベースと既存のインストールのバックアップ](#back-up-the-database-and-the-existing-installation)を参照してください。
1. 以前のAdobe Campaign版パッケージをアンインストールする：[Adobe Campaignの以前のバージョンのパッケージのアンインストール](#uninstalling-adobe-campaign-previous-version-packages)を参照してください。
1. プラットフォームの移行：[Adobe Campaignv7](#deploying-adobe-campaign-v7)の導入を参照してください。
1. 再開始サービス：[サービスの再起動](#re-starting-services)を参照してください。

## サービス停止{#service-stop}

まず、関連するすべてのマシン上のデータベースにアクセスできるすべてのプロセスを停止します。

1. **root**&#x200B;としてログインします。
1. リダイレクトモジュール（**webmdl**&#x200B;サービス）を使用するすべてのサーバーを停止する必要があります。 Apacheの場合は、次のコマンドを実行します。

   ```
   /etc/init.d/apache2 stop
   ```

1. **root**&#x200B;として再度ログインします。
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

## データベースと既存のインストール{#back-up-the-database-and-the-existing-installation}をバックアップします。

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5.11からの移行{#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. **neolane**&#x200B;としてログインし、次のコマンドを使用して&#x200B;**nl5**&#x200B;ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl5 nl5.back
   ```

   >[!IMPORTANT]
   >
   >予防策として、**nl5.back**&#x200B;フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. **config-`<instance name>`.xml** （**nl5.back**&#x200B;フォルダー内）を編集して、**mta**、**wfserver**、**stat a10/>などが発生しないようにします。**&#x200B;サービスが自動的に開始されない。 例えば、**autoStart**&#x200B;を&#x200B;**_autoStart**&#x200B;に置き換えます（**neolane**&#x200B;のまま）。

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
1. **neolane**&#x200B;としてログインし、次のコマンドを使用して&#x200B;**nl6**&#x200B;ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防策として、**nl6.back**&#x200B;フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. **config-`<instance name>`.xml** （**nl6.back**&#x200B;フォルダー内）を編集して、**mta**、**wfserver**、**stat a10/>などが発生しないようにします。**&#x200B;サービスが自動的に開始されない。 例えば、**autoStart**&#x200B;を&#x200B;**_autoStart**&#x200B;に置き換えます(**Adobe Campaign**&#x200B;のまま)。

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

### Adobe Campaignv6.1からの移行{#migrating-from-adobe-campaign-v6-1}

1. Adobe Campaignデータベースのバックアップを作成します。
1. **neolane**&#x200B;としてログインし、次のコマンドを使用して&#x200B;**nl6**&#x200B;ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防策として、**nl6.back**&#x200B;フォルダーをzipファイルに圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

## Adobe Campaignの以前のバージョンのパッケージをアンインストールしています{#uninstalling-adobe-campaign-previous-version-packages}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5パッケージ{#uninstalling-adobe-campaign-v5-packages}をアンインストールしています

1. **root**&#x200B;としてログインします。
1. 次のコマンドを使用して、インストールされるAdobe Campaignパッケージを識別します。

   * **Debian**&#x200B;内：

      ```
      dpkg -l | grep nl
      ```

      インストール済みパッケージのリストが表示されます。

      ```
      ii  nlserver5                       5762                     nlserver5-5762
      ii  nlthirdparty5                   5660                     nlthirdparty5-5660
      ```

   * **Red Hat**&#x200B;内：

      ```
      rpm -qa | grep nl
      ```

1. Adobe Campaignv5パッケージをアンインストールします。

   * **Debian**&#x200B;内：

      ```
      dpkg --purge nlserver5 nlthirdparty5
      ```

   * **Red Hat**&#x200B;内：

      ```
      rprm -ev nlserver5 nlthirdparty5
      ```

### Adobe Campaignv6パッケージ{#uninstalling-adobe-campaign-v6-packages}をアンインストールしています

この節では、Adobe Campaignv6.02またはv6.1のパッケージをアンインストールする方法を示します。

1. **root**&#x200B;としてログインします。
1. 次のコマンドを使用して、インストールされるAdobe Campaignパッケージを識別します。

   * **Debian**&#x200B;内：

      ```
      dpkg -l | grep nl
      ```

      インストール済みパッケージのリストが表示されます。

      ```
      ii  nlserver6                       XXXX                     nlserver6-XXXX
      ii  nlthirdparty6                   XXXX                     nlthirdparty6-XXXX
      ```

   * **Red Hat**&#x200B;内：

      ```
      rpm -qa | grep nl
      ```

1. Adobe Campaignv6パッケージをアンインストールします。

   * **Debian**&#x200B;内：

      ```
      dpkg --purge nlserver6 nlthirdparty6
      ```

   * **Red Hat**&#x200B;内：

      ```
      rprm -ev nlserver6 nlthirdparty6
      ```

## Adobe Campaignv7の導入{#deploying-adobe-campaign-v7}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5.11からの移行{#migrating-from-adobe-campaign-v5_11-1}

Adobe Campaignのデプロイには、次の2つの段階があります。

* Adobe Campaignv7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後の手順：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順を適用します。

1. 次のコマンドを使用して、最新Adobe Campaignのv7パッケージをインストールします。

   * **Debian**&#x200B;内：

      ```
      dpkg -i nlserver6-XXXX-linux-2.6-intel.deb
      ```

   * **Red Hat**&#x200B;内：

      ```
      rpm -Uvh nlserver6-XXXX-0.x86_64.rpm
      ```
   >[!IMPORTANT]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >v5.11から移行する際、Adobe Campaignはデフォルトで&#x200B;**/usr/local/neolane/nl6/**&#x200B;ディレクトリにインストールされます。
   >
   >パッケージがインストールされると、次のメッセージが表示されます。**&#39;WdbcTimeZone&#39;オプションがありません**。 これは正常です。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順に従って、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでのAdobe Campaignのインストール方法の詳細は、[この](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

1. **.bashrd**&#x200B;ファイルを変更します。このファイルは、**neolane**&#x200B;ユーザーと一致します。 **neolane**&#x200B;としてログオンし、次のコマンドを実行します。

   ```
   su - neolane
   vim ~/.bashrc
   ```

   >[!NOTE]
   >
   >**neolane**&#x200B;としてログインすると、次のメッセージが表示されます。**nl5/env.sh :該当するファイルまたはディレクトリ**&#x200B;はありません。 これは正常です。

   ファイルの末尾で、**nl5/env.sh**&#x200B;を&#x200B;**nl6/env.sh**&#x200B;に置き換えます。

1. **root**&#x200B;としてログインし、次のコマンドを使用してインスタンスを準備します。

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
   >次の各コマンドを使用して、Adobe Campaignv6の内部ファイルシステムを作成できます。**conf**&#x200B;ディレクトリ（**config-default.xml**&#x200B;ファイルと&#x200B;**serverConf.xml**&#x200B;ファイルを含む）、**var**&#x200B;ディレクトリ。

1. **nl5.back**&#x200B;バックアップフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 **neolane**&#x200B;としてログインし、次のコマンドを実行します。

   >[!IMPORTANT]
   >
   >以下の最初のコマンドでは、**config-default.xml**&#x200B;ファイルをコピーしないでください。

   ```
   su - neolane
   
   cp nl5.back/conf/config-<instance name>.xml nl6/conf/
   cp nl5.back/customer.sh nl6/
   cp -r nl5.back/customers/* nl6/customers/
   cp -r nl5.back/var/* nl6/var/
   ```

1. Adobe Campaignv7の&#x200B;**serverConf.xml**&#x200B;ファイルと&#x200B;**config-default.xml**&#x200B;ファイルで、Adobe Campaignv5に対して設定した固有の設定を適用します。 **serverConf.xml**&#x200B;ファイルの場合は、**nl5/conf/serverConf.xml.diff**&#x200B;ファイルを使用します。

   >[!NOTE]
   >
   >Adobe Campaignv5からAdobe Campaignv7へのレポート設定では、物理ディレクトリへのパスがAdobe Campaignv5ではなくAdobe Campaignv7へのパスになっていることを確認します。

1. 移行は一般的なインストールではないので、**trackinglogd**&#x200B;サービスを強制的に再起動する必要があります。 これを行うには、**nl6/conf/config-default.xml**&#x200B;ファイルを開き、**trackinglogd**&#x200B;サービスがアクティブになっていることを確認します（トラッキング/リダイレクトサーバーでのみ）。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >トラッキングサーバーで&#x200B;**trackinglogd**&#x200B;サービスが開始されていない場合、トラッキング情報は転送されません。

1. 次のコマンドを使用して、Adobe Campaignv7の設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します（**neolane**&#x200B;のまま）。

   ```
   su - neolane
   nlserver config -timezone:<time zone> -postupgrade -instance:<instance name>
   ```

   >[!IMPORTANT]
   >
   >アップグレード後の時点で（**-timezone**&#x200B;オプションを使用して）、どのタイムゾーンを参照として使用するかを指定する必要があります。 この場合、Europe/Paris timezone **-timezoneを使用しています。&quot;Europe/Paris&quot;**.

   >[!NOTE]
   >
   >ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションの詳細については、[タイムゾーン](../../migration/using/general-configurations.md#time-zones)の節を参照してください。

>[!IMPORTANT]
>
>まだ開始Adobe Campaignサービスを使用しない：変更はApacheで行う必要があります。

### Adobe Campaignv6.02からの移行{#migrating-from-adobe-campaign-v6_02-1}

Adobe Campaignのデプロイには、次の2つの段階があります。

* Adobe Campaignv7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後の手順：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順を適用します。

1. 次のコマンドを使用して、最新Adobe Campaignのv7パッケージをインストールします。

   * **Debian**&#x200B;内：

      ```
      dpkg -i nlserver6-XXXX-amd64_debX.deb
      ```

   * **Red Hat**&#x200B;内：

      ```
      rpm -Uvh nlserver6-XXXX-x86_64_rhX.rpm
      ```
   >[!IMPORTANT]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >Adobe Campaignv7は、デフォルトでAdobe Campaignv6.02と同じディレクトリにインストールされます。**/usr/local/neolane/nl6/**

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順に従って、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでのAdobe Campaignのインストール方法の詳細は、[この](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

1. 移行は一般的なインストールではないので、**trackinglogd**&#x200B;サービスを強制的に再起動する必要があります。 これを行うには、**nl6/conf/config-default.xml**&#x200B;ファイルを開き、**trackinglogd**&#x200B;サービスがアクティブになっていることを確認します（トラッキング/リダイレクトサーバーでのみ）。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >トラッキングサーバーで&#x200B;**trackinglogd**&#x200B;サービスが開始されていない場合、トラッキング情報は転送されません。

1. **nl6.back**&#x200B;バックアップフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 **neolane**&#x200B;としてログインし、次のコマンドを実行します。

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

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します（**neolane**&#x200B;のまま）。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

   >[!NOTE]
   >
   >「マルチタイムゾーン」モードは、PostgreSQLデータベースエンジン用のv6.02でのみ使用可能でした。 どのバージョンのデータベースエンジンを使用していても使用できるようになりました。 ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションの詳細については、[タイムゾーン](../../migration/using/general-configurations.md#time-zones)の節を参照してください。

### Adobe Campaignv6.1からの移行{#migrating-from-adobe-campaign-v6_1-1}

Adobe Campaignのデプロイには、次の2つの段階があります。

* Adobe Campaignv7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後の手順：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順を適用します。

1. 次のコマンドを使用して、最新Adobe Campaignのv7パッケージをインストールします。

   * **Debian**&#x200B;内：

      ```
      dpkg -i nlserver6-XXXX-amd64_debX.deb
      ```

   * **Red Hat**&#x200B;内：

      ```
      rpm -Uvh nlserver6-XXXX-x86_64_rhX.rpm
      ```
   >[!IMPORTANT]
   >
   >次の手順に進む前に、パッケージを正常にインストールする必要があります。

   >[!NOTE]
   >
   >Adobe Campaignv7は、デフォルトで&#x200B;**/usr/local/neolane/nl6/**&#x200B;ディレクトリにインストールされます。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順に従って、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでのAdobe Campaignのインストール方法の詳細は、[この](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

1. **nl6.back**&#x200B;バックアップフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 **neolane**&#x200B;としてログインし、次のコマンドを実行します。

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

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します（**neolane**&#x200B;のまま）。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

## リダイレクトサーバー(Apache)を移行中{#migrating-the-redirection-server--apache-}

>[!NOTE]
>
>この節は、Adobe Campaignv5.11から移行する場合にのみ適用されます。

この段階で、Apacheを停止する必要があります。 参照先：[サービスは停止](#service-stop)します。

1. **root**&#x200B;としてログインします。
1. Apache環境変数を変更して、**nl6**&#x200B;ディレクトリにリンクさせます。

   * **Debian**&#x200B;内：

      ```
      vi /etc/apache2/envvars
      ```

   * **Red Hat**&#x200B;内：

      ```
      vi /usr/local/apache2/bin/envvars
      ```

1. 次に、次のコマンドを実行します。

   * **Debian**&#x200B;内：

      **nlsrv.load**&#x200B;ファイルで、**nl5**&#x200B;を&#x200B;**nl6**&#x200B;に置き換えます。

      ```
      vi /etc/apache2/mods-available/nlsrv.load
      ```

      **nlsrv.conf**&#x200B;ファイルのリンクを削除し、新しいファイルを作成します。

      ```
      rm /etc/apache2/mods-available/nlsrv.conf 
      ln -s /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf /etc/apache2/
      mods-available/nlsrv.conf
      ```

   * **Red Hat**&#x200B;内：

      **/usr/local/apache2/conf**&#x200B;ディレクトリに移動し、**http.conf**&#x200B;ファイルを編集し、次の行で&#x200B;**nl5**&#x200B;を&#x200B;**nl6**&#x200B;に置き換えます。

      **RHEL 7/Debian 8**:

      ```
      LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
      Include /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf
      ```

1. **alias.conf**&#x200B;ファイルに移動し、すべての&#x200B;**nl5**&#x200B;を&#x200B;**nl6**&#x200B;に置き換えます。 Debianでこれを行うには、次のコマンドを実行します。

   ```
   vi /etc/apache2/mods-available/alias.conf
   ```

## セキュリティゾーン{#security-zones}

v6.02以前から移行する場合は、サービスを開始する前にセキュリティゾーンを構成する必要があります。 詳しくは、[セキュリティ](../../migration/using/general-configurations.md#security)を参照してください。

## サービスの再起動{#re-starting-services}

手順は、Adobe Campaignの以前のバージョンによって異なります。

### Adobe Campaignv5.11からの移行{#migrating-from-adobe-campaign-v5_11-2}

**config-`<instance name>`.xml**&#x200B;ファイルで、**mta**、**wfserver**、**stat**&#x200B;などの自動起動を再開します。 サービス。

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

次の手順に進む前に、新しいインストールの完全なテストを実行し、回帰がないこと、および[一般的な設定](../../migration/using/general-configurations.md)セクションの推奨事項に従って動作することを確認してください。

### Adobe Campaignv6.02からの移行{#migrating-from-adobe-campaign-v6_02-2}

**config-`<instance name>`.xml**&#x200B;ファイルで、**mta**、**wfserver**、**stat**&#x200B;などの自動起動を再開します。 サービス。

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

新しいインストールを完全にテストし、復元されないこと、および[一般的な設定](../../migration/using/general-configurations.md)セクションの推奨事項に従って正しく動作していることを確認します。

### Adobe Campaignv6.1からの移行{#migrating-from-adobe-campaign-v6_1-2}

次の各サーバー上の開始ApacheおよびAdobe Campaignサービス：

1. トラッキングとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

新しいインストールを完全にテストし、復元されないこと、および[一般的な設定](../../migration/using/general-configurations.md)セクションの推奨事項に従って正しく動作していることを確認します。

## クレンジングAdobe Campaignv5の削除{#deleting-and-cleansing-adobe-campaign-v5}

>[!NOTE]
>
>この節は、Adobe Campaignv5.11から移行する場合にのみ適用されます。

Adobe Campaignv5のインストールを削除およびクリーニングする前に、次の推奨事項を適用する必要があります。

* 新しいインストールの完全なチェックを実行するには、機能チームに依頼します。
* Adobe Campaignv5は、ロールバックが必要ないことが確実にわかった場合にのみアンインストールします。

**nl5.back**&#x200B;ディレクトリを削除します。 **neolane**&#x200B;としてログインし、次のコマンドを実行します。

```
su - neolane
rm -rf nl5.back
```

サーバーの開始を再度行います。
