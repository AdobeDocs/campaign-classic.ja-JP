---
product: campaign
title: Linux での Adobe Campaign 7 への移行
description: Linux での Adobe Campaign 7 への移行
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
exl-id: 9dc0699c-0fbf-4f8e-81f7-8ca3d7e98798
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1890'
ht-degree: 1%

---

# Linux での Adobe Campaign 7 への移行{#migrating-in-linux-for-adobe-campaign-v}

## 一般的な手順{#general-procedure}

Linuxでの移行手順は次のとおりです。

1. サービスの停止：[サービス停止](#service-stop)を参照してください。
1. データベースを保存します。[データベースと既存のインストールのバックアップ](#back-up-the-database-and-the-existing-installation)を参照してください。
1. 以前のAdobe Campaignバージョンパッケージをアンインストールします。[Adobe Campaignの以前のバージョンパッケージのアンインストール](#uninstalling-adobe-campaign-previous-version-packages)を参照してください。
1. プラットフォームの移行：[Adobe Campaign v7のデプロイ](#deploying-adobe-campaign-v7)を参照してください。
1. サービスの再起動：[サービスの再起動](#re-starting-services)を参照してください。

## サービス停止{#service-stop}

まず、関係するすべてのマシン上のデータベースにアクセスできるすべてのプロセスを停止します。

1. **root**&#x200B;としてログインします。
1. リダイレクトモジュール（**webmdl**&#x200B;サービス）を使用するすべてのサーバーを停止する必要があります。 Apacheの場合は、次のコマンドを実行します。

   ```
   /etc/init.d/apache2 stop
   ```

1. **root**&#x200B;として再度ログインします。
1. Adobe Campaignの以前のバージョンのサービスをすべてのサーバーで停止します。

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

   アクティブなプロセスのリストとそのID(PID)が表示されます。

1. 数分後に1つ以上のAdobe Campaignプロセスがアクティブまたはブロックされたままの場合は、それらを強制終了します。

   ```
   killall nlserver
   ```

1. 数分後に一部のプロセスがアクティブなままの場合は、次のコマンドを使用してプロセスを強制的に閉じることができます。

   ```
   killall -9 nlserver
   ```

## データベースと既存のインストール{#back-up-the-database-and-the-existing-installation}をバックアップします。

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5.11からの移行{#migrating-from-adobe-campaign-v5-11}

1. Adobe Campaignデータベースのバックアップを作成します。
1. **neolane**&#x200B;としてログインし、次のコマンドを使用して&#x200B;**nl5**&#x200B;ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl5 nl5.back
   ```

   >[!IMPORTANT]
   >
   >予防措置として、**nl5.back**&#x200B;フォルダーをzip形式で圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. **config-`<instance name>`.xml**（**nl5.back**&#x200B;フォルダー内）を編集し、**mta**、**wfserver**、**stat**&#x200B;などを防ぎます。 サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart**&#x200B;を&#x200B;**_autoStart**&#x200B;に置き換えます（**neolane**&#x200B;と同じ）。

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
1. **neolane**&#x200B;としてログインし、次のコマンドを使用して&#x200B;**nl6**&#x200B;ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防措置として、**nl6.back**&#x200B;フォルダーをzip形式で圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

1. **config-`<instance name>`.xml**（**nl6.back**&#x200B;フォルダー内）を編集して、**mta**、**wfserver**、**stat**&#x200B;などを防ぎます。 サービスが自動的に開始されない問題を修正しました。 例えば、 **autoStart**&#x200B;を&#x200B;**_autoStart**&#x200B;に置き換えます(**Adobe Campaign**&#x200B;と同じです)。

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

### Adobe Campaign v6.1からの移行{#migrating-from-adobe-campaign-v6-1}

1. Adobe Campaignデータベースのバックアップを作成します。
1. **neolane**&#x200B;としてログインし、次のコマンドを使用して&#x200B;**nl6**&#x200B;ディレクトリのバックアップを作成します。

   ```
   su - neolane
   mv nl6 nl6.back
   ```

   >[!IMPORTANT]
   >
   >予防措置として、**nl6.back**&#x200B;フォルダーをzip形式で圧縮し、サーバー以外の安全な場所に保存することをお勧めします。

## Adobe Campaign以前のバージョンのパッケージのアンインストール{#uninstalling-adobe-campaign-previous-version-packages}

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5パッケージ{#uninstalling-adobe-campaign-v5-packages}のアンインストール

1. **root**&#x200B;としてログインします。
1. 次のコマンドを使用して、インストールされたAdobe Campaignパッケージを特定します。

   * **Debian**&#x200B;では、次のようになります。

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

1. Adobe Campaign v5パッケージをアンインストールします。

   * **Debian**&#x200B;では、次のようになります。

      ```
      dpkg --purge nlserver5 nlthirdparty5
      ```

   * **Red Hat**&#x200B;内：

      ```
      rprm -ev nlserver5 nlthirdparty5
      ```

### Adobe Campaign v6パッケージ{#uninstalling-adobe-campaign-v6-packages}のアンインストール

この節では、Adobe Campaign v6.02またはv6.1パッケージのアンインストール方法を示します。

1. **root**&#x200B;としてログインします。
1. 次のコマンドを使用して、インストールされたAdobe Campaignパッケージを特定します。

   * **Debian**&#x200B;では、次のようになります。

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

1. Adobe Campaign v6パッケージをアンインストールします。

   * **Debian**&#x200B;では、次のようになります。

      ```
      dpkg --purge nlserver6 nlthirdparty6
      ```

   * **Red Hat**&#x200B;内：

      ```
      rprm -ev nlserver6 nlthirdparty6
      ```

## Adobe Campaign v7 {#deploying-adobe-campaign-v7}のデプロイ

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5.11からの移行{#migrating-from-adobe-campaign-v5_11-1}

Adobe Campaignのデプロイには、次の2つの段階があります。

* Adobe Campaign v7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. 次のコマンドを使用して、最新のAdobe Campaign v7パッケージをインストールします。

   * **Debian**&#x200B;では、次のようになります。

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
   >v5.11から移行する場合、Adobe Campaignはデフォルトで&#x200B;**/usr/local/neolane/nl6/**&#x200B;ディレクトリにインストールされます。
   >
   >パッケージがインストールされると、次のメッセージが表示されます。**&#39;WdbcTimeZone&#39;オプションが見つかりません**。 これは正常です。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順に従って、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでのAdobe Campaignのインストール方法について詳しくは、[この節](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

1. **.bashrd**&#x200B;ファイルを変更します。このファイルは、**neolane**&#x200B;ユーザーと一致します。 **neolane**&#x200B;としてログオンし、次のコマンドを実行します。

   ```
   su - neolane
   vim ~/.bashrc
   ```

   >[!NOTE]
   >
   >**neolane**&#x200B;としてログインすると、次のメッセージが表示されます。**nl5/env.sh :そのようなファイルやディレクトリはありません。** これは正常です。

   ファイルの最後で、 **nl5/env.sh**&#x200B;を&#x200B;**nl6/env.sh**&#x200B;に置き換えます。

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
   >次のコマンドを使用して、Adobe Campaign v6の内部ファイルシステムを作成できます。**conf**&#x200B;ディレクトリ（**config-default.xml**&#x200B;および&#x200B;**serverConf.xml**&#x200B;ファイルを含む）、**var**&#x200B;ディレクトリ。

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

1. Adobe Campaign v7の&#x200B;**serverConf.xml**&#x200B;ファイルと&#x200B;**config-default.xml**&#x200B;ファイルで、Adobe Campaign v5に対して行った特定の設定を適用します。 **serverConf.xml**&#x200B;ファイルの場合は、**nl5/conf/serverConf.xml.diff**&#x200B;ファイルを使用します。

   >[!NOTE]
   >
   >Adobe Campaign v5からAdobe Campaign v7への設定をレポートする場合、物理ディレクトリへのパスがAdobe Campaign v5ではなくAdobe Campaign v7に続くことを確認します。

1. 移行は一般的なインストールではないので、**trackinglogd**&#x200B;サービスを強制的に再起動する必要があります。 これをおこなうには、**nl6/conf/config-default.xml**&#x200B;ファイルを開き、**trackinglogd**&#x200B;サービスが有効になっていることを確認します（トラッキング/リダイレクトサーバー上のみ）。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >**trackinglogd**&#x200B;サービスがトラッキングサーバーで開始されていない場合、トラッキング情報は転送されません。

1. 次のコマンドを使用して、Adobe Campaign v7設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します（**neolane**&#x200B;として）。

   ```
   su - neolane
   nlserver config -timezone:<time zone> -postupgrade -instance:<instance name>
   ```

   >[!IMPORTANT]
   >
   >アップグレード後に（**-timezone**&#x200B;オプションを使用して）参照として使用するタイムゾーンを指定する必要があります。 この場合、Europe/Parisタイムゾーン&#x200B;**-timezoneを使用します。&quot;Europe/Paris&quot;**。

   >[!NOTE]
   >
   >ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションについて詳しくは、[タイムゾーン](../../migration/using/general-configurations.md#time-zones)の節を参照してください。

>[!IMPORTANT]
>
>まだAdobe Campaignサービスを開始しない：変更は、引き続きApacheでおこなう必要があります。

### Adobe Campaign v6.02からの移行{#migrating-from-adobe-campaign-v6_02-1}

Adobe Campaignのデプロイには、次の2つの段階があります。

* Adobe Campaign v7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. 次のコマンドを使用して、最新のAdobe Campaign v7パッケージをインストールします。

   * **Debian**&#x200B;では、次のようになります。

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
   >Adobe Campaign v7は、デフォルトでAdobe Campaign v6.02と同じディレクトリにインストールされます。**/usr/local/neolane/nl6/**.

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順に従って、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでのAdobe Campaignのインストール方法について詳しくは、[この節](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

1. 移行は一般的なインストールではないので、**trackinglogd**&#x200B;サービスを強制的に再起動する必要があります。 これをおこなうには、**nl6/conf/config-default.xml**&#x200B;ファイルを開き、**trackinglogd**&#x200B;サービスが有効になっていることを確認します（トラッキング/リダイレクトサーバー上のみ）。

   ```
   <trackinglogd autoStart="true"/>
   ```

   >[!IMPORTANT]
   >
   >**trackinglogd**&#x200B;サービスがトラッキングサーバーで開始されていない場合、トラッキング情報は転送されません。

1. **nl6.back**&#x200B;バックアップフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 **neolane**&#x200B;としてログインし、次のコマンドを実行します。

   ```
   su - neolane
   
   cp nl6.back/conf/config*.xml nl6/conf/
   cp nl6.back/customer.sh nl6/
   cp -r nl6.back/customers/* nl6/customers/
   cp -r nl6.back/var/* nl6/var/
   ```

1. 次のコマンドを使用して、Adobe Campaign v7設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します（**neolane**&#x200B;として）。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

   >[!NOTE]
   >
   >「マルチタイムゾーン」モードは、PostgreSQLデータベースエンジンのv6.02でのみ使用できました。 どのバージョンのデータベースエンジンを使用していても使用できるようになりました。 ベースを「マルチタイムゾーン」にアップグレードすることを強くお勧めします。 タイムゾーンオプションについて詳しくは、[タイムゾーン](../../migration/using/general-configurations.md#time-zones)の節を参照してください。

### Adobe Campaign v6.1からの移行{#migrating-from-adobe-campaign-v6_1-1}

Adobe Campaignのデプロイには、次の2つの段階があります。

* Adobe Campaign v7パッケージのインストール：この操作は、各サーバーで実行する必要があります。
* アップグレード後：このコマンドは、各インスタンスで起動する必要があります。

Adobe Campaignをデプロイするには、次の手順に従います。

1. 次のコマンドを使用して、最新のAdobe Campaign v7パッケージをインストールします。

   * **Debian**&#x200B;では、次のようになります。

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
   >Adobe Campaign v7は、デフォルトで&#x200B;**/usr/local/neolane/nl6/**&#x200B;ディレクトリにインストールされます。

1. クライアントコンソールのインストールプログラムを使用可能にするには、次の手順に従って、Adobe Campaignのインストールディレクトリにコピーします。

   ```
   cp setup-client-7.0.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
   ```

   >[!NOTE]
   >
   >LinuxでのAdobe Campaignのインストール方法について詳しくは、[この節](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

1. **nl6.back**&#x200B;バックアップフォルダーに移動し、各インスタンスの設定ファイルとサブフォルダーをコピー（上書き）します。 **neolane**&#x200B;としてログインし、次のコマンドを実行します。

   ```
   su - neolane
   
   cp nl6.back/conf/config*.xml nl6/conf/
   cp nl6.back/customer.sh nl6/
   cp -r nl6.back/customers/* nl6/customers/
   cp -r nl6.back/var/* nl6/var/
   ```

1. 次のコマンドを使用して、Adobe Campaign v7設定を再読み込みします。

   ```
   nlserver config -reload
   ```

1. 次のコマンドを使用して、アップグレード後のプロセスを開始します（**neolane**&#x200B;として）。

   ```
   su - neolane
   nlserver config -postupgrade -instance:<instance name>
   ```

## リダイレクションサーバー(Apache) {#migrating-the-redirection-server--apache-}の移行

>[!NOTE]
>
>この節は、Adobe Campaign v5.11から移行する場合にのみ適用されます。

この段階で、Apacheを停止する必要があります。 次を参照してください。[サービス停止](#service-stop)。

1. **root**&#x200B;としてログインします。
1. Apache環境変数を変更して、**nl6**&#x200B;ディレクトリにリンクします。

   * **Debian**&#x200B;では、次のようになります。

      ```
      vi /etc/apache2/envvars
      ```

   * **Red Hat**&#x200B;内：

      ```
      vi /usr/local/apache2/bin/envvars
      ```

1. 次に、次のコマンドを実行します。

   * **Debian**&#x200B;では、次のようになります。

      **nlsrv.load**&#x200B;ファイルで、**nl5**&#x200B;を&#x200B;**nl6**&#x200B;に置き換えます。

      ```
      vi /etc/apache2/mods-available/nlsrv.load
      ```

      **nlsrv.conf**&#x200B;ファイルのリンクを削除し、新しく作成します。

      ```
      rm /etc/apache2/mods-available/nlsrv.conf 
      ln -s /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf /etc/apache2/
      mods-available/nlsrv.conf
      ```

   * **Red Hat**&#x200B;内：

      **/usr/local/apache2/conf**&#x200B;ディレクトリに移動し、**http.conf**&#x200B;ファイルを編集して、次の行で&#x200B;**nl5**&#x200B;を&#x200B;**nl6**&#x200B;に置き換えます。

      **RHEL 7/Debian 8**:

      ```
      LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
      Include /usr/local/neolane/nl6/tomcat-6/conf/apache_neolane.conf
      ```

1. **alias.conf**&#x200B;ファイルに移動し、すべての&#x200B;**nl5**&#x200B;を&#x200B;**nl6**&#x200B;に置き換えます。 Debianでこれをおこなうには、次のコマンドを実行します。

   ```
   vi /etc/apache2/mods-available/alias.conf
   ```

## セキュリティゾーン{#security-zones}

v6.02以前から移行する場合は、サービスを開始する前にセキュリティゾーンを設定する必要があります。 詳しくは、[セキュリティ](../../migration/using/general-configurations.md#security)を参照してください。

## サービス{#re-starting-services}を再開しています

手順は、以前のバージョンのAdobe Campaignによって異なります。

### Adobe Campaign v5.11からの移行{#migrating-from-adobe-campaign-v5_11-2}

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

次の各サーバーでApacheおよびAdobe Campaignサービスを開始します。

1. 追跡サーバーとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

次の手順に進む前に、新しいインストールの完全なテストを実行し、リグレッションがなく、[一般設定](../../migration/using/general-configurations.md)セクションのすべての推奨事項に従ってすべてが動作することを確認します。

### Adobe Campaign v6.02からの移行{#migrating-from-adobe-campaign-v6_02-2}

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

次の各サーバーでApacheおよびAdobe Campaignサービスを開始します。

1. 追跡サーバーとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

新しいインストールを完全にテストし、再生されないことを確認し、[一般設定](../../migration/using/general-configurations.md)の節に記載されている推奨事項に従って、すべてが正しく動作していることを確認します。

### Adobe Campaign v6.1からの移行{#migrating-from-adobe-campaign-v6_1-2}

次の各サーバーでApacheおよびAdobe Campaignサービスを開始します。

1. 追跡サーバーとリダイレクトサーバー。
1. ミッドソーシングサーバー.
1. マーケティングサーバー。

新しいインストールを完全にテストし、再生されないことを確認し、[一般設定](../../migration/using/general-configurations.md)の節に記載されている推奨事項に従って、すべてが正しく動作していることを確認します。

## Adobe Campaign v5 {#deleting-and-cleansing-adobe-campaign-v5}の削除とクレンジング

>[!NOTE]
>
>この節は、Adobe Campaign v5.11から移行する場合にのみ適用されます。

Adobe Campaign v5のインストールを削除してクレンジングする前に、次の推奨事項を適用する必要があります。

* 機能チームに新しいインストールの完全なチェックを実行してもらう。
* ロールバックが必要ないことが確実である場合は、Adobe Campaign v5をアンインストールする必要があります。

**nl5.back**&#x200B;ディレクトリを削除します。 **neolane**&#x200B;としてログインし、次のコマンドを実行します。

```
su - neolane
rm -rf nl5.back
```

サーバーを再起動します。
