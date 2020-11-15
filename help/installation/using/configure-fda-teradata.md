---
title: Teradata へのアクセスの設定
description: FDAでTeradataへのアクセスを設定する方法を説明します
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
translation-type: tm+mt
source-git-commit: 022fe39e849ceafa6678120ff455d07432fb9a1f
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 80%

---


# Teradata へのアクセスの設定 {#configure-access-to-teradata}

キャンペーン [Federated Data Access](../../installation/using/about-fda.md) (FDA)オプションを使用して、外部データベースに保存された情報を処理します。 次の手順に従って、Teradataへのアクセスを設定します。

1. Teradataドライバーのインスト [ールと構成](#teradata-config)
1. キャンペーンでのTeradata [外部アカウントの設定](#teradata-external)
1. Teradataおよびキャンペーンサーバーの [追加設定](#teradata-additional-configurations)

## Teradata設定 {#teradata-config}

キャンペーンへの接続を実装するには、Teradata用のドライバをインストールする必要があります。

1. [Teradata 用の ODBC ドライバー](https://downloads.teradata.com/download/connectivity/odbc-driver/linux)をインストールします。

   これは 3 つのパッケージで構成され、Red Hat（または CentOS）／Suse に次の順序でインストールできます。

   * TeraGSS
   * tdicu1510（setup_wrapper.sh を使用してインストール）
   * tdodbc1510（setup_wrapper.sh を使用してインストール）

1. ODBC ドライバーを設定します。設定は、標準のファイル（一般的なパラメーターは **/etc/odbc.ini**、ドライバーの宣言は /etc/odbcinst.ini）でおこなえます。

   * **/etc/odbc.ini**

      ```
      [ODBC]
      InstallDir=/etc/
      ```

      「InstallDir」は、**odbcinst.ini** ファイルの保存場所です。

   * **/etc/odbcinst.ini**

      ```
      [ODBC DRIVERS]
      teradata=Installed
      
      [teradata]
      Driver=/opt/teradata/client/15.10/lib64/tdata.so
      APILevel=CORE
      ConnectFunctions=YYY
      DriverODBCVer=3.51
      SQLLevel=1
      ```

1. Adobe Campaign サーバーの環境変数を指定します。

   * **LD_LIBRARY_PATH**：/opt/teradata/client/15.10/lib64 および /opt/teradata/client/15.10/odbc_64/lib。
   * **ODBCINI**：odbc.ini ファイルの保存場所（例：/etc/odbc.ini）。
   * **NLSPATH**：opermsgs.cat ファイルの保存場所（/opt/teradata/client/15.10/msg/opermsgs.cat）。

>[!NOTE]
>
>FDAでTeradata外部データベースに接続するには、Adobe Campaignサーバーで追加の設定手順が必要です。 [詳細情報](#teradata-additional-configurations)。


## Teradata 外部アカウント{#teradata-external}

Teradata 外部アカウントを使用すれば、Campaign インスタンスを Teradata 外部データベースに接続することができます。

1. From Campaign **[!UICONTROL Explorer]**, click **[!UICONTROL Administration]** / **[!UICONTROL Platform]** / **[!UICONTROL External accounts]**.

1. 「**[!UICONTROL 新規]**」をクリックし、「**[!UICONTROL タイプ]**」として「**[!UICONTROL 外部データベース]**」を選択します。

   ![](assets/ext_account_19.png)

1. Teradata **[!UICONTROL 外部アカウントを設定するには]**、次を指定する必要があります。

   * **[!UICONTROL タイプ]**:「 **[!UICONTROL Teradata]** 」タイプを選択します。

   * **[!UICONTROL サーバー]**:TeradataサーバーのURLまたは名前

   * **[!UICONTROL アカウント]**:Teradataデータベースへのアクセスに使用するアカウントの名前

   * **[!UICONTROL パスワード]**:Teradataデータベースへの接続に使用するパスワード

   * **[!UICONTROL データベース]**:データベースの名前（オプション）

   * 
      * **[!UICONTROL オプション]**:Teradata経由で渡すオプションです。 次の形式を使用します。&#39;parameter=value&#39;. 値の区切り文字としてセミコラムを使用します。
   * 
      * **[!UICONTROL タイムゾーン]**:Teradataで設定されるタイムゾーン。 [詳細情報](#timezone)


### Query Banding

複数の Adobe Campaign ユーザーが同じ FDA Teradata 外部アカウントに接続する場合は、「**[!UICONTROL Query banding]**」タブを使用するとクエリバンドを設定できます（例：セッションでのキー／値のペアのセットなど）。

![](assets/ext_account_20.png)

このオプションを設定すると、キャンペーンユーザーがTeradataデータベースでクエリを実行するたびに、Adobe Campaignは、このユーザーに関連付けられたキーのリストで構成されるメタデータを送信します。 Teradata 管理者は、このデータを監査目的や、アクセス権の管理に使用できます。

>[!NOTE]
>
>**[!UICONTROL Query banding]** について詳しくは、[Teradata ドキュメント](https://docs.teradata.com/reader/cY5B~oeEUFWjgN2kBnH3Vw/a5G1iz~ve68yTMa24kVjVw)を参照してください。

クエリバンディングを設定するには、次の手順に従います。

1. Use the  **[!UICONTROL Default]** to enter a default query band that will be used if a user has no associated query band. このフィールドが空になっている場合、クエリバンドがないユーザーは Teradata を使用できません。

1. Use the **[!UICONTROL Users]** field to specify a query band for each user. キーと値のペアを必要な数だけ追加できます。例：priority=1;workload=highユーザーにクエリバンドが割り当てられていない場合は、「**[!UICONTROL デフォルト]**」フィールドが適用されます。

1. この機能を有効にするには、「**[!UICONTROL アクティブ]**」ボックスをオンにします。

#### 外部アカウントのトラブルシューティング {#external-account-troubleshooting}

接続のテスト中にエラー **TIM-030008 Date &#39;2&#39;: missing character(s) (iRc=-53)**、が表示される場合は、ODBC ドライバーが正しくインストールされていること、および Campaign サーバーに対して LD_LIBRARY_PATH（Linux）または PATH（Windows）が設定されていることを確認してください。

エラー **ODB-240000 ODBC error: [Microsoft][ODBC Driver Manager] Data source name not found and no default driver specified.** は、Windows で 16.X ドライバーを使用した場合に発生します。Adobe Campaign の odbcinst.ini では、Teradata のメタデータ名は「{teradata}」である必要があります。


* キャンペーン18.10から、外部アカウントのオプションにODBCDriverName=&quot;Teradata Database ODBC Driver 16.10&quot;を追加できます。 バージョン番号は異なる場合があります。正確な番号は、odbcad32.exe を実行して「ドライバー」タブにアクセスすると見つかります。


* 古いキャンペーンバージョンを使用している場合は、ドライバのインストールで作成されたodbcinst.iniのTeradataセクションをTeradataという新しいセクションにコピーする必要があります。 この場合は、Regeditを使用できます。 If your base is in latin1, you will have to add **APICharSize=1** in the options.

## 任意の追加設定 {#teradata-additional-configurations}

<!--
### Compatibility {#teradata-compatibility}

**Based in Unicode**

| Database version | Driver version |  Minimal Campaign version required |  Note |
|:-:|:-:|:-:|:-:|
| 15  |  15 |  Campaign Classic 17.9 | Under Linux: Queries with timestamp may fail (fixed in build 8937 for 18.4 and 8977 for 18.10) In debug mode, warnings relative to bad memory usage in the driver may occur. |
| 15  | 16  | Campaign Classic 17.9  | Recommended setup for a Teradata 15 database under Linux.  |
|  16 | 16  | Campaign Classic 18.10 |  Unicode characters with surrogate pairs are not fully handled. Using surrogate characters in data should work. Using surrogates in a filtering condition of a query will not work without this change. |
| 16  |  15 |  Campaign Classic 19.0 |  &nbsp; |

**Based in Latin1**

Versions previous to Adobe Campaign Classic 17.9 only supported Teradata Latin-1 database.

Starting from Adobe Campaign Classic 17.9, we now support by default Teradata database in Unicode.

Customers with a Latin-1 Teradata database migrating to a recent Campaign Classic release will have to add the parameter APICharSize=1 in the options of the external account.
-->

### ユーザー設定 {#user-configuration}

外部データベースには、次の権限が必要です。カスタムプロシージャの作成/ドロップ/実行、テーブルの作成/ドロップ/挿入/選択 また、Adobe Campaign インスタンスで md5 および sha2 関数を使用する場合は、ユーザーモード関数を作成する必要が生じる場合もあります。

正しいタイムゾーンを設定してください。タイムゾーンは、Adobe Campaign インスタンスで作成される外部アカウントで設定される値と一致する必要があります。

Adobe Campaign は、データベース内で作成するオブジェクトに対して保護モード（フォールバック）を設定しません。次のクエリを使用して、Adobe Campaign が Teradata データベースへの接続に使用するデフォルトをユーザーに対して設定する必要がある場合があります。

| disable default fallback |
| :-: |
| ```MODIFY USER $login$ AS NO FALLBACK;``` |

### MD5 のインストール {#md5-installation}

Adobe Campaign インスタンスで md5 関数を使用する場合は、この[ページ](https://downloads.teradata.com/download/extensibility/md5-message-digest-udf)の Teradata データベースにユーザーモード関数をインストールする必要があります（md5_20080530.zip）。

ダウンロードファイルの sha1 は「65cc0bb6935f72fcd84fef1ebcd64c00115dfd1e」です。

md5 をインストールするには、以下を実行します。

1. md5_20080530.zip ファイルを解凍します。

1. md5/src ディレクトリに移動します。

1. bteq を使用して Teradata データベースに接続します。

1. 次の bteq コマンドを実行します。

   ```
   .run file = hash_md5.btq
   ```

### SHA2 のインストール {#sha2-installation}

Adobe Campaign インスタンスで sha2 関数を使用する場合は、この[ページ](https://github.com/akuroda/teradata-udf-sha2/archive/v1.0.zip)から Teradata データベースにユーザーモード関数をインストールする必要があります（teradata-udf-sha2-1.0.zip）。

ダウンロードファイルの sha1 は「e87438d37424836358bd3902cf1adeb629349780」です。

sha2 をインストールするには、以下を実行します。

1. teradata-udf-sha2-1.0.zip ファイルを解凍します。

1. teradata-udf-sha2-1.0/src ディレクトリに移動します。

1. bteq を使用して Teradata データベースに接続します。

1. 次の 2 つの bteq コマンドを実行します。

   ```
   .run file = hash_sha256.sql
   .run file = hash_sha512.sql
   ```

### UDF_UTF16TO8 のインストール {#UDF-UTF16TO8-installation}

Adobe Campaign インスタンスで udf_utf16to8 関数を使用する場合は、この[ページ](https://downloads.teradata.com/download/tools/unicode-tool-kit)の **Teradata unicode ツールキット**（utk_release1.7.0.0.zip）から Teradata データベースにユーザーモード関数をインストールする必要があります。

ダウンロードファイルの sha1 は「e58235f434f52c71316a577cb48e20b97d24f470」です。

udf_utf16to8 をインストールするには、以下を実行します。

1. utk_release1.7.0.0.zip ファイルを解凍します。

1. 抽出したファイルから udf_utf16to8.o を探し、このファイルが格納されているディレクトリに移動します。ディレクトリの名前は utk_release1.7.0.0/utk_release1.7.0.0/04 TranslationUDFs/01 Teradata UDFs/suselinux-x8664/udf_installation/ です。

1. bteq を使用して Teradata データベースに接続します。

1. 次の bteq コマンドを入力します。

   ```
   REPLACE FUNCTION udf_utf16to8 (
   inputString VARCHAR(8000) CHARACTER SET UNICODE
   ) RETURNS VARCHAR(16000) CHARACTER SET LATIN
   LANGUAGE C
   NO SQL
   EXTERNAL NAME 'CO!i18n103!udf_utf16to8.o!F!udf_utf16to8'
   PARAMETER STYLE SQL;
   
   -- Test: should return 410042
   SELECT CAST(Char2HexInt(UDF_UTF16to8(_UNICODE'004100000042'XC)) AS VARCHAR(100));
   ```

## Linux の Campaign サーバー設定 {#campaign-server-linux}

ドライバーのインストールには次が必要です。

* Teradata ODBC ドライバー（この[ページ](https://downloads.teradata.com/download/connectivity/odbc-driver/linux)にあります）

* Teradata ツールおよびユーティリティ（一括読み込みに使用）（この[ページ](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-linux-installation-package-0)にあります）

ファイル名と sha1：

* tdodbc1620__linux_indep.16.20.00.00-1.tar.gz 121fdd978b56fe1304fc5cb7819741b0847f44fd

* TeradataToolsAndUtilitiesBase__linux_indep.16.20.01.00.tar.gz b 29d0af5ffd8dcf68a9dbbaa6f8639387b19c563

お使いの Linux ディストリビューション用のパッケージがない場合は、CentOS 7 での説明に従ってインストール（例えば docker を使用）し、Adobe Campaign サーバーの /opt/teradata の内容をコピーします。

### ODBC ドライバーのインストール {#odbc-installation}

ODBC ドライバーをインストールするには、以下を実行します。

1. tdodbc1620__linux_indep.16.20.00.00-1.tar.gz ファイルを抽出します。

1. tdodbc1620 ディレクトリに移動します。

1. セットアップスクリプトの修正が必要になる場合があります。

   ```
   "sed -i s/16.10/16.20/ setup_wrapper.sh".
   ```

1. setup_wrapper.sh を実行します。

### Teradata ツールとユーティリティのインストール {#teradata-tools-installation}

ツールをインストールするには、以下を実行します。

1. TeradataToolsAndUtilitiesBase__linux_indep.16.20.01.00.tar.gz ファイルを展開します。

1. TeradataToolsAndUtilitiesBase/Linux/i386-x8664/tdicu ディレクトリに移動します。

1. setup_wrapper.sh を実行します。

1. TeradataToolsAndUtilitiesBase/Linux/i386-x8664/cliv2 ディレクトリに移動します。

1. setup_wrapper.sh を実行します。

1. TeradataToolsAndUtilitiesBase/Linux/i386-x8664/tptbase ディレクトリに移動します。

1. setup_wrapper.sh を実行します。

1. Libtelapi.so ファイルは /opt/teradata/client/16.20/lib64 にあります。

## Windows の Campaign サーバーの設定 {#campaign-server-windows}

最初に、Windows 用の Teradata ツールとユーティリティをダウンロードする必要があります。この[ページ](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package)からダウンロードできます。

ODBC ドライバーと Teradata Parallel Transporter Base を必ずインストールしてください。Teradata データベースに一括読み込みをおこなう際に使用する telapi.dll をインストールします。

ドライバーとユーティリティのパスが、実行中に nlserver が持つ PATH 変数に含まれていることを確認します。デフォルトパスは C:\Program Files (x86)\Teradata\Client\15.10\bin（Windows 32 ビット）または C:\Program Files\Teradata\Client\15.10\bin（64 ビット）です。

## タイムゾーン {#timezone}

Teradata は、標準ではないタイムゾーン名を使用しています。リストは [Teradata サイト](https://docs.teradata.com/reader/rgAb27O_xRmMVc_aQq2VGw/oGKvgl7gCeBMTGrp59BnwA)で見つかります。Adobe Campaign は、外部設定で指定されたタイムゾーンを Teradata が理解できるものに変換しようとします。該当するものが見つからない場合は、セッションに一番近い GMT+X（または GMT-X）タイムゾーンが使用されて、ログに警告が表示されます。

変換は、teradata_timezones.txt ファイルを読み取っておこなわれます。このファイルは linux では datakit ディレクトリ（/usr/local/neolane/nl6/datakit）にあります。このファイルを編集する場合は、Adobe Campaign チームに連絡してソースコードを変更してください。これを怠ると、次回 Campaign アップデートした時にこのファイルが上書きされます。

接続に使用されるタイムゾーンは、nlserver を -verbose スイッチで実行するときに示されます。例：

```
15:04:04 >   ODB-240007 Teradata: will use 'Europe Central' as session time zone.
```

使用するタイムゾーンが正しくない場合は、外部アカウントに「TimeZoneName」オプションを追加できます。この場合は、「TimeZoneName=Europe Central」のように Teradata 値を使用します。

Teradata ドキュメントで一括読み込みまたは「高速読み込み」を使用している場合、Campaign はタイムゾーンを示すことができません。したがって、Campaign が接続に使用するユーザーのデフォルトのタイムゾーンを設定することをお勧めします。

```
MODIFY USER $login$ AS TIME ZONE = 'Europe Central';
```
