---
product: campaign
title: サーバー設定ファイル
description: サーバー設定ファイル
audience: installation
content-type: reference
topic-tags: appendices
exl-id: 70cd6a4b-c839-4bd9-b9a7-5a12e59c0cbf
source-git-commit: e719c8c94f1c08c6601b3386ccd99d250c9e606b
workflow-type: tm+mt
source-wordcount: '7969'
ht-degree: 39%

---

# サーバー設定ファイル{#the-server-configuration-file}

![](../../assets/v7-only.svg)

Adobe Campaignの全体的な設定は、インストールディレクトリの **conf** ディレクトリにある **serverConf.xml** ファイルで定義されます。 この節では、**serverConf.xml** ファイルの様々なノードとパラメーターをすべて示します。

>[!NOTE]
>
>サーバー側の設定は、AdobeがホストするデプロイメントのAdobeでのみ実行できます。 様々なデプロイメントの詳細については、[ モデルのホスティング ](../../installation/using/hosting-models.md) の節または [ このページ ](../../installation/using/capability-matrix.md) を参照してください。 ホストモデルとハイブリッドモデルのインストールと設定の手順については、この [ 節 ](../../installation/using/hosting-models.md) を参照してください。

最初のパラメータは **共有** ノード内にあります。 これらはインスタンスに関連しています。 これらは、すべての nlserver コマンド（nlserver web、nlserver wfserver など）で使用される可能性があります。 その他のセクションは、特定の nlserver サブコマンドに関連しています。

**共有パラメーター**

* [認証](#authentication)
* [dataStore](#datastore)
* [dnsConfig](#dnsconfig)
* [exec](#exec)
* [htmlToPdf](#htmltopdf)
* [ims](#ims)
* [javaScript](#javascript)
* [mailExchanger](#mailexchanger)
* [モジュール](#module)
* [監視](#monitoring)
* [オーコン](#ooconv)
* [proxyConfig](#proxyconfig)
* [threadPool](#threadpool)
* [urlPermission](#urlpermission)
* [xtkJobs](#xtkjobs)

**その他のパラメーター**

* [アーカイブ](#archiving)
* [inMail](#inmail)
* [相互作用する](#interactiond)
* [MTA](#mta)
* [nmac](#nmac)
* [パイプライン](#pipelined)
* [修理](#repair)
* [securityZone](#securityzone)
* [SMS](#sms)
* [stat](#stat)
* [syslogd](#syslogd)
* [tracking](#tracking)
* [trackinglogd](#trackinglogd)
* [Web](#web)
* [wfserver](#wfserver)

## 認証 {#authentication}

**認証** ノードの異なるパラメータを次に示します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> checkIPConsistent<br /> </td> 
   <td> IP アドレス検査を有効にする.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> defaultMode<br /> </td> 
   <td> デフォルトの識別モード.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nl'<br /> </td> 
  </tr> 
  <tr> 
   <td> longSessionTimeOutSec<br /> </td> 
   <td> 長いセッションのタイムアウト（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1296000<br /> </td> 
  </tr> 
  <tr> 
   <td> securityTimeOutSec<br /> </td> 
   <td> セキュリティトークンのタイムアウト（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionCacheSec<br /> </td> 
   <td> キャッシュ時間：セッション情報のキャッシュ（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionTimeOutSec<br /> </td> 
   <td> セッションのタイムアウト（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
 </tbody> 
</table>

### XTK {#xtk}

**認証/XTK** ノードの異なるパラメーターを次に示します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> internalPassword<br /> </td> 
   <td> 内部アカウントのパスワード.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> internalSecurityZone<br /> </td> 
   <td> 内部アカウントのセキュリティゾーン：内部アカウントの許可されたゾーン。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'lan'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## dataStore {#datastore}

**dataStore** ノードの異なるパラメーターを次に示します。 サーバーのデータソースが定義される場所です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> exportDirectory<br /> </td> 
   <td> 書き出しディレクトリ：書き出されたデータの宛先ディレクトリのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/export/' <br /> </td> 
  </tr> 
  <tr> 
   <td> extraSandboxedDirectories<br /> </td> 
   <td> 追加のサンドボックス化ディレクトリ：サンドボックスに追加する他のパス（コンマ区切り）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/home/customers/,/sftp/' <br /> </td> 
  </tr> 
  <tr> 
   <td> formCacheTimeToLive<br /> </td> 
   <td> フォームキャッシュの有効期限の遅延：キャッシュエントリが無効化されるまでの時間（秒）。 キャッシュエントリは、パブリッシュ時にのみ更新されます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> hosts<br /> </td> 
   <td> DNS マスク：このインスタンスが提供する DNS マスクのリスト（コンマ区切り、*と？を使用可能） パターン )。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '*'<br /> </td> 
  </tr> 
  <tr> 
   <td> interactionCacheTimeToLive<br /> </td> 
   <td> インタラクション JSSP キャッシュの有効期限の遅延：キャッシュエントリが無効化されるまでの時間（秒）。 負の値の場合、キャッシュは常に無効化されます。 '0'、空または無効な値は 60 と見なされます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> lang<br /> </td> 
   <td> インスタンスの言語（列挙）。 有効な値は、「fr_FR」(Français)、「en_GB」( 英語 (UK))、「en_US」( 英語（米国）)、「de_DE」(Deutsch)、「ja_JP」（日本語）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'en_US'<br /> </td> 
  </tr> 
  <tr> 
   <td> uploadDirectory<br /> </td> 
   <td> アップロードフォルダー：アップロードされたデータの宛先ディレクトリのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/upload/' <br /> </td> 
  </tr> 
  <tr> 
   <td> uploadAllowlist<br /> </td> 
   <td> ダウンロードを許可されたファイル (「,」区切り)。この文字列は Java の有効な正規表現である必要があります。<a href="file-res-management.md" target="_blank"> アップロード可能ファイルの制限 </a>.<br /> を参照してください。 </td> 
   <td> 文字列<br /> </td> 
   <td> '.+' <br /> </td> 
  </tr> 
  <tr> 
   <td> useVault<br /> </td> 
   <td> Vault に秘密鍵を保存する：Hashicorp Vault を使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultSecretPath<br /> </td> 
   <td> Vault の秘密鍵のパス<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/v1/secret/campaign/'<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultTokenPath<br /> </td> 
   <td> Vault トークンを含むファイルのローカルパス. このパスでは$(HOME) を使用できます（他の env 変数は使用できません）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(HOME)/.vaulttoken'<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultUrl<br /> </td> 
   <td> Hashicorp Vault URL <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> viewCacheTimeToLive<br /> </td> 
   <td> ビューキャッシュの有効期間：キャッシュエントリが無効化されるまでの時間（秒）。 負の値の場合、キャッシュは常に無効化されます。 '0'、空または無効な値は 60 と見なされます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> workingDirectory<br /> </td> 
   <td> 作業ディレクトリの XPath。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> workingDirectory :作業ディレクトリの XPath。 デフォルト：'$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/workspace/'<br /> </td> 
  </tr> 
 </tbody> 
</table>

### proxyAdjust {#proxyadjust}

**dataStore > proxyAdjust** ノードの異なるパラメータを次に示します。 正規表現と一致する URL は、urlBase で定義された URL に基づいて再生成されます。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> urlBase<br /> </td> 
   <td> 外部 URL の生成時に使用するベース。例 : https://server.domain.com<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> urlRegEx<br /> </td> 
   <td> URL を照合する正規表現。例 : http://server\.lan\.net.*<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

### dataSource {#datasource}

**dataStore > dataSource** ノードの異なるパラメーターを次に示します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> name<br /> </td> 
   <td> データソース名 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> デフォルト<br /> </td> 
  </tr> 
 </tbody> 
</table>

**dataStore > dataSource > dbcnx** ノードで、接続設定を指定します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> NChar<br /> </td> 
   <td> Unicode ストレージ<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> dbSchema<br /> </td> 
   <td> ワークスペース<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 暗号化 <br /> </td> 
   <td> 暗号化されたパスワード<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> login<br /> </td> 
   <td> アカウント<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> password<br /> </td> 
   <td> パスワード<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> プロバイダー<br /> </td> 
   <td> タイプ（列挙）。 指定できる値は、「Oracle」、「MSSQL」(Microsoft SQL Server)、「PostgreSQL」(PostgreSQL)、「Teradata」、「DB2」、「MySQL」、「Netezza」、「AsterData」、「SAPHANA」(SAP HANA)、「RedShift」(AmazonRedshift)、ODBC`(ODBC(Sybase ASE、Sybase IQ)、`Relay`（リモートデータベースへの HTTP リレー）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'Oracle'<br /> </td> 
  </tr> 
  <tr> 
   <td> server<br /> </td> 
   <td> サーバー<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> timezone<br /> </td> 
   <td> タイムゾーン：<a href="../../installation/using/time-zone-management.md" target="_blank"> タイムゾーン管理 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> unicodeData<br /> </td> 
   <td> データベースの Unicode データ<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> useTimestampTZ<br /> </td> 
   <td> タイムゾーンを持つ日付フィールド：<a href="../../installation/using/time-zone-management.md" target="_blank"> タイムゾーン管理 </a> を参照してください。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**dataStore > dataSource > sqlParams** ノードで、SQL パラメーターを設定します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> funcPrefix<br /> </td> 
   <td> 関数のプレフィックス<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

**dataStore > dataSource > pool** ノードで、関連する接続プールのパラメーターを設定します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> aliveTestDelaySec<br /> </td> 
   <td> 接続の有効性チェック処理間の遅延。<br /> </td> 
   <td> ショート<br /> </td> 
  </tr> 
  <tr> 
   <td> freeCnx<br /> </td> 
   <td> プールに保存されている空き接続数.<br /> </td> 
   <td> ショート<br /> </td> 
  </tr> 
  <tr> 
   <td> maxCnx<br /> </td> 
   <td> 新しい接続を拒否する前に許可された接続の最大数。この <a href="https://helpx.adobe.com/campaign/kb/how-to-increase-the-maximum-number-of-database-connections-from-.html"> テクニカルノート </a>.<br /> を参照してください。 </td> 
   <td> ショート<br /> </td> 
  </tr> 
  <tr> 
   <td> maxIdleDelaySec<br /> </td> 
   <td> 接続の最大アイドル時間。0 はデフォルト値です.<br /> </td> 
   <td> ショート<br /> </td> 
  </tr> 
 </tbody> 
</table>

### virtualDir {#virtualdir}

**dataStore > virtualDir** ノードの異なるパラメータを次に示します。 これは、仮想ディレクトリと実ディレクトリのマッピングの設定です。

詳しくは、[ パブリックリソースの管理 ](file-res-management.md) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> name<br /> </td> 
   <td> 仮想ディレクトリの名前 <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> path<br /> </td> 
   <td> 実際のディレクトリのフルパス<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルトの設定を次に示します。

```
<virtualDir name="images" path="$(XTK_INSTALL_DIR)/var/res/img/"/>
<virtualDir name="formCache" path="$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/formCache/"/>
<virtualDir name="publicFileRes" path="$(XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)"/>
```

### preprocessCommand {#preprocesscommand}

**dataStore > preprocessCommand** ノードの異なるパラメーターを次に示します。 これらは、「ファイル読み込み」ワークフローアクティビティの前処理用に許可されたコマンドです。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> command<br /> </td> 
   <td> コマンドライン <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> label<br /> </td> 
   <td> コマンドラインラベル<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> name<br /> </td> 
   <td> コマンドライン名<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルトの設定を次に示します。

```
<preprocessCommand command="" label="None" name="none"/>
<preprocessCommand command="zcat &quot;$fileName&quot;" label="Decompression" name="zcat"/><preprocessCommand command="gpg --decrypt &quot;$fileName&quot;" label="Decrypt" name="gpg"/>
```

## dnsConfig {#dnsconfig}

**dnsConfig**（DNS 設定）ノードの異なるパラメータを次に示します。

詳しくは、この [ 節 ](../../installation/using/configuring-campaign-server.md) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> localDomain<br /> </td> 
   <td> ドメイン名：デフォルトのドメイン名。 SMTP HELO コマンドで使用されます。 デフォルトでは、は Windows で宣言された最初のネットワークインターフェイスのネットワークパラメータを使用します。または、Linux（ドメインまたは検索エントリ）でfile/etc/resolv.confを解析します。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> nameServers<br /> </td> 
   <td> DNS サーバー：ドメインネームサーバー (DNS) のコンマ区切りリスト。 以下の注意を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 再試行 <br /> </td> 
   <td> DNS クエリの再試行数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト<br /> </td> 
   <td> DNS クエリのタイムアウト（ミリ秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5000<br /> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>**nameSevers** に関する注意：デフォルトでは、はネットワークを使用します
>Windows で宣言された最初のネットワークインターフェイスのパラメータ
>UNIX では定義されていません。 ドメインネームサーバー (DNS) を定義します
>MTA が、
>ドメイン。
>
>この値を定義しない場合、MTA はホストネットワーク設定でこの情報をシークします。 複数の DNS が可能な場合は、異なる DNS アドレスをコンマで区切る必要があります ( 例：212.155.207.1,212.155.207.2)。 配信サーバーに複数のネットワークインターフェイスがある場合、MTA が使用する DNS リストが最初のものになります。 この場合、曖昧さを避けるために、**nameServer** パラメーターを指定することをお勧めします。

>[!CAUTION]
>
>ネットワークホストの設定で DHCP を使用している場合、MTA は DHCP から提供された DNS リストを見つけません。 この場合、Windows コントロールパネルのネットワークパラメーターで DNS リストを指定することをお勧めします。

## exec {#exec}

**exec**（コマンド実行）ノードの異なるパラメータを次に示します。

詳しくは、[ 許可された外部コマンドの制限 ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> blacklistFile<br /> </td> 
   <td> パスに追加するコマンドを含むファイルのパ許可リストス。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ユーザー<br /> </td> 
   <td> 別のユーザーとしてコマンドを実行.<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## htmlToPdf {#htmltopdf}

**htmlToPdf** ノードの異なるパラメータを次に示します。 Web ページを PDF ドキュメントに変換するサービスの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> command<br /> </td> 
   <td> 変換を実行するコマンドライン（'other'モード）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessCount<br /> </td> 
   <td> 最大1 台のマシンで一度に許可される変換プロセスの数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> mode<br /> </td> 
   <td> 変換に使用するツール。 次の値を指定できます。phantomjs, wkhtmltopdf，その他， disabled<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'phantomjs' <br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト<br /> </td> 
   <td> 変換のタイムアウト：最大変換時間（秒）。 このしきい値を超えると、変換処理が停止し、エラーが発生します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 120<br /> </td> 
  </tr> 
  <tr> 
   <td> verbose<br /> </td> 
   <td> 詳細モード：エラーの可能性を診断するために、詳細モードで起動します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> waitTime<br /> </td> 
   <td> プロセス待機時間の遅延：遅延時間（秒）。すべてのプロセスが同時に使用され、プロセスの解放を待機している場合。 この遅延を超えると、変換が停止し、エラーが発生します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
 </tbody> 
</table>

phantomjs の例：

```
phantomjs - -ignore-ssl-errors=true '$(XTK_INSTALL_DIR)/bin/htmlToPdf.js' '-out:{outPdf}' '-post:{postFile}' '-url:{originUrl}' -sessiontoken:{sessiontoken} -format:{format} -orientation:{orientation} -marginTop:{marginTop} -marginLeft:{marginLeft} -marginRight:{marginRight} -marginBottom:{marginBottom}
```

## ims {#ims}

**ims** ノードの異なるパラメーターを次に示します。 これは、[IMS](../../integrations/using/about-adobe-id.md) を使用して別のサービスに接続する Campaign の設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> authIMSClientId<br /> </td> 
   <td> クライアント ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSClientSecret<br /> </td> 
   <td> 秘密鍵 (AES で暗号化)<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSCode<br /> </td> 
   <td> 承認コード (AES で暗号化)<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSEndpoint<br /> </td> 
   <td> IMS サーバー URL<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://ims-na1.adobelogin.com'<br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSTAClientId<br /> </td> 
   <td> テクニカルアカウントクライアント ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSTAClientSecret<br /> </td> 
   <td> テクニカルアカウント秘密鍵 (AES で暗号化)<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSTAId<br /> </td> 
   <td> テクニカルアカウント ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSTAPrivateKey<br /> </td> 
   <td> テクニカルアカウント秘密鍵 (AES で暗号化)<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## JavaScript {#javascript}

**javaScript** ノードの異なるパラメーターを次に示します。 これは JavaScript インタープリタの設定です。

詳しくは、[ レポートのドキュメント ](../../reporting/using/actions-on-reports.md#memory-allocation) およびこの [ テクニカルノート ](https://helpx.adobe.com/campaign/kb/out-of-memory-error-in-js-code-activity-in-workflows.html) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> maxMB<br /> </td> 
   <td> ガベージコレクターを実行する前の最大サイズ（MB 単位）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 512 <br /> </td> 
  </tr> 
  <tr> 
   <td> stackSizeKB<br /> </td> 
   <td> 各スタックチャンクのサイズ（キロオクテット）。 これは、ほとんどのユーザーが調整すべきでないメモリ管理チューニングパラメータです。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
 </tbody> 
</table>

## mailExchanger {#mailexchanger}

**mailExchanger** ノードの異なるパラメータを次に示します。 SMTP サーバーの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> mxAddress<br /> </td> 
   <td> SMTP サーバー：電子メールの転送に使用する SMTP サーバーの IP アドレス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> mxPort<br /> </td> 
   <td> E メール転送に使用される SMTP サーバーの TCP ポート。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## モジュール {#module}

**module** ノードの異なるパラメータを次に示します。 これは、名前空間制限モジュール xtk の設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> defaultNameSpace<br /> </td> 
   <td> 新しいエンティティの作成時に使用されるデフォルトの名前空間.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'cus'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 監視 {#monitoring}

**監視** ノードの異なるパラメータを次に示します。 これは、監視サービスの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> maxPreparationJobsSec<br /> </td> 
   <td> 最大準備時間：配信アクションの準備が完了するまでの時間（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
  <tr> 
   <td> unixScript<br /> </td> 
   <td> 監視サービスにより実行される Unix スクリプト.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> winScript<br /> </td> 
   <td> 監視サービスにより実行される Windows スクリプト.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## オーコン {#ooconv}

**ooconv** ノードの異なるパラメータを次に示します。 これは、ドキュメント変換サーバーの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> maxConversions<br /> </td> 
   <td> OpenOffice サーバーでの実行が許可されたコンバージョンの最大数です。この数を超えると、サーバーは再起動されます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxServerIdleSec<br /> </td> 
   <td> OpenOffice サーバーが強制終了するまでの最大アイドル時間。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 7200<br /> </td> 
  </tr> 
  <tr> 
   <td> portRange<br /> </td> 
   <td> OpenOffice サーバーがリスニングしているポートの間隔.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 8101-8110<br /> </td> 
  </tr> 
  <tr> 
   <td> url<br /> </td> 
   <td> 文書変換サーバーの URL.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'http://localhost:8080/nl/jsp/ooconv.jsp'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## proxyConfig {#proxyconfig}

**proxyConfig** ノードの異なるパラメータを次に示します。 これは、プロキシパラメーターの設定です。

詳しくは、[ プロキシ接続の設定 ](file-res-management.md) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 有効<br /> </td> 
   <td> プロキシサーバーを使用.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> override<br /> </td> 
   <td> 例外：プロキシパラメータを無視するアドレスのリスト <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'localhost*' <br /> </td> 
  </tr> 
  <tr> 
   <td> useSingleProxy<br /> </td> 
   <td> 一意のプロキシサーバー：すべての種類のプロキシで同じ設定を使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
 </tbody> 
</table>

### HTTP プロキシ/セキュアプロキシ {#http-proxy---secure-proxy-}

**proxyConfig > HTTP プロキシ/セキュアプロキシ** ノードで、次のパラメーターを設定します。

詳しくは、[ プロキシ接続の設定 ](file-res-management.md) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> address<br /> </td> 
   <td> プロキシサーバーのアドレス<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> login<br /> </td> 
   <td> プロキシサーバーに接続するためのログイン<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> password<br /> </td> 
   <td> プロキシサーバーへの接続用パスワード<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> プロキシサーバーポート<br /> </td> 
   <td> ショート<br /> </td> 
  </tr> 
 </tbody> 
</table>

## threadPool {#threadpool}

**threadPool** ノードの異なるパラメータを次に示します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> maxThreadCount<br /> </td> 
   <td> プール内の最大スレッド数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## urlPermission {#urlpermission}

**urlPermission** ノードの様々なパラメーターを次に示します。 これは、JavaScript コードがアクセスできる URL のリストです。

JavaScript コードで検出された URL をAdobe Campaignサーバーで使用できるかどうかを指定するドメインと正規表現のリストです。

URL が見つからない場合は、指定したデフォルトのモードに従って、デフォルトのアクションが実行されます。

詳しくは、[ 発信接続の保護 ](../../installation/using/configuring-campaign-server.md#url-permissions) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> action<br /> </td> 
   <td> URL が許可リストにない場合のデフォルトのアクション（列挙）。 値は'ignore' （警告メッセージなしで承認する、保護を無効にする必要がある）、'warn' （許可して警告メッセージを発行）、'deny' （URL へのアクセスを禁止する）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> deny<br /> </td> 
  </tr> 
  <tr> 
   <td> debugTrace<br /> </td> 
   <td> URL 選択メカニズムのデバッグトレース：は、URL 検証プロセス中に追加のメッセージを発行します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
 </tbody> 
</table>

### url {#url}

各 URL に、次のパラメーターを持つ **url** ノードを追加します。

詳しくは、[ 発信接続の保護 ](../../installation/using/configuring-campaign-server.md#url-permissions) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> dnsSuffix<br /> </td> 
   <td> URL に関係するドメイン名またはドメインの親：検証を高速化するために、検証する URL のドメインのすべてまたは一部。 URL のドメインに dsnSuffix が含まれている場合にのみ、URL が正規表現に関して検証されます。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> urlRegEx<br /> </td> 
   <td> このドメインに属する URL の検証を絞り込むための正規表現：URL が dnsSuffix に対応している場合、URL が検証する必要がある正規表現。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

レコードが **dnsSuffix** を満たし、**urlRegEx** を満たさない場合、次のレコードが調べられます。

例えば、ドメイン business.com のすべての URL へのアクセスを承認するために、2 つのレコードを定義できます。

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;http://.*&quot;

および

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;https://.*&quot;

デフォルトの設定を次に示します。

```
<url dnsSuffix="api.omniture.com" urlRegEx="https://api.omniture.com/genesis/i/3.1.*"   />
<url dnsSuffix="omniture.com" urlRegEx="https://api[1-5].omniture.com/genesis/i/3.1.*"  />
<url dnsSuffix="marketing.adobe.com"                     urlRegEx="https://.*"                                    />
<url dnsSuffix="fcm.googleapis.com"                      urlRegEx="https://fcm.googleapis.com/fcm/send.*"       />
<url dnsSuffix="graph.facebook.com"                      urlRegEx="https://.*"                                    />
<url dnsSuffix="api.line.me"                             urlRegEx="https://api.line.me/.*"                      />
<url dnsSuffix="api.twitter.com"                         urlRegEx="https://api.twitter.com/1.1.*"              />
<url dnsSuffix="adobeid-na1.services.adobe.com"          urlRegEx="https://.*"                                    />
<url dnsSuffix="adobeid-na1-stg1.services.adobe.com"     urlRegEx="https://.*"                                    />
<url dnsSuffix="deliverability.neolane.net"              urlRegEx="https://deliverability.neolane.net/jssp/dm/renderingSeed.jssp" />
<url dnsSuffix="deliverability.neolane.net"              urlRegEx="https://deliverability.neolane.net/nl/jsp/soaprouter.jsp" />
<url dnsSuffix="localhost"                               urlRegEx="http://localhost:8080/nms/jsp/.*"              />
<url dnsSuffix="localhost"                               urlRegEx="http://localhost:8080/nl/jsp/.*"               />
<url dnsSuffix="localhost"                               urlRegEx="http://localhost:8080/xtk/jsp/.*"              />
```

## xtkJobs {#xtkjobs}

**xtkJobs** ノードの異なるパラメーターを次に示します。 これは、サーバージョブの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> purgeLogsPeriod<br /> </td> 
   <td> サーバー処理のメモリステータスの更新期間 (ms).<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## アーカイブ {#archiving}

**アーカイブ** ノードの異なるパラメータを次に示します。 これは、バックグラウンドで実行されたアーカイブ操作の設定です。

詳しくは、[ 電子メールアーカイブの有効化（オンプレミス）](../../installation/using/email-archiving.md#activating-email-archiving--on-premise-) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> acquireLimit<br /> </td> 
   <td> 同時に処理する EML の数<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> archivingType<br /> </td> 
   <td> 送信されたメッセージのアーカイブ戦略（列挙）。 指定できる値は'0' （アーカイブなし）と'1' （送信されたメッセージのアーカイブを SMTP サーバに転送）です。<br /> </td> 
   <td> バイト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> compressBatchSize<br /> </td> 
   <td> 圧縮アーカイブのサイズ：圧縮アーカイブの最大ファイル数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 10000<br /> </td> 
  </tr> 
  <tr> 
   <td> compressionFormat<br /> </td> 
   <td> アーカイブ中に使用される圧縮形式（列挙）。 指定できる値は'0' （圧縮なし）と'1' （zip 形式で送信したメッセージを圧縮）です。<br /> </td> 
   <td> バイト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> expirationDelay<br /> </td> 
   <td> 未処理の E メールを自動アーカイブする前の遅延：未処理の電子メールがアーカイブされるまでの日数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollDelay<br /> </td> 
   <td> 各更新イベント間の遅延（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeArchivesDelay<br /> </td> 
   <td> 未処理の E メールが削除されるまでの日数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 7<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpBccAddress<br /> </td> 
   <td> ターゲットの宛先のアーカイブ <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> smtpEnableTLS<br /> </td> 
   <td> SMTPS サポートのアクティブ化：リモートサーバーでサポートされている場合に、セーフモード (STARTTLS/SMTPS) での E メールの配信を有効化します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpNbConnection<br /> </td> 
   <td> アーカイブ SMTP サーバーへの接続数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpRelayAddress<br /> </td> 
   <td> 使用する SMTP リレーの DNS 名または IP アドレスのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> smtpRelayPort<br /> </td> 
   <td> SMTP サーバーの IP ポート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## inMail {#inmail}

**inMail** ノードの異なるパラメータを次に示します。 これは、インバウンド E メール管理モジュールの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> checkInstanceName<br /> </td> 
   <td> インスタンス名の確認：true の場合、Message-ID ヘッダーに含まれるAdobe Campaignインスタンスの名前は、現在のインスタンスと同じにする必要があります。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> defaultForwardAddress<br /> </td> 
   <td> 転送アドレス：デフォルトの電子メール転送アドレスがルールで処理されていません。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> errorForwardAddress<br /> </td> 
   <td> エラーのアドレス：無効な E メール（MIME エンコードが正しくない）の転送に使用されるデフォルトのアドレス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ignoreSize<br /> </td> 
   <td> メッセージのサイズを無視：は、POP3 サーバーから返されるメッセージのサイズを無視するために使用されます。 この場合、モジュールは「。」 を送信します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> inMailPeriodSec<br /> </td> 
   <td> メッセージ読み取り期間：メッセージキューのポーリング頻度。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxBroadLog<br /> </td> 
   <td> 更新するログの最大数：データベースを更新する前にメモリに保持するログメッセージの最大数を定義します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 20<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMsgPerSession<br /> </td> 
   <td> POP3 セッションで読み取るメッセージの最大数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 200<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSessionTTLSec<br /> </td> 
   <td> セッション時間：メッセージ処理セッションの最大時間。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> popMailPeriodSec<br /> </td> 
   <td> POP3 ポーリング期間 <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> popQueueSize<br /> </td> 
   <td> 読み取りメッセージのキューサイズ<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> popTimeoutSec<br /> </td> 
   <td> POP3 サーバーとの通信タイムアウト。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriodSec<br /> </td> 
   <td> ポーリングするアカウントのデータベース再読み込み頻度。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

### msgDump {#msgdump}

**inMail > msgDump** ノードで、次のパラメータを設定します。 これは、処理されたメッセージのダンプの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> dump<br /> </td> 
   <td> すべてのインバウンドメッセージをテキスト形式で保存します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> msgPath<br /> </td> 
   <td> メッセージダンプのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/tmp/inMail'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 相互作用する {#interactiond}

**interactiond** ノードの異なるパラメータを次に示します。 これは、受信インタラクションイベントの書き込みデーモンの設定です。

詳しくは、[ インタラクション — データバッファ ](../../installation/using/interaction---data-buffer.md) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> callDataSize<br /> </td> 
   <td> 最大呼び出しデータ用に共有メモリに格納されている文字の数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedEntries<br /> </td> 
   <td> 最大共有メモリに格納されたイベントの数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> nextOffersSize<br /> </td> 
   <td> 提案直後に並べ替えられ、統計用に保存される適格オファーの最大数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> statsPeriod<br /> </td> 
   <td> 応答時間統計の集計時間（秒）。 0 は、統計の保存が無効化されたことを意味します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> targetKeySize<br /> </td> 
   <td> 最大個人を識別するために共有メモリに格納される文字の数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 16<br /> </td> 
  </tr> 
 </tbody> 
</table>

## MTA {#mta}

**mta** ノードの異なるパラメータを次に示します。 これは、配信エージェントの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '-tracefilter:nlmta' <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> dataLogPath<br /> </td> 
   <td> 送信した電子メールのパスを保存：空でない場合は、送信した電子メールのすべてのソースファイルが保存されるパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> debugPath<br /> </td> 
   <td> ダンプディレクトリ：空でない場合は、このディレクトリに送信したメールメッセージの MIME エンベロープをコピーします。 トラブルシューティングに使用します。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> dnsRequestLogDelayMs<br /> </td> 
   <td> DNS クエリログの遅延：ログを表示する時間（ミリ秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> errorPeriodSec<br /> </td> 
   <td> エラー統計の頻度：統計の生成からデータベースへの格納までの時間。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> logEmailErrors<br /> </td> 
   <td> エラー統計を生成してデータベースに保存します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> logLevel<br /> </td> 
   <td> ログメッセージのレベルを表示します。データベースに書き込まれるログの重大度レベル。 MTA によって生成されるログメッセージは、必ずしもデータベースに書き込まれるわけではありません。 このパラメーターを使用して、メッセージをデータベースに書き込む必要があると考えるレベルを定義できます。 レベル 2 を定義すると、レベル 1 と 0 のメッセージも書き込まれ、レベル 1 を定義すると、レベル 1 と 0 のメッセージのみが書き込まれます。 次の値を指定できます。0（エラー）、1（警告）、2（情報）<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMemoryMb<br /> </td> 
   <td> MTA プロセスが使用できる最大メモリサイズ (MB)。この制限を超えると MTA プロセスが再起動され、使用しているメモリはシステムに解放されます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> minConnectionsToLog<br /> </td> 
   <td> 考慮する接続しきい値. errorPeriodSec で指定される期間の接続の合計数がしきい値よりも厳密に低い場合、エラー統計は指定のパスに対して生成されません。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> minErrorsToLog<br /> </td> 
   <td> 考慮するエラーしきい値：errorPeriodSec で指定された期間のエラーの総数がしきい値より厳密に少ない場合、指定されたパスに対してエラー統計は生成されません。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> minMessagesToLog<br /> </td> 
   <td> 考慮するメッセージしきい値. errorPeriodSec で指定する期間に送信されたメッセージの合計数が厳密にはしきい値を下回る場合、指定されたパスに対するエラー統計は生成されません。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：HostName：通知のリレーに使用するポート。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeDataLogDelay<br /> </td> 
   <td> アーカイブ済みの電子メールが削除されるまでの遅延：dataLogPath で指定したディレクトリ内のアーカイブ済み電子メールがパージされるまでの日数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
  <tr> 
   <td> retryLostMessages<br /> </td> 
   <td> 失われたメッセージの再試行：子プロセスが無効な場合、配信の一部が再試行されます。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> signEmailLinks<br /> </td> 
   <td> 署名メカニズムを有効にします。 これにより、E メール内のリンクの追跡に関するセキュリティが向上します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr>
  <tr> 
   <td> statServerAddress<br /> </td> 
   <td> 配信統計サーバーのアドレス ( 
    &lt;dns または ip&gt; 
      <code>[</code>: 
     &lt;port&gt; 
       <code>]</code>. 詳しくは、 
      <a href="../../installation/using/email-deliverability.md#coordinates-of-the-statistics-server" target="_blank"> 統計サーバの座標 </a>。 
      <br /> 
     </td> 
   <td> 文字列<br /> </td> 
   <td> 定義されていない場合、デフォルトのポートは 7777.<br /> です。 </td> 
  </tr> 
  <tr> 
   <td> statServerTLSSupport<br /> </td> 
   <td> ドメイン別の TLS を有効にする：MX で設定可能な TLS を有効にします（最新の統計サーバが必要です）。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true <br /> </td> 
  </tr> 
  <tr> 
   <td> statServerVersion<br /> </td> 
   <td> 使用するプロトコルのバージョン：通信プロトコルのバージョン（v5.11 および 6.0.2 サーバーの場合は 1、v6.1 サーバーの場合は 2）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 定義されていない場合は、最新バージョンが使用されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> useMomentum<br /> </td> 
   <td> "true"に設定した場合、インスタンスは <a href="../../delivery/using/sending-with-enhanced-mta.md" target="_blank">Enhanced MTA</a>.<br /> を使用しています </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td>b 
  </tr>
  <tr> 
   <td> verifyMode<br /> </td> 
   <td> 検証モード：検証モードを有効にします（メッセージの物理的な送信は行いません）。シミュレーションとテストに使用 )。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> workingPath<br /> </td> 
   <td> 作業ディレクトリ：MTA が子プロセスとの通信に使用する一時ファイルの場所。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/mta/' <br /> </td> 
  </tr> 
  <tr> 
   <td> xMailer<br /> </td> 
   <td> X-Mailer フィールド：SMTP メールヘッダーのフィールド'X-Mailer'の値。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nlserver, Build $(PRODUCT_VERSION)'<br /> </td> 
  </tr>  
 </tbody> 
</table>

### キャッシュ {#cache}

**cache** ノードで、次のパラメーターを設定します。 これは、ローカルファイルキャッシュの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> maxPeriodSec<br /> </td> 
   <td> リサイクル後：キャッシュからファイルを自動的に削除してストレージを再利用する期間（秒単位）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 244800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSizeOnDiskMb<br /> </td> 
   <td> 最大キャッシュサイズ (MB)。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> purgePeriodSec<br /> </td> 
   <td> パージ頻度：キャッシュパージメカニズムの実行間隔（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リレー {#relay}

**mta > relay** ノードで、次のパラメーターを設定します。 これは、メッセージ配信用のメールサーバーの設定です。

このリストは、MX DNS クエリが返す MX のリストと同じ方法で処理されます。通常、最初の MX は使用可能な場合に使用され、次の MX が使用される場合などに使用されます。

詳しくは、[SMTP リレー ](../../installation/using/configuring-campaign-server.md#smtp-relay) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> アドレス <br /> </td> 
   <td> 使用する SMTP リレーの DNS 名または IP アドレスのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> SMTP サーバーの IP ポート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

### プライマリ {#master}

**mta > master** ノードで、次のパラメーターを設定します。 これは、メインサーバーの設定です。

詳しくは、この [ 節 ](../../installation/using/configuring-campaign-server.md#mta-child-processes) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> dataBasePoolPeriodSec<br /> </td> 
   <td> 配信するジョブに対するデータベースポーリング頻度。この値はデータベースのポーリング頻度 (秒) を示します。配信待ちのジョブのリストを取得するために、MTA は定期的にデータベースをポーリングします。待機中のジョブがない場合、ポーリング期間はこの値によって定義されます。待機中のジョブがあり、ジョブが子サーバーに転送された場合は、できるだけ早く新しいジョブを再び処理できるようにするために (つまりできるだけ早く子サーバーが再び利用可能になるように)、このポーリング期間は自動的に 1 秒に短縮されます。これは、子サーバーが再び利用可能になるまでデータベースクエリが毎秒実行されるということを意味しません。実際は、少なくとも 1 つの子サーバーが利用可能になった場合にのみデータベースアクセスがおこなわれます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> dataBaseRetryDelaySec<br /> </td> 
   <td> データベースへの接続の失敗後に待機する期間。通常、データベース接続が失敗する原因は、データベースサーバー自体にあります。例えば、サーバーは、メンテナンスのために停止されることもあります。データベース接続が失敗した場合に接続を再試行するまでの時間は、DataBaseRetryDelay パラメーターで定義します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> domainKeysReloadPeriodSec<br /> </td> 
   <td> 秘密鍵のキャッシュの有効期間 (DomainKeys)。DomainKeys の推奨事項 (http://antispam.yahoo.com/domainkeys) に従った E メールへの署名に使用される秘密鍵は、データベース内にオプションとして保存されます。domainKeysReloadPeriodSec パラメーターに、MTA がこれらの鍵をキャッシュに保持できる秒数を定義します。この時間が過ぎた後は、すべての鍵をデータベースから再度読み込む必要があります。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSpareServers<br /> </td> 
   <td> 子サーバーの最大数。実行しているサービスの最大数を表します。サーバーメモリリソースと互換性がある最適値で制限することをお勧めします。これは、配信中にチェックできます。使用されるメモリは、利用可能な物理メモリの 3 分の 1 以下にする必要があります。それ以上になると、スワップが使用されます。<a href="../../installation/using/configuring-campaign-server.md#mta-child-processes" target="_blank">MTA 子プロセス </a>.<br /> を参照してください。 </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> minSpareServers<br /> </td> 
   <td> 子サーバーの最小数。MTA は少なくともこの数のサーバーが実行され続けるようにします。サーバーの数がこれよりも少ない場合は、この値に達するまで毎秒新しいサーバーを再起動します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> startSpareServers<br /> </td> 
   <td> 起動時の子サーバーの数。子サーバーの数が動的に監視されます。MTA の起動時に、この値で指定した最大数の子サーバーが作成されます。通常、子サーバーは、ホストリソースを保存するために、秒単位の 1 台のサーバーより速く開始することはできません。ただし、MTA を起動した場合、子サーバーができるだけ早く使用可能になるように、この制限は上書きされます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 子 {#child}

**mta > child** ノードで、次のパラメーターを設定します。 子サーバーの設定です。

詳しくは、[E メール送信の最適化 ](../../installation/using/email-deliverability.md#email-sending-optimization) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> extraArgs<br /> </td> 
   <td> オプションのコマンドライン引数 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> idleChildTimeoutSec<br /> </td> 
   <td> アイドル状態の子サーバーが停止するまで中断。子サーバーのアイドル時間がこのパラメーターより大きい場合、自分自身を自動的に kill してホストのリソースを解放します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> maxAgeSec<br /> </td> 
   <td> 最大メッセージ保持時間. 準備されたメッセージがスロットルによって送信されなかった場合やターゲット MTA に接続できなかった場合、メッセージは破棄され、次の再試行で処理されます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxGCMConnectPerChild<br /> </td> 
   <td> 各子サーバーによって開始された FCM に対する並列 HTTP リクエストの最大数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMsgPerChild<br /> </td> 
   <td> 子サーバーごとの最大メッセージ数。それぞれの MTA の子はこの数のメッセージを処理して終了します。MTA でのメモリまたはリソースリークが悪影響を及ぼさない程度の数を指定することが重要です (通常は数千)。MTA コード内に既知のメモリリークが存在していない場合でも、埋め込まれた JavaScript  および XSL エンジンは完全に信頼できるものではありません。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5000000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWaitingMessages<br /> </td> 
   <td> 保留中のメッセージ：メモリ内で配信を待機するメッセージの最大数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWorkingSetMb<br /> </td> 
   <td> 子プロセスが使用できる最大メモリサイズ（MB 単位）。この制限を超えると、プロセスが停止し、使用するメモリがシステムに解放されます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 128<br /> </td> 
  </tr> 
  <tr> 
   <td> soapConnectorTimeoutSec<br /> </td> 
   <td> 配信コネクタの SOAP 接続が破棄されるまでのタイムアウト (秒)。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> startWithFirstMX<br /> </td> 
   <td> 常に最優先 MX で開始.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> timeToLive<br /> </td> 
   <td> 再開時に連続して再試行する最大回数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 48<br /> </td> 
  </tr> 
 </tbody> 
</table>

**mta > child > smtp** ノードで、次のパラメーターを設定します。 これは、SMTP セッションの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> enableTLS<br /> </td> 
   <td> リモートサーバーでサポートされる場合、セーフモードで E メールの配信を有効化します (STARTTLS/SMTPS)。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> idleSessionTimeoutSec<br /> </td> 
   <td> アイドルセッションがタイムアウトになりました。このパラメーターは、あるドメインに対して複数のメッセージを転送するためにセッションが再利用される場合にのみ使用されます。MTA によってメッセージの転送が完了した場合、使用していた SMTP セッションはシステム的にはクローズされません。この同じドメインへのメッセージの送信準備が整えば、同じ SMTP セッションが再利用されます。このため、セッションは自動的にクローズされません。パラメーター IdleSessionTimeout では、別のメッセージを待機するために SMTP セッションがアクティブな状態を維持できる時間を定義します。その時間が経過した後、セッションは自動的にクローズされます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> initialDelaySec<br /> </td> 
   <td> 接続を再試行する前の初期遅延. この遅延は、接続が失敗するたびに 2 倍になります。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSessionsPerChild<br /> </td> 
   <td> 子サーバーによる SMTP セッションの最大数。メッセージを配信するために、この MTA は受信者 MTA との SMTP 接続を初期化します。1 台の子サーバーでのアクティブな同時 SMTP セッションの最大数はこの値によって制限されます。この値と maxSpareServers の値を乗算すると、1 台の子サーバーで同時に処理できるメッセージの最大数がわかります。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

**mta > child > smtp > IPAffinity** ノードで、次のパラメーターを設定します。 これは、最適化された送信 SMTP トラフィックの IP アドレスを使用したアフィニティの管理の設定です。

詳しくは、[ 使用する IP アドレスのリスト ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use) および [ アフィニティ ](../../installation/using/configuring-campaign-server.md#managing-outbound-smtp-traffic-with-affinities) を使用した送信 SMTP トラフィックの管理を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> localDomain<br /> </td> 
   <td> ドメイン名：IP アドレスにリンクされたローカルドメイン名。 SMTP HELO コマンドを発行する際に使用します。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> name<br /> </td> 
   <td> 論理名：ユーザーによってアフィニティにリンクされた名前。 名前はセミコロンで区切られます。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

**mta > child > smtp > IP** ノードで、次のパラメーターを設定します。

詳しくは、[ 使用する IP アドレスのリスト ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> アドレス <br /> </td> 
   <td> 関連する物理アドレス。例：'192.168.0.1'<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> publicId<br /> </td> 
   <td> 関連付けられたパブリックアドレス ID です。統計サーバーのキーとして使用されます。数値で指定する必要があります。<a href="../../installation/using/email-deliverability.md#managing-ip-addresses">こちら</a>を参照してください。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
  </tr> 
  <tr> 
   <td> 重み付け<br /> </td> 
   <td> この IP の使用頻度を他の IP に相対的に指定します (重みを大きくすると頻度が高くなります)。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
  </tr> 
  <tr> 
   <td> includeDomains<br /> </td> 
   <td> 含めるドメインマスクのコンマ区切りリスト.<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> excludeDomains<br /> </td> 
   <td> 除外するドメインマスクのコンマ区切りのリスト.<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> heloHost<br /> </td> 
   <td> IP アドレスにリンクされたコンピューター名です。SMTP HELO コマンドの発行時に使用します。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## nmac {#nmac}

**nmac** ノードの異なるパラメータを次に示します。 これは、プッシュ通知配信のの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> useHTTPProxy<br /> </td> 
   <td> 共有 / プロキシ HTTP で定義された HTTP プロキシを使用. <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リレー {#relay-1}

**nmac > relay** ノードの異なるパラメータを次に示します。 これにより、メッセージ配信（ios http2 コネクタ）にリレーを使用するように設定します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> アドレス <br /> </td> 
   <td> 使用するリレーの DNS アドレスまたは名前。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> リレーポート<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 443<br /> </td> 
  </tr> 
  <tr> 
   <td> trustedCertsChain<br /> </td> 
   <td> 証明書チェーン (PEM ファイル)。モックサーバー使用時に役立ちます.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## パイプライン {#pipelined}

**pipelined** ノードの異なるパラメータを次に示します。 これは、パイプラインサービスのイベント処理モジュールの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> appName<br /> </td> 
   <td> 公開鍵の保存時に Developer Connection で生成されたアプリケーションの名前。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authGatewayEndpoint<br /> </td> 
   <td> ゲートウェイトークンを取得する URL.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://api.omniture.com' <br /> </td> 
  </tr> 
  <tr> 
   <td> authPrivateKey<br /> </td> 
   <td> トークンを取得するための秘密鍵 (AES で XtkKey オプションを指定して暗号化).<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始 <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> disableAuth<br /> </td> 
   <td> 認証の無効化：認証なしでパイプラインサービスに接続します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> discoverPipelineEndpoint<br /> </td> 
   <td> パイプラインサービス URL を検出するための URL.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://producer-pipeline-pnw.adobe.net'<br /> </td> 
  </tr> 
  <tr> 
   <td> dumpStatePeriodSec<br /> </td> 
   <td> ステータス保存期間：プロセスの内部情報がファイルに保存される頻度。 0 の場合は非アクティブです。 <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> forcedPipelineEndpoint<br /> </td> 
   <td> リスニング URL:パイプラインサービスのリスニング URL を強制的に設定します。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> monitorServerPort<br /> </td> 
   <td> ステータスサーバーポート：プロセスのステータスを問い合わせる HTTP サーバーポート。 0.<br /> の場合は非アクティブ </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 7781<br /> </td> 
  </tr> 
  <tr> 
   <td> pointerFlushMessageCount<br /> </td> 
   <td> この数のメッセージが処理されるたびにポインターがデータベースに格納されます。<br /> </td> 
   <td> <br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> pointerFlushPeriodSec<br /> </td> 
   <td> ポインタが保存されるまでの遅延：この期間中に少なくとも 1 回はデータベースにポインタが格納されます（アクティビティが低い場合に便利です）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> processingJSThreads<br /> </td> 
   <td> パーソナライズされた JavaScript コネクタによるイベント処理のスレッド数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> processingThreads<br /> </td> 
   <td> イベント処理用のスレッド数<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> retryPeriodSec<br /> </td> 
   <td> 失敗があった場合の処理間の遅延.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> retryValiditySec<br /> </td> 
   <td> この期間を過ぎると破棄：この期間が過ぎても処理が失敗し続ける場合は、イベントを破棄します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 修理 {#repair}

**repair** ノードの異なるパラメータを次に示します。 これは、データベース修復モジュールの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> repairActionDelayMin<br /> </td> 
   <td> 配信アクションの修復モジュール：修復モジュールで配信アクションを処理できるまでの遅延（分）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
 </tbody> 
</table>

## securityZone {#securityzone}

**securityZone** ノードの異なるパラメータを次に示します。

詳しくは、[ セキュリティゾーンの定義 ](../../installation/using/security-zones.md) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> allowDebug<br /> </td> 
   <td> Web アプリケーションのデバッグモードを許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> allowEmptyPassword<br /> </td> 
   <td> パスワードなしでアプリケーションを使用することをユーザーに許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> allowHTTP<br /> </td> 
   <td> オペレーターのログオンに HTTP の使用を許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> allowSQLInjection<br /> </td> 
   <td> 式で SQLDATA の使用を承認.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> allowUserPassword<br /> </td> 
   <td> ユーザー / パスワードセッショントークンを許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> label<br /> </td> 
   <td> ラベル<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewLabel()<br /> </td> 
  </tr> 
  <tr> 
   <td> name<br /> </td> 
   <td> 内部名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewName() <br /> </td> 
  </tr> 
  <tr> 
   <td> sessionTokenOnly<br /> </td> 
   <td> セキュリティトークンを使用しない.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> showErrors<br /> </td> 
   <td> エラーの詳細を表示<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルトの設定を次に示します。

```
<securityZone allowDebug="false" allowHTTP="false" allowSQLInjection="false" label="Public Network" name="public">
  <subNetwork name="all" label="All addresses" mask="*" proxy="127.0.0.1, ::1"/>

  <securityZone allowDebug="true" allowHTTP="false" allowSQLInjection="false" label="Private Network (VPN)"
                name="vpn" showErrors="true">

    <securityZone allowDebug="true" allowEmptyPassword="false" allowHTTP="true" allowUserPassword="false"
                  allowSQLInjection="false" label="Private Network (LAN)" name="lan" sessionTokenOnly="true"
                  showErrors="true">
      <subNetwork name="lan1" label="Lan 1" mask="192.168.0.0/16" proxy="127.0.0.1, ::1"/>
      <subNetwork name="lan2" label="Lan 2" mask="172.16.0.0/12" proxy="127.0.0.1, ::1"/>
      <subNetwork name="lan3" label="Lan 3" mask="10.0.0.0/8" proxy="127.0.0.1, ::1"/>
      <subNetwork name="localhost" label="Localhost" mask="127.0.0.0/8" proxy="127.0.0.1, ::1"/>
      <subNetwork name="lan6"  label="Lan (IPv6)" mask="fc00::/7" proxy="127.0.0.1, ::1"/>
      <subNetwork name="lan6b" label="Lan (IPv6)" mask="fe80::/10" proxy="127.0.0.1, ::1"/>
      <subNetwork name="localhost6" label="Localhost (IPv6)" mask="::1/128" proxy="127.0.0.1, ::1"/>
    </securityZone>

  </securityZone>
</securityZone>
```

### subNetwork {#subnetwork}

**securityZone > subNetwork** ノードの異なるパラメーターを次に示します。

詳しくは、[ セキュリティゾーンの定義 ](../../installation/using/security-zones.md) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> label<br /> </td> 
   <td> ラベル<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewLabel()<br /> </td> 
  </tr> 
  <tr> 
   <td> mask<br /> </td> 
   <td> マスクまたはアドレス<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> name<br /> </td> 
   <td> 内部名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewName() <br /> </td> 
  </tr> 
  <tr> 
   <td> プロキシ <br /> </td> 
   <td> このサブネットワークでインスタンスにアクセスするために使用されている (リバース) プロキシのマスクまたはアドレス。この場合、「X-Forwarded-For」ヘッダーがこのプロキシの代わりにテストされます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 127.0.0.1 <br /> </td> 
  </tr> 
 </tbody> 
</table>

## SMS {#sms}

**sms** ノードの異なるパラメーターを次に示します。 これは、インバウンド SMS 管理モジュールの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> dataRetentionDays<br /> </td> 
   <td> SMPP コネクタで保持される作業ファイルの最大数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> dataSizeMo<br /> </td> 
   <td> SMPP 作業ファイルの最大サイズ (MB)。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 512<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> keepAlivePeriod<br /> </td> 
   <td> セッション継続フレームの繰り返し：最大 受信セッションがまだ有効であることを通知する 2 つのフレーム間の時間（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollPeriod<br /> </td> 
   <td> 検索頻度：SMS アカウントのポーリング期間 <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriod<br /> </td> 
   <td> アカウントの再読み込み頻度：データベースの再読み込み頻度を調整します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> srReadDelay<br /> </td> 
   <td> SR 処理の遅延秒数：現在の時刻から srReadDelay に指定した時間（秒）を引いた値より前の回復日を持つ SR のみ。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト<br /> </td> 
   <td> SMS ゲートウェイでの通信タイムアウト。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
 </tbody> 
</table>

### netsize {#netsize}

**sms > netsize** ノードの異なるパラメータを次に示します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> netsizeConnectionTimeout<br /> </td> 
   <td> Netsize との接続を確立する際のタイムアウト（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
 </tbody> 
</table>

## stat {#stat}

**stat** ノードの異なるパラメータを次に示します。 これは、MTA 統計モジュールの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> サーバーリスニングポート. <a href="../../installation/using/email-deliverability.md#definition-of-the-server-port">こちら</a>を参照してください。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## syslogd {#syslogd}

**syslogd** ノードの異なるパラメータを次に示します。 これは、ログ管理モジュールの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxFileSizeMb<br /> </td> 
   <td> ログファイルの最大サイズ（MB 単位）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> maxNumberOfLoginsFiles<br /> </td> 
   <td> 保持する logins.log ファイルの最大数. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 365<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## tracking {#tracking}

**tracking** ノードの異なるパラメータを次に示します。 これは、トラッキングサーバーの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> blockRedirectForUnsignedTrackingLink<br /> </td> 
   <td> 以前のビルドで生成された、形式が正しくない URL を無効にします。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> consolidationPeriodSec<br /> </td> 
   <td> 統合期間<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> dedupOpenPeriodMin<br /> </td> 
   <td> 開口部の重複排除：重複するオープントラッキングログを削除して、Outlook などのメールリーダーでのメールプレビューの効果を制限します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePercent<br /> </td> 
   <td> 最大 X%のエラーを無視：まだ考慮されていない仕訳の比率がこの値に達していない限り、追跡指標を更新しないでください。<br /> </td> 
   <td> バイト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePeriod<br /> </td> 
   <td> エラーインジケーターの更新：エラー指標が再計算されるまでの最大時間 <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> indicatorsDuration<br /> </td> 
   <td> 次の期間に指標を計算：統合指標が計算されなくなった、配信の有効日以降の期間。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2592000<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> logCountPerRequest<br /> </td> 
   <td> リモートトラッキングサーバーに対する呼び出しによってリクエストされたログの数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> phishbowlServiceAPIKey<br /> </td> 
   <td> Phishbowl サービスエンドポイント統合の API キー。 これにより、古いビルドで生成された、形式が正しくない URL のリダイレクトを保護します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> phishbowlServiceEndpoint<br /> </td> 
   <td> Phishbowl サービスエンドポイント統合のエンドポイント。 これにより、古いビルドから生成された不正な URL のリダイレクトを保護します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePercent<br /> </td> 
   <td> 最大 X%の追跡を無視：まだ考慮されていない仕訳の比率がこの値に達していない限り、追跡指標を更新しないでください。<br /> </td> 
   <td> バイト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePeriod<br /> </td> 
   <td> トラッキング指標の更新：追跡指標が再計算されるまでの最大時間 <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> userAgentCacheSize<br /> </td> 
   <td> ブラウザー識別子のキャッシュのサイズ<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## trackinglogd {#trackinglogd}

**trackinglogd** ノードの異なるパラメータを次に示します。 これは、トラッキングログ書き込みデーモンの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxCreateFileRetry<br /> </td> 
   <td> 最大書き込み再試行回数：ログファイルへの書き込みに失敗した場合に作成できるファイルの最大数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> maxLogsSizeOnDiskMb<br /> </td> 
   <td> 最大ログサイズ：ディスク上のログに使用される最大容量（MB 単位）。 100 MB 以上にする必要があります。 <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedLogs<br /> </td> 
   <td> 最大ログ数：共有メモリに格納されるログの最大数。 10000より小さい値は指定できません。 <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeLogsPeriod<br /> </td> 
   <td> パージ前のログ数：ログファイルのパージを開始する前に挿入されたログの数。 50000.<br /> より小さくはなりません。 </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 50000<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> webTrackingParamSize<br /> </td> 
   <td> 追加の Web トラッキングパラメーターの共有メモリに保存される最大文字数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 64<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Web {#web}

**web** ノードの異なるパラメータを次に示します。 Web モジュールの設定です。

詳しくは、この [ 節 ](configuring-campaign-server.md#default-port-for-tomcat) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> JVMOptions<br /> </td> 
   <td> 文字列として渡される JVM オプション。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> MaxThreads<br /> </td> 
   <td> スレッドの最大数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 75<br /> </td> 
  </tr> 
  <tr> 
   <td> MinSpareThreads<br /> </td> 
   <td> スレッドの最小数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> controlPort<br /> </td> 
   <td> Tomcat リスニング制御ポート：<a href="configure-tomcat.md" target="_blank">Tomcat の設定 </a> を参照してください。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 8005<br /> </td> 
  </tr> 
  <tr> 
   <td> httpPort<br /> </td> 
   <td> Tomcat HTTP リスニングポート：<a href="configure-tomcat.md" target="_blank">Tomcat の設定 </a> を参照してください。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 8080<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxDeliveryQueueSize<br /> </td> 
   <td> SubmitDelivery 呼び出しのキューのサイズ：キューに格納できる SubmitDelivery SOAP 呼び出しの最大数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 50<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告 <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：HostName:Port 通知のリレーを有効にしています。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> startSoapRouterInModule<br /> </td> 
   <td> モジュールモードで SOAP ルーターを起動します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
 </tbody> 
</table>

### jsp {#jsp}

**web > jsp** ノードの異なるパラメータを次に示します。 これは、JSP で使用されるパラメータの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> debug<br /> </td> 
   <td> デバッグモードで JSP を実行するかどうか.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> downloadPath<br /> </td> 
   <td> ダウンロードフォルダ：クライアントコンソールのインストールプログラムのダウンロードパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(XTK_INSTALL_DIR)/datakit/nl/eng/jsp'<br /> </td> 
  </tr> 
  <tr> 
   <td> foFileName<br /> </td> 
   <td> .fo ファイルのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> soapRouter<br /> </td> 
   <td> SOAP ルーターの URL (http://myserver/xxx, http://jni or mailto:xxx).<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'http://jni'<br /> </td> 
  </tr> 
 </tbody> 
</table>

**web > jsp > classpath** ノードには、JVM の起動時に使用するすべてのクラスパスのリストが含まれます。 デフォルトの設定を次に示します。

```
'$(XTK_INSTALL_DIR)/tomcat-8/bin/bootstrap.jar
          $(XTK_INSTALL_DIR)/tomcat-8/bin/tomcat-juli.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/tomcat-coyote.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/tomcat-util.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/tomcat-api.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/servlet-api.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/jsp-api.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/el-api.jar
          $(XTK_INSTALL_DIR)/java/lib/log4j-1.2.11.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/annotations-api.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/catalina.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/websocket-api.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/tomcat7-websocket.jar
          $(XTK_INSTALL_DIR)/java/lib/pdfbox-2.0.4.jar
          $(XTK_INSTALL_DIR)/java/lib/FontBox-0.1.0.jar
          $(XTK_INSTALL_DIR)/java/lib/AGJavaEndpoint.22.jar
          $(XTK_INSTALL_DIR)/java/lib/NSGConstants.jar
          $(XTK_INSTALL_DIR)/java/lib/smpp.jar
          $(XTK_INSTALL_DIR)/java/lib/nlweb.jar
          $(XTK_INSTALL_DIR)/java/lib/jcaptcha-all.jar
          $(XTK_INSTALL_DIR)/java/lib/apns-1.0.0.Beta6-jar-with-dependencies.jar
          $(XTK_INSTALL_DIR)/java/lib/commons-collections-3.2.2.jar
          $(XTK_INSTALL_DIR)/java/lib/jcommon-1.0.16.jar
          $(XTK_INSTALL_DIR)/java/lib/jfreechart-1.0.13.jar
          $(XTK_INSTALL_DIR)/java/lib/barcode4j-light.jar
          $(XTK_INSTALL_DIR)/java/lib/zxing.jar
          $(XTK_INSTALL_DIR)/java/lib/raztec.jar
          $(XTK_INSTALL_DIR)/java/lib/gson-2.7.jar
          $(XTK_INSTALL_DIR)/java/lib/alpn-api-1.1.3.v20160715.jar
          $(XTK_INSTALL_DIR)/java/lib/netty-all-4.1.6.Final.jar
          $(XTK_INSTALL_DIR)/java/lib/netty-tcnative-boringssl-static-1.1.33.Fork22.jar
          $(XTK_INSTALL_DIR)/java/lib/pushy-0.8.1.jar
          $(XTK_INSTALL_DIR)/java/lib/slf4j-api-1.7.21.jar
          $(XTK_INSTALL_DIR)/java/lib/slf4j-simple-1.7.21.jar'
```

### jssp {#jssp}

**web > jssp** ノードの異なるパラメーターを次に示します。 これは、JSSP で使用されるパラメーターの設定です。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> collectsGarbageAfterRequest<br /> </td> 
   <td> 各クエリの後で JavaScript コンテキストのガベージコレクターを有効にします。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> timeToLive<br /> </td> 
   <td> JavaScript コンテキストで提供される最大ページ数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

**web > jsp > classpath** ノードには、JVM の起動時に使用するすべてのクラスパスのリストが含まれます。

### リレー {#relay-2}

**web > relay** ノードの異なるパラメータを次に示します。 これは、2 つのゾーン間の HTTP 要求のリレーの設定です。

詳しくは、この [ 節 ](../../installation/using/deploying-an-instance.md#synchronizing-public-resources) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> debugRelay<br /> </td> 
   <td> Web サーバー内の HTTP リレーモジュールをデバッグモードで起動します.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInAuthority<br /> </td> 
   <td> 禁止文字（ドメイン）:URI の「権限」セクションの禁止文字のリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.?#@/:' <br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInPath<br /> </td> 
   <td> 禁止文字（パス）:URI の「パス」セクションにある禁止文字のリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '?#/'<br /> </td> 
  </tr> 
  <tr> 
   <td> modDir<br /> </td> 
   <td> 'mod_dir'モジュールオプションの値：フォルダーに対するクエリ中に使用するファイルのリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'index.md' <br /> </td> 
  </tr> 
  <tr> 
   <td> startRelay<br /> </td> 
   <td> HTTP リレーモジュールを開始.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> startRelayInModule<br /> </td> 
   <td> Web サーバー内で HTTP リレーモジュールを起動します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト<br /> </td> 
   <td> 禁止された URL を削除するまでの待機時間です.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '60'<br /> </td> 
  </tr> 
 </tbody> 
</table>

**Web > リレー > url** ノードを、次のパラメーターでリレーする URL ごとに追加します（優先順位を挿入）。

詳しくは、[ 動的ページのセキュリティとリレー ](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays) および [ の節 ](../../installation/using/deploying-an-instance.md#synchronizing-public-resources) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> IPMask<br /> </td> 
   <td> 承認済み IP:このマスクのリレーを使用できる送信元 IP アドレスのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> deny<br /> </td> 
   <td> これらの URL へのアクセスを拒否します (HTTP 403 エラーを返します)<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> hostMask<br /> </td> 
   <td> リレーする DNS エイリアス：中継する DNS エイリアスマスクのコンマ区切りリスト ( 例：'*.adobe.com').<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> httpAllowed<br /> </td> 
   <td> HTTP アクセスは、セキュリティゾーン（webApps など）に関係なく許可されます。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayHost<br /> </td> 
   <td> 元のホストを追加：中継時に元のリクエストの HTTP 'Host'ヘッダーを使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayPath<br /> </td> 
   <td> 初期 URL パスを追加：リレーする URL の完全パスをターゲットページの URL に追加します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> status<br /> </td> 
   <td> パブリックリソースの同期ステータス（列挙）。 指定できる値は、「通常」（通常の実行）、「ブラックリスト」（エラー 404 の場合はに追加される URL）、「スペア」（既存の場合はスペアサーバにファイルをアップロードする）でブロックリストす。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> normal<br /> </td> 
  </tr> 
  <tr> 
   <td> targetUrl<br /> </td> 
   <td> ターゲットページの URL:<a href="configure-tomcat.md" target="_blank">Tomcat の設定 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト<br /> </td> 
   <td> 中継される要求の最大実行時間（秒）。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> urlPath<br /> </td> 
   <td> 中継する URL のマスク (例 : 「/nl*」、「*.jsp」)。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルトの設定を次に示します。

```
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true"
     status="normal" targetUrl="http://localhost:7781" timeout="" urlPath="/pipelined/*"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="false" urlPath="/view/*"/>
<url IPMask="" deny="true" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="false" urlPath="*ooconv.jsp*"/>
<url IPMask="" deny="true" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="false" urlPath="/res/*.jsp*"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="*/sc.jssp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="*/interactionProposal.jssp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="*/zoneJson.jssp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="/nms/jsp/barcode.jsp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="/nms/jsp/captcha.jsp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="/nms/jsp/webForm.jsp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="/xtk/jsp/zoneinfo.jsp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="*/facebookCallback.jssp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="/nl/jsp/m.jsp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="/nl/jsp/s.jsp"/>

<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="blacklist" httpAllowed="false" urlPath="/nms/jsp/*.jsp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="blacklist" httpAllowed="false" urlPath="/xtk/jsp/*.jsp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="blacklist" httpAllowed="false" urlPath="/nl/jsp/*.jsp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="blacklist" httpAllowed="false" urlPath="*.jssp"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="blacklist" httpAllowed="true" urlPath="/webApp/*"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="blacklist" httpAllowed="false" urlPath="/report/*"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="blacklist" httpAllowed="false" urlPath="/jssp/*"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="false" urlPath="/strings/*"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="/interaction/*"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="/barcode/*"/>
<url IPMask="" deny="" hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080"
     timeout="" status="normal" httpAllowed="true" urlPath="/lineImage/*"/>

<url IPMask="" deny="" hostMask="" relayHost="false" relayPath="false" targetUrl=""
     timeout="" status="spare" httpAllowed="true" urlPath="/favicon.*"/>
<url IPMask="" deny="" hostMask="" relayHost="false" relayPath="false" targetUrl=""
     timeout="" status="spare" httpAllowed="true" urlPath="/*.md"/>
<url IPMask="" deny="" hostMask="" relayHost="false" relayPath="false" targetUrl=""
     timeout="" status="spare" httpAllowed="true" urlPath="/*.png"/>
<url IPMask="" deny="" hostMask="" relayHost="false" relayPath="false" targetUrl=""
     timeout="" status="spare" httpAllowed="true" urlPath="/*.jpg"/>
```

リレーに転送された応答に追加する HTTP ヘッダーごとに、**Web > リレー > responseHeader** ノードを追加します。

詳しくは、[HTTP ヘッダーの管理 ](../../installation/using/configuring-campaign-server.md#managing-http-headers) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> name<br /> </td> 
   <td> ヘッダー名<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> value<br /> </td> 
   <td> ヘッダーの値 <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルトの設定を次に示します。

```
<responseHeader name="X-XSS-Protection" value="1; mode=block"/>
```

### リダイレクト {#redirection}

**web > redirection** ノードの異なるパラメータを次に示します。 これは、リダイレクトモジュールの設定です。

詳しくは、この [ 節 ](../../installation/using/deploying-an-instance.md#synchronizing-public-resources) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> IMSOrgId<br /> </td> 
   <td> Identity Managementシステム (IMS) の組織 ID:Adobe Experience Cloud内の一意の組織 ID。特に VisitorID サービスおよび IMS SSO で使用されます。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> P3PCompactPolicy<br /> </td> 
   <td> 永続 Cookie に使用するポリシーを記述する値（P3P コンパクトポリシー形式に準拠）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'CAO DSP COR CURA DEVa TAa OUR BUS IND UNI COM NAV'<br /> </td> 
  </tr> 
  <tr> 
   <td> cookieDomain<br /> </td> 
   <td> Cookie を設定するドメインを明示的に示すために設定する、ドメインのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> databaseId<br /> </td> 
   <td> トラッキングインスタンスに関連付けられたデータベース識別子.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> defLogCount<br /> </td> 
   <td> 呼び出し別のログ数：メソッド GetTrackingLogs.<br /> の呼び出し時にデフォルトで返されるログの数 </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> expirationURL<br /> </td> 
   <td> 期限切れのリダイレクトのページ：配信アクションのリダイレクトが期限切れになったときに、リダイレクションサーバーが既定で使用する Web ページの URL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxJobsInCache<br /> </td> 
   <td> 最大ジョブ数：キャッシュ内の配信アクションの最大数。 50 以下にする必要があります。 <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> startRedirection<br /> </td> 
   <td> リダイレクトサービスを開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> startRedirectionInModule<br /> </td> 
   <td> モジュールモードでリダイレクトサービスを開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> trackWebVisitors<br /> </td> 
   <td> Web トラッキング：不明なユーザーが訪問したページのログの作成。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingPassword<br /> </td> 
   <td> リダイレクションサーバーが使用するパスワード.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

**web > redirection > spareServer** ノードの異なるパラメータを次に示します。

詳しくは、[ 冗長な追跡 ](../../installation/using/configuring-campaign-server.md#redundant-tracking) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> enabledIf<br /> </td> 
   <td> 次の場合に考慮：式が true を返した場合は、トラッキングサーバーが考慮されます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ID<br /> </td> 
   <td> 名前<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> url<br /> </td> 
   <td> 予備リダイレクトサーバー URL<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

### spamCheck {#spamcheck}

**web > spamCheck** ノードの様々なパラメーターを次に示します。 これは、E メールのスパム対策スコアリング評価パラメーターの設定です。

詳しくは、[SpamAssassin の設定 ](../../installation/using/configuring-spamassassin.md) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> command<br /> </td> 
   <td> E メールのスパム対策スコアを評価するために実行するコマンド ( 例：'perl spamcheck.pl').<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## wfserver {#wfserver}

**wfserver** ノードの異なるパラメータを次に示します。 これは、ワークフロープロセスの設定です。

詳しくは、[ 高可用性のワークフローとアフィニティ ](../../installation/using/configuring-campaign-server.md#high-availability-workflows-and-affinities) を参照してください。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> アフィニティ<br /> </td> 
   <td> アフィニティ<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> いいえ<br /> </td> 
  </tr> 
  <tr> 
   <td> dataBasePoolPeriodSec<br /> </td> 
   <td> 期間<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 20<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費された RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：HostName:Port 通知のリレーを有効にしています。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>
