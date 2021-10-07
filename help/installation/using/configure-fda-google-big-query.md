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

Adobe Campaign Classic **Federated Data Access** (FDA) オプションを使用して、外部データベースに保存された情報を処理します。 次の手順に従って、[!DNL Google BigQuery] へのアクセスを設定します。

1. [Windows](#google-windows) または [Linux](#google-linux) で [!DNL Google BigQuery] を設定します
1. Adobe Campaign Classicで [!DNL Google BigQuery] [ 外部アカウント ](#google-external) を設定します
1. [Windows](#bulk-load-windows) または [Linux](#bulk-load-linux) で [!DNL Google BigQuery] コネクタの一括読み込みを設定します

>[!NOTE]
>
> [!DNL Google BigQuery] コネクタは、ハイブリッドおよびオンプレミスのデプロイメントで使用できます。詳しくは、[このページ](../../installation/using/capability-matrix.md)を参照してください。

![](assets/snowflake_3.png)

## Google BigQuery（Windows 版） {#google-windows}

### Windows でドライバを設定 {#driver-window}

1. [Windows 用の ODBC ドライバー](https://cloud.google.com/bigquery/docs/reference/odbc-jdbc-drivers)をダウンロードします。

1. Windows で ODBC ドライバーを設定します。 詳しくは、[このページ](https://storage.googleapis.com/simba-bq-release/jdbc/Simba%20JDBC%20Driver%20for%20Google%20BigQuery%20Install%20and%20Configuration%20Guide.pdf)を参照してください。

1. [!DNL Google BigQuery] コネクタを機能させるには、Adobe Campaign Classicで接続する次のパラメーターが必要です。

   * **[!UICONTROL プロジェクト]**:既存のプロジェクトを作成または使用します。

      詳しくは、[このページ](https://cloud.google.com/resource-manager/docs/creating-managing-projects)を参照してください。

   * **[!UICONTROL サービスアカウント]**:サービスアカウントを作成します。

      詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-accounts)を参照してください。

   * **[!UICONTROL キーファイルパス]**:サービス **[!UICONTROL アカウ]** ントには、ODBC を介し **[!UICONTROL た接]** 続に対するキ [!DNL Google BigQuery] ーファイルが必要です。

      詳しくは、[このページ](https://cloud.google.com/iam/docs/creating-managing-service-account-keys)を参照してください。

   * **[!UICONTROL データセット]**: **** ODBC 接続の場合、データセットはオプションです。各クエリはテーブルのあるデータセットを提供する必要があるので、Adobe Campaign Classicの [!DNL Google BigQuery]FDA コネクタには **[!UICONTROL データセット]** を指定する必要があります。

      詳しくは、[このページ](https://cloud.google.com/bigquery/docs/datasets)を参照してください。

1. Adobe Campaign Classicでは、[!DNL Google BigQuery] 外部アカウントを設定できます。 外部アカウントの設定方法について詳しくは、[ この節 ](#google-external) を参照してください。

### Windows での一括読み込みの設定 {#bulk-load-window}

>[!NOTE]
>
>Google Cloud SDK を動作させるには、Python がインストールされている必要があります。
>
>Python3 を使用することをお勧めします。詳しくは、[ ページ ](https://www.python.org/downloads/) を参照してください。

一括読み込みユーティリティを使用すると、Google Cloud SDK を通じて高速転送が可能です。

1. この [ ページ ](https://cloud.google.com/sdk/docs/downloads-versioned-archives) から Windows 64 ビット (x86_64) アーカイブをダウンロードし、対応するディレクトリに展開します。

1. `google-cloud-sdk\install.sh` スクリプトを実行します。 path 変数の設定を受け入れる必要があります。

1. インストール後に、パス変数 `...\google-cloud-sdk\bin` が設定されていることを確認します。 そうでない場合は、手動で追加します。

1. `..\google-cloud-sdk\bin\bq.cmd` ファイルに `CLOUDSDK_PYTHON` ローカル変数を追加します。この変数は、Python インストール先にリダイレクトされます。

   例：

   ![](assets/google-big-query_1.png)

1. Adobe Campaign Classicを再起動して、変更を反映します。

## Google BigQuery(Linux) {#google-linux}

### Linux でのドライバの設定 {#driver-linux}

1. ODBC ドライバーをインストールする前に、システムを更新する必要があります。 Linux または CentOS で、次のコマンドを実行します。

   ```
   yum update
   # install unixODBC driver manager
   yum install unixODBC
   ```

1. 次のコマンドを使用して、unixODBC ドライバーマネージャーをインストールする必要があります。

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

1. [Magnitude Simba Linux ODBC Driver (.tar.gz)](https://cloud.google.com/bigquery/docs/reference/odbc-jdbc-drivers) をダウンロードします。 次に、tarball ファイルをマシン上の一時フォルダーに転送するか、wget コマンドを使用します。

   ```
   # in this example driver version is 2.3.1.1001
   wget https://storage.googleapis.com/simba-bq-release/odbc/SimbaODBCDriverforGoogleBigQuery_[Version]-Linux.tar.gz
   ```

1. 主な tarball ファイルを次のように抽出します。 **TarballName** は、ドライバを含む tarball パッケージの名前です。

   ```
   tar --directory=/tmp -zxvf [TarballName]
   ```

1. 抽出したフォルダにアクセスし、ドライバのバージョンに対応する内部 tarball ファイルを抽出します。 次の例の BigQueryDriver で、別の一時フォルダーにインストールします。

   ```
   mkdir /tmp/BigQueryDriver/
   cd /tmp/SimbaODBCDriverforGoogleBigQuery_[Version]-Linux/
   tar --directory=/tmp/BigQueryDriver/ -zxvf SimbaODBCDriverforGoogleBigQuery[Bitness]_[Version].tar.gz
   ```

1. メインの tarball ファイルが抽出された一時的な場所にアクセスし、`GoogleBigQueryODBC.did` ファイルと `setup/simba.googlebigqueryodbc.ini` ファイルを、前の手順で作成した新しいフォルダーにコピーします。

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

1. インストールディレクトリの `simba.googlebigqueryodbc.ini` の `<INSTALLDIR>` を `/opt/simba/googlebigqueryodbc` に置き換えます。

   ```
   cd /opt/simba/googlebigqueryodbc/lib/
   sed -i 's/<INSTALLDIR>/\/opt\/simba\/googlebigqueryodbc/g' simba.googlebigqueryodbc.ini
   ```

1. `simba.googlebigqueryodbc.ini` で `DriverManagerEncoding` を UTF-16 に、`SwapFilePath` を  に変更します。 必要に応じて、ログ設定を変更することもできます。

   次の例は、更新されたドライバ全体の設定ファイルを示しています。

   ```
   # /opt/simba/googlebigqueryodbc/lib/simba.googlebigqueryodbc.ini
   [Driver]
   DriverManagerEncoding=UTF-16
   ErrorMessagesPath=opt/simba/googlebigqueryodbc/ErrorMessages
   LogLevel=6
   LogPath=/tmp
   SwapFilePath=/tmp
   ```

1. システムドライバファイルまたは現在の `odbcinst.ini` ファイルを使用している場合は、Google BigQuery ドライバの場所 `/opt/simba/googlebigqueryodbc/lib/libgooglebigqueryodbc_sb[Bitness].so` を指すように `/etc/odbcinst.ini` を設定します。

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

1. unixODBC ドライバーマネージャーライブラリの場所を探し、 `unixODBC` と `googlebigqueryodbc` ライブラリパスを `LD_LIBRARY_PATH environment` 変数に追加します。

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

1. Adobe Campaign Classicでは、[!DNL Google BigQuery] 外部アカウントを設定できます。 外部アカウントの設定方法について詳しくは、[ この節 ](#google-external) を参照してください。

### Linux での一括読み込みの設定 {#bulk-load-linux}

>[!NOTE]
>
>Google Cloud SDK を動作させるには、Python がインストールされている必要があります。
>
>Python3 を使用することをお勧めします。詳しくは、[ ページ ](https://www.python.org/downloads/) を参照してください。

一括読み込みユーティリティを使用すると、Google Cloud SDK を通じて高速転送が可能です。

1. この [ ページ ](https://cloud.google.com/sdk/docs/downloads-versioned-archives) に Linux 64 ビット (x86_64) アーカイブをダウンロードし、対応するディレクトリに展開します。

1. `google-cloud-sdk\install.sh` スクリプトを実行します。 path 変数の設定を受け入れる必要があります。

1. インストール後に、パス変数 `...\google-cloud-sdk\bin` が設定されていることを確認します。 そうでない場合は、手動で追加します。

1. `PATH` 変数を使用しない場合や、`google-cloud-sdk` ディレクトリを別の場所に移動する場合は、**[!UICONTROL 外部アカウント]** を設定する際に `bqpath` オプション値を使用して、システム上の bin ディレクトリの正確なパスを指定します。

1. Adobe Campaign Classicを再起動して、変更を反映します。

## Google BigQuery 外部アカウント {#google-external}

Adobe Campaign Classicインスタンスを [!DNL Google BigQuery] 外部データベースに接続するには、[!DNL Google BigQuery] 外部アカウントを作成する必要があります。

1. Adobe Campaign Classic **[!UICONTROL エクスプローラー]** から、**[!UICONTROL 管理]** &#39;>&#39; **[!UICONTROL プラットフォーム]** &#39;>&#39; **[!UICONTROL 外部アカウント]** をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. [!DNL Google BigQuery] 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：[!DNL Google BigQuery]

   * **[!UICONTROL サービスアカウント]**:サービスアカウント **[!UICONTROL の電子メール]**。詳しくは、[Google Cloud のドキュメント ](https://cloud.google.com/iam/docs/creating-managing-service-accounts) を参照してください。

   * **[!UICONTROL プロジェクト]**:プロジェクト **[!UICONTROL の名前]**。詳しくは、[Google Cloud のドキュメント ](https://cloud.google.com/resource-manager/docs/creating-managing-projects) を参照してください。

   * **[!UICONTROL キーファイルのパス]**:
      * **[!UICONTROL キーファイルをサーバーにアップロードします]**。「 Adobe Campaign Classicを使 **[!UICONTROL 用してキーをアッ]** プロードする場合は、ここをクリックしてアップロードします」を選択します。

      * **[!UICONTROL 手動でキーのファイルパスを入力します]**。既存のキーを使用する場合は、このフィールドに絶対パスをコピー&amp;ペーストします。
   * **[!UICONTROL データセット]**:データセット **[!UICONTROL の名前]**。詳しくは、[Google Cloud のドキュメント ](https://cloud.google.com/bigquery/docs/datasets-intro) を参照してください。
   ![](assets/google-big-query.png)
