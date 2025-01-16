---
product: campaign
title: Linux でのパッケージのインストール
description: Linux でのパッケージのインストール
feature: Installation, Application Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: f41c7510-5ad7-44f3-9485-01f54994b6cb
source-git-commit: ab38c7fd45513c6f7a8ecf7ef8601f0b5a4b5757
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 2%

---

# Linux でのパッケージのインストール {#installing-packages-with-linux}

Adobe Campaignには、特定のバージョンのバイナリと設定ファイルを含む **nlserver** パッケージが付属しています。

インストールコマンドを使用すると、次のことができます。

* ファイルを **/usr/local/neolane にコピーします**
* Adobe Campaign Linux アカウント（および関連するグループ）を作成します。このアカウントは **/usr/local/neolane** をホームディレクトリとして作成されます
* 起動時に使用する自動スクリプト **/etc/init.d/nlserver6** を作成するか、または systemd ユニットを作成します

>[!NOTE]
>
>コマンドを実行する前に、**neolane** システム ユーザーを作成しないでください。 **neolane** ユーザーは、インストール時に自動的に作成されます。
>
>**neolane** ユーザーにリンクされている **home** ディレクトリも **[!UICONTROL /usr/local/neolane]** に自動的に作成されます。 **[!UICONTROL /usr/local]** ディスクに十分な空き容量があることを確認してください。

**ping`hostname`** コマンドを実行すると、サーバーが自分自身に到達できることを確認できます。

## RPM パッケージに基づく配布 {#distribution-based-on-rpm--packages}

>[!AVAILABILITY]
>
>v7.4.1 以降、RPM Linux パッケージ用の XML ライブラリは Campaign に含まれなくなりました。これらのライブラリをインストールしてください。
> 

Adobe Campaignを RPM （RHEL、CentOS）オペレーティングシステムにインストールするには、次の手順に従います。

1. Adobe Campaign パッケージを取得します。 ファイル名は **nlserver6-v7-XXXX-0.x86_64.rpm** です。ここで **XXXX** はAdobe Campaignのビルド番号です。

   >[!CAUTION]
   >
   >この節のコマンドサンプルでは、使用しているAdobe Campaignのバージョンに適したファイル名を使用していることを確認してください。

1. インストールするには、**root** として接続し、次のコマンドを実行します。ここで **XXXX** はAdobe Campaignのビルド番号です。

   ```sql
   yum install nlserver6-v7-XXXX-0.x86_64.rpm
   ```

   rpm ファイルは、CentOS/Red Hat ディストリビューションで見つけることができるパッケージに依存しています。 これらの依存関係の一部を使用しない場合（例えば、OpenJDK ではなくOracle JDK を使用する場合）、rpm の「nodeps」オプションを使用する必要がある可能性があります。

   ```sql
   rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
   ```

リストに表示される依存関係のほとんどは必須であり、インストールされていない場合は起動で `nlserver` ません（例外は opendk です。別の JDK をインストールできます）。

[netreport](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts) の実行に必須の `bc` コマンドは、デフォルトでは、すべての Linux ディストリビューションで使用することはできません。 コマンドが使用可能かどうかを確認するには、`which bc` コマンドを実行します。 そうでない場合は、インストールする必要があります。

CentOS では、bc.x86_64 パッケージをインストールする必要があります。connect as **root** を実行して、次のコマンドを実行します。

```sql
yum install bc.x86_64
```


### オンプレミスデプロイメント用の RHEL 9 {#rhel-9-update}

Campaign v7.4.1 を RHEL 9 を使用するオンプレミス環境のお客様としてDKIM（Domain Keys Identified Mail）認証を使用する場合、システム設定を更新する必要があります。

これを実行するには、次の手順に従います。

1. root として、次のコマンドを実行します。

```sql
update-crypto-policies --set LEGACY
```

1. MTA モジュールを再起動します。

```sql
nlserver restart mta@<instance-name>
```

## APT （Debian）に基づく配布 {#distribution-based-on-apt--debian-}

Adobe Campaignを Debian 64 ビットオペレーティングシステムにインストールするには、次の手順に従います。

1. Adobe Campaign パッケージを取得します。 ファイル名は **nlserver6-v7-XXXX-linux-2.6-amd64.deb** です。ここで **XXXX** はAdobe Campaignのビルド番号です。

   >[!CAUTION]
   >
   >この節のコマンドサンプルでは、使用しているAdobe Campaignのバージョンに適したファイル名を使用していることを確認してください。

1. インストールするには、**root** として接続し、次のコマンドを実行します。ここで **XXXX** はAdobe Campaignのビルド番号です。

   ```sql
   apt install ./nlserver6-v7-XXXX-linux-2.6-amd64.deb
   ```


## パラメーターのパーソナライズ {#personalizing-parameters}

一部のパラメーターは、**customer.sh** ファイルを介してパーソナライズできます

初めてインストールを実行する場合は、**customer.sh** ファイルがサーバーにまだ存在していない可能性があります。

作成し、実行権限があることを確認します。 これに該当しない場合は、次のコマンドを入力します。

```sql
chmod +x /usr/local/neolane/nl6/customer.sh
```

### サーバーエンコーディング {#server-encoding}

デフォルトでは、サーバーは iso8859-15 環境で起動されます。 ただし、サーバーは UTF-8 環境で起動できます。

>[!CAUTION]
>
>この変更は、ファイルシステム（ワークフローまたはJavaScript スクリプトを使用して読み込まれたファイル）とのインタラクションと、ファイルのエンコーディングに影響を与えます。 そのため、デフォルトの環境を使用することをお勧めします。

**日本語インスタンス** を作成するには、UTF-8 環境を使用する必要があります。

UTF-8 環境を有効にするには、次のコマンドを使用します。

```sql
mkdir -p /usr/local/neolane/nl6 
touch /usr/local/neolane/nl6/unicodeenv
```

### 環境変数 {#environment-variables}

次の環境変数を正しく定義する必要があります。

特定の組み合わせでは、Adobe Campaignの実行に使用する環境を変更する必要があります。 特定のファイル（`/usr/local/neolane/nl6/customer.sh`）を作成および編集して、Adobe Campaign環境に固有の変更を追加できます。

必要に応じて、**vi customer.sh** コマンドを使用して **customer.sh** ファイルを編集し、設定を調整するか、不足している行を追加します。

* oracleクライアントの場合：

  ```sql
  export ORACLE_HOME=/usr/local/instantclient_10_2
  export TNS_ADMIN=/etc/oracle
  export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH 
  ```

  oracle変数 ENVIRONMENT_HOME の内容は、Oracleのインストールディレクトリと一致します。

  TNS_ADMIN 変数の内容は、**tnsnames.ora** ファイルの場所と一致する必要があります。

* LibreOffice:

  既存バージョンの LibreOffice でAdobe Campaignを実行するには、さらに設定が必要です。インストールディレクトリへのアクセスパスを指定する必要があります。 次に例を示します。

   * Debian

     OOO_INSTALL_DIR と OOO_BASIS_INSTALL_DIR のデフォルト値が提供されます。 LibreOffice インストールのレイアウトが異なる場合は、**customer.sh** で上書きできます。

     ```sql
     export OOO_BASIS_INSTALL_DIR=/usr/lib/libreoffice/ 
     export OOO_INSTALL_DIR=/usr/lib/libreoffice/
     ```

   * CentOS

     次のデフォルト値を使用します。

     ```sql
     export OOO_BASIS_INSTALL_DIR=/usr/lib64/libreoffice/
     export OOO_INSTALL_DIR=/usr/lib64/libreoffice/
     ```

* Java Development Kit （JDK）の場合：

  デフォルトでは、Adobe Campaign環境（`~/nl6/env.sh`）の設定スクリプトは、JDK インストールディレクトリを検索します。 ただし、使用する JDK を指定することをお勧めします。 それには、次のコマンドを使用して **JDK_HOME** 環境変数を強制的に指定します。

  ```sql
  export JDK_HOME=/usr/java/jdkX.Y.Z
  ```

  >[!NOTE]
  >
  >使用する JDK バージョンがディレクトリ名と一致することを確認します。

  JDK 設定をテストするには、次のコマンドでAdobe Campaign システムユーザーとしてログインします。

  ```sql
  su - neolane
  ```

変更内容を反映するには、Adobe Campaign サービスを再起動する必要があります。

コマンドは次のとおりです。

```sql
systemctl stop nlserver
systemctl start nlserver
```

### Linux のOracleクライアント {#oracle-client-in-linux}

Adobe CampaignでOracleを使用する場合、Linux でOracleクライアントレイヤーを設定する必要があります。

* 完全なクライアントを使用
* TNS の定義

  TNS 定義は、インストール段階で追加する必要があります。 これを行うには、次のコマンドを使用します。

  ```sql
  cd /etc
  mkdir oracle
  cd oracle
  vi tnsnames.ora
  ```

* 環境変数

  [ 環境変数 ](#environment-variables) を参照してください。

* Adobe Campaignの設定

  Adobe CampaignのOracleクライアントのインストールを完了するには、Adobe Campaignが使用する **.so** ファイルのシンボリックリンクを作成する必要があります。

  これを行うには、次のコマンドを使用します。

  ```sql
  cd /usr/lib/oracle/10.2.0.4/client/lib
  ln -s libclntsh.so.10.1 libclntsh.so
  ```

問題が発生した場合は、Oracleのインストールドキュメントに記載されているパッケージが正しくインストールされていることを確認してください。

## インストールチェック {#installation-checks}

これで、次のコマンドを使用して初期インストールテストを実行できます。

```sql
su - neolane
nlserver pdump
```

Adobe Campaignを起動しない場合の応答は次のとおりです。

```sql
no task
```

## サーバーの初回起動 {#first-start-up-of-the-server}

インストールテストが完了したら、次のコマンドを入力します。

```sql
nlserver web
```

次の情報が表示されます。

```sql
17:11:03 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
17:11:03 >   Web server start (pid=17546, tid=-151316352)...
17:11:03 >   Creating server configuration file '/usr/local/[INSTALL]/nl6/conf/serverConf.xml' via '/usr/local/[INSTALL]/nl6/conf/fra/serverConf.xml.sample'
17:11:03 >   Creating server configuration file '/usr/local/[INSTALL]/nl6/conf/config-default.xml' via '/usr/local/[INSTALL]/nl6/conf/models/config-default.xml'
17:11:03 >   Server started
17:11:08 >   Stop requested (pid=17546)
17:11:08 >   Web server stop(pid=17546, tid=-151316352)...
```

これらのコマンドを使用すると、**config-default.xml** および **serverConf.xml** 設定ファイルを作成できます。 **serverConf.xml** で使用可能なすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に一覧表示されます。

**Ctrl+C** を押してプロセスを停止し、次のコマンドを入力します。

```sql
nlserver start web
```

次の情報が表示されます。

```sql
12:17:21 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:17:21 >   Running task 'web@default' ('nlserver web -tracefile:web@default -instance:default -detach -tomcat -autorepair') in a new process
12:17:21 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:17:21 >   Web server start (pid=29188, tid=-1224824320)...
12:17:21 >   Creating server configuration file '/usr/local/[INSTALL]/nl6/conf/serverConf.xml' via '/usr/local/[INSTALL]/nl6/conf/fra/serverConf.xml.sample'
12:17:22 >   Tomcat started
12:17:22 >   Server started
```

停止するには、次のように入力します。

```sql
nlserver stop web
```

次の情報が表示されます。

```sql
12:18:31 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:18:31 >   Stop requested for 'web@default' ('nlserver web -tracefile:web@default -instance:default -detach -tomcat -autorepair', pid=29188, tid=-1224824320)...
12:18:31 >   Stop requested (pid=29188)
12:18:31 >   Web server stopped (pid=29188, tid=-1224824320)...
```

## 内部識別子のパスワード {#password-for-the-internal-identifier}

Adobe Campaign サーバーは、すべてのインスタンスに対するすべての権限を持つ **internal** というテクニカルログインを定義します。 インストール直後は、ログインにパスワードがありません。 定義する必要があります。

詳しくは、[こちら](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。
