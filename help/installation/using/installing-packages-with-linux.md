---
product: campaign
title: Linux でのパッケージのインストール
description: Linux でのパッケージのインストール
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: f41c7510-5ad7-44f3-9485-01f54994b6cb
source-git-commit: 32f55d02920b0104198f809b1be0a91306a4d9e4
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---

# Linux でのパッケージのインストール{#installing-packages-with-linux}

![](../../assets/v7-only.svg)

Linux 32ビットプラットフォームの場合は、Adobe Campaign 32ビットをインストールします。 Linux 64ビットプラットフォームの場合は、Adobe Campaign 64ビットをインストールします。

Adobe Campaignには、これらのバージョンごとに1つのパッケージが付属しています。**nlserver**&#x200B;を呼び出します。 このパッケージには、特定のバージョンのバイナリと設定ファイルが含まれます。

インストールコマンドを使用すると、次の操作を実行できます。

* ファイルを&#x200B;**/usr/local/neolane**&#x200B;にコピーします。
* **/usr/local/neolane**&#x200B;をホームディレクトリとして使用して作成されたAdobe Campaign Linuxアカウント（および関連するグループ）を作成します。
* 起動時に使用する自動スクリプト&#x200B;**/etc/init.d/nlserver6**&#x200B;を作成するか、systemdユニットを作成します（20.1以降）。

>[!NOTE]
>
>**neolane**&#x200B;システムユーザーは、コマンドを実行する前に作成してはいけません。 **neolane**&#x200B;ユーザーは、インストール中に自動的に作成されます。
>
>**neolane**&#x200B;ユーザーにリンクされた&#x200B;**home**&#x200B;ディレクトリも&#x200B;**[!UICONTROL /usr/local/neolane]**&#x200B;に自動的に作成されます。 **[!UICONTROL /usr/local]**&#x200B;ディスクに十分な空き領域があることを確認してください（数GB）。

**ping`hostname`**&#x200B;コマンドを実行して、サーバーが自身に到達できることを確認できます。

## RPMパッケージに基づく配布 {#distribution-based-on-rpm--packages}

Adobe CampaignをRPM(RHEL、CentOS、SUSE)オペレーティングシステムにインストールするには、次の手順に従います。

1. 最初に、Adobe Campaignパッケージを入手する必要があります。

   ファイルの名前は次のようになります。 **XXXX**&#x200B;はAdobe Campaignのビルド番号です。

   * **nlserver6-v7-XXXX-0.x86_64.rpmfor v7** の場合。
   * **nlserver6-XXXX-0.x86_64.rpmfor v6.1** の場合は次のようになります。

   >[!CAUTION]
   >
   >この節のコマンドサンプルで、ご使用のバージョンのAdobe Campaignに対して正しいファイル名を使用していることを確認してください。

1. インストールするには、**root**&#x200B;として接続し、次のコマンドを実行します(**XXXX**&#x200B;はAdobe Campaignのビルド番号です)。

   ```
   yum install nlserver6-v7-XXXX-0.x86_64.rpm
   ```

   rpmファイルは、CentOS/Red Hatディストリビューションで見つけられるパッケージに依存しています。 これらの依存関係の一部を使用しない場合(例えば、OpenJDKの代わりにOracleJDKを使用する場合)、rpmの「nodeps」オプションを使用する必要がある場合があります。

   ```
   rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
   ```

ネットポートの実行に必要な&#39;bc&#39;コマンド（詳しくは[この節](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts)を参照）は、デフォルトではすべてのLinuxディストリビューションで使用できません。 コマンドが使用可能かどうかを確認するには、&#39;which bc&#39;コマンドを実行します。 そうでない場合は、インストールする必要があります。

CentOSを使用する場合は、bc.x86_64パッケージをインストールする必要があります。**root**&#x200B;として接続し、次のコマンドを実行します。

```
yum install bc.x86_64
```

## APT(Debian)に基づく配布 {#distribution-based-on-apt--debian-}

### Debian 64ビットの場合 {#in-debian-64-bits}

Adobe Campaign 64ビットをDebian 64ビットオペレーティングシステムにインストールするには、次の手順に従います。

1. 最初に、Adobe Campaignパッケージを入手する必要があります。

   * **nlserver6-v7-XXXX-linux-2.6-amd64.** debfor v7.
   * **nlserver6-XXXX-linux-2.6-amd64.** debfor v6.1

   **** XXXXはAdobe Campaignのビルド番号です。

   >[!CAUTION]
   >
   >この節のコマンドサンプルで、ご使用のバージョンのAdobe Campaignに対して正しいファイル名を使用していることを確認してください。

1. インストールするには、**root**&#x200B;として接続し、次のコマンドを実行します(**XXXX**&#x200B;はAdobe Campaignのビルド番号です)。

   ```
   dpkg -i nlserver6-v7-XXXX-linux-2.6-amd64.deb
   ```

   依存関係が見つからない場合は、次のコマンドを実行します。

   ```
   apt-get install -f
   ```

**Debian 8/9の詳細**

Debian 8/9オペレーティングシステムにAdobe Campaignをインストールする場合は、次の点を考慮してください。

* 事前にOpenSSLをインストールしておく必要があります。
* 次のコマンドを使用して、libicu52(Debian 8)またはlibicu57(Debian 9)、libprotobuf9(Debian8)およびlibc-ares2をインストールします。

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

## パラメーターのパーソナライズ {#personalizing-parameters}

一部のパラメーターは、**customer.sh**&#x200B;ファイルを使用してパーソナライズできます

初めてインストールを実行する場合は、**customer.sh**&#x200B;ファイルがまだサーバーに存在していない可能性があります。 作成し、実行権限があることを確認します。 そうでない場合は、次のコマンドを入力します。

```
chmod +x /usr/local/neolane/nl6/customer.sh
```

### サーバーエンコーディング {#server-encoding}

デフォルトでは、サーバーはiso8859-15環境で起動されます。 ただし、サーバーはUTF-8環境で起動できます。

>[!CAUTION]
>
>この変更は、ファイルシステム（ワークフローまたはJavaScriptスクリプトを使用して読み込まれたファイル）とのやり取りと、ファイルのエンコーディングに影響します。 したがって、デフォルトの環境を使用することをお勧めします。

ただし、**日本語インスタンス**&#x200B;を作成する場合は、UTF-8環境を使用する必要があります。

UTF-8環境を有効にするには、次のコマンドを使用します。

```
mkdir -p /usr/local/neolane/nl6 
touch /usr/local/neolane/nl6/unicodeenv
```

### サーバーのデフォルト言語 {#default-language-for-the-server}

英語とフランス語の両方をサポートしています。 デフォルトでは英語が使用されます。

フランス語に切り替えるには、次のコマンドを入力します。

```
su - neolane
vi nl6/customer.sh
```

次の行を追加します。

```
export neolane_LANG=fra
```

システムメッセージを正しく読み取るには、コンソールをその言語に対応するコードページ（フランス語の場合はISO-8859-1または —15）に配置する必要があります。

### 環境変数 {#environment-variables}

次の環境変数を正しく定義する必要があります。

特定の組み合わせでは、Adobe Campaignの実行に使用する環境を変更する必要があります。 特定のファイル(`/usr/local/neolane/nl6/customer.sh`)を作成および編集して、Adobe Campaign環境に固有の変更を追加できます。

必要に応じて、 **customer.sh**&#x200B;ファイルを&#x200B;**vi customer.sh**&#x200B;コマンドを使用して編集し、設定を調整するか、見つからない行を追加します。

* oracle・クライアントの場合：

   ```
   export ORACLE_HOME=/usr/local/instantclient_10_2
   export TNS_ADMIN=/etc/oracle
   export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH 
   ```

   環境変数content_HOMEの内容は、ORACLEのインストールディレクトリにOracleします。

   TNS_ADMIN変数の内容は、**tnsnames.ora**&#x200B;ファイルの場所と一致する必要があります。

* LibreOfficeの場合：

   既存のバージョンのLibreOfficeでAdobe Campaignを実行するには、追加の設定が必要です。インストールディレクトリへのアクセスパスを指定する必要があります。 例：

   * Debian

      OOO_INSTALL_DIR、OOO_BASIS_INSTALL_DIR、OOO_URE_INSTALL_DIRのデフォルト値が提供されます。 LibreOfficeインストールのレイアウトが異なる場合は、 **customer.sh**&#x200B;で上書きできます。

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

   デフォルトでは、Adobe Campaign環境の設定スクリプト(`~/nl6/env.sh`)は、JDKインストールディレクトリを検索します。 この動作は100%の信頼性がないので、使用する必要のあるJDKを指定する必要があります。 これを行うには、次のコマンドを使用して、**JDK_HOME**&#x200B;環境変数を強制的に指定します。

   ```
   export JDK_HOME=/usr/java/jdk1.6.0_07
   ```

   >[!NOTE]
   >
   >これは一例です。使用するJDKのバージョンがディレクトリ名と一致していることを確認します。

   JDKの設定をテストするには、次のコマンドを使用して、Adobe Campaignシステムユーザーとしてログインします。

   ```
   su - neolane
   ```

変更を反映するには、Adobe Campaignサービスを再起動する必要があります。

コマンドは次のとおりです。

```
/etc/init.d/nlserver6 stop
/etc/init.d/nlserver6 start
```

20.1以降では、代わりに次のコマンドを使用することをお勧めします。

```
systemctl stop nlserver
systemctl start nlserver
```

### Linuxのoracleクライアント {#oracle-client-in-linux}

Adobe CampaignでOracleを使用する場合は、LinuxでOracleクライアントレイヤーを設定する必要があります。

* 完全なクライアントの使用
* TNSの定義

   TNS定義は、インストールフェーズで追加する必要があります。 これを行うには、次のコマンドを使用します。

   ```
   cd /etc
   mkdir oracle
   cd oracle
   vi tnsnames.ora
   ```

* 環境変数

   [環境変数](../../installation/using/installing-packages-with-linux.md#environment-variables)を参照してください。

* Adobe Campaignの設定

   Adobe Campaign用のOracleクライアントのインストールを完了するには、Adobe Campaignで使用する&#x200B;**.so**&#x200B;ファイルのシンボリックリンクを作成する必要があります。

   これを行うには、次のコマンドを使用します。

   ```
   cd /usr/lib/oracle/10.2.0.4/client/lib
   ln -s libclntsh.so.10.1 libclntsh.so
   ```

問題が発生した場合は、[Oracleのインストールに関するドキュメント](https://docs.oracle.com/)に記載されているパッケージが正しくインストールされていることを確認してください。

## インストールの確認 {#installation-checks}

次のコマンドを使用して、初期インストールテストを実行できます。

```
su - neolane
nlserver pdump
```

Adobe Campaignが起動されていない場合の応答は次のようになります。

```
no task
```

## サーバーの最初の起動 {#first-start-up-of-the-server}

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

これらのコマンドを使用して、**config-default.xml**&#x200B;および&#x200B;**serverConf.xml**&#x200B;設定ファイルを作成できます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に記載されています。

**Ctrl+C**&#x200B;キーを押してプロセスを停止し、次のコマンドを入力します。

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

Adobe Campaignサーバーは、すべてのインスタンスに対するすべての権限を持つ、**内部**&#x200B;というテクニカルログインを定義します。 インストール直後に、ログインにパスワードが含まれていません。 定義する必要があります。

詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。
