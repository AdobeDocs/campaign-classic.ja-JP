---
product: campaign
title: Linux でのパッケージのインストール
description: Linux でのパッケージのインストール
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: f41c7510-5ad7-44f3-9485-01f54994b6cb
source-git-commit: c281d437907efb4d514bec7cacc698c383f3fe53
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---

# Linux でのパッケージのインストール{#installing-packages-with-linux}

![](../../assets/v7-only.svg)

Linux 32 ビットプラットフォームの場合は、Adobe Campaign 32 ビットをインストールします。 Linux 64 ビットプラットフォームの場合は、Adobe Campaign 64 ビットをインストールします。

Adobe Campaignには、これらの各バージョンに対して 1 つのパッケージが付属しています。**nlserver**。 このパッケージには、特定のバージョンのバイナリと設定ファイルが含まれます。

インストールコマンドを使用すると、次のことができます。

* ファイルを **/usr/local/neolane** にコピーします。
* **/usr/local/neolane** をホームディレクトリとして使用して作成されたAdobe Campaign Linux アカウント（および関連するグループ）を作成します。
* 起動時に使用する自動スクリプト **/etc/init.d/nlserver6** を作成するか、systemd ユニットを作成します（20.1 以降）。

>[!NOTE]
>
>**neolane** システムユーザーは、コマンドを実行する前に作成してはいけません。 **neolane** ユーザーはインストール中に自動的に作成されます。
>
>**neolane** ユーザーにリンクされた **home** ディレクトリも **[!UICONTROL /usr/local/neolane]** に自動的に作成されます。 **[!UICONTROL /usr/local]** ディスクに十分な空き領域があることを確認してください（数 GB）。

**ping`hostname`** コマンドを実行して、サーバーが自身に到達できることを確認できます。

## RPM パッケージに基づく配布 {#distribution-based-on-rpm--packages}

Adobe Campaignを RPM（RHEL、CentOS および SUSE）オペレーティングシステムにインストールするには、次の手順に従います。

1. まず、Adobe Campaignパッケージを入手する必要があります。

   ファイルの名前は次のようになります。 **XXXX** はAdobe Campaignのビルド番号です。

   * **nlserver6-v7-XXXX-0.x86_64.rpmfor v7。** 
   * **nlserver6-XXXX-0.x86_64.** rpmfor v6.1

   >[!CAUTION]
   >
   >この節のコマンドサンプルで、ご使用のバージョンのAdobe Campaignに対して正しいファイル名を使用してください。

1. インストールするには、**root** として接続し、次のコマンドを実行します (**XXXX** はAdobe Campaignのビルド番号です )。

   ```
   yum install nlserver6-v7-XXXX-0.x86_64.rpm
   ```

   rpm ファイルは、CentOS/Red Hat ディストリビューションで見つけられるパッケージに依存しています。 これらの依存関係の一部を使用しない場合 ( 例えば、OpenJDK の代わりにOracleJDK を使用する場合 )、rpm の&quot;nodeps&quot;オプションを使用する必要がある場合があります。

   ```
   rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
   ```

ネットポートの実行に必要な&#39;bc&#39;コマンド（詳細は [ この節 ](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts) を参照）は、Linux ディストリビューションではデフォルトでは利用できません。 コマンドが使用可能かどうかを確認するには、&#39;which bc&#39;コマンドを実行します。 そうでない場合は、インストールする必要があります。

CentOS では、bc.x86_64 パッケージをインストールする必要があります。**root** として接続し、次のコマンドを実行します。

```
yum install bc.x86_64
```

## APT(Debian) に基づく配布 {#distribution-based-on-apt--debian-}

### Debian 64 ビット {#in-debian-64-bits}

Adobe Campaign 64 ビットを Debian 64 ビットオペレーティングシステムにインストールするには、次の手順に従います。

1. まず、Adobe Campaignパッケージを入手する必要があります。

   * **nlserver6-v7-XXXX-linux-2.6-amd64.** debfor v7.
   * **nlserver6-XXXX-linux-2.6-amd64.** debfor v6.1

   **** XXXX はAdobe Campaignのビルド番号です。

   >[!CAUTION]
   >
   >この節のコマンドサンプルで、ご使用のバージョンのAdobe Campaignに対して正しいファイル名を使用してください。

1. インストールするには、**root** として接続し、次のコマンドを実行します (**XXXX** はAdobe Campaignのビルド番号です )。

   ```
   dpkg -i nlserver6-v7-XXXX-linux-2.6-amd64.deb
   ```

   存在しない依存関係がある場合は、次のコマンドを実行します。

   ```
   apt-get install -f
   ```

**Debian 8/9 の詳細**

Debian 8/9 オペレーティングシステムにAdobe Campaignをインストールする際は、次の点に注意してください。

* 事前に OpenSSL をインストールしておく必要があります。
* 次のコマンドを使用して、libicu52(Debian 8) または libicu57(Debian 9)、libprotobuf9(Debian8) および libc-ares2 をインストールします。

   ```
   aptitude install libicu52 (Debian 8) libicu57 (Debian 9)
   ```

   ```
   aptitude install libc-ares2
   ```

   ```
   aptitude install libprotobuf9 (only Debian 8)
   ```

* 次のコマンドを使用して JDK7 をインストールします。

   ```
   aptitude install openjdk-7-jdk (Debian 8)
   ```

   ```
   aptitude install openjdk-7-jdk (Debian 9)
   ```

## パラメーターのパーソナライズ {#personalizing-parameters}

**customer.sh** ファイルを使用してパーソナライズできるパラメーターもあります

初めてインストールを実行する場合は、**customer.sh** ファイルがまだサーバーに存在しない可能性があります。 作成し、実行権限があることを確認します。 そうでない場合は、次のコマンドを入力します。

```
chmod +x /usr/local/neolane/nl6/customer.sh
```

### サーバーエンコーディング {#server-encoding}

デフォルトでは、サーバーは iso8859-15 環境で起動されます。 ただし、サーバーは UTF-8 環境で起動できます。

>[!CAUTION]
>
>この変更は、ファイルシステム（ワークフローまたは JavaScript スクリプトを介して読み込まれたファイル）とのやり取りと、ファイルのエンコードに影響します。 したがって、デフォルトの環境を使用することをお勧めします。

ただし、**日本語のインスタンス** を作成する場合は、UTF-8 環境を使用する必要があります。

UTF-8 環境を有効にするには、次のコマンドを使用します。

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

システムメッセージが正しく読み取られるようにするには、コンソールがその言語に対応するコードページにある必要があります（フランス語の場合は ISO-8859-1 または —15）。

### 環境変数 {#environment-variables}

次の環境変数を正しく定義する必要があります。

組み合わせによっては、Adobe Campaignの実行に使用する環境を変更する必要があります。 特定のファイル (`/usr/local/neolane/nl6/customer.sh`) を作成および編集して、Adobe Campaign環境に固有の変更を追加できます。

必要に応じて、**customer.sh** ファイルを **vi customer.sh** コマンドを使用して編集し、設定を変更するか、見つからない行を追加します。

* oracleクライアントの場合：

   ```
   export ORACLE_HOME=/usr/local/instantclient_10_2
   export TNS_ADMIN=/etc/oracle
   export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH 
   ```

   環境変数ORACLE_HOME の内容は、Oracleのインストールディレクトリに一致します。

   TNS_ADMIN 変数の内容は、**tnsnames.ora** ファイルの場所と一致する必要があります。

* LibreOffice の場合：

   既存のバージョンの LibreOffice でAdobe Campaignを実行するには、次の追加の設定が必要です。インストールディレクトリへのアクセスパスを指定する必要があります。 例：

   * Debian

      OOO_INSTALL_DIR、OOO_BASIS_INSTALL_DIR、OOO_URE_INSTALL_DIR のデフォルト値が提供されます。 LibreOffice のインストールのレイアウトが異なる場合は、 **customer.sh** で上書きできます。

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

* Java 開発キット (JDK) の場合：

   デフォルトでは、Adobe Campaign環境の設定スクリプト (`~/nl6/env.sh`) は JDK インストールディレクトリを検索します。 この動作は 100%信頼できないので、使用する必要のある JDK を指定する必要があります。 これを行うには、次のコマンドを使用して、**JDK_HOME** 環境変数を強制的に指定します。

   ```
   export JDK_HOME=/usr/java/jdk1.6.0_07
   ```

   >[!NOTE]
   >
   >これは一例です。使用する JDK のバージョンがディレクトリ名と一致していることを確認します。

   JDK 設定をテストするには、次のコマンドを使用して、Adobe Campaignシステムユーザーとしてログインします。

   ```
   su - neolane
   ```

変更内容を反映するには、Adobe Campaignサービスを再起動する必要があります。

コマンドは次のとおりです。

```
/etc/init.d/nlserver6 stop
/etc/init.d/nlserver6 start
```

20.1 以降では、代わりに次のコマンドを使用することをお勧めします。

```
systemctl stop nlserver
systemctl start nlserver
```

### Linux のoracleクライアント {#oracle-client-in-linux}

Adobe CampaignでOracleを使用する場合は、Linux でOracleクライアントレイヤーを設定する必要があります。

* 完全なクライアントを使用
* TNS の定義

   TNS 定義は、インストールフェーズで追加する必要があります。 これをおこなうには、次のコマンドを使用します。

   ```
   cd /etc
   mkdir oracle
   cd oracle
   vi tnsnames.ora
   ```

* 環境変数

   [ 環境変数 ](../../installation/using/installing-packages-with-linux.md#environment-variables) を参照してください。

* Adobe Campaignの設定

   Adobe Campaign用のOracleクライアントのインストールを完了するには、Adobe Campaignで使用する **.so** ファイルのシンボリックリンクを作成する必要があります。

   これをおこなうには、次のコマンドを使用します。

   ```
   cd /usr/lib/oracle/10.2.0.4/client/lib
   ln -s libclntsh.so.10.1 libclntsh.so
   ```

問題が発生した場合は、[Oracleのインストールに関するドキュメント ](https://docs.oracle.com/) に記載されているパッケージが正しくインストールされていることを確認してください。

## インストールのチェック {#installation-checks}

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

これらのコマンドを使用して、**config-default.xml** および **serverConf.xml** 設定ファイルを作成できます。 **serverConf.xml** で使用できるすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に記載されています。

**Ctrl+C** キーを押してプロセスを停止し、次のコマンドを入力します。

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

Adobe Campaignサーバーでは、**内部** と呼ばれる技術的なログインが定義され、すべてのインスタンスに対するすべての権限を持ちます。 インストール直後に、ログインにパスワードが含まれていません。 定義する必要があります。

詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。
