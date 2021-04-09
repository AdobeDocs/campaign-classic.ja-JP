---
solution: Campaign Classic
product: campaign
title: Linux でのパッケージのインストール
description: Linux でのパッケージのインストール
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: f41c7510-5ad7-44f3-9485-01f54994b6cb
translation-type: tm+mt
source-git-commit: b0a1e0596e985998f1a1d02236f9359d0482624f
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 2%

---

# Linux でのパッケージのインストール{#installing-packages-with-linux}

Linux 32ビットプラットフォームの場合は、Adobe Campaign32ビットをインストールします。 Linux 64ビットプラットフォームの場合は、Adobe Campaign64ビットをインストールします。

これらの各バージョンに対して、Adobe Campaignには次のパッケージが1つ付属しています。**nlserver**. このパッケージには、特定のバージョンのバイナリと設定ファイルが含まれています。

インストールコマンドを使用すると、次のことができます。

* ファイルを&#x200B;**/usr/local/neolane**&#x200B;にコピーします。
* Adobe CampaignのLinuxアカウント（および関連するグループ）を作成します。このアカウントは、**/usr/local/neolane**&#x200B;をホームディレクトリとして作成します。
* 起動時に使用する自動スクリプト&#x200B;**/etc/init.d/nlserver6**&#x200B;を作成するか、システムユニットを作成します（20.1以降）。

>[!NOTE]
>
>**neolane**&#x200B;システムユーザーは、コマンドを実行する前に作成してはなりません。 **neolane**&#x200B;ユーザーは、インストール中に自動的に作成されます。
>
>**neolane**&#x200B;ユーザーにリンクされた&#x200B;**home**&#x200B;ディレクトリも&#x200B;**[!UICONTROL /usr/local/neolane]**&#x200B;に自動的に作成されます。 **[!UICONTROL /usr/local]**&#x200B;ディスクに十分な空き容量があることを確認してください（数GB）。

**ping`hostname`**&#x200B;コマンドを実行して、サーバが自分にアクセスできることを確認します。

## RPMパッケージに基づく配布{#distribution-based-on-rpm--packages}

RPM（RHEL、CentOS、およびSUSE）オペレーティングシステムにAdobe Campaignをインストールするには、次の手順を実行します。

1. 最初にAdobe Campaignパッケージを入手する必要があります。

   ファイルの名前は次のようになります。**XXXX**&#x200B;はAdobe Campaignビルド番号です。

   * **nlserver6-v7-XXXX-0.x86_64.** rpmfor v7
   * **nlserver6-XXXX-0.x86_64.** rpmfor v6.1

   >[!CAUTION]
   >
   >この節のコマンドサンプルで、ご使用のAdobe Campaignのバージョンに適したファイル名を使用していることを確認してください。

1. インストールするには、**root**&#x200B;として接続し、次のコマンドを実行します(**XXXX**&#x200B;はAdobe Campaignのビルド番号です)。

   ```
   yum install nlserver6-v7-XXXX-0.x86_64.rpm
   ```

   rpmファイルはCentOS/Red Hatディストリビューションで見つけられるパッケージに依存しています。 これらの依存関係の一部を使用したくない場合(例えば、OpenJDKではなくOracleJDKを使用したい場合)、rpmの「nodeps」オプションを使用しなければならない場合があります。

   ```
   rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
   ```

ネットポートの実行に必要な&#39;bc&#39;コマンド（詳細は[この](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts)を参照）は、デフォルトでは全てのLinuxディストリビューションで利用できません。 コマンドが使用可能かどうかを確認するには、&#39;which bc&#39;コマンドを実行します。 インストールされていない場合は、インストールする必要があります。

CentOSを使う場合は、bc.x86_64パッケージをインストールする必要があります。**root**&#x200B;として接続し、次のコマンドを実行します。

```
yum install bc.x86_64
```

## APT (Debian)に基づく配布{#distribution-based-on-apt--debian-}

### Debianでは64ビット{#in-debian-64-bits}

64ビットのAdobe CampaignをDebian 64ビットのオペレーティングシステムにインストールするには、次の手順を適用します。

1. 最初にAdobe Campaignパッケージを入手する必要があります。

   * **nlserver6-v7-XXXX-linux-2.6-amd64.** debfor v7.
   * **nlserver6-XXXX-linux-2.6-amd64.** debfor v6.1

   **** XXXXはAdobe Campaignのビルド番号です。

   >[!CAUTION]
   >
   >この節のコマンドサンプルで、ご使用のAdobe Campaignのバージョンに適したファイル名を使用していることを確認してください。

1. インストールするには、**root**&#x200B;として接続し、次のコマンドを実行します(**XXXX**&#x200B;はAdobe Campaignのビルド番号です)。

   ```
   dpkg -i nlserver6-v7-XXXX-linux-2.6-amd64.deb
   ```

   依存関係がない場合は、次のコマンドを実行します。

   ```
   apt-get install -f
   ```

**Debian 8/9の詳細**

Debian 8/9オペレーティングシステムにAdobe Campaignをインストールする場合は、次の点を考慮してください。

* OpenSSLは事前にインストールする必要があります。
* 次のコマンドを使用して、libicu52 (Debian 8)またはlibicu57 (Debian 9)、libprotobuf9 (Debian8)、libc-ares2をインストールします。

   ```
   aptitude install libicu52 (Debian 8) libicu57 (Debian 9)
   ```

   ```
   aptitude install libc-ares2
   ```

   ```
   aptitude install libprotobuf9 (only Debian 8)
   ```

* 次のコマンドを使用してJDK7をインストールします。

   ```
   aptitude install openjdk-7-jdk (Debian 8)
   ```

   ```
   aptitude install openjdk-7-jdk (Debian 9)
   ```

## パラメーターのパーソナライズ{#personalizing-parameters}

一部のパラメーターは、**customer.sh**&#x200B;ファイルを使用してパーソナライズできます

初めてインストールを実行する場合、**customer.sh**&#x200B;ファイルがまだサーバーに存在しない可能性があります。 作成し、実行権限があることを確認します。 そうでない場合は、次のコマンドを入力します。

```
chmod +x /usr/local/neolane/nl6/customer.sh
```

### サーバーエンコーディング{#server-encoding}

デフォルトでは、iso8859-15環境でサーバーが起動します。 ただし、UTF-8環境でサーバーを起動できます。

>[!CAUTION]
>
>この変更は、ファイルシステム（ワークフローまたはJavaScriptスクリプトを介して読み込まれたファイル）とのやり取りとファイルエンコーディングに影響します。 したがって、デフォルトの環境を使用することをお勧めします。

ただし、**日本語インスタンス**&#x200B;を作成する場合は、UTF-8環境を使用する必要があります。

UTF-8環境を有効にするには、次のコマンドを使用します。

```
mkdir -p /usr/local/neolane/nl6 
touch /usr/local/neolane/nl6/unicodeenv
```

### サーバーのデフォルト言語{#default-language-for-the-server}

インストールでは、英語とフランス語の両方をサポートしています。 デフォルトでは英語が使用されます。

フランス語に切り替えるには、次のコマンドを入力します。

```
su - neolane
vi nl6/customer.sh
```

次の行を追加します。

```
export neolane_LANG=fra
```

システムメッセージを正しく読み取るためには、コンソールがその言語に対応するコードページにある必要があります（フランス語の場合はISO-8859-1または —15）。

### 環境変数 {#environment-variables}

次の環境変数は正しく定義されている必要があります。

特定の組み合わせでは、Adobe Campaignの実行に使用する環境の変更が必要です。 特定のファイル(`/usr/local/neolane/nl6/customer.sh`)を作成および編集して、Adobe Campaign環境に固有の変更を追加できます。

必要に応じて、**customer.sh**&#x200B;ファイルを&#x200B;**vi customer.sh**&#x200B;コマンドを使用して編集し、設定を調整するか、行を追加します。

* oracleクライアントの場合：

   ```
   export ORACLE_HOME=/usr/local/instantclient_10_2
   export TNS_ADMIN=/etc/oracle
   export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH 
   ```

   oracle_HOME環境変数の内容は、Oracleのインストールディレクトリと一致します。

   TNS_ADMIN変数の内容は、**tnsnames.ora**&#x200B;ファイルの場所と一致する必要があります。

* LibreOfficeの場合：

   既存のバージョンのLibreOfficeでAdobe Campaignを実行するには、次の追加設定が必要です。インストールディレクトリへのアクセスパスを指定する必要があります。 例えば、次のようにします。

   * Debian

      OO_INSTALL_DIR、OO_BASIS_INSTALL_DIR、OO_URE_INSTALL_DIRのデフォルト値が提供されます。 LibreOfficeのインストールレイアウトが異なる場合は、**customer.sh**&#x200B;で上書きできます。

      ```
      export OOO_BASIS_INSTALL_DIR=/usr/lib/libreoffice/ 
      export OOO_INSTALL_DIR=/usr/lib/libreoffice/
      export OOO_URE_INSTALL_DIR=/usr/lib/ure/share/
      ```

   * CentOS

      次のデフォルト値を使用します。

      ```
      export OOO_BASIS_INSTALL_DIR=/usr/lib64/libreoffice/
      export OOO_INSTALL_DIR=/usr/lib64/libreoffice/
      export OOO_URE_INSTALL_DIR=/usr/lib64/libreoffice/ure/share/
      ```

* Java開発キット(JDK)の場合：

   デフォルトでは、Adobe Campaign環境の設定スクリプト(`~/nl6/env.sh`)はJDKのインストールディレクトリを検索します。 この動作は100%信頼性が低いので、使用するJDKを指定する必要があります。 これを行うには、次のコマンドを使用して&#x200B;**JDK_HOME**&#x200B;環境変数を強制的に指定します。

   ```
   export JDK_HOME=/usr/java/jdk1.6.0_07
   ```

   >[!NOTE]
   >
   >これは一例です。使用するJDKのバージョンがディレクトリ名と一致していることを確認してください。

   JDKの設定をテストするには、Adobe Campaignシステムユーザーとして次のコマンドでログインします。

   ```
   su - neolane
   ```

変更を考慮するには、Adobe Campaignサービスを再起動する必要があります。

コマンドは次のとおりです。

```
/etc/init.d/nlserver6 stop
/etc/init.d/nlserver6 start
```

20.1からは、代わりに次のコマンドを使用することをお勧めします。

```
systemctl stop nlserver
systemctl start nlserver
```

### Linuxのoracleクライアント{#oracle-client-in-linux}

Adobe CampaignでOracleを使用する場合は、LinuxでOracleクライアントレイヤーを設定する必要があります。

* フルクライアントを使用する
* TNSの定義

   TNS定義は、インストール段階で追加する必要があります。 これを行うには、次のコマンドを使用します。

   ```
   cd /etc
   mkdir oracle
   cd oracle
   vi tnsnames.ora
   ```

* 環境変数

   [環境変数](../../installation/using/installing-packages-with-linux.md#environment-variables)を参照してください。

* Adobe Campaignの設定

   Adobe Campaign用のOracleクライアントのインストールを終了するには、Adobe Campaignで使用する&#x200B;**.so**&#x200B;ファイルのシンボリックリンクを作成する必要があります。

   これを行うには、次のコマンドを使用します。

   ```
   cd /usr/lib/oracle/10.2.0.4/client/lib
   ln -s libclntsh.so.10.1 libclntsh.so
   ```

問題が発生した場合は、[Oracleのインストールドキュメント](https://www.oracle.com/pls/db112/portal.portal_db?selected=11)に記載されているパッケージが正しくインストールされていることを確認してください。

## インストールの確認{#installation-checks}

次のコマンドを使用して、初期インストールテストを実行できるようになりました。

```
su - neolane
nlserver pdump
```

Adobe Campaignが開始されていない場合の応答は次のとおりです。

```
no task
```

## サーバの最初の開始アップ{#first-start-up-of-the-server}

インストールテストが完了したら、次のコマンドを入力します。

```
nlserver web
```

次の情報が表示されます。

```
17:11:03 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
17:11:03 >   Web server start (pid=17546, tid=-151316352)...
17:11:03 >   Creating server configuration file '/usr/local/[INSTALL]/nl6/conf/serverConf.xml' via '/usr/local/[INSTALL]/nl6/conf/fra/serverConf.xml.sample'
17:11:03 >   Creating server configuration file '/usr/local/[INSTALL]/nl6/conf/config-default.xml' via '/usr/local/[INSTALL]/nl6/conf/models/config-default.xml'
17:11:03 >   Server started
17:11:08 >   Stop requested (pid=17546)
17:11:08 >   Web server stop(pid=17546, tid=-151316352)...
```

これらのコマンドを使用すると、**config-default.xml**&#x200B;および&#x200B;**serverConf.xml**&#x200B;の設定ファイルを作成できます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

**Ctrl+C**&#x200B;キーを押して処理を停止し、次のコマンドを入力します。

```
nlserver start web
```

次の情報が表示されます。

```
12:17:21 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:17:21 >   Running task 'web@default' ('nlserver web -tracefile:web@default -instance:default -detach -tomcat -autorepair') in a new process
12:17:21 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:17:21 >   Web server start (pid=29188, tid=-1224824320)...
12:17:21 >   Creating server configuration file '/usr/local/[INSTALL]/nl6/conf/serverConf.xml' via '/usr/local/[INSTALL]/nl6/conf/fra/serverConf.xml.sample'
12:17:22 >   Tomcat started
12:17:22 >   Server started
```

停止するには、次のように入力します。

```
nlserver stop web
```

次の情報が表示されます。

```
12:18:31 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:18:31 >   Stop requested for 'web@default' ('nlserver web -tracefile:web@default -instance:default -detach -tomcat -autorepair', pid=29188, tid=-1224824320)...
12:18:31 >   Stop requested (pid=29188)
12:18:31 >   Web server stopped (pid=29188, tid=-1224824320)...
```

## 内部識別子{#password-for-the-internal-identifier}のパスワード

Adobe Campaignサーバは、すべてのインスタンスに対してすべての権限を持つ、**internal**&#x200B;という技術的なログインを定義します。 インストール直後は、ログインにパスワードがありません。 定義する必要があります。

詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。
