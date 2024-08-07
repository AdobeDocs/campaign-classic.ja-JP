---
product: campaign
title: Teradata へのアクセスの設定
description: FDA でTeradataへのアクセスを設定する方法を学ぶ
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 3a5856c3-b642-4722-97ff-6ae7107efdbe
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 66%

---

# Teradata へのアクセスの設定 {#configure-access-to-teradata}



Campaign [Federated Data Access](../../installation/using/about-fda.md) （FDA）オプションを使用して、外部データベースに保存されている情報を処理します。 teradataへのアクセスを設定するには、次の手順に従います。

1. [Teradata ドライバのインストールと構成 ](#teradata-config)
1. Campaign でのTeradata[ 外部アカウント ](#teradata-external) の設定
1. teradataおよび Campaign サーバーの [ 追加設定 ](#teradata-additional-configurations) を設定します

## Teradata設定 {#teradata-config}

Campaign への接続を実装するには、Teradataのドライバーをインストールする必要があります。

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
     Driver=/opt/teradata/client/17.10/lib64/tdataodbc_sb64.so
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
>FDA でTeradata外部データベースに接続するには、Adobe Campaign サーバーで追加の設定手順が必要です。 [詳細情報](#teradata-additional-configurations)。
>

## Teradata 外部アカウント{#teradata-external}

teradata外部アカウントを使用すると、Campaign インスタンスをTeradata外部データベースに接続できます。

1. Campaign **[!UICONTROL エクスプローラー]** で、**[!UICONTROL 管理]**/**[!UICONTROL プラットフォーム]**/**[!UICONTROL 外部アカウント]** をクリックします。

1. 「**[!UICONTROL 新規]**」をクリックし、「**[!UICONTROL タイプ]**」として「**[!UICONTROL 外部データベース]**」を選択します。

   ![](assets/ext_account_19.png)

1. Teradata **[!UICONTROL 外部アカウントを設定するには]**、次を指定する必要があります。

   * **[!UICONTROL 種類]**: **[!UICONTROL Teradata]** の種類を選択します。

   * **[!UICONTROL Server]**:Teradataサーバーの URL または名前

   * **[!UICONTROL アカウント]**:Teradataデータベースへのアクセスに使用するアカウント名

   * **[!UICONTROL Password]**:Teradataデータベースへの接続に使用するパスワード

   * **[!UICONTROL Database]**：データベースの名前（オプション）

   * **[!UICONTROL Options]**:Teradataを通じて渡されるオプション。 「parameter=value」の形式を使用します。 値間の区切り文字としてセミコロンを使用します。

   * **[!UICONTROL タイムゾーン]**:Teradataに設定されたタイムゾーン。 [詳細情報](#timezone)

コネクタは、次のオプションをサポートしています。

| オプション | 説明 |
|---|---|
| TD_MAX_SESSIONS | オペレータージョブに対してTeradata パラレル トランスポーターが取得できるログオン セッションの最大数を指定します。 |
| TimeZoneName | サーバータイムゾーンの名前。 |
| CharacterSet | teradata文字セットの設定に使用します。 <br>詳しくは、[このページ](https://docs.teradata.com/r/ODBC-Driver-for-Teradata-User-Guide/May-2017/Configuration-of-odbc.ini-in-UNIX/Linux-and-Apple-OS-X/Teradata-DSN-Options#rub1478609534082__table_N102D3_N102B6_N102B3_N10001)を参照してください。 |
| IANAAppCodePage | ODBC アプリケーション コード ページ。 <br> 詳しくは、[ このページ ](https://docs.teradata.com/r/ODBC-Driver-for-Teradata-User-Guide/May-2017/ODBC-Driver-for-Teradata-Application-Development/International-Character-Set-Support/Application-Code-Page) を参照してください。 |

### 追加の ODBC 外部アカウント {#add-external}

>[!NOTE]
>
> このオプションは、バージョン 7.3.1 より古いビルドでは使用できません。

teradata ドライバは独自の ODBC ライブラリを提供しますが、このライブラリは他の ODBC 外部アカウントと互換性がない可能性があります。

ODBC も使用する別の外部アカウント（Snowflakeなど）を設定する場合は、デフォルトの ODBC ライブラリ（Debian の場合は `/usr/lib/x86_64-linux-gnu/libodbc.so`、RHEL/CentOS の場合は `/usr/lib64/libodbc.so`）のパスに ODBCLib オプションを追加する必要があります。

![](assets/ext_account_24.png)

### Query Banding

複数の Adobe Campaign ユーザーが同じ FDA Teradata 外部アカウントに接続する場合は、「**[!UICONTROL Query banding]**」タブを使用するとクエリバンドを設定できます（例：セッションでのキー／値のペアのセットなど）。

![](assets/ext_account_20.png)

このオプションを設定すると、Campaign ユーザーがTeradataデータベースに対してクエリを実行するたびに、Adobe Campaignからメタデータが送信されます。メタデータは、このユーザーに関連付けられたキーのリストで構成されます。 Teradata 管理者は、このデータを監査目的や、アクセス権の管理に使用できます。

>[!NOTE]
>
>**[!UICONTROL Query banding]** について詳しくは、[Teradata ドキュメント](https://docs.teradata.com/reader/cY5B~oeEUFWjgN2kBnH3Vw/a5G1iz~ve68yTMa24kVjVw)を参照してください。

クエリバンドを設定するには、次の手順に従います。

1. **[!UICONTROL Default]** を使用して、ユーザーに関連付けられたクエリーの帯がない場合に使用されるデフォルトのクエリーの帯を入力します。 このフィールドが空になっている場合、クエリバンドがないユーザーは Teradata を使用できません。

1. 「**[!UICONTROL ユーザー]**」フィールドを使用して、各ユーザーのクエリの帯を指定します。 キーと値のペアを必要な数だけ追加できます。例：priority=1;workload=highユーザーにクエリバンドが割り当てられていない場合は、「**[!UICONTROL デフォルト]**」フィールドが適用されます。

1. この機能を有効にするには、「**[!UICONTROL アクティブ]**」ボックスをオンにします。

#### 外部アカウントのトラブルシューティング {#external-account-troubleshooting}

接続のテスト中にエラー **TIM-030008 Date &#39;2&#39;: missing character(s) (iRc=-53)**、が表示される場合は、ODBC ドライバーが正しくインストールされていること、および Campaign サーバーに対して LD_LIBRARY_PATH（Linux）または PATH（Windows）が設定されていることを確認してください。

エラー **ODB-240000 ODBC error: [Microsoft][ODBC Driver Manager] Data source name not found and no default driver specified.** は、Windows で 16.X ドライバーを使用した場合に発生します。Adobe Campaignでは、odbcinst.ini のteradataに&#39;{teradata}&#39;という名前を付ける必要があります。

* Campaign 18.10 以降では、外部アカウントのオプションに ODBCDriverName=&quot;Teradataデータベース ODBC ドライバー 16.10&quot;を追加できます。 バージョン番号は変更できます。正確な名前は、odbcad32.exe を実行して [ ドライバ ] タブにアクセスすることで見つけることができます。

* 古いバージョンの Campaign を使用している場合は、ドライバのインストール時に作成された odbcinst.ini のTeradata セクションを、Teradataという新しいセクションにコピーする必要があります。 この場合は、Regedit を使用できます。 ベースが latin1 の場合は、オプションに **APICharSize=1** を追加する必要があります。

## その他の設定 {#teradata-additional-configurations}

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

外部データベースに次の権限が必要です：カスタムプロシージャの作成/ドロップ/実行、テーブルの作成/ドロップ/挿入/選択。 また、Adobe Campaign インスタンスで md5 および sha2 関数を使用する場合は、ユーザーモード関数を作成する必要が生じる場合もあります。

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

### SHA2 インストール {#sha2-installation}

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

### UDF_UTF16TO8 インストール {#UDF-UTF16TO8-installation}

Adobe Campaign インスタンスで udf_utf16to8 関数を使用する場合は、**Teradata Unicode ツールキット** からTeradataデータベースにユーザーモード関数をインストールします。

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

## Linux 用 Campaign サーバーの設定 {#campaign-server-linux}

ドライバーのインストールには次が必要です。

* Teradata ODBC ドライバー（この[ページ](https://downloads.teradata.com/download/connectivity/odbc-driver/linux)にあります）

* Teradata ツールおよびユーティリティ（一括読み込みに使用）（この[ページ](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-linux-installation-package-0)にあります）

ファイル名と sha1：

* tdodbc1620__linux_indep.16.20.00.00-1.tar.gz 121fdd978b56fe1304fc5cb7819741b0847f44fd

* TeradataToolsAndUtilitiesBase__linux_indep.16.20.01.00.tar.gz b 29d0af5ffd8dcf68a9dbbaa6f8639387b19c563

お使いの Linux ディストリビューション用のパッケージがない場合は、CentOS 7 での説明に従ってインストール（例えば docker を使用）し、Adobe Campaign サーバーの /opt/teradata の内容をコピーします。

### ODBC ドライバのインストール {#odbc-installation}

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

## Windows 用 Campaign サーバーの設定 {#campaign-server-windows}

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
