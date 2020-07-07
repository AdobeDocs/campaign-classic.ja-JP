---
title: 付録
seo-title: FDA付録
description: FDA付録
seo-description: null
page-status-flag: never-activated
uuid: 2596fabc-679a-45c8-a62a-165c221654b7
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: a84a73a9-9930-449f-8b81-007a0e9d5233
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 353f5df040087175c9f211308704f1af1844ef2c
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 1%

---


# 付録 {#fda-appendices}

## Teradata追加の設定 {#teradata-configuration}

### 互換性 {#teradata-compatibility}

**Unicodeベース**

| データベースのバージョン | ドライバーのバージョン | 最小限のキャンペーンバージョンが必要 | 注意 |
|:-:|:-:|:-:|:-:|
| 15 | 15 | Campaign Classic17.9 | Linuxの場合： タイムスタンプのあるクエリは失敗する場合があります（18.4の場合は8937でビルド、18.10の場合は8977で修正）。デバッグモードでは、ドライバのメモリ使用量の不良に関する警告が発生する場合があります。 |
| 15 | 16 | Campaign Classic17.9 | LinuxでのTeradata 15データベースの推奨セットアップ。 |
| 16 | 16 | Campaign Classic18.10 | サロゲートペアを持つUnicode文字は、完全には処理されません。 データでのサロゲート文字の使用は、有効です。 クエリのフィルタリング条件でサロゲートを使うのは、この変更なしでは動作しません。 |
| 16 | 15 | サポートされていません |   |

**Latin1に基づく**

Adobe CampaignClassic 17.9より前のバージョンでは、Teradata Latin-1データベースのみがサポートされていました。

Adobe CampaignClassic 17.9以降、UnicodeのデフォルトのTeradataデータベースがサポートされるようになりました。

Latin-1 Teradataデータベースを最新のCampaign Classicリリースに移行する場合は、外部アカウントのオプションにパラメータAPICharSize=1を追加する必要があります。

### データベースの設定 {#database-configuration}

#### ユーザー設定 {#user-configuration}

次の権限が必要です。 カスタムプロシージャの作成/ドロップ/実行、テーブルの作成/ドロップ/挿入/選択 また、Adobe Campaignインスタンスでmd5およびsha2関数を使用する場合は、ユーザーモード関数を作成する必要がある場合もあります。

正しいタイムゾーンを設定してください。 これは、Adobe Campaignインスタンスで作成される外部アカウントで設定される値と一致する必要があります。

Adobe Campaignは、データベース内で作成するオブジェクトに対して保護モード（フォールバック）を設定しません。 次のクエリを使用して、Adobe CampaignがTeradataデータベースへの接続に使用するデフォルトのユーザーを設定する必要がある場合があります。

| デフォルトのフォールバックを無効にする |
| :-: |
| ```MODIFY USER $login$ AS NO FALLBACK;``` |

#### MD5のインストール {#md5-installation}

Adobe Campaignインスタンスでmd5関数を使用する場合は、この [ページ](https://downloads.teradata.com/download/extensibility/md5-message-digest-udf) (md5_20080530.zip)のTeradataデータベースにuser mode関数をインストールする必要があります。

ダウンロードしたファイルのsha1は、次のとおりです。65cc0bb6935f72fcd84fef1ebcd64c00115dfd1e

md5をインストールするには：

1. md5_20080530.zipファイルを解凍します。

1. md5/srcディレクトリに移動します。

1. bteqを使用してTeradataデータベースに接続します。

1. 次のbteqコマンドを実行します。

   ```
   .run file = hash_md5.btq
   ```

#### SHA2のインストール {#sha2-installation}

Adobe Campaignインスタンスでsha2関数を使用する場合は、この [ページ](https://github.com/akuroda/teradata-udf-sha2/archive/v1.0.zip) (teradata-udf-sha2-1.0.zip)からTeradataデータベースにuser mode関数をインストールする必要があります。

ダウンロードしたファイルのsha1は、次のとおりです。e87438d37424836358bd3902cf1adeb629349780

sha2をインストールするには：

1. teradata-udf-sha2-1.0.zipファイルを解凍します。

1. teradata-udf-sha2-1.0/srcディレクトリに移動します。

1. bteqを使用してTeradataデータベースに接続します。

1. 次の2つのbteqコマンドを実行します。

   ```
   .run file = hash_sha256.sql
   .run file = hash_sha512.sql
   ```

#### UDF_UTF16TO8のインストール {#UDF-UTF16TO8-installation}

Adobe Campaignインスタンスでudf_utf16to8関数を使用する場合は、この **ページのTeradata unicodeツールキット** (utk_release1.7.0.0.zip)からTeradataデータベースにユーザーモード関数をインスト [](https://downloads.teradata.com/download/tools/unicode-tool-kit) ールする必要があります。

ダウンロードしたファイルのsha1は、次のとおりです。e58235f434f52c71316a577cb48e20b97d24f470

udf_utf16to8をインストールするには：

1. utk_release1.7.0.0.zipファイルを解凍します。

1. 抽出したファイル内でudf_utf16to8.oを探し、そのファイルが格納されているディレクトリに移動します。 この変数にはutk_release1.7.0.0/utk_release1.7.0.0/04 TranslationUDFs/01 Teradata UDFs/suselinux-x8664/udf_installation/という名前を付ける必要があります。

1. bteqを使用してTeradataデータベースに接続します。

1. 次のbteqコマンドを入力します。

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
   
### Linuxのキャンペーンサーバーの設定 {#campaign-server-linux}

ドライバのインストールには次が必要です。

* Teradata ODBC Driver(この [ページにあります)](https://downloads.teradata.com/download/connectivity/odbc-driver/linux)

* Teradata Tools and Utilities（一括読み込みに使用）。この [ページにあります。](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-linux-installation-package-0)

ファイル名とsha1:

* tdodbc1620__linux_indep.16.20.00.00-1.tar.gz 121fdd978b56fe1304fc5cb7819741b0847f44fd

* TeradataToolsAndUtilitiesBase__linux_indep.16.20.01.00.tar.gz b 29d0af5ffd8dcf68a9dbbaa6f8639387b19c563

お使いのLinuxディストリビューション用のパッケージがない場合は、CentOS 7 （例えばdockerを使う）での説明に従ってインストールし、Adobe Campaignサーバーに/opt/teradataの内容をコピーします。

#### ODBCドライバのインストール {#odbc-installation}

ODBCドライバをインストールするには：

1. tdodbc1620__linux_indep.16.20.00.00-1.tar.gzファイルを抽出します。

1. tdodbc1620ディレクトリに移動します。

1. セットアップスクリプトの修正が必要になる場合があります。

   ```
   "sed -i s/16.10/16.20/ setup_wrapper.sh".
   ```

1. setup_wrapper.shを実行します。

#### Teradataツールとユーティリティのインストール {#teradata-tools-installation}

ツールをインストールするには：

1. TeradataToolsAndUtilitiesBase__linux_indep.16.20.01.00.tar.gzファイルを展開します。

1. TeradataToolsAndUtilitiesBase/Linux/i386-x8664/tdicuディレクトリに移動します。

1. setup_wrapper.shを実行します。

1. TeradataToolsAndUtilitiesBase/Linux/i386-x8664/cliv2ディレクトリに移動します。

1. setup_wrapper.shを実行します。

1. TeradataToolsAndUtilitiesBase/Linux/i386-x8664/tptbaseディレクトリに移動します。

1. setup_wrapper.shを実行します。

1. libtelapi.soファイルは、/opt/teradata/client/16.20/lib64で入手できる必要があります。

#### ドライバの構成 {#driver-configuration}

ドライバ設定の詳細については、この [節を参照してください](../../platform/using/legacy-connectors.md#configure-access-to-teradata)。

#### 環境変数 {#environment-varaiables}

Adobe Campaignサーバの環境変数の詳細については、この [節を参照してください](../../platform/using/legacy-connectors.md#configure-access-to-teradata)。

### Windowsのキャンペーンサーバーの設定#キャンペーン — サーバー —windows}

最初に、Windows用のTeradataツールとユーティリティをダウンロードする必要があります。 この [ページからダウンロードできます](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package)

ODBCドライバとTeradata Parallel Transporter Baseを必ずインストールしてください。 Teradataデータベースに一括読み込みを行う際に使用するtelapi.dllをインストールします。

ドライバとユーティリティのパスが、実行中にnlserverが持つPATH変数に含まれていることを確認します。 デフォルトでは、パスはC:\Program Files (x86)\Teradata\Client\15.10\bin on Windows 32 bits or C:\プログラムFiles\Teradata\Client\15.10\bin on 64 bit)です。

### 外部アカウントのトラブルシューティング {#external-account-troubleshooting}

接続 **TIM-030008日付&#39;2&#39;のテスト中に次のエラーが表示される場合： 文字(iRc=-53)が見つからない場合は** 、ODBCドライバが正しくインストールされていること、およびLD_LIBRARY_PATH (Linux) / PATH (Windows)がキャンペーンサーバに設定されていることを確認してください。

エラー **ODB-240000 ODBCエラー：[Microsoft][ODBC Driver Manager]Data source名が見つからず、既定のドライバが指定されていません。** 16.Xドライバを使用する場合にWindowsで発生します。 Adobe Campaignでは、odbcinst.iniのメタデータ名が&#39;{teradata}&#39;である必要があります。
18.10Adobe Campaignサーバーのバージョンがある場合は、外部アカウントのオプションにODBCDriverName=&quot;Teradata Database ODBC Driver 16.10&quot;を追加できます。 バージョン番号が変わる場合があります。正確な名前は、 odbcad32.exeを実行し、[ドライバ]タブにアクセスすると見つかります。
バージョン18.10より前の場合は、ドライバのインストールで作成されたodbcinst.iniのTeradataセクションをTeradataという新しいセクションにコピーする必要があります。この場合は、regeditを使用できます。

ベースがlatin1の場合は、オプションにAPICharSize=1を追加する必要があります。

### タイムゾーン {#timezone}

Teradataは、標準ではないタイムゾーン名を使用しています。Teradataサイトでリストを見つけることが [できます](https://docs.teradata.com/reader/rgAb27O_xRmMVc_aQq2VGw/oGKvgl7gCeBMTGrp59BnwA)。 Adobe Campaignは、外部設定で指定されたタイムゾーンをTeradataが理解できるものに変換しようとします。 通信が見つからない場合は、クローゼットのGMT+X（またはGMT-X）タイムゾーンがセッションで見つかり、ログに警告が表示されます。

変換は、次のデータキットディレクトリにある必要があるteradata_timezones.txtというファイルを読み取って行われます。 linuxでは/usr/local/neolane/nl6/datakitが有効です。 このファイルを編集する場合は、Adobe Campaignチームに連絡してソースコードを変更してください。変更しないと、次回のキャンペーン更新時にこのファイルが上書きされます。

接続に使用されるタイムゾーンは、 nlserverを —verboseスイッチで実行するときに示されます。例：

```
15:04:04 >   ODB-240007 Teradata: will use 'Europe Central' as session time zone.
```

使用するタイムゾーンが正しくない場合は、「TimeZoneName」という名前の外部アカウントをオプションに追加できます。 この場合は、TimeZoneName=Europe CentralのようにTeradata値を使用します。

Teradataドキュメントで一括読み込みまたは「高速読み込み」を使用している場合、キャンペーンはタイムゾーンを示すことができません。 したがって、キャンペーンが接続に使用するユーザーのデフォルトのタイムゾーンを設定することをお勧めします。

```
MODIFY USER $login$ AS TIME ZONE = 'Europe Central';
```

## MySQL 5.7設定 {#mysql-57-configuration}

### サーバー設定 {#server-configuration-mysql}

サーバー設定には、特定のインストール手順は必要ありません。 Adobe Campaignは、latin1データベース、MySQLのデフォルト、またはunicodeデータベースで動作します。

### ドライバのインストール {#driver-installation-mysql}

#### Debian {#debian-mysql}

この [ページからmysql-apt-config.debをダウンロードします](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en)。

クライアントライブラリのインストール：

```
$ dpkg -i mysql-apt-config_*_all.deb # choose mysql-5.7 in the configuration menu
$ apt update
$ apt install libmysqlclient20
```

#### Windows [#windows-mysql}

この [ページからCコネクタをダウンロードします](https://dev.mysql.com/downloads/connector/c)。 バージョン5.7をダウンロードすることをお勧めします。

libmysqlclient.dllを含むディレクトリが、nlserverが使用するPATH環境変数に追加されていることを確認します。

#### CentOS {#centos-mysql}

この [ページからmysql57-community-release.noarch.rpmをダウンロードしてください](https://dev.mysql.com/downloads/repo/yum)。

クライアントライブラリのインストール：

$ yum install mysql57-community-release-el7-9.noarch.rpm$ yum install mysql-community-libs

### 外部アカウント設定 {#external-account-mysql}

外部アカウントの設定には、特別な手順は必要ありません。 タイムゾーンとUse unicodeデータがデータベースに従って設定されていることを確認します。
