---
product: campaign
title: Google BigQuery へのアクセスの設定
description: FDA でGoogle BigQuery へのアクセスを設定する方法を説明します
audience: platform
content-type: reference
topic-tags: connectors
exl-id: ebaad59f-0607-4090-92d0-e457fbf9a348
source-git-commit: 6d53ba957fb567a9a921544418a73a9bde37c97b
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 7%

---

# Google BigQuery へのアクセスの設定 {#configure-fda-google-big-query}

![](../../assets/v7-only.svg)

Adobe Campaign Classicを使用 **Federated Data Access** (FDA) 外部データベースに保存された情報を処理するオプション。 次の手順に従って、へのアクセスを設定します。 [!DNL Google BigQuery].

1. 設定 [!DNL Google BigQuery] オン [Windows](#google-windows) または [Linux](#google-linux)
1. の設定 [!DNL Google BigQuery] [外部アカウント](#google-external) Adobe Campaign Classic
1. 設定 [!DNL Google BigQuery] コネクタの一括読み込み [Windows](#bulk-load-windows) または [Linux](#bulk-load-linux)

>[!NOTE]
>
> [!DNL Google BigQuery] コネクタは、ハイブリッドおよびオンプレミスのデプロイメントで使用できます。 詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

![](assets/snowflake_3.png)

## Google BigQuery（Windows 上） {#google-windows}

### Windows でのドライバのセットアップ {#driver-window}

1. [Windows 用の ODBC ドライバー](https://cloud.google.com/bigquery/docs/reference/odbc-jdbc-drivers)をダウンロードします。

1. Windows で ODBC ドライバーを設定します。 詳しくは、[このページ](https://storage.googleapis.com/simba-bq-release/jdbc/Simba%20JDBC%20Driver%20for%20Google%20BigQuery%20Install%20and%20Configuration%20Guide.pdf)を参照してください。

1. の [!DNL Google BigQuery] コネクタが機能するには、Adobe Campaign Classicが接続するには次のパラメーターが必要です。

   * **[!UICONTROL プロジェクト]**:既存のプロジェクトを作成するか、使用します。

      詳しくは、[このページ](https://cloud.google.com/resource-manager/docs/creating-managing-projects)を参照してください。

   * **[!UICONTROL サービスアカウント]**:サービスアカウントを作成します。

      詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-accounts)を参照してください。

   * **[!UICONTROL キーファイルのパス]**:の **[!UICONTROL サービスアカウント]** にはが必要です **[!UICONTROL キーファイル]** の [!DNL Google BigQuery] ODBC を介した接続

      詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)を参照してください。

   * **[!UICONTROL データセット]**: **[!UICONTROL データセット]** は、ODBC 接続の場合はオプションです。 各クエリは、テーブルの場所にあるデータセットを提供し、 **[!UICONTROL データセット]** は必須です [!DNL Google BigQuery] Adobe Campaign Classicの FDA コネクタ。

      詳しくは、[このページ](https://cloud.google.com/bigquery/docs/datasets)を参照してください。

1. Adobe Campaign Classicで、 [!DNL Google BigQuery] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#google-external).

### Windows での一括読み込みの設定 {#bulk-load-window}

>[!NOTE]
>
>Google Cloud SDK を動作させるには、Python がインストールされている必要があります。
>
>Python3 の使用をお勧めします。詳しくは、 [ページ](https://www.python.org/downloads/).

一括読み込みユーティリティを使用すると、Google Cloud SDK を通じてより高速に転送できます。

1. このから Windows 64 ビット (x86_64) アーカイブをダウンロード [ページ](https://cloud.google.com/sdk/docs/downloads-versioned-archives) 対応するディレクトリに抽出します。

1. を実行します。 `google-cloud-sdk\install.sh` スクリプト path 変数の設定を受け入れる必要があります。

1. インストール後に、パス変数を確認します。 `...\google-cloud-sdk\bin` が設定されている。 そうでない場合は、手動で追加します。

1. 内  `..\google-cloud-sdk\bin\bq.cmd` ファイルを開き、 `CLOUDSDK_PYTHON` ローカル変数を使用して、Python のインストール場所にリダイレクトされます。

   例：

   ![](assets/google-big-query_1.png)

1. Adobe Campaign Classicを再起動して、変更を反映させます。

## Google BigQuery（Linux 上） {#google-linux}

### Linux でのドライバの設定 {#driver-linux}

1. ODBC ドライバーをインストールする前に、システムを更新する必要があります。 Linux または CentOS で、次のコマンドを実行します。

   ```
   yum update
   # install unixODBC driver manager
   yum install unixODBC
   ```

1. その後、次のコマンドを使用して unixODBC ドライバーマネージャーをインストールする必要があります。

   ```
   # switch to root user
   sudo su
   ```

   Debian の場合：

   ```
   apt-get update
   apt-get upgrade
   # install unixODBC driver manager
   apt-get install unixODBC
   ```

1. をダウンロードします。 [Magnitude Simba Linux ODBC ドライバ (.tar.gz)](https://cloud.google.com/bigquery/docs/reference/odbc-jdbc-drivers). 次に、tarball ファイルをマシン上の一時フォルダーに転送するか、wget コマンドを使用します。

   ```
   # in this example driver version is 2.3.1.1001
   wget https://storage.googleapis.com/simba-bq-release/odbc/SimbaODBCDriverforGoogleBigQuery_[Version]-Linux.tar.gz
   ```

1. メインの tarball ファイルを次のように抽出します。 **TarballName** は、ドライバーが含まれている tarball パッケージの名前です。

   ```
   tar --directory=/tmp -zxvf [TarballName]
   ```

1. 抽出したフォルダにアクセスし、ドライバのバージョンに対応する内部 tarball ファイルを抽出します。 次の例の BigQueryDriver で、別の一時フォルダーにインストールします。

   ```
   mkdir /tmp/BigQueryDriver/
   cd /tmp/SimbaODBCDriverforGoogleBigQuery_[Version]-Linux/
   tar --directory=/tmp/BigQueryDriver/ -zxvf SimbaODBCDriverforGoogleBigQuery[Bitness]_[Version].tar.gz
   ```

1. メインの tarball ファイルが抽出された一時的な場所にアクセスし、 `GoogleBigQueryODBC.did` および `setup/simba.googlebigqueryodbc.ini` ファイルは、前の手順で作成した新しいフォルダーに格納されます。

   ```
   cd /tmp/SimbaODBCDriverforGoogleBigQuery_[Version]-Linux/
   cp GoogleBigQueryODBC.did /tmp/BigQueryDriver/SimbaODBCDriverforGoogleBigQuery[Bitness]_[Version]/lib/
   cp setup/simba.googlebigqueryodbc.ini /tmp/BigQueryDriver/SimbaODBCDriverforGoogleBigQuery[Bitness]_[Version]/lib/
   ```

1. 次のように、インストールディレクトリを作成します。

   ```
   mkdir -p /opt/simba/googlebigqueryodbc/
   ```

1. ディレクトリの内容を新しいインストールディレクトリにコピーします。

   ```
   cp -r /tmp/BigQueryDriver/SimbaODBCDriverforGoogleBigQuery[Bitness]_[Version]/* /opt/simba/googlebigqueryodbc/
   ```

1. 置換 `<INSTALLDIR>` と `/opt/simba/googlebigqueryodbc` in `simba.googlebigqueryodbc.ini` インストールディレクトリ内：

   ```
   cd /opt/simba/googlebigqueryodbc/lib/
   sed -i 's/<INSTALLDIR>/\/opt\/simba\/googlebigqueryodbc/g' simba.googlebigqueryodbc.ini
   ```

1. を `DriverManagerEncoding` を UTF-16 に設定し、 `SwapFilePath` in `simba.googlebigqueryodbc.ini`. 必要に応じて、ログ設定を変更することもできます。

   次に、更新されたドライバ全体の構成ファイルの例を示します。

   ```
   # /opt/simba/googlebigqueryodbc/lib/simba.googlebigqueryodbc.ini
   [Driver]
   DriverManagerEncoding=UTF-16
   ErrorMessagesPath=opt/simba/googlebigqueryodbc/ErrorMessages
   LogLevel=6
   LogPath=/tmp
   SwapFilePath=/tmp
   ```

1. システムドライバファイルまたは現在の `odbcinst.ini` ファイル、設定 `/etc/odbcinst.ini` Google BigQuery ドライバーの場所を示す `/opt/simba/googlebigqueryodbc/lib/libgooglebigqueryodbc_sb[Bitness].so`.

   例：

   ```
   # /etc/odbcinst.ini
   # Make sure to use Simba ODBC Driver for Google BigQuery as a driver name.
   
   [ODBC Drivers]
   Simba ODBC Driver for Google BigQuery=Installed
   
   [Simba ODBC Driver for Google BigQuery]
   Description=Simba ODBC Driver for Google BigQuery(64-bit)
   Driver=/opt/simba/googlebigqueryodbc/lib/libgooglebigqueryodbc_sb64.so
   ```

1. unixODBC ドライバーマネージャーライブラリの場所を探し、 `unixODBC` および `googlebigqueryodbc` へのライブラリパス `LD_LIBRARY_PATH environment` 変数を使用します。

   ```
   find / -name 'lib*odbc*.so*' -print
   #output:
   /usr/lib/x86_64-linux-gnu/libodbccr.so.2
   /usr/lib/x86_64-linux-gnu/libodbcinst.so.2.0.0
   /usr/lib/x86_64-linux-gnu/libodbccr.so.1
   .
   .
   /opt/simba/googlebigqueryodbc/lib/libgooglebigqueryodbc_sb64.so
   
   #the command would look like this
   export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/simba/googlebigqueryodbc:/usr/lib
   ```

1. Adobe Campaign Classicで、 [!DNL Google BigQuery] 外部アカウント。 外部アカウントの設定方法について詳しくは、 [この節](#google-external).

### Linux での一括読み込みの設定 {#bulk-load-linux}

>[!NOTE]
>
>Google Cloud SDK を動作させるには、Python がインストールされている必要があります。
>
>Python3 の使用をお勧めします。詳しくは、 [ページ](https://www.python.org/downloads/).

一括読み込みユーティリティを使用すると、Google Cloud SDK を通じてより高速に転送できます。

1. このファイルに Linux 64 ビット (x86_64) アーカイブをダウンロード [ページ](https://cloud.google.com/sdk/docs/downloads-versioned-archives) を抽出し、対応するディレクトリに抽出します。

1. を実行します。 `google-cloud-sdk\install.sh` スクリプト path 変数の設定を受け入れる必要があります。

1. インストール後に、パス変数を確認します。 `...\google-cloud-sdk\bin` が設定されている。 そうでない場合は、手動で追加します。

1. を使用しない場合は、 `PATH` 変数を使用するか、 `google-cloud-sdk` ディレクトリを別の場所に移動するには、 `bqpath` オプション値（設定時） **[!UICONTROL 外部アカウント]** をクリックして、システム上の bin ディレクトリの正確なパスを指定します。

1. Adobe Campaign Classicを再起動して、変更を反映させます。

## Google BigQuery 外部アカウント {#google-external}

次を作成する必要があります： [!DNL Google BigQuery] Adobe Campaign Classicインスタンスを [!DNL Google BigQuery] 外部データベース。

1. Adobe Campaign Classicから **[!UICONTROL エクスプローラ]**&#x200B;をクリックし、 **[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL Platform]** &#39;>&#39; **[!UICONTROL 外部アカウント]**.

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. [!DNL Google BigQuery] 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：[!DNL Google BigQuery]

   * **[!UICONTROL サービスアカウント]**:メール **[!UICONTROL サービスアカウント]**. 詳しくは、 [Google Cloud ドキュメント](https://cloud.google.com/iam/docs/creating-managing-service-accounts).

   * **[!UICONTROL プロジェクト]**:の名前 **[!UICONTROL プロジェクト]**. 詳しくは、 [Google Cloud ドキュメント](https://cloud.google.com/resource-manager/docs/creating-managing-projects).

   * **[!UICONTROL キーファイルのパス]**:
      * **[!UICONTROL キーファイルをサーバーにアップロード]**:選択 **[!UICONTROL ここをクリックしてアップロード]** Adobe Campaign Classicを使用してキーをアップロードする場合。

      * **[!UICONTROL 手動でキーのファイルパスを入力]**:既存のキーを使用する場合は、このフィールドに絶対パスをコピーして貼り付けます。
   * **[!UICONTROL データセット]**:の名前 **[!UICONTROL データセット]**. 詳しくは、 [Google Cloud ドキュメント](https://cloud.google.com/bigquery/docs/datasets-intro).
   ![](assets/google-big-query.png)
