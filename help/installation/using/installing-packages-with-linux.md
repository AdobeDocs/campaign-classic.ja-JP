---
product: campaign
title: Linux でのパッケージのインストール
description: Linux でのパッケージのインストール
feature: Installation, Application Settings
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: f41c7510-5ad7-44f3-9485-01f54994b6cb
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 1%

---

# Linux でのパッケージのインストール{#installing-packages-with-linux}



Linux 32 ビットプラットフォームの場合は、Adobe Campaign 32 ビットをインストールします。 Linux 64 ビットプラットフォームの場合は、Adobe Campaign 64 ビットをインストールします。

Adobe Campaignには、これらのバージョンごとに 1 つのパッケージが用意されています。 **nlserver**. このパッケージには、特定のバージョンのバイナリと設定ファイルが含まれています。

インストールコマンドを使用すると、次のことができます。

* ファイルをにコピーします **/usr/local/neolane**
* で作成されるAdobe Campaign Linux アカウント（および関連するグループ）を作成します。 **/usr/local/neolane** ホームディレクトリとして
* 自動スクリプトの作成 **/etc/init.d/nlserver6** 起動時に使用する場合、または systemd ユニットを作成します（20.1 以降）。

>[!NOTE]
>
>この **ネオラン** コマンドを実行する前に、システム ユーザーを作成しないでください。 この **ネオラン** ユーザーはインストール時に自動的に作成されます。
>
>この **ホーム** にリンクされているディレクトリ **ネオラン** ユーザーはでも自動的に作成されます **[!UICONTROL /usr/local/neolane]**. に十分なスペースがあることを確認してください。 **[!UICONTROL /usr/local]** ディスク（数 GB）。

を実行できます **ping`hostname`** コマンドを使用して、サーバーが自分自身に到達できることを確認します。

## RPM パッケージに基づく配布 {#distribution-based-on-rpm--packages}

Adobe Campaignを RPM （RHEL、CentOS および SUSE）オペレーティングシステムにインストールするには、次の手順に従います。

1. 最初にAdobe Campaign パッケージを取得する必要があります。

   ファイルの名前は次のようになります。 **XXXX** はAdobe Campaignのビルド番号です。 **nlserver6-v7-XXXX-0.x86_64.rpm**.

   >[!CAUTION]
   >
   >この節のコマンドサンプルでは、使用しているAdobe Campaignのバージョンに適したファイル名を使用していることを確認してください。

1. インストールするには、として接続します **root** さらに、次のコマンドを実行します（このコマンドの条件は、 **XXXX** はAdobe Campaignのビルド番号です）。

   ```
   yum install nlserver6-v7-XXXX-0.x86_64.rpm
   ```

   rpm ファイルは、CentOS/Red Hat ディストリビューションで見つけることができるパッケージに依存しています。 これらの依存関係の一部を使用しない場合（例えば、OpenJDK ではなくOracle JDK を使用する場合）、rpm の「nodeps」オプションを使用する必要がある可能性があります。

   ```
   rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
   ```

netreport の実行に必要な「bc」コマンド（を参照） [この節](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts) 詳しくは、を参照してください）。は、すべての Linux ディストリビューションでデフォルトでは使用できません。 コマンドが使用可能かどうかを確認するには、「which bc」コマンドを実行します。 そうでない場合は、インストールする必要があります。

CentOS では、bc.x86_64 パッケージをインストールする必要があります。connect as **root** さらに、次のコマンドを実行します。

```
yum install bc.x86_64
```

## APT （Debian）に基づく配布 {#distribution-based-on-apt--debian-}

### Debian 64 ビット {#in-debian-64-bits}

Adobe Campaign 64 ビットを Debian 64 ビットオペレーティングシステムにインストールするには、次の手順に従います。

1. 最初にAdobe Campaign パッケージを取得する必要があります。 **nlserver6-v7-XXXX-linux-2.6-amd64.deb**、ここで **XXXX** はビルド番号です。

   >[!CAUTION]
   >
   >この節のコマンドサンプルでは、使用しているAdobe Campaignのバージョンに適したファイル名を使用していることを確認してください。

1. インストールするには、として接続します **root** さらに、次のコマンドを実行します（このコマンドの条件は、 **XXXX** はAdobe Campaignのビルド番号です）。

   ```
   dpkg -i nlserver6-v7-XXXX-linux-2.6-amd64.deb
   ```

   依存関係がない場合は、次のコマンドを実行します。

   ```
   apt-get install -f
   ```

**Debian 8/9 の詳細**

Debian 8/9 オペレーティングシステムにAdobe Campaignをインストールする場合は、次の点を考慮してください。

* 事前に OpenSSL をインストールしておく必要があります。
* libicu52 （Debian 8）または libicu57 （Debian 9）、libprotobuf9 （Debian8）および libc-ares2 を、次のコマンドでインストールします。

  ```
  aptitude install libicu52 (Debian 8) libicu57 (Debian 9)
  ```

  ```
  aptitude install libc-ares2
  ```

  ```
  aptitude install libprotobuf9 (only Debian 8)
  ```

* 次のコマンドで JDK7 をインストールします。

  ```
  aptitude install openjdk-7-jdk (Debian 8)
  ```

  ```
  aptitude install openjdk-7-jdk (Debian 9)
  ```

## パラメーターのパーソナライズ {#personalizing-parameters}

一部のパラメーターは、 **customer.sh** ファイル

初めてインストールを実行する場合は、 **customer.sh** ファイルがまだサーバーに存在しない可能性があります。 作成し、実行権限があることを確認します。 これに該当しない場合は、次のコマンドを入力します。

```
chmod +x /usr/local/neolane/nl6/customer.sh
```

### サーバーエンコーディング {#server-encoding}

デフォルトでは、サーバーは iso8859-15 環境で起動されます。 ただし、サーバーは UTF-8 環境で起動できます。

>[!CAUTION]
>
>この変更は、ファイルシステム（ワークフローまたは JavaScript スクリプトを使用して読み込まれたファイル）とのインタラクションと、ファイルエンコーディングに影響を与えます。 そのため、デフォルトの環境を使用することをお勧めします。

ただし、を作成する場合は **日本語インスタンス**&#x200B;は、UTF-8 環境を使用する必要があります。

UTF-8 環境を有効にするには、次のコマンドを使用します。

```
mkdir -p /usr/local/neolane/nl6 
touch /usr/local/neolane/nl6/unicodeenv
```

### サーバーのデフォルト言語 {#default-language-for-the-server}

インストールは英語とフランス語の両方をサポートしています。 デフォルトでは、英語が使用されます。

フランス語に切り替えるには、次のコマンドを入力します。

```
su - neolane
vi nl6/customer.sh
```

さらに、次の行を追加します。

```
export neolane_LANG=fra
```

システムメッセージが正しく読まれるようにするために、コンソールは言語に対応するコードページ（フランス語の場合は ISO-8859-1 または–15）に配置する必要があります。

### 環境変数 {#environment-variables}

次の環境変数を正しく定義する必要があります。

特定の組み合わせでは、Adobe Campaignの実行に使用する環境を変更する必要があります。 特定のファイル （`/usr/local/neolane/nl6/customer.sh`）を作成および編集して、Adobe Campaign環境に固有の変更を追加できます。

必要に応じて、 **customer.sh** を使用したファイル **vi customer.sh** コマンドを実行して設定を調整するか、不足している行を追加します。

* oracleクライアントの場合：

  ```
  export ORACLE_HOME=/usr/local/instantclient_10_2
  export TNS_ADMIN=/etc/oracle
  export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH 
  ```

  oracle変数 ENVIRONMENT_HOME の内容は、Oracleのインストールディレクトリと一致します。

  TNS_ADMIN 変数の内容は、の場所と一致する必要があります。 **tnsnames.ora** ファイル。

* LibreOffice:

  既存バージョンの LibreOffice でAdobe Campaignを実行するには、さらに設定が必要です。インストールディレクトリへのアクセスパスを指定する必要があります。 次に例を示します。

   * Debian

     OOO_INSTALL_DIR と OOO_BASIS_INSTALL_DIR のデフォルト値が提供されます。 以下で上書きできます **customer.sh** libreOffice インストールのレイアウトが異なる場合：

     ```
     export OOO_BASIS_INSTALL_DIR=/usr/lib/libreoffice/ 
     export OOO_INSTALL_DIR=/usr/lib/libreoffice/
     ```

   * CentOS

     次のデフォルト値を使用します。

     ```
     export OOO_BASIS_INSTALL_DIR=/usr/lib64/libreoffice/
     export OOO_INSTALL_DIR=/usr/lib64/libreoffice/
     ```

* Java Development Kit （JDK）の場合：

  デフォルトでは、Adobe Campaign環境の設定スクリプト （`~/nl6/env.sh`）を選択して、JDK インストールディレクトリを検索します。 この動作は 100% 信頼できないので、使用する JDK を指定する必要があります。 それには、以下を強制します **JDK_HOME** 次のコマンドを使用する環境変数。

  ```
  export JDK_HOME=/usr/java/jdk1.6.0_07
  ```

  >[!NOTE]
  >
  >これは一例です。使用する JDK バージョンがディレクトリ名と一致することを確認します。

  JDK 設定をテストするには、次のコマンドでAdobe Campaign システムユーザーとしてログインします。

  ```
  su - neolane
  ```

変更内容を反映するには、Adobe Campaign サービスを再起動する必要があります。

コマンドは次のとおりです。

```
/etc/init.d/nlserver6 stop
/etc/init.d/nlserver6 start
```

20.1 以降は、代わりに次のコマンドを使用することをお勧めします。

```
systemctl stop nlserver
systemctl start nlserver
```

### Linux のOracleクライアント {#oracle-client-in-linux}

Adobe CampaignでOracleを使用する場合、Linux でOracleクライアントレイヤーを設定する必要があります。

* 完全なクライアントを使用
* TNS の定義

  TNS 定義は、インストール段階で追加する必要があります。 これを行うには、次のコマンドを使用します。

  ```
  cd /etc
  mkdir oracle
  cd oracle
  vi tnsnames.ora
  ```

* 環境変数

  こちらを参照してください [環境変数](../../installation/using/installing-packages-with-linux.md#environment-variables).

* Adobe Campaignの設定

  Adobe CampaignのOracleクライアントのインストールを完了するには、のシンボリックリンクを作成する必要があります **.so** Adobe Campaignが使用するファイル。

  これを行うには、次のコマンドを使用します。

  ```
  cd /usr/lib/oracle/10.2.0.4/client/lib
  ln -s libclntsh.so.10.1 libclntsh.so
  ```

問題が発生した場合は、にリストされているパッケージを確認します [Oracleインストールドキュメント](https://docs.oracle.com/) が正しくインストールされている。

## インストールチェック {#installation-checks}

これで、次のコマンドを使用して初期インストールテストを実行できます。

```
su - neolane
nlserver pdump
```

Adobe Campaignを起動しない場合の応答は次のとおりです。

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

これらのコマンドを使用すると、以下を作成できます **config-default.xml** および **serverConf.xml** 設定ファイル。 で使用できるすべてのパラメーター **serverConf.xml** の一覧はこちら [セクション](../../installation/using/the-server-configuration-file.md).

押す **Ctrl+C** プロセスを停止するには、次のコマンドを入力します。

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

Adobe Campaign サーバーは、というテクニカルログインを定義します。 **内部** すべてのインスタンスに対してすべての権限を持っています。 インストール直後は、ログインにパスワードがありません。 定義する必要があります。

詳しくは、[こちら](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。
