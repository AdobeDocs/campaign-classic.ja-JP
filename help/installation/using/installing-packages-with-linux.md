---
title: Linux でのパッケージのインストール
seo-title: Linux でのパッケージのインストール
description: Linux でのパッケージのインストール
seo-description: null
page-status-flag: never-activated
uuid: d83f00b5-500b-406a-a3d6-ea5639f244f0
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
discoiquuid: 04faa9f3-d160-4060-b26e-44333f2faf71
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 2%

---


# Linux でのパッケージのインストール{#installing-packages-with-linux}

Linux 32ビットプラットフォームの場合は、Adobe Campaign32ビットをインストールします。 Linux 64ビットプラットフォームの場合は、Adobe Campaign64ビットをインストールします。

これらの各バージョンに対して、Adobe Campaignには次のパッケージが1つ付属しています。 **nlserver**. このパッケージには、特定のバージョンのバイナリと設定ファイルが含まれています。

インストールコマンドを使用すると、次のことができます。

* ファイルを **/usr/local/neolaneにコピーします。**
* Adobe CampaignのLinuxアカウント（および関連するグループ）を作成します。このアカウントは、 **/usr/local/neolane** をホームディレクトリとして作成します。
* 起動時に使用する自動スクリプト/etc/init.d **/nlserver6** を作成するか、システムユニットを作成します（20.1以降）。

>[!NOTE]
>
>コマンドを実行する前に **neolane** system userを作成しておく必要はありません。 **Neolane** ユーザーは、インストール時に自動的に作成されます。
>
>また、 **neolane** ユーザにリンクされた **ホームディレクトリは、** /usr/local/neolaneに自動的に作成されます ****。 /usr/local **[!UICONTROL ディスクに十分な空き容量（数GB）があることを確認してください]** 。

サーバが自身にアクセスできることを確認するには、 **ping`hostname`** コマンドを実行します。

## RPMパッケージに基づく配布 {#distribution-based-on-rpm--packages}

RPM（RHEL、CentOS、およびSUSE）オペレーティングシステムにAdobe Campaignをインストールするには、次の手順を実行します。

1. 最初にAdobe Campaignパッケージを入手する必要があります。

   ファイルの名前は次のとおりです。 **XXXX** はAdobe Campaignビルド番号です。

   * **nlserver6-v7-XXXX-0.x86_64.rpm** （v7の場合）
   * **v6.1では、nlserver6-XXXX-0.x86_64.rpm** 。

   >[!CAUTION]
   >
   >この節のコマンドサンプルで、ご使用のAdobe Campaignのバージョンに適したファイル名を使用していることを確認してください。

1. インストールするには、 **rootとして接続し** 、次のコマンドを実行します( **XXXX** はAdobe Campaignビルド番号)。

   ```
   yum install nlserver6-v7-XXXX-0.x86_64.rpm
   ```

   rpmファイルはCentOS/Red Hatディストリビューションで見つけられるパッケージに依存しています。 これらの依存関係の一部を使用しない場合（例えば、OpenJDKではなくOracle JDKを使用する場合）、rpmの「nodeps」オプションを使用する必要がある場合があります。

   ```
   rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
   ```

ネットポートの実行に必要な&#39;bc&#39;コマンド(詳細は [この節を参照](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts) )は、デフォルトでは全てのLinuxディストリビューションで利用できません。 コマンドが使用可能かどうかを確認するには、&#39;which bc&#39;コマンドを実行します。 インストールされていない場合は、インストールする必要があります。

CentOSを使う場合は、bc.x86_64パッケージをインストールする必要があります。root **として接続し** 、次のコマンドを実行します。

```
yum install bc.x86_64
```

## APTに基づく配布(Debian) {#distribution-based-on-apt--debian-}

### Debian 64ビット {#in-debian-64-bits}

64ビットのAdobe CampaignをDebian 64ビットのオペレーティングシステムにインストールするには、次の手順を適用します。

1. 最初にAdobe Campaignパッケージを入手する必要があります。

   * **nlserver6-v7-XXXX-linux-2.6-amd64.deb** for v7
   * **v6.1では、nlserver6-XXXX-linux-2.6-amd64.deb** 。

   **XXXX** :Adobe Campaignビルド番号です。

   >[!CAUTION]
   >
   >この節のコマンドサンプルで、ご使用のAdobe Campaignのバージョンに適したファイル名を使用していることを確認してください。

1. インストールするには、 **rootとして接続し** 、次のコマンドを実行します( **XXXX** はAdobe Campaignビルド番号)。

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

## パラメータの個人化 {#personalizing-parameters}

一部のパラメーターは、 **customer.sh** ファイルを使用してパーソナライズできます。

初めてインストールを実行する場合、 **customer.sh** ファイルがまだサーバーに存在しない可能性があります。 作成し、実行権限があることを確認します。 そうでない場合は、次のコマンドを入力します。

```
chmod +x /usr/local/neolane/nl6/customer.sh
```

### サーバーエンコーディング {#server-encoding}

デフォルトでは、iso8859-15環境でサーバーが起動します。 ただし、UTF-8環境でサーバーを起動できます。

>[!CAUTION]
>
>この変更は、ファイルシステム（ワークフローまたはJavaScriptスクリプトを介して読み込まれたファイル）とのやり取りとファイルエンコーディングに影響します。 したがって、デフォルトの環境を使用することをお勧めします。

ただし、 **日本語インスタンスを作成する場合は**、UTF-8環境を使用する必要があります。

UTF-8環境を有効にするには、次のコマンドを使用します。

```
mkdir -p /usr/local/neolane/nl6 
touch /usr/local/neolane/nl6/unicodeenv
```

### サーバーのデフォルト言語 {#default-language-for-the-server}

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

必要に応じて、 **customer.sh** ファイルを **vi customer.sh** コマンドを使用して編集し、設定を調整するか、行を追加します。

* Oracleクライアントの場合：

   ```
   export ORACLE_HOME=/usr/local/instantclient_10_2
   export TNS_ADMIN=/etc/oracle
   export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH 
   ```

   ORACLE_HOME環境変数の内容は、Oracleインストール・ディレクトリと一致します。

   TNS_ADMIN変数の内容は、tnsnames.ora **** ファイルの場所と一致する必要があります。

* LibreOfficeの場合：

   既存のバージョンのLibreOfficeでAdobe Campaignを実行するには、次の追加設定が必要です。インストールディレクトリへのアクセスパスを指定する必要があります。 例えば、次のようにします。

   * Debian

      OO_INSTALL_DIR、OO_BASIS_INSTALL_DIR、OO_URE_INSTALL_DIRのデフォルト値が提供されます。 LibreOfficeのインストールレイアウトが異なる場合は、 **customer.sh** :

      ```
      export OOO_BASIS_INSTALL_DIR=/usr/lib/libreoffice/ 
      export OOO_INSTALL_DIR=/usr/lib/libreoffice/
      export OOO_URE_INSTALL_DIR=/usr/lib/ure/share/
      ```

   * CentOs

      次のデフォルト値を使用します。

      ```
      export OOO_BASIS_INSTALL_DIR=/usr/lib64/libreoffice/
      export OOO_INSTALL_DIR=/usr/lib64/libreoffice/
      export OOO_URE_INSTALL_DIR=/usr/lib64/libreoffice/ure/share/
      ```

* Java開発キット(JDK)の場合：

   デフォルトでは、Adobe Campaign環境(`~/nl6/env.sh`)の設定スクリプトはJDKのインストールディレクトリを検索します。 この動作は100%信頼性が低いので、使用するJDKを指定する必要があります。 これを行うには、次のコマンドを使用して **JDK_HOME** 環境変数を強制的に設定します。

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

### LinuxでのOracleクライアント {#oracle-client-in-linux}

Adobe CampaignでOracleを使用する場合、LinuxでOracleクライアントレイヤーを設定する必要があります。

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

   「 [環境変数](../../installation/using/installing-packages-with-linux.md#environment-variables)」を参照してください。

* Adobe Campaignの設定

   Adobe Campaign用のOracleクライアントのインストールを終了するには、Adobe Campaignが使用する **.so** ファイルのシンボリック・リンクを作成する必要があります。

   これを行うには、次のコマンドを使用します。

   ```
   cd /usr/lib/oracle/10.2.0.4/client/lib
   ln -s libclntsh.so.10.1 libclntsh.so
   ```

問題が発生した場合は、 [Oracleインストールマニュアルに記載されているパッケージが正しくインストールされていることを確認し](https://www.oracle.com/pls/db112/portal.portal_db?selected=11) 、

## インストールの確認 {#installation-checks}

次のコマンドを使用して、初期インストールテストを実行できるようになりました。

```
su - neolane
nlserver pdump
```

Adobe Campaignが開始されていない場合の応答は次のとおりです。

```
no task
```

## サーバーの最初の開始アップ {#first-start-up-of-the-server}

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

これらのコマンドを使用して、 **config-default.xml** 設定ファイルと **** serverConf.xml設定ファイルを作成できます。 serverConf.xmlで使用可能なすべてのパラメ **ーターをこの** 節に示します [](../../installation/using/the-server-configuration-file.md)。

Ctrl **** +Cを押して処理を停止し、次のコマンドを入力します。

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

## 内部識別子のパスワード {#password-for-the-internal-identifier}

Adobe Campaignサーバは、すべてのインスタンスに対してすべての権限を持つ **internal** という技術的なログインを定義します。 インストール直後は、ログインにパスワードがありません。 定義する必要があります。

「 [内部識別子](../../installation/using/campaign-server-configuration.md#internal-identifier)」を参照してください。
