---
title: Hadoop へのアクセスの設定
description: FDAでのHadoopへのアクセスを設定する方法
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
translation-type: tm+mt
source-git-commit: 9bbde65aea6735e30e95e75c2b6ae5445d4a2bdd
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 84%

---


# Hadoop へのアクセスの設定 {#configure-access-to-hadoop}

キャンペーン **Federated Data Access** (FDA)オプションを使用して、外部データベースに保存された情報を処理します。 次の手順に従って、Hadoopへのアクセスを設定します。

1. Hadoopデータベース [の設定](#configuring-hadoop)
1. キャンペーンでのHadoop [外部アカウントの設定](#hadoop-external)

## Hadoop 3.0 の設定 {#configuring-hadoop}

FDA で Hadoop 外部データベースに接続するには、Adobe Campaign サーバーで次の設定が必要になります。この設定は、Windows と Linux の両方で利用できます。

1. ご使用の OS のバージョンに応じて、Hadoop 用の ODBC ドライバーをダウンロードします。ドライバーは[このページ](https://www.cloudera.com/downloads.html)にあります。

1. 次に、ODBC ドライバーをインストールし、Hive 接続用の DSN を作成する必要があります。手順は、[このページ](https://docs.cloudera.com/documentation/other/connectors/hive-odbc/2-6-5/Cloudera-ODBC-Driver-for-Apache-Hive-Install-Guide.pdf)に記載されています。

1. ODBC ドライバーをダウンロードしてインストールした後、Campaign Classic を再起動する必要があります。これをおこなうには、次のコマンドを実行します。

   ```
   systemctl stop nlserver.service
   systemctl start nlserver.service
   ```

1. Campaign Classic では、[!DNL Hadoop] 外部アカウントを設定できます。For more on how to configure your external account, refer to [this section](#hadoop-external).

## Hadoop 外部アカウント {#hadoop-external}

[!DNL Hadoop] 外部アカウントを使用すれば、Campaign インスタンスを Hadoop 外部データベースに接続することができます。

1. Campaign Classic で、[!DNL Hadoop] 外部アカウントを設定します。**[!UICONTROL エクスプローラー]**&#x200B;で、**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL 外部アカウント]**&#x200B;をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックします。

1. 外部アカウント&#x200B;**[!UICONTROL タイプ]**&#x200B;として、「**[!UICONTROL 外部データベース]**」を選択します。

1. **[!UICONTROL Hadoop]** 外部アカウントを設定するには、次を指定する必要があります。

   * **[!UICONTROL タイプ]**：ODBC（Sybase ASE、Sybase IQ）

   * **[!UICONTROL サーバー]**：DNS の名前

   * **[!UICONTROL アカウント]**：ユーザーの名前

   * **[!UICONTROL パスワード]**：ユーザーアカウントのパスワード

   * **[!UICONTROL データベース]**：DSN で指定されていない場合のデータベースの名前。DSN で指定した場合は、空のままにできます

   * **[!UICONTROL タイムゾーン]**：サーバーのタイムゾーン

   ![](assets/hadoop3.png)

コネクタは、次の ODBC オプションをサポートしています。

| 名前 | 値 |
|---|---|
| ODBCMgr | iODBC |
| warehouse | 1/2/4 |

コネクタは、次の Hive オプションもサポートします。

| 名前 | 値 | 説明 |
|---|---|---|
| bulkKey | Azure BLOB または DataLake アクセスキー | wasb:// または wasbs:// の一括ローダーの場合（wasb:// または wasbs:// で始まる一括ロードツールの場合）。<br>一括読み込みの BLOB または DataLake バケットのアクセスキーです。 |
| hdfsPort | ポート番号<br>（デフォルトでは 8020 に設定） | HDFS の一括ローダーの場合（webhdfs:// または webhdfss:// で始まる一括ロードツールの場合）。 |
| bucketsNumber | 20 | クラスター化テーブルを作成する際のバケット数。 |
| fileFormat | PARQUET | 作業用テーブルのデフォルトのファイル形式です。 |


## Hadoop 2.1 の設定 {#configure-access-hadoop-2}

Hadoop 2.1に接続する必要がある場合は、 [Windows](#for-windows) または [Linuxで次に説明する手順に従います](#for-linux)。

### Windows用Hadoop 2.1 {#for-windows}

1. Windows 用の ODBC ドライバーと [Azure HD Insight](https://www.microsoft.com/en-us/download/details.aspx?id=40886) ドライバーをインストールします。
1. ODBC DataSource Adminstrator ツールを実行して、DSN（データソース名）を作成します。ユーザーが変更できる Hive 用 System DSN サンプルが提供されています。

   ```
   Description: vorac (or any name you like)
   Host: vorac.azurehdinsight.net
   Port: 443
   Database: sm_tst611 (or your database name)
   Mechanism: Azure HDInsight Service
   User/Password: admin/<your password here>
   ```

1. Create the Hadoop external account, as detailed in [this section](#hadoop-external).

### Hadoop 2.1（Linux用） {#for-linux}

1. Linux 用の unixODBC をインストールします。

   ```
   apt-get install unixodbc
   ```

1. HortonWorks（[https://www.hortonworks.com/downloads/](https://www.hortonworks.com/downloads/)）から Apache Hive 用の ODBC ドライバーをダウンロードして、インストールします。

   ```
   dpkg -i hive-odbc-native_2.1.10.1014-2_amd64.deb
   ```

1. ODBC ファイルの場所を確認します。

   ```
   root@campadpac71:/tmp# odbcinst -j
   unixODBC 2.3.1
   DRIVERS............: /etc/odbcinst.ini
   SYSTEM DATA SOURCES: /etc/odbc.ini
   FILE DATA SOURCES..: /etc/ODBCDataSources
   USER DATA SOURCES..: /root/.odbc.ini
   SQLULEN Size.......: 8
   SQLLEN Size........: 8
   SQLSETPOSIROW Size.: 8
   ```

1. DSN（データソース名）を作成し、odbc.ini ファイルを編集します。次に、Hive 接続用の DSN を作成します。

   HDInsight で「バイラル」と呼ばれる接続を設定する場合の例を以下に示します。

   ```
   [ODBC Data Sources]
   vorac 
   
   [vorac]
   Driver=/usr/lib/hive/lib/native/Linux-amd64-64/libhortonworkshiveodbc64.so
   HOST=vorac.azurehdinsight.net
   PORT=443
   Schema=sm_tst611
   HiveServerType=2
   AuthMech=6
   UID=admin
   PWD=<your password here>
   HTTPPath=
   UseNativeQuery=1
   ```

   >[!NOTE]
   >
   >ここで、**UseNativeQuery** パラメーターは非常に重要です。Campaign は Hive 対応ですが、UseNativeQuery を設定しないと正しく機能しません。通常、ドライバーまたは Hive SQL コネクタがクエリを上書きして列の順序を勝手に変更してしまいます。

   認証設定は Hive や Hadoop の構成に依存します。例えば HD Insight では、[ここ](https://www.simba.com/products/Spark/doc/ODBC_InstallGuide/unix/content/odbc/hi/configuring/authenticating/azuresvc.htm)で説明しているように、ユーザー／パスワード認証に AuthMech=6 を使用します。

1. 変数をエクスポートします。

   ```
   export ODBCINI=/etc/myodbc.ini
   export ODBCSYSINI=/etc/myodbcinst.ini
   ```

1. Hortonworks ドライバーを /usr/lib/hive/lib/native/Linux-amd64-64/hortonworks.hiveodbc.ini を介して設定します。

   Campaign と unix-odbc（libodbcinst）に接続するには、UTF-16 を使用する必要があります。

   ```
   [Driver]
   
   DriverManagerEncoding=UTF-16
   ErrorMessagesPath=/usr/lib/hive/lib/native/hiveodbc/ErrorMessages/
   LogLevel=0
   LogPath=/tmp/hive
   SwapFilePath=/tmp
   
   ODBCInstLib=libodbcinst.so
   ```

1. これで、isql を使用した接続をテストできます。

   ```
   isql vorac
   isql vorac -v
   ```

1. Create the Hadoop external account, as detailed in [this section](#hadoop-external).

