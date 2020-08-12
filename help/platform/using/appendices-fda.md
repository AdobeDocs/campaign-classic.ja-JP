---
title: 付録
seo-title: FDA 付録
description: FDA 付録
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
translation-type: ht
source-git-commit: e7cf3b189f328cd1ea6ca8b67a3fc4c0c0bddd84
workflow-type: ht
source-wordcount: '1417'
ht-degree: 100%

---


# 付録 {#fda-appendices}

## Teradata 追加設定 {#teradata-configuration}

### 互換性 {#teradata-compatibility}

**Unicode ベース**

| データベースのバージョン | ドライバーのバージョン | 必要な Campaign 最小バージョン | 注意 |
|:-:|:-:|:-:|:-:|
| 15 | 15 | Campaign Classic 17.9 | Linux の場合：タイムスタンプのあるクエリは失敗する場合があります（18.4 の場合はビルド 8937、18.10 の場合はビルド 8977 で修正）。デバッグモードでは、ドライバーのメモリ使用量の不良に関する警告が発生する場合があります。 |
| 15 | 16 | Campaign Classic 17.9 | Linux での Teradata 15 データベースの推奨セットアップ。 |
| 16 | 16 | Campaign Classic 18.10 | サロゲートペアを持つ Unicode 文字は、完全には処理されません。データでのサロゲート文字の使用は有効です。クエリのフィルタリング条件でのサロゲートの使用は、この変更なしでは動作しません。 |
| 16 | 15 | サポートされていません |   |

**Latin1 ベース**

Adobe CampaignClassic 17.9 以前のバージョンでは、Teradata Latin-1 データベースのみがサポートされていました。

Adobe CampaignClassic 17.9 以降、デフォルトで Teradata Unicode データベースがサポートされるようになりました。

Latin-1 Teradata データベースを最新の Campaign Classic リリースに移行する場合は、外部アカウントのオプションにパラメーター「APICharSize=1」を追加する必要があります。

### データベース設定 {#database-configuration}

#### ユーザー設定 {#user-configuration}

カスタムプロシージャの作成／ドロップ／実行およびテーブルの作成／ドロップ／挿入／選択の権限が必要です。また、Adobe Campaign インスタンスで md5 および sha2 関数を使用する場合は、ユーザーモード関数を作成する必要が生じる場合もあります。

正しいタイムゾーンを設定してください。タイムゾーンは、Adobe Campaign インスタンスで作成される外部アカウントで設定される値と一致する必要があります。

Adobe Campaign は、データベース内で作成するオブジェクトに対して保護モード（フォールバック）を設定しません。次のクエリを使用して、Adobe Campaign が Teradata データベースへの接続に使用するデフォルトをユーザーに対して設定する必要がある場合があります。

| disable default fallback |
| :-: |
| ```MODIFY USER $login$ AS NO FALLBACK;``` |

#### MD5 のインストール {#md5-installation}

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

#### SHA2 のインストール {#sha2-installation}

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

#### UDF_UTF16TO8 のインストール {#UDF-UTF16TO8-installation}

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

### Linux の Campaign サーバー設定 {#campaign-server-linux}

ドライバーのインストールには次が必要です。

* Teradata ODBC ドライバー（この[ページ](https://downloads.teradata.com/download/connectivity/odbc-driver/linux)にあります）

* Teradata ツールおよびユーティリティ（一括読み込みに使用）（この[ページ](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-linux-installation-package-0)にあります）

ファイル名と sha1：

* tdodbc1620__linux_indep.16.20.00.00-1.tar.gz 121fdd978b56fe1304fc5cb7819741b0847f44fd

* TeradataToolsAndUtilitiesBase__linux_indep.16.20.01.00.tar.gz b 29d0af5ffd8dcf68a9dbbaa6f8639387b19c563

お使いの Linux ディストリビューション用のパッケージがない場合は、CentOS 7 での説明に従ってインストール（例えば docker を使用）し、Adobe Campaign サーバーの /opt/teradata の内容をコピーします。

#### ODBC ドライバーのインストール {#odbc-installation}

ODBC ドライバーをインストールするには、以下を実行します。

1. tdodbc1620__linux_indep.16.20.00.00-1.tar.gz ファイルを抽出します。

1. tdodbc1620 ディレクトリに移動します。

1. セットアップスクリプトの修正が必要になる場合があります。

   ```
   "sed -i s/16.10/16.20/ setup_wrapper.sh".
   ```

1. setup_wrapper.sh を実行します。

#### Teradata ツールとユーティリティのインストール {#teradata-tools-installation}

ツールをインストールするには、以下を実行します。

1. TeradataToolsAndUtilitiesBase__linux_indep.16.20.01.00.tar.gz ファイルを展開します。

1. TeradataToolsAndUtilitiesBase/Linux/i386-x8664/tdicu ディレクトリに移動します。

1. setup_wrapper.sh を実行します。

1. TeradataToolsAndUtilitiesBase/Linux/i386-x8664/cliv2 ディレクトリに移動します。

1. setup_wrapper.sh を実行します。

1. TeradataToolsAndUtilitiesBase/Linux/i386-x8664/tptbase ディレクトリに移動します。

1. setup_wrapper.sh を実行します。

1. Libtelapi.so ファイルは /opt/teradata/client/16.20/lib64 にあります。

#### ドライバーの構成 {#driver-configuration}

ドライバー設定の詳細については、この[節](../../platform/using/legacy-connectors.md#configure-access-to-teradata)を参照してください。

#### 環境変数 {#environment-varaiables}

Adobe Campaign サーバーの環境変数の詳細については、この[節](../../platform/using/legacy-connectors.md#configure-access-to-teradata)を参照してください。

### Windows の Campaign サーバーの設定 #campaign-server-windows}

最初に、Windows 用の Teradata ツールとユーティリティをダウンロードする必要があります。この[ページ](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package)からダウンロードできます。

ODBC ドライバーと Teradata Parallel Transporter Base を必ずインストールしてください。Teradata データベースに一括読み込みをおこなう際に使用する telapi.dll をインストールします。

ドライバーとユーティリティのパスが、実行中に nlserver が持つ PATH 変数に含まれていることを確認します。デフォルトパスは C:\Program Files (x86)\Teradata\Client\15.10\bin（Windows 32 ビット）または C:\Program Files\Teradata\Client\15.10\bin（64 ビット）です。

### 外部アカウントのトラブルシューティング {#external-account-troubleshooting}

接続のテスト中にエラー **TIM-030008 Date &#39;2&#39;: missing character(s) (iRc=-53)**、が表示される場合は、ODBC ドライバーが正しくインストールされていること、および Campaign サーバーに対して LD_LIBRARY_PATH（Linux）または PATH（Windows）が設定されていることを確認してください。

エラー **ODB-240000 ODBC error:[Microsoft][ODBC Driver Manager]Data source name not found and no default driver specified.** は、Windows で 16.X ドライバーを使用した場合に発生します。Adobe Campaign の odbcinst.ini では、Teradata のメタデータ名は「{teradata}」である必要があります。
Adobe Campaign サーバーのバージョンが 18.10 の場合、外部アカウントのオプションに「ODBCDriverName=&quot;Teradata Database ODBC Driver 16.10&quot;」を追加できます。バージョン番号は異なる場合があります。正確な番号は、odbcad32.exe を実行して「ドライバー」タブにアクセスすると見つかります。
バージョン 18.10 以前の場合は、ドライバーのインストールで作成された odbcinst.ini の Teradata セクションを Teradata という新しいセクションにコピーする必要があります。この場合は、regedit を使用できます。

ベースが latin1 の場合は、オプションに「APICharSize=1」を追加する必要があります。

### タイムゾーン {#timezone}

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

## MySQL 5.7 設定 {#mysql-57-configuration}

### サーバー設定 {#server-configuration-mysql}

サーバー設定には、特定のインストール手順は必要ありません。Adobe Campaign は、latin1 データベース、MySQL のデフォルト、または unicode データベースで動作します。

### ドライバーのインストール {#driver-installation-mysql}

#### Debian {#debian-mysql}

この[ページ](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en)から mysql-apt-config.deb をダウンロードします。

クライアントライブラリのインストール：

```
$ dpkg -i mysql-apt-config_*_all.deb # choose mysql-5.7 in the configuration menu
$ apt update
$ apt install libmysqlclient20
```

#### Windows {#windows-mysql}

この[ページ](https://dev.mysql.com/downloads/connector/c)から C コネクタをダウンロードします。バージョン 5.7 をダウンロードすることをお勧めします。

libmysqlclient.dll を含むディレクトリが、nlserver が使用する PATH 環境変数に追加されていることを確認します。

#### CentOS {#centos-mysql}

この[ページ](https://dev.mysql.com/downloads/repo/yum)から mysql57-community-release.noarch.rpm をダウンロードします。

クライアントライブラリのインストール：

$ yum install mysql57-community-release-el7-9.noarch.rpm
$ yum install mysql-community-libs

### 外部アカウントの設定 {#external-account-mysql}

外部アカウントの設定には、特別な手順は必要ありません。タイムゾーンと unicode 使用データがデータベースに従って設定されていることを確認します。
