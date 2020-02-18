---
title: Linuxでのパッケージのインストール
seo-title: Linuxでのパッケージのインストール
description: Linuxでのパッケージのインストール
seo-description: null
page-status-flag: never-activated
uuid: d83f00b5-500b-406a-a3d6-ea5639f244f0
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
discoiquuid: 04faa9f3-d160-4060-b26e-44333f2faf71
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: de04b5d3ceb883a571ee665f630be931a68a5a3e

---


# Linuxでのパッケージのインストール{#installing-packages-with-linux}

Linux 32ビットプラットフォームの場合は、Adobe Campaign 32ビットをインストールします。 Linux 64ビットプラットフォームの場合は、Adobe Campaign 64ビットをインストールします。

Adobe Campaignには、これらの各バージョンに対して1つのパッケージが付属しています。 **nlserver**。 このパッケージには、指定したバージョンのバイナリと設定ファイルが含まれています。

インストールコマンドを使用すると、次のことができます。

* ファイルを/usr/local/ **neolaneにコピーします。**
* Adobe Campaign linuxアカウント（および関連するグループ）を作成します。このアカウントは、 **/usr/local/neolaneをホームディレクトリとして** 作成します。
* 起動時に使用する自動 **スクリプト/etc/init.d/nlserver6** を作成するか、システムユニット（20.1以降）を作成します。

>[!NOTE]
>
>このコ **マンドを実行する前に** 、neolaneシステムユーザーを作成しておく必要はありません。 neolaneユー **ザーは** 、インストール時に自動的に作成されます。
>
>また、 **neolaneユーザーにリン** クされた **homeディレクトリも** 、で自動的に作成されま **[!UICONTROL /usr/local/neolane]**&#x200B;す。 ディスク上に十分な空き領域があることを確 **[!UICONTROL /usr/local]** 認してください（数GB）。

pingコマンドを実行して、 **サー`hostname`**バが自身にアクセスできることを確認できます。

## RPMパッケージに基づく配布 {#distribution-based-on-rpm--packages}

RPM（RHEL、CentOSおよびSUSE）オペレーティングシステムにAdobe Campaignをインストールするには、次の手順を適用します。

1. 最初にAdobe Campaignパッケージを入手する必要があります。

   ファイルの名前は次のとおりです。 **XXXX** はAdobe Campaignビルド番号です。

   * **nlserver6-v7-XXXX-0.x86_64.rpm** （v7の場合）。
   * **v6.1の場合は、nlserver6-XXXX-0.x86_64.rpm** 。
   >[!CAUTION]
   >
   >この節のコマンドサンプルで、お使いのバージョンのAdobe Campaignの正しいファイル名を使用してください。

1. インストールするには、 **root** として接続し、次のコマンドを実行します( **XXXX** はAdobe Campaignビルド番号です)。

   ```
   yum install nlserver6-v7-XXXX-0.x86_64.rpm
   ```

   rpmファイルは、CentOS/Red hatディストリビューションで見つけられるパッケージに依存しています。 これらの依存関係の一部を使用しない場合（例えば、OpenJDKではなくOracle JDKを使用する場合）、rpmの「nodeps」オプションを使用する必要がある場合があります。

   ```
   rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
   ```

「bc」コマンドは、ネットポートを実行するのに必要です(詳しくは [この節を参照](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts) )。デフォルトでは、すべてのLinuxディストリビューションで利用できません。 コマンドが使用可能かどうかを確認するには、&#39;which bc&#39;コマンドを実行します。 インストールされていない場合は、インストールする必要があります。

CentOSでは、bc.x86_64パッケージをインストールする必要があります。rootとして接 **続し** 、次のコマンドを実行します。

```
yum install bc.x86_64
```

## APTに基づく配布(Debian) {#distribution-based-on-apt--debian-}

### Debian 64ビット {#in-debian-64-bits}

Debian 64ビットオペレーティングシステムにAdobe Campaign 64ビットをインストールするには、次の手順を適用します。

1. 最初にAdobe Campaignパッケージを入手する必要があります。

   * **nlserver6-v7-XXXX-linux-2.6-amd64.deb** for v7.
   * **v6.1の場合は、nlserver6-XXXX-linux-2.6-amd64.deb** 。
   **XXXXは** 、Adobe Campaignのビルド番号です。

   >[!CAUTION]
   >
   >この節のコマンドサンプルで、お使いのバージョンのAdobe Campaignの正しいファイル名を使用してください。

1. インストールするには、 **root** として接続し、次のコマンドを実行します( **XXXX** はAdobe Campaignビルド番号です)。

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
* 次のコマンドを使用して、libicu52 (Debian 8)またはlibicu57 (Debian 9)、libprotobuf9 (Debian8)およびlibc-ares2をインストールします。

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

## パラメータのパーソナライズ {#personalizing-parameters}

一部のパラメーターは、 **customer.shファイルを使用してパーソナライズできます** 。

初めてインストールを実行する場合、 **customer.sh** ファイルがまだサーバーに存在しない可能性があります。 作成し、実行権限があることを確認します。 そうでない場合は、次のコマンドを入力します。

```
chmod +x /usr/local/neolane/nl6/customer.sh
```

### サーバーエンコーディング {#server-encoding}

デフォルトでは、サーバーはiso8859-15環境で起動されます。 ただし、UTF-8環境でサーバーを起動することはできます。

>[!CAUTION]
>
>この変更は、ファイルシステム（ワークフローまたはJavaScriptスクリプトを介して読み込まれたファイル）とのやり取りとファイルのエンコーディングに影響します。 したがって、デフォルトの環境を使用することをお勧めします。

ただし、日本語インスタ **ンスを作成する場合**、UTF-8環境を使用する必要があります。

UTF-8環境を有効にするには、次のコマンドを使用します。

```
mkdir -p /usr/local/neolane/nl6 
touch /usr/local/neolane/nl6/unicodeenv
```

### サーバーのデフォルト言語 {#default-language-for-the-server}

インストールでは、英語とフランス語の両方がサポートされます。 デフォルトでは英語が使用されます。

フランス語に切り替えるには、次のコマンドを入力します。

```
su - neolane
vi nl6/customer.sh
```

次の行を追加します。

```
export neolane_LANG=fra
```

システムメッセージが正しく読み取られるように、コンソールは言語に対応するコードページ（フランス語の場合はISO-8859-1または —15）にある必要があります。

### 環境変数 {#environment-variables}

次の環境変数を正しく定義する必要があります。

特定の組み合わせでは、Adobe Campaignの実行に使用する環境の変更が必要です。 特定のファイル(`/usr/local/neolane/nl6/customer.sh`)を作成および編集して、Adobe Campaign環境に固有の変更を追加できます。

必要に応じて、 **vi customer.sh** コマンドを使用してcustomer.sh **** ファイルを編集し、設定を調整するか、行を追加します。

* Oracleクライアントの場合：

   ```
   export ORACLE_HOME=/usr/local/instantclient_10_2
   export TNS_ADMIN=/etc/oracle
   export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH 
   ```

   ORACLE_HOME環境変数の内容は、Oracleインストール・ディレクトリと一致します。

   TNS_ADMIN変数の内容は、tnsnames.oraファイルの場所と一致する必要 **があります** 。

* LibreOfficeの場合：

   既存のバージョンのLibreOfficeでAdobe Campaignを実行するには、次の追加設定が必要です。インストールディレクトリへのアクセスパスを指定する必要があります。 例：

   * デビアン

      OOO_INSTALL_DIR、OOO_BASIS_INSTALL_DIR、OOO_URE_INSTALL_DIRのデフォルト値が提供されます。 LibreOfficeのインストールレイアウトが異な **る場合は** 、customer.shでこれらを上書きできます。

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

   デフォルトでは、Adobe Campaign環境(`~/nl6/env.sh`)の設定スクリプトはJDKのインストールディレクトリを検索します。 この動作は100%の信頼性がないので、使用する必要のあるJDKを指定する必要があります。 これを行うには、次のコマンドを使用し **てJDK_HOME** 環境変数を強制的に設定します。

   ```
   export JDK_HOME=/usr/java/jdk1.6.0_07
   ```

   >[!NOTE]
   >
   >これは一例です。使用するJDKのバージョンがディレクトリ名と一致することを確認します。

   JDK設定をテストするには、次のコマンドを使用してAdobe Campaignシステムユーザーとしてログインします。

   ```
   su - neolane
   ```

変更を反映するには、Adobe Campaignサービスを再起動する必要があります。

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

### LinuxのOracleクライアント {#oracle-client-in-linux}

Adobe CampaignでOracleを使用する場合は、LinuxでOracleクライアントレイヤーを設定する必要があります。

* フルクライアントの使用
* TNS定義

   TNS定義は、インストール段階で追加する必要があります。 これを行うには、次のコマンドを使用します。

   ```
   cd /etc
   mkdir oracle
   cd oracle
   vi tnsnames.ora
   ```

* 環境変数

   環境変数を [参照](../../installation/using/installing-packages-with-linux.md#environment-variables)。

* Adobe Campaignの設定

   Adobe Campaign用のOracleクライアントのインストールを完了するには、Adobe Campaignで使用する **.so** fileのシンボリックリンクを作成する必要があります。

   これを行うには、次のコマンドを使用します。

   ```
   cd /usr/lib/oracle/10.2.0.4/client/lib
   ln -s libclntsh.so.10.1 libclntsh.so
   ```

問題が発生した場合は、 [Oracleインストールドキュメントに記載されているパッケージが正しくインストールされてい](https://www.oracle.com/pls/db112/portal.portal_db?selected=11) ることを確認してください。

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

## サーバーの初回起動 {#first-start-up-of-the-server}

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

これらのコマンドを使用す **ると、config-default.xml** および **serverConf.xml設定ファイルを作成できます** 。 serverConf.xmlで使用可能なすべてのパ **ラメーターを** 、この節に示 [します](../../installation/using/the-server-configuration-file.md)。

Ctrl + cキ **ーを押して** 、処理を停止し、次のコマンドを入力します。

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

これを停止するには、次のように入力します。

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

Adobe Campaignサーバーは、すべてのインスタンスに対してすべての権限を持つ **internal** （内部）と呼ばれる技術的なログインを定義します。 インストール直後に、ログインにパスワードが設定されていません。 1つを定義する必要があります。

内部識別子を参 [照してください](../../installation/using/campaign-server-configuration.md#internal-identifier)。
