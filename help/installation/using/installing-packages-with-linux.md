---
product: campaign
title: Linuxでのパッケージのインストール
description: Linuxでのパッケージのインストール
feature: Installation, Application Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: f41c7510-5ad7-44f3-9485-01f54994b6cb
TQID: https://experienceleague.adobe.com/mpN0TwuPILae7Y-jbkyvbBR1zdo4IvtnuzGQObLI0rc
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 1150
ht-degree: 4%

---

# Linuxでのパッケージのインストール {#installing-packages-with-linux}

Adobe Campaignには、特定のバージョンのバイナリと設定ファイルを含む&#x200B;**nlserver** パッケージが付属しています。

インストールコマンドを使用すると、次のことが可能になります。

* ファイルを&#x200B;**/usr/local/neolane**&#x200B;にコピー
* **/usr/local/neolane**&#x200B;をホームディレクトリとして作成したAdobe Campaign Linux アカウント（および関連グループ）を作成します
* 起動時に使用する自動スクリプト **/etc/init.d/nlserver6**&#x200B;を作成するか、systemd ユニットを作成します

>[!NOTE]
>
>コマンドを実行する前に、**neolane** システム ユーザーを作成してはいけません。 **neolane** ユーザーは、インストール中に自動的に作成されます。
>
>**neolane** ユーザーにリンクされた&#x200B;**home** ディレクトリも、**[!UICONTROL /usr/local/neolane]**&#x200B;に自動的に作成されます。 **[!UICONTROL /ユーザー/ローカル]** ディスクに十分な空き容量があることを確認してください。

**ping`hostname`** コマンドを実行して、サーバーが自分自身に到達できることを確認できます。

## RPM パッケージに基づく配布 {#distribution-based-on-rpm--packages}

>[!AVAILABILITY]
>
>v7.4.1 以降、RPM Linux パッケージ用の XML ライブラリは Campaign に含まれなくなりました。 これらのライブラリをインストールしてください。
> 

Adobe CampaignをRPM （RHEL、CentOS）オペレーティングシステムにインストールするには、次の手順に従います。

1. Adobe Campaign パッケージを入手します。 ファイルの名前は&#x200B;**nlserver6-v7-XXXX-0.x86_64.rpm**&#x200B;です。**XXXX**&#x200B;はAdobe Campaignのビルド番号です。

   >[!CAUTION]
   >
   >このセクションのコマンドサンプルでは、Adobe Campaignのバージョンに正しいファイル名を使用していることを確認してください。

1. インストールするには、**root**&#x200B;として接続し、次のコマンドを実行します。ここで、**XXXX**&#x200B;はAdobe Campaignのビルド番号です。

   ```sql
   yum install nlserver6-v7-XXXX-0.x86_64.rpm
   ```

   rpm ファイルは、CentOS/Red Hat ディストリビューションで見つけることができるパッケージに依存しています。 これらの依存関係の一部を使用したくない場合（例えば、OpenJDKの代わりにOracle JDKを使用したい場合）は、rpmの「nodeps」オプションを使用する必要があります。

   ```sql
   rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
   ```

リストされている依存関係のほとんどは必須であり、インストールされていない場合は`nlserver`を開始できません（例外はopendkです。別のJDKをインストールできます）。

[netreport](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts)の実行に必須の`bc` コマンドは、すべてのLinux ディストリビューションでデフォルトでは使用できません。 コマンドが使用可能かどうかを確認するには、`which bc` コマンドを実行します。 そうでない場合は、インストールする必要があります。

CentOSでは、bc.x86_64 パッケージをインストールする必要があります。**root**&#x200B;として接続し、次のコマンドを実行します。

```sql
yum install bc.x86_64
```


### オンプレミスでのデプロイメント用RHEL 9 {#rhel-9-update}

Campaign v7.4.1では、RHEL 9を使用するオンプレミスのお客様として、DKIM（Domain Keys Identified Mail）認証を使用する場合は、システム設定を更新する必要があります。

これを実行するには、次の手順に従います。

1. rootとして次のコマンドを実行します。

```sql
update-crypto-policies --set LEGACY
```

1. MTA モジュールを再起動します。

```sql
nlserver restart mta@<instance-name>
```

## APT （Debian）に基づく配布 {#distribution-based-on-apt--debian-}

Debian 64 ビットオペレーティングシステムにAdobe Campaignをインストールするには、次の手順を実行します。

1. Adobe Campaign パッケージを入手します。 ファイルの名前は&#x200B;**nlserver6-v7-XXXX-linux-2.6-amd64.deb**&#x200B;です。**XXXX**&#x200B;はAdobe Campaignのビルド番号です。

   >[!CAUTION]
   >
   >このセクションのコマンドサンプルでは、Adobe Campaignのバージョンに正しいファイル名を使用していることを確認してください。

1. インストールするには、**root**&#x200B;として接続し、次のコマンドを実行します。ここで、**XXXX**&#x200B;はAdobe Campaignのビルド番号です。

   ```sql
   apt install ./nlserver6-v7-XXXX-linux-2.6-amd64.deb
   ```


## パラメーターのパーソナライズ {#personalizing-parameters}

一部のパラメーターは、**customer.sh** ファイルを使用してパーソナライズできます

初めてインストールを実行する場合は、**customer.sh** ファイルがまだサーバーに存在しない可能性があります。

作成して、実行権限があることを確認します。 そうでない場合は、次のコマンドを入力します。

```sql
chmod +x /usr/local/neolane/nl6/customer.sh
```

### サーバーエンコーディング {#server-encoding}

デフォルトでは、サーバーはiso8859-15環境で起動されます。 ただし、サーバーはUTF-8環境で起動できます。

>[!CAUTION]
>
>この変更は、ファイルシステム（ワークフローまたはJavaScript スクリプトを介して読み込まれたファイル）とファイルエンコーディングのインタラクションに影響を与えます。 したがって、デフォルトの環境を使用することをお勧めします。

**日本語インスタンス**&#x200B;を作成するには、UTF-8環境を使用する必要があります。

UTF-8環境を有効にするには、次のコマンドを使用します。

```sql
mkdir -p /usr/local/neolane/nl6 
touch /usr/local/neolane/nl6/unicodeenv
```

### 環境変数 {#environment-variables}

次の環境変数を正しく定義する必要があります。

一部の組み合わせでは、Adobe Campaignの実行に使用する環境を変更する必要があります。 特定のファイル （`/usr/local/neolane/nl6/customer.sh`）を作成して編集し、Adobe Campaign環境に固有の変更を追加できます。

必要に応じて、**vi customer.sh** コマンドを使用して&#x200B;**customer.sh** ファイルを編集し、設定を適応させるか、欠落している行を追加します。

* Oracle クライアントの場合

  ```sql
  export ORACLE_HOME=/usr/local/instantclient_10_2
  export TNS_ADMIN=/etc/oracle
  export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH 
  ```

  Oracle_HOME環境変数の内容は、Oracleのインストールディレクトリと一致します。

  TNS_ADMIN変数の内容は、**tnsnames.ora** ファイルの場所と一致している必要があります。

* LibreOfficeの場合

  既存のバージョンのLibreOfficeでAdobe Campaignを実行するには、追加の設定が必要です。インストールディレクトリへのアクセスパスを指定する必要があります。 例：

   * Debian

     OOO_INSTALL_DIRおよびOOO_BASIS_INSTALL_DIRのデフォルト値が提供されています。 LibreOffice インストールのレイアウトが異なる場合は、**customer.sh**&#x200B;で上書きできます。

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

  デフォルトでは、Adobe Campaign環境（`~/nl6/env.sh`）の設定スクリプトがJDK インストールディレクトリを検索します。 ただし、使用する必要があるJDKを指定することをお勧めします。 これを行うには、次のコマンドを使用して&#x200B;**JDK_HOME**&#x200B;環境変数を強制的に指定できます。

  ```sql
  export JDK_HOME=/usr/java/jdkX.Y.Z
  ```

  >[!NOTE]
  >
  >使用するJDK バージョンがディレクトリ名と一致することを確認します。

  JDK設定をテストするには、次のコマンドを使用してAdobe Campaign システムユーザーとしてログインします。

  ```sql
  su - neolane
  ```

変更を考慮に入れるには、Adobe Campaign サービスを再起動する必要があります。

コマンドは次のとおりです。

```sql
systemctl stop nlserver
systemctl start nlserver
```

### LinuxでのOracle クライアント {#oracle-client-in-linux}

Adobe CampaignでOracleを使用する場合は、LinuxでOracle クライアントレイヤーを設定する必要があります。

* 完全なクライアントを使用
* TNSの定義

  TNS定義は、インストール段階で追加する必要があります。 これを行うには、次のコマンドを使用します。

  ```sql
  cd /etc
  mkdir oracle
  cd oracle
  vi tnsnames.ora
  ```

* 環境変数

  [環境変数](#environment-variables)を参照してください。

* Adobe Campaignの設定

  Adobe Campaign用Oracle クライアントのインストールを完了するには、Adobe Campaignで使用する&#x200B;**.so** ファイルのシンボリックリンクを作成する必要があります。

  これを行うには、次のコマンドを使用します。

  ```sql
  cd /usr/lib/oracle/10.2.0.4/client/lib
  ln -s libclntsh.so.10.1 libclntsh.so
  ```

問題が発生した場合は、Oracle インストールドキュメントに記載されているパッケージが正しくインストールされていることを確認してください。

## インストールの確認 {#installation-checks}

次のコマンドを使用して、初期インストールテストを実行できるようになりました。

```sql
su - neolane
nlserver pdump
```

Adobe Campaignが開始されない場合、応答は次のとおりです。

```sql
no task
```

## サーバーの最初の起動 {#first-start-up-of-the-server}

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

これらのコマンドを使用すると、**config-default.xml**&#x200B;および&#x200B;**serverConf.xml**&#x200B;設定ファイルを作成できます。 **serverConf.xml**&#x200B;で使用可能なすべてのパラメーターは、この[ セクション ](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

**Ctrl+C**&#x200B;を押してプロセスを停止し、次のコマンドを入力します。

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

Adobe Campaign サーバーは、すべてのインスタンスに対するすべての権限を持つ&#x200B;**internal**&#x200B;というテクニカルログインを定義します。 インストール直後に、ログインにパスワードがありません。 1を定義することは必須です。

詳しくは、[こちら](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。
