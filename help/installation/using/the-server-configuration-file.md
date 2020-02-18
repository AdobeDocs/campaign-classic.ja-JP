---
title: サーバー設定ファイル
seo-title: サーバー設定ファイル
description: サーバー設定ファイル
seo-description: null
page-status-flag: never-activated
uuid: 8ef7168b-3543-4830-80b0-65a023158b3f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: appendices
discoiquuid: da2198a3-7cef-4419-894d-e5bb51bb480c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 09fa3751d94fd71a68470174dd0b4a48d94d3f44

---


# サーバー設定ファイル{#the-server-configuration-file}

Adobe Campaignの全体的な設定は、インストールディレクトリの **conf****** ディレクトリにあるserverConf.xmlファイルで定義されます。 この節では、 **serverConf.xmlファイルのすべての異なるノードとパラメーターを示します** 。

>[!NOTE]
>
>サーバー側の設定は、アドビがホストするデプロイメントに対してのみ実行できます。 各デプロイメントの詳細については、「ホスティングモデル」の節 [または](../../installation/using/hosting-models.md) 、この記事を参照 [してください](https://helpx.adobe.com/campaign/kb/acc-on-prem-vs-hosted.html)。 この節では、ホストモデルとハイブリッドモデルのインストールと設定の手順を示 [します](../../installation/using/hosted-model.md)。

最初のパラメーターは共有ノード内 **にあり** ます。 これらはインスタンスに関連しています。 これらは、すべてのnlserverコマンド（nlserver web、nlserver wfserverなど）で使用される可能性があります。 その他のセクションは、特定のnlserverサブコマンドに関連しています。

**共有パラメーター**

* [認証](#authentication)
* [dataStore](#datastore)
* [dnsConfig](#dnsconfig)
* [exec](#exec)
* [htmlToPdf](#htmltopdf)
* [javaScript](#javascript)
* [mailExchanger](#mailexchanger)
* [モジュール](#module)
* [監視](#monitoring)
* [オコン](#ooconv)
* [proxyConfig](#proxyconfig)
* [threadPool](#threadpool)
* [urlPermission](#urlpermission)
* [xtkJobs](#xtkjobs)

**その他のパラメーター**

* [アーカイブ](#archiving)
* [inMail](#inmail)
* [相互作用の](#interactiond)
* [MTA](#mta)
* [nmac](#nmac)
* [パイプの](#pipelined)
* [修理](#repair)
* [securityZone](#securityzone)
* [SMS](#sms)
* [stat](#stat)
* [syslogd](#syslogd)
* [tracking](#tracking)
* [trackinglogd](#trackinglogd)
* [Web](#web)
* [wfserver](#wfserver)

## authentication {#authentication}

認証ノードの様々なパラメーターを次に **示します** 。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> defaultMode<br /> </td> 
   <td> デフォルトの識別モード.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nl'<br /> </td> 
  </tr> 
  <tr> 
   <td> longSessionTimeOutSec<br /> </td> 
   <td> Timeout of long sessions in seconds.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1296000<br /> </td> 
  </tr> 
  <tr> 
   <td> securityTimeOutSec<br /> </td> 
   <td> Security token timeout in seconds.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionCacheSec<br /> </td> 
   <td> キャッシュ時間：セッション情報のキャッシュ（秒単位）。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionTimeOutSec<br /> </td> 
   <td> Session timeout in seconds.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
 </tbody> 
</table>

### XTK {#xtk}

次に、認証/XTKノードの様々なパ **ラメーターを示します** 。

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
   <td> 内部アカウントセキュリティゾーン：社内アカウントの認証済みゾーン。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'lan'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## dataStore {#datastore}

dataStoreノードの様々なパラメーターを次に **示します** 。 ここでサーバーのデータソースが定義されます。

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
   <td> Export directory: path of destination directory for the exported data.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/export/' <br /> </td> 
  </tr> 
  <tr> 
   <td> extraSandboxedDirectories<br /> </td> 
   <td> Extra sandboxed directories: other paths to be added in the sandbox (coma separated).<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/home/customers/,/sftp/' <br /> </td> 
  </tr> 
  <tr> 
   <td> formCacheTimeToLive<br /> </td> 
   <td> フォームキャッシュの有効期限の遅延：キャッシュエントリが無効になるまでのタイムアウト（秒）。 キャッシュエントリはパブリケーション時にのみ更新されます。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> ホスト<br /> </td> 
   <td> DNSマスク：このインスタンスが提供するDNSマスクのリスト（コンマ区切り、*と？を使用できます） パターンを参照)。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '*'<br /> </td> 
  </tr> 
  <tr> 
   <td> interactionCacheTimeToLive<br /> </td> 
   <td> インタラクションJSSPキャッシュの有効期限の遅延：キャッシュエントリが無効になるまでのタイムアウト（秒）。 負の値は、キャッシュが常に無効化されることを意味します。 「0」の場合、空の値または無効な値は60と見なされます。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> lang<br /> </td> 
   <td> インスタンス言語（列挙）。 使用可能な値は、「fr_FR」（フランス語）、「en_GB」(英語（英国）)、「en_US」(英語（米国）)、「de_DE」（ドイツ語）および「ja_JP」（日本語）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'en_US'<br /> </td> 
  </tr> 
  <tr> 
   <td> uploadDirectory<br /> </td> 
   <td> Upload folder: path of destination directory for the uploaded data.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/upload/' <br /> </td> 
  </tr> 
  <tr> 
   <td> uploadWhitelist<br /> </td> 
   <td> ダウンロードを許可されたファイル (「,」区切り)。この文字列は有効かつ標準の Java 式である必要があります。アップロード可 <a href="../../installation/using/configuring-campaign-server.md#limiting-uploadable-files" target="_blank">能ファイルの制限を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.+' <br /> </td> 
  </tr> 
  <tr> 
   <td> useVault<br /> </td> 
   <td> Vaultに秘密を保存する：Hashicorp vaultを使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultSecretPath<br /> </td> 
   <td> Vault の秘密鍵のパス<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/v1/secret/campaign/'<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultTokenPath<br /> </td> 
   <td> Vault トークンを含むファイルのローカルパス. このパスでは$(HOME)を使用できます（他のenv変数は使用できません）。<br /> </td> 
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
   <td> ビューキャッシュの有効期間：キャッシュエントリが無効になるまでのタイムアウト（秒）。 負の値は、キャッシュが常に無効化されることを意味します。 「0」の場合、空の値または無効な値は60と見なされます。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> workingDirectory<br /> </td> 
   <td> 作業ディレクトリの XPath。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> workingDirectory :作業ディレクトリのXPath。 デフォルト：'$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/workspace/'<br /> </td> 
  </tr> 
 </tbody> 
</table>

### proxyAdjust {#proxyadjust}

dataStore/proxyAdjustノードの様々なパラメ **ーターを示します** 。 正規表現に一致するURLは、urlBaseで定義されたURLに基づいて再生成されます。

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

dataStore/dataSourceノードの様々なパラメ **ーターを示します** 。

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
   <td> データソース名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> default<br /> </td> 
  </tr> 
 </tbody> 
</table>

「 **dataStore」>「dataSource」>「dbcnx** 」ノードで、接続設定を指定します。

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
   <td> 暗号化<br /> </td> 
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
   <td> タイプ（列挙）。 使用可能な値は、「Oracle」、「MSSQL」(Microsoft SQL Server)、「PostgreSQL」(PostgreSQL、Greenplum)、「Teradata」、「DB2」、「MySQL」、「Netezza」、「AsterData」、「SAPHANA」(SAP HANA)、redShift'(Amazon Redshift)、'ODBC'(ODBC(Sybase ASE、Sybase IQ)、'Relay'（リモート・データベースへのHTTPリレー）。<br /> </td> 
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
   <td> タイムゾーン：タイムゾ <a href="../../installation/using/time-zone-management.md" target="_blank">ーン管理を参照してください</a>。<br /> </td> 
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
   <td> タイムゾーンを持つ日付フィールド：タイムゾ <a href="../../installation/using/time-zone-management.md" target="_blank">ーン管理を参照してください</a>。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

dataStore/dataSource/ **sqlParamsノードで** 、SQLパラメーターを設定します。

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

dataStore/dataSource/ **poolノードで** 、関連する接続プールのパラメーターを設定します。

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
   <td> 短い<br /> </td> 
  </tr> 
  <tr> 
   <td> freeCnx<br /> </td> 
   <td> プールに保存されている空き接続数.<br /> </td> 
   <td> 短い<br /> </td> 
  </tr> 
  <tr> 
   <td> maxCnx<br /> </td> 
   <td> 新しい接続を拒否する前に許可された接続の最大数。このテクノ <a href="https://helpx.adobe.com/campaign/kb/how-to-increase-the-maximum-number-of-database-connections-from-.html">ート</a>。<br /> </td> 
   <td> 短い<br /> </td> 
  </tr> 
  <tr> 
   <td> maxIdleDelaySec<br /> </td> 
   <td> 接続の最大アイドル時間。0 はデフォルト値です.<br /> </td> 
   <td> 短い<br /> </td> 
  </tr> 
 </tbody> 
</table>

### virtualDir {#virtualdir}

dataStore/virtualDirノードの様々なパラメ **ーターを示します** 。 これは、仮想ディレクトリと実ディレクトリのマッピングの設定です。

詳しくは、「パブリックリソースの管 [理」を参照してください](../../installation/using/configuring-campaign-server.md#managing-public-resources)。

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

デフォルトの設定は次のとおりです。

```
<virtualDir name="images" path="$(XTK_INSTALL_DIR)/var/res/img/"/>
<virtualDir name="formCache" path="$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/formCache/"/>
<virtualDir name="publicFileRes" path="$(XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)"/>
```

### preprocessCommand {#preprocesscommand}

dataStore/preprocessCommandノードの様々なパラメ **ーターを示します** 。 これらは、「ファイルを読み込み」ワークフローアクティビティの前処理に使用する許可されたコマンドです。

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

デフォルトの設定は次のとおりです。

```
<preprocessCommand command="" label="None" name="none"/>
<preprocessCommand command="zcat &quot;$fileName&quot;" label="Decompression" name="zcat"/><preprocessCommand command="gpg --decrypt &quot;$fileName&quot;" label="Decrypt" name="gpg"/>
```

## dnsConfig {#dnsconfig}

dnsConfig **** （DNS構成）ノードの様々なパラメーターを次に示します。

For additional information, refer to this [section](../../installation/using/configuring-campaign-server.md).

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
   <td> ドメイン名：デフォルトのドメイン名。 SMTP HELOコマンドで使用されます。 By default, uses the network parameters of the first network interface declared in Windows; or parses the file/etc/resolv.conf under Linux (domain or search entry). <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> nameServers<br /> </td> 
   <td> DNSサーバー：ドメインネームサーバー(DNS)のコンマ区切りリスト。 以下の注を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> retry<br /> </td> 
   <td> DNS クエリの再試行数.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> Timeout in milliseconds for a DNS query.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 5000<br /> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>nameServersに関す **る注意**:デフォルトでは、ネットワークを使用します。
>windowsで宣言された最初のネットワーク・インタフェースのパラメータ
>UNIXでは定義されていません。 ドメインネームサーバー(DNS)を定義します
>MTAが、
>ドメイン。
>
>この値が定義されていない場合、MTAはホストネットワーク設定でこの情報をシークします。 複数のDNSが可能な場合は、異なるDNSアドレスをコンマで区切る必要があります(例：212.155.207.1,212.155.207.2)。 配信サーバーに複数のネットワークインターフェイスがある場合、MTAが使用するDNSリストが最初に表示されます。 この場合、曖昧さを避けるために **nameServer** パラメーターを指定することをお勧めします。

>[!CAUTION]
>
>ネットワークホスト構成でDHCPを使用している場合、MTAはDHCPから提供されたDNSリストを見つけません。 この場合、WindowsのコントロールパネルのネットワークパラメーターでDNSリストを指定することをお勧めします。

## exec {#exec}

以下に、 **exec** （コマンド実行）ノードの異なるパラメータを示します。

詳しくは、認証済み外部コマンドの [制限を参照してください](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)。

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
   <td> ブラックリスト登録のコマンドを含むファイルへのパス. <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> user<br /> </td> 
   <td> 別のユーザーとしてコマンドを実行.<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## htmlToPdf {#htmltopdf}

htmlToPdfノードの様々なパラメーターを次に **示します** 。 WebページをPDFドキュメントに変換するサービスの設定です。

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
   <td> 変換を実行するためのコマンドライン（「その他」モード）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessCount<br /> </td> 
   <td> Max. number of conversion processes allowed at a time on one machine.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> mode<br /> </td> 
   <td> 変換に使用するツール。 使用可能な値は次のとおりです。phantomjs、wkhtmltopdf、other、disabled<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 「幻の」 <br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> 変換のタイムアウト：最大変換時間（秒単位）。 このしきい値を超えると、変換処理が停止し、エラーが発生します。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 120<br /> </td> 
  </tr> 
  <tr> 
   <td> verbose<br /> </td> 
   <td> Verbose mode: start in verbose mode to diagnose possible errors.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> waitTime<br /> </td> 
   <td> プロセス待機時の遅延：すべてのプロセスが同時に使用され、プロセスの解放を待機する場合は、秒単位で遅延します。 この遅延を超えると、変換が停止し、エラーが発生します。 <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
 </tbody> 
</table>

ファントムジスの例：

```
phantomjs - -ignore-ssl-errors=true '$(XTK_INSTALL_DIR)/bin/htmlToPdf.js' '-out:{outPdf}' '-post:{postFile}' '-url:{originUrl}' -sessiontoken:{sessiontoken} -format:{format} -orientation:{orientation} -marginTop:{marginTop} -marginLeft:{marginLeft} -marginRight:{marginRight} -marginBottom:{marginBottom}
```

## javaScript {#javascript}

次に、 **javaScriptノードの様々なパラメーターを示します** 。 これは、JavaScriptインタープリタの設定です。

詳しくは、レポートのドキュメント [とこのテクノ](../../reporting/using/actions-on-reports.md#memory-allocation) ートを参照して [ください](https://helpx.adobe.com/campaign/kb/out-of-memory-error-in-js-code-activity-in-workflows.html)。

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
   <td> Maximum size in megabytes before running the garbage collector.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 512 <br /> </td> 
  </tr> 
  <tr> 
   <td> stackSizeKB<br /> </td> 
   <td> 各スタックチャンクのサイズ（キロオクテット）。 これはメモリ管理チューニングパラメータで、ほとんどのユーザは調整しないでください。 <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
 </tbody> 
</table>

## mailExchanger {#mailexchanger}

mailExchangerノードの異なるパラメー **ター** 。 SMTPサーバーの設定です。

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
   <td> SMTP server: IP address of SMTP server for the transfer of emails.<br /> </td> 
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

## module {#module}

モジュールノードの様々なパラメー **ター** 。 これは、名前空間制限モジュールxtkの設定です。

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

## monitoring {#monitoring}

監視ノードの異なるパラメータを次に **示します** 。 これは監視サービスの設定です。

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
   <td> Maximum preparation time: duration in seconds after which a delivery action should no longer be in preparation.<br /> </td> 
   <td> 長い<br /> </td> 
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

## オコン {#ooconv}

ooconvノードの異なるパラメーターを次に **示します** 。 これは、ドキュメント変換サーバーの設定です。

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
   <td> 長い<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxServerIdleSec<br /> </td> 
   <td> OpenOffice サーバーが強制終了するまでの最大アイドル時間。<br /> </td> 
   <td> 長い<br /> </td> 
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

proxyConfigノードの異なるパラメーターを次に **示します** 。 これは、プロキシパラメーターの設定です。

詳しくは、プロキシ接続の設定 [を参照してください](../../installation/using/configuring-campaign-server.md#proxy-connection-configuration)。

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
   <td> enabled<br /> </td> 
   <td> プロキシサーバーを使用.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> override<br /> </td> 
   <td> Exceptions: list of addresses for which proxy parameters shall be ignored.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'localhost*' <br /> </td> 
  </tr> 
  <tr> 
   <td> useSingleProxy<br /> </td> 
   <td> 一意のプロキシサーバー：すべてのタイプのプロキシに同じ設定を使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### HTTPプロキシ/セキュアプロキシ {#http-proxy---secure-proxy-}

proxyConfig/HTTPプ **ロキシ** /セキュアプロキシノードで、次のパラメーターを設定します。

詳しくは、プロキシ接続の設定 [を参照してください](../../installation/using/configuring-campaign-server.md#proxy-connection-configuration)。

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
   <td> 短い<br /> </td> 
  </tr> 
 </tbody> 
</table>

## threadPool {#threadpool}

threadPoolノードの様々なパラメーターを次に **示します** 。

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
   <td> Maximum number of threads in pool. <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## urlPermission {#urlpermission}

urlPermissionノードの様々なパラメーターを次に **示します** 。 これは、JavaScriptコードがアクセスできるURLのリストです。

JavaScriptコード内でURLを検出した場合に、Adobe Campaignサーバーで使用できるか、使用できないかを指定するドメインと正規表現のリストです。

URLが見つからない場合は、指定されたデフォルトのモードに従って、デフォルトのアクションが実行されます。

詳細については、「送信接続の保護」を [参照してください](../../installation/using/configuring-campaign-server.md#url-permissions)。

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
   <td> URLが許可されたリストにない場合のデフォルトのアクション（列挙）。 使用可能な値は、「ignore」（警告メッセージなしで承認、保護を無効にする必要があります）、「warn」（許可して警告メッセージを発行）、「deny」（URLへのアクセスを禁止）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> deny<br /> </td> 
  </tr> 
  <tr> 
   <td> debugTrace<br /> </td> 
   <td> URL選択メカニズムのデバッグトレース：url検証プロセス中に追加のメッセージが発行されます。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### url {#url}

各URLに対して、次のパラメーター **を持つ** URLノードを追加します。

詳細については、「送信接続の保護」を [参照してください](../../installation/using/configuring-campaign-server.md#url-permissions)。

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
   <td> URLに関係するドメイン名またはドメインの親：検証を高速化するために、検証するURLのドメインのすべてまたは一部。 URLが正規表現に関して検証されるのは、ドメインにdsnSuffixが含まれている場合のみです。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> urlRegEx<br /> </td> 
   <td> このドメインに属するURLの検証を絞り込む正規表現：dnssuffixに対応するURLで検証する必要がある正規表現。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

レコードが **dnsSuffix** ( **urlRegEx**)を満たすが、urlRegExを満たさない場合、次のレコードが調べられます。

例えば、ドメインbusiness.comのすべてのURLへのアクセスを許可するには、次の2つのレコードを定義します。

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;http://.*&quot;

および

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;https://.*&quot;

デフォルトの設定は次のとおりです。

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

xtkJobsノードの様々なパラメータ **を示します** 。 これは、サーバージョブの設定です。

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
   <td> 長い<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## archiving {#archiving}

アーカイブ・ノードの様々なパラメー **ター** 。 これは、バックグラウンドで実行されるアーカイブ操作の設定です。

詳しくは、「電子メールアーカイブのア [クティブ化（オンプレミス）」を参照してくださ](../../installation/using/email-archiving.md#activating-email-archiving--on-premise-)い。

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
   <td> 長い<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> archivingType<br /> </td> 
   <td> 送信メッセージのアーカイブ方法（列挙）。 指定可能な値は「0」（アーカイブなし）と「1」（送信されたメッセージのアーカイブをSMTPサーバーに転送）です。<br /> </td> 
   <td> Byte<br /> </td> 
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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> compressBatchSize<br /> </td> 
   <td> 圧縮アーカイブのサイズ：圧縮アーカイブ内の最大ファイル数。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 10000<br /> </td> 
  </tr> 
  <tr> 
   <td> compressionFormat<br /> </td> 
   <td> アーカイブ中に使用される圧縮形式（列挙）。 指定できる値は「0」（圧縮なし）と「1」（送信されたメッセージをzip形式で圧縮）です。<br /> </td> 
   <td> Byte<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> expirationDelay<br /> </td> 
   <td> 未処理の電子メールの自動アーカイブの前に遅延：未処理の電子メールがアーカイブされるまでの日数。<br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollDelay<br /> </td> 
   <td> Delay (in seconds) between each update event.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeArchivesDelay<br /> </td> 
   <td> 未処理の E メールが削除されるまでの日数.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 7<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpBccAddress<br /> </td> 
   <td> ターゲットのアーカイブ先<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> smtpEnableTLS<br /> </td> 
   <td> Activate SMTPS support: activates the delivery of emails in safe mode (STARTTLS/SMTPS) when supported by the remote server.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpNbConnection<br /> </td> 
   <td> アーカイブ SMTP サーバーへの接続数.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpRelayAddress<br /> </td> 
   <td> Comma-separated list of DNS names or IP addresses of SMTP relays to use. <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> smtpRelayPort<br /> </td> 
   <td> SMTP サーバーの IP ポート。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## inMail {#inmail}

inMailノードの異なるパラメー **ター** 。 これは、受信電子メール管理モジュールの設定です。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> checkInstanceName<br /> </td> 
   <td> Verify instance name: if true, the name of the Adobe Campaign instance contained in the Message-ID headers must be the same as the current instance. <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> defaultForwardAddress<br /> </td> 
   <td> Forwarding address: default email transfer address not processed by a rule. <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> errorForwardAddress<br /> </td> 
   <td> Address for errors: default address used to transfer invalid Emails (bad MIME encoding). <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ignoreSize<br /> </td> 
   <td> メッセージサイズを無視：は、POP3サーバから返されるメッセージのサイズを無視するために使用されます。 この場合、モジュールは'.'が必要です。 at the end of the messages. <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> inMailPeriodSec<br /> </td> 
   <td> メッセージ読み取り期間：メッセージキューのポーリング頻度。<br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> 更新するログの最大数：データベースを更新する前にメモリ内に保持するログメッセージの最大数を定義します。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 20<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMsgPerSession<br /> </td> 
   <td> POP3 セッションで読み取るメッセージの最大数。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 200<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSessionTTLSec<br /> </td> 
   <td> セッション時間：メッセージ処理セッションの最大時間。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> popMailPeriodSec<br /> </td> 
   <td> POP3 polling period<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> popQueueSize<br /> </td> 
   <td> 読み取りメッセージのキューサイズ<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> popTimeoutSec<br /> </td> 
   <td> Communication timeout with POP3 server. <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriodSec<br /> </td> 
   <td> ポーリングするアカウントのデータベース再読み込み頻度。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

### msgDump {#msgdump}

inMail > msgDumpノ **ードで** 、次のパラメータを設定します。 これは、処理されたメッセージのダンプの設定です。

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
   <td> ダンプ<br /> </td> 
   <td> Save all inbound messages in text format. <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> msgPath<br /> </td> 
   <td> メッセージダンプのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/tmp/inMail'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 相互作用の {#interactiond}

ここでは、対話型ノードの様々なパラメ **ーター** 。 これは、受信インタラクションイベントの書き込みデーモンの設定です。

詳しくは、インタラクション — データバ [ッファーを参照してください](../../installation/using/interaction---data-buffer.md)。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> callDataSize<br /> </td> 
   <td> Max. number of characters stored in the shared memory for call data.<br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedEntries<br /> </td> 
   <td> Max. number of events stored in the shared memory.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> nextOffersSize<br /> </td> 
   <td> 提案直後に並べ替えられ、統計用に保存される適格オファーの最大数.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> statsPeriod<br /> </td> 
   <td> 応答時間統計の集計時間（秒）。 0は、統計の保存が非アクティブ化されたことを意味します。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> targetKeySize<br /> </td> 
   <td> Max. number of characters stored in the shared memory for identifying individuals.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 16<br /> </td> 
  </tr> 
 </tbody> 
</table>

## MTA {#mta}

mtaノードの様々なパラメーターを次に **示します** 。 これは、配信エージェントの設定です。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataLogPath<br /> </td> 
   <td> 送信した電子メールのパスの保存：空でない場合は、送信された電子メールのすべてのソースファイルが保存されるパス。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> debugPath<br /> </td> 
   <td> ダンプディレクトリ：空でない場合は、このディレクトリに送信されたメールメッセージのMIMEエンベロープをコピーします。 トラブルシューティングに使用します。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> dnsRequestLogDelayMs<br /> </td> 
   <td> DNSクエリログの遅延：ログを表示する時間（ミリ秒）。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> errorPeriodSec<br /> </td> 
   <td> Error statistics frequency: time between generation of statistics and storage in the database. <br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> ログメッセージのレベルを表示します。データベースに書き込まれるログの重大度レベル。 MTAによって生成されたログメッセージは、必ずしもデータベースに書き込まれるわけではありません。 このパラメーターを使用して、メッセージをデータベースに書き込む必要があると考えられるレベルを定義できます。 レベル2を定義すると、レベル1と0のメッセージも書き込まれ、レベル1と0のメッセージのみが書き込まれます。 使用可能な値は次のとおりです。0（エラー）、1（警告）、2（情報）<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMemoryMb<br /> </td> 
   <td> MTA プロセスが使用できる最大メモリサイズ (MB)。この制限を超えると MTA プロセスが再起動され、使用しているメモリはシステムに解放されます。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> minConnectionsToLog<br /> </td> 
   <td> 考慮する接続しきい値. errorPeriodSec で指定される期間の接続の合計数がしきい値よりも厳密に低い場合、エラー統計は指定のパスに対して生成されません。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> minErrorsToLog<br /> </td> 
   <td> Error threshold to take into account: error statistics are not generated for a given path if the total number of errors for the period specified by errorPeriodSec is strictly lower than the threshold.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> minMessagesToLog<br /> </td> 
   <td> 考慮するメッセージしきい値. errorPeriodSec で指定する期間に送信されたメッセージの合計数が厳密にはしきい値を下回る場合、指定されたパスに対するエラー統計は生成されません。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：HostName：通知の中継に使用するポート。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeDataLogDelay<br /> </td> 
   <td> アーカイブ済みの電子メールが削除されるまでの遅延：datalogpathで指定されたディレクトリ内のアーカイブ済み電子メールが削除されるまでの日数。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
  <tr> 
   <td> retryLostMessages<br /> </td> 
   <td> Retry lost messages: parts of deliveries will be retried if the child process is dead.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> statServerAddress<br /> </td> 
   <td> 配信統計サーバーのアドレス。&lt;dnsまたはip&gt; [:
     &lt;port&gt; ]. 詳しくは、 <a href="../../installation/using/email-deliverability.md#coordinates-of-the-statistics-server" target="_blank">統計サーバの座標を参照してください</a>。 
      <br /> 
     </td> 
   <td> 文字列<br /> </td> 
   <td> 定義されていない場合、デフォルトのポートは7777です。<br /> </td> 
  </tr> 
  <tr> 
   <td> statServerTLSSupport<br /> </td> 
   <td> ドメイン別のTLSを有効にする：mxで設定できるTLSを有効にします（最新の統計サーバーが必要です）。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true <br /> </td> 
  </tr> 
  <tr> 
   <td> statServerVersion<br /> </td> 
   <td> 使用するプロトコルのバージョン：通信プロトコルのバージョン（v5.11および6.0.2サーバーの場合は1、v6.1サーバーの場合は2）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 未定義の場合は、最新バージョンが使用されます。 <br /> </td> 
  </tr> 
  <tr> 
   <td> useMomentum<br /> </td> 
   <td> 「true」に設定した場合、インスタンスは拡張MTAを使 <a href="https://helpx.adobe.com/campaign/kb/campaign-enhanced-mta.html" target="_blank">用します</a>。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td>b 
  </tr>
  <tr> 
   <td> verifyMode<br /> </td> 
   <td> Verification mode: activates the verify mode (no physical transmission of messages; used for simulation and tests).<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> workingPath<br /> </td> 
   <td> Working directory: location of temporary files used by the MTA to communicate with its child processes.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/mta/' <br /> </td> 
  </tr> 
  <tr> 
   <td> xMailer<br /> </td> 
   <td> X-Mailer field: value of field 'X-Mailer' in SMTP mail header.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nlserver, Build $(PRODUCT_VERSION)'<br /> </td> 
  </tr>  
 </tbody> 
</table>

### キャッシュ {#cache}

キャッシュノ **ードで** 、次のパラメーターを設定します。 これは、ローカルファイルキャッシュの設定です。

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
   <td> Recycled after: period, expressed in seconds, after which the file is automatically deleted from the cache to reclaim storage.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 244800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSizeOnDiskMb<br /> </td> 
   <td> 最大キャッシュサイズ (MB)。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> purgePeriodSec<br /> </td> 
   <td> Purge frequency: period in seconds between executions of the cache purge mechanism.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
 </tbody> 
</table>

### relay {#relay}

mta > relayノ **ードで** 、次のパラメーターを設定します。 これは、メッセージ配信用のメールサーバーの設定です。

詳細は、「 [SMTPリレー」を参照してください](../../installation/using/configuring-campaign-server.md#smtp-relay)。

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
   <td> address<br /> </td> 
   <td> Comma-separated list of DNS names or IP addresses of SMTP relays to use. <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> SMTP サーバーの IP ポート。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

### マスター {#master}

mta/masterノ **ードで** 、次のパラメーターを設定します。 これは、メインサーバーの設定です。

For additional information, refer to this [section](../../installation/using/configuring-campaign-server.md#mta-child-processes).

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
   <td> 長い<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> dataBaseRetryDelaySec<br /> </td> 
   <td> データベースへの接続の失敗後に待機する期間。通常、データベース接続が失敗する原因は、データベースサーバー自体にあります。例えば、サーバーは、メンテナンスのために停止されることもあります。データベース接続が失敗した場合に接続を再試行するまでの時間は、DataBaseRetryDelay パラメーターで定義します。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> domainKeysReloadPeriodSec<br /> </td> 
   <td> 秘密鍵のキャッシュの有効期間 (DomainKeys)。DomainKeys の推奨事項 (http://antispam.yahoo.com/domainkeys) に従った E メールへの署名に使用される秘密鍵は、データベース内にオプションとして保存されます。domainKeysReloadPeriodSec パラメーターに、MTA がこれらの鍵をキャッシュに保持できる秒数を定義します。この時間が過ぎた後は、すべての鍵をデータベースから再度読み込む必要があります。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSpareServers<br /> </td> 
   <td> 子サーバーの最大数。実行しているサービスの最大数を表します。サーバーメモリリソースと互換性がある最適値で制限することをお勧めします。これは、配信中にチェックできます。使用されるメモリは、利用可能な物理メモリの 3 分の 1 以下にする必要があります。それ以上になると、スワップが使用されます。詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#mta-child-processes" target="_blank">MTA子プロセスを参照してください</a>。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> minSpareServers<br /> </td> 
   <td> 子サーバーの最小数。MTA は少なくともこの数のサーバーが実行され続けるようにします。サーバーの数がこれよりも少ない場合は、この値に達するまで毎秒新しいサーバーを再起動します。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> startSpareServers<br /> </td> 
   <td> 起動時の子サーバーの数。子サーバーの数が動的に監視されます。MTA の起動時に、この値で指定した最大数の子サーバーが作成されます。通常、子サーバーは、ホストリソースを保存するために、秒単位の 1 台のサーバーより速く開始することはできません。ただし、MTA を起動した場合、子サーバーができるだけ早く使用可能になるように、この制限は上書きされます。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 小児 {#child}

mta/子ノ **ードで** 、次のパラメーターを設定します。 これは、子サーバーの設定です。

詳しくは、「電子メール送信の最適化」 [を参照してください](../../installation/using/email-deliverability.md#email-sending-optimization)。

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
   <td> 長い<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> maxAgeSec<br /> </td> 
   <td> 最大メッセージ保持時間. 準備されたメッセージがスロットルによって送信されなかった場合やターゲット MTA に接続できなかった場合、メッセージは破棄され、次の再試行で処理されます。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxGCMConnectPerChild<br /> </td> 
   <td> 各子サーバーによって開始された FCM に対する並列 HTTP リクエストの最大数.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMsgPerChild<br /> </td> 
   <td> 子サーバーごとの最大メッセージ数。それぞれの MTA の子はこの数のメッセージを処理して終了します。MTA でのメモリまたはリソースリークが悪影響を及ぼさない程度の数を指定することが重要です (通常は数千)。MTA コード内に既知のメモリリークが存在していない場合でも、埋め込まれた JavaScript  および XSL エンジンは完全に信頼できるものではありません。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 5000000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWaitingMessages<br /> </td> 
   <td> Pending messages: maximum number of messages waiting in memory to be delivered. <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 2000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWorkingSetMb<br /> </td> 
   <td> Maximum memory size (in MB) that a child process can use. Above this limit, the process is stopped so that the memory it uses is released to the system. <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 128<br /> </td> 
  </tr> 
  <tr> 
   <td> soapConnectorTimeoutSec<br /> </td> 
   <td> 配信コネクタの SOAP 接続が破棄されるまでのタイムアウト (秒)。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> startWithFirstMX<br /> </td> 
   <td> 常に最優先 MX で開始.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> timeToLive<br /> </td> 
   <td> 再開時に連続して再試行する最大回数。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 48<br /> </td> 
  </tr> 
 </tbody> 
</table>

mta/子/ **smtpノードで** 、次のパラメーターを設定します。 これはSMTPセッションの設定です。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> idleSessionTimeoutSec<br /> </td> 
   <td> アイドルセッションがタイムアウトになりました。このパラメーターは、あるドメインに対して複数のメッセージを転送するためにセッションが再利用される場合にのみ使用されます。MTA によってメッセージの転送が完了した場合、使用していた SMTP セッションはシステム的にはクローズされません。この同じドメインへのメッセージの送信準備が整えば、同じ SMTP セッションが再利用されます。このため、セッションは自動的にクローズされません。パラメーター IdleSessionTimeout では、別のメッセージを待機するために SMTP セッションがアクティブな状態を維持できる時間を定義します。その時間が経過した後、セッションは自動的にクローズされます。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> initialDelaySec<br /> </td> 
   <td> 接続を再試行する前の初期遅延. この遅延は、接続が失敗するたびに2倍になります。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSessionsPerChild<br /> </td> 
   <td> 子サーバーによる SMTP セッションの最大数。メッセージを配信するために、この MTA は受信者 MTA との SMTP 接続を初期化します。1 台の子サーバーでのアクティブな同時 SMTP セッションの最大数はこの値によって制限されます。この値と maxSpareServers の値を乗算すると、1 台の子サーバーで同時に処理できるメッセージの最大数がわかります。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

mta/子/ **smtp/IPAffinityノードで** 、次のパラメーターを設定します。 これは、送信SMTPトラフィックを最適化するためのIPアドレスとの親和性の管理の設定です。

詳しくは、「使用するIPアドレスのリスト [」および「親和性を](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use) 持つ送信SMTPトラフィックの管理 [」を参照してください](../../installation/using/configuring-campaign-server.md#managing-outbound-smtp-traffic-with-affinities)。

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
   <td> ドメイン名：IPアドレスにリンクされたローカルドメイン名。 SMTP HELOコマンドを発行する場合に使用します。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> name<br /> </td> 
   <td> 論理名：ユーザーによって親和性にリンクされた名前。 名前はセミコロンで区切ります。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

mta > child > smtp > IP **** nodeで、次のパラメーターを設定します。

詳しくは、使用するIPアド [レスのリストを参照してください](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)。

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
   <td> Associated physical address. Eg: '192.168.0.1'<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> publicId<br /> </td> 
   <td> 関連付けられたパブリックアドレス ID です。統計サーバーのキーとして使用されます。数値で指定する必要があります。See this <a href="../../installation/using/email-deliverability.md#managing-ip-addresses">section</a>.<br /> </td> 
   <td> 長い<br /> </td> 
  </tr> 
  <tr> 
   <td> 重み付け<br /> </td> 
   <td> この IP の使用頻度を他の IP に相対的に指定します (重みを大きくすると頻度が高くなります)。<br /> </td> 
   <td> 長い<br /> </td> 
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

nmacノードの様々なパラメーターを **示します** 。 これは、プッシュ通知配信の設定です。

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
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### relay {#relay-1}

nmac > relayノードの異なるパ **ラメータを示します** 。 これにより、メッセージ配信（ios http2コネクタ）にリレーを使用するように設定されます。

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
   <td> address<br /> </td> 
   <td> DNS address or name of the relay to use. <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> リレーポート<br /> </td> 
   <td> 長い<br /> </td> 
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

## パイプの {#pipelined}

パイプラインノードの異なるパラメ **ータを示し** ます。 これは、パイプラインサービスのイベント処理モジュールの設定です。

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
   <td> Name of the application generated in the Developer connection when the public key is saved. <br /> </td> 
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
   <td> トークンを取得するときに使用する秘密鍵 (AES で XtkKey オプションを指定して暗号化).<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動で開始 <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> disableAuth<br /> </td> 
   <td> 認証の無効化：認証なしでパイプラインサービスに接続します。 <br /> </td> 
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
   <td> ステータス保存期間：プロセスの内部情報がファイルに保存される頻度。 0の場合は非アクティブです。 <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> forcedPipelineEndpoint<br /> </td> 
   <td> Listening URL: force the listening URL of the Pipeline Services. <br /> </td> 
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
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> monitorServerPort<br /> </td> 
   <td> ステータスサーバーポート：プロセスのステータスを問い合わせることができるHTTPサーバーポート。 0の場合は非アクティブです。<br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> Delay before the pointer is stored: the pointer will be stored in the database at least once during this period (useful in case of low activity).<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> processingJSThreads<br /> </td> 
   <td> パーソナライズされた JavaScript コネクタによるイベント処理のスレッド数。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> processingThreads<br /> </td> 
   <td> イベント処理用のスレッド数<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> retryPeriodSec<br /> </td> 
   <td> 失敗があった場合の処理間の遅延.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> retryValiditySec<br /> </td> 
   <td> この期間後に放棄：この期間後も処理が失敗し続ける場合は、イベントを破棄します。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 修理 {#repair}

修復ノードの異なるパラメー **ター** 。 これは、データベース修復モジュールの構成です。

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
   <td> Delivery actions repair module: delay (in minutes) after which delivery actions can be processed by the repair module. <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
 </tbody> 
</table>

## securityZone {#securityzone}

securityZoneノードの様々なパラメーターを次に **示します** 。

詳細については、 [Defining security zonesを参照してください](../../installation/using/configuring-campaign-server.md#defining-security-zones)。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowEmptyPassword<br /> </td> 
   <td> パスワードなしでアプリケーションを使用することをユーザーに許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowHTTP<br /> </td> 
   <td> オペレーターのログオンに HTTP の使用を許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowSQLInjection<br /> </td> 
   <td> 式で SQLDATA の使用を承認.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowUserPassword<br /> </td> 
   <td> ユーザー / パスワードセッショントークンを許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> showErrors<br /> </td> 
   <td> エラーの詳細を表示<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルトの設定は次のとおりです。

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

securityZone/subNetworkノードの異なるパラメ **ーターを示します** 。

詳細については、 [Defining security zonesを参照してください](../../installation/using/configuring-campaign-server.md#defining-security-zones)。

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
   <td> proxy<br /> </td> 
   <td> このサブネットワークでインスタンスにアクセスするために使用されている (リバース) プロキシのマスクまたはアドレス。この場合、「X-Forwarded-For」ヘッダーがこのプロキシの代わりにテストされます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 127.0.0.1 <br /> </td> 
  </tr> 
 </tbody> 
</table>

## sms {#sms}

以下に、 **smsノードの異なるパラメータを示** します。 受信SMS管理モジュールの構成です。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataRetentionDays<br /> </td> 
   <td> SMPP コネクタで保持される作業ファイルの最大数。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> dataSizeMo<br /> </td> 
   <td> SMPP 作業ファイルの最大サイズ (MB)。<br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> セッション継続フレームの繰り返し：最大 period in seconds between two frames for notifying that the receiving session is still enabled.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollPeriod<br /> </td> 
   <td> 検索頻度：SMSアカウントのポーリング期間。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriod<br /> </td> 
   <td> アカウントの再読み込み頻度：ポーリングするアカウントのデータベース再読み込み頻度。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> srReadDelay<br /> </td> 
   <td> SR処理の遅延秒数：srReadDelayで指定された時間（秒）を引いた現在時間より前の回復日のSRのみ。 <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> SMS ゲートウェイでの通信タイムアウト。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
 </tbody> 
</table>

### netsize {#netsize}

以下に、 **sms > netsizeノードの異なるパラメータを示します** 。

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
   <td> Timeout in seconds when establishing a connection with Netsize.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
 </tbody> 
</table>

## stat {#stat}

statノードの様々なパラメータを次に示 **します** 。 これは、MTA統計モジュールの設定です。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> サーバーリスニングポート. See this <a href="../../installation/using/email-deliverability.md#definition-of-the-server-port">section</a>.<br /> </td> 
   <td> 短い<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## syslogd {#syslogd}

次に、 syslogdノードの異なるパラメ **ータ** 。 これは、ログ管理モジュールの設定です。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxFileSizeMb<br /> </td> 
   <td> Maximum size in Mb for a log file. <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> maxNumberOfLoginsFiles<br /> </td> 
   <td> 保持する logins.log ファイルの最大数. <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 365<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## tracking {#tracking}

トラッキングノードの様々なパラメー **ター** 。 これは、トラッキングサーバーの設定です。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> consolidationPeriodSec<br /> </td> 
   <td> 統合期間<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> dedupOpenPeriodMin<br /> </td> 
   <td> Deduplicate openings: remove duplicate open tracking logs to limit the effects of mail previews in mail readers like Outlook.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePercent<br /> </td> 
   <td> Ignore up to X% of errors: do not update tracking indicators as long as the ratio of journals not already taken into account does not reach this value. <br /> </td> 
   <td> Byte<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePeriod<br /> </td> 
   <td> エラーインジケータの更新：エラーインジケーターが再計算されるまでの最大時間。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> indicatorsDuration<br /> </td> 
   <td> Compute indicators during: duration after the validity date of a delivery after which consolidated indicators are no longer computed.<br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> 長い<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePercent<br /> </td> 
   <td> Ignore up to X% of tracking: do not update tracking indicators as long as the ratio of journals not already taken into account does not reach this value.<br /> </td> 
   <td> Byte<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePeriod<br /> </td> 
   <td> 追跡インジケーターの更新：追跡インジケーターが再計算されるまでの最大時間。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> userAgentCacheSize<br /> </td> 
   <td> ブラウザー識別子のキャッシュのサイズ<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## trackinglogd {#trackinglogd}

以下に、trackinglogdノードの様々なパラメー **タを示します** 。 これは、トラッキングログ書き込みデーモンの設定です。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxCreateFileRetry<br /> </td> 
   <td> Max writing retries: maximum number of files that can be created in case of writing failure in log files.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> maxLogsSizeOnDiskMb<br /> </td> 
   <td> 最大ログサイズ：ディスク上のログが使用する最大領域(MB)。 100 MB以上にする。 <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedLogs<br /> </td> 
   <td> 最大ログ数：共有メモリに格納されるログの最大数。 10000未満にすることはできません。 <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeLogsPeriod<br /> </td> 
   <td> パージ前のログ数：ログファイルのパージを開始する前に挿入されたログの数。 50,000以下にする。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 50000<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> webTrackingParamSize<br /> </td> 
   <td> 追加の Web トラッキングパラメーターの共有メモリに保存される最大文字数.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 64<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Web {#web}

Webノードの様々なパラメーターを次に **示します** 。 これはWebモジュールの設定です。

For additional information, refer to this [section](../../installation/using/configuring-campaign-server.md#default-port-for-tomcat).

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
   <td> 長い<br /> </td> 
   <td> 75<br /> </td> 
  </tr> 
  <tr> 
   <td> MinSpareThreads<br /> </td> 
   <td> スレッドの最小数。<br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> controlPort<br /> </td> 
   <td> Tomcatリスニング制御ポート：「Tomcatの設定 <a href="../../installation/using/configuring-campaign-server.md#configuring-tomcat" target="_blank">」を参照</a>。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 8005<br /> </td> 
  </tr> 
  <tr> 
   <td> httpPort<br /> </td> 
   <td> Tomcat HTTPリスニングポート：「Tomcatの設定 <a href="../../installation/using/configuring-campaign-server.md#configuring-tomcat" target="_blank">」を参照</a>。<br /> </td> 
   <td> 短い<br /> </td> 
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
   <td> SubmitDelivery呼び出しのキューのサイズ：キューに格納できるSubmitDelivery SOAP呼び出しの最大数。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 50<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：HostName：通知のリレーを有効にするポート。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> startSoapRouterInModule<br /> </td> 
   <td> モジュールモードで SOAP ルーターを起動します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### jsp {#jsp}

web/jspノードの様々なパラ **メータを示します** 。 これは、JSPで使用されるパラメータの設定です。

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
   <td> Download folder: download path of installation programs for the client consoles.<br /> </td> 
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

Web > **jsp > classpathノードには** 、JVMの起動時に使用するすべてのクラスパスのリストが含まれます。 デフォルトの設定は次のとおりです。

```
'$(XTK_INSTALL_DIR)/tomcat-7/bin/bootstrap.jar
          $(XTK_INSTALL_DIR)/tomcat-7/bin/tomcat-juli.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/tomcat-coyote.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/tomcat-util.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/tomcat-api.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/servlet-api.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/jsp-api.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/el-api.jar
          $(XTK_INSTALL_DIR)/java/lib/log4j-1.2.11.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/annotations-api.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/catalina.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/websocket-api.jar
          $(XTK_INSTALL_DIR)/tomcat-7/lib/tomcat7-websocket.jar
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

web > jsspノードの様々なパ **ラメーターを示します** 。 これは、JSSPが使用するパラメーターの設定です。

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
   <td> Maximum number of pages served by a JavaScript context. <br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

Web > **jsp > classpathノードには** 、JVMの起動時に使用するすべてのクラスパスのリストが含まれます。

### relay {#relay-2}

web > relayノードの異なるパ **ラメータを示します** 。 これは、2つのゾーン間のHTTP要求のリレーの設定です。

For additional information, refer to this [section](../../installation/using/deploying-an-instance.md#synchronizing-public-resources).

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInAuthority<br /> </td> 
   <td> 禁止文字（ドメイン）:URIの「authority」セクションの禁止文字のリストです。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.?#@/:' <br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInPath<br /> </td> 
   <td> 禁止文字（パス）:URIの「パス」セクションの禁止文字のリストです。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '?#/'<br /> </td> 
  </tr> 
  <tr> 
   <td> modDir<br /> </td> 
   <td> 'mod_dir'モジュールオプションの値：フォルダーのクエリー中に使用するファイルのリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'index.md' <br /> </td> 
  </tr> 
  <tr> 
   <td> startRelay<br /> </td> 
   <td> HTTP リレーモジュールを開始.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> startRelayInModule<br /> </td> 
   <td> Start the HTTP relay module within the Web server. <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> 禁止された URL を削除するまでの待機時間です.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '60'<br /> </td> 
  </tr> 
 </tbody> 
</table>

中継する各URL **に対して、次のパラメーターを使用して、** web > relay > url nodeを追加します（挿入順序は優先順位を定義します）。

詳しくは、「動的ページのセキュリティ [とリレー」の節を参照し](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays) て [ください](../../installation/using/deploying-an-instance.md#synchronizing-public-resources)。

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
   <td> Authorized IPs: comma separated list of source IP addresses allowed to use the relay for this mask.<br /> </td> 
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
   <td> リレーするDNSエイリアス：中継するDNSエイリアスマスクのコンマ区切りリスト(例：'*.adobe.com')。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> httpAllowed<br /> </td> 
   <td> HTTP access authorized no matter what the security zone (like webApps). <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayHost<br /> </td> 
   <td> Add original host: use the HTTP 'Host' header of the original request when relaying.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayPath<br /> </td> 
   <td> Add initial URL path: append the complete path of the URLs to relay to the URL of the target page. <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ステータス<br /> </td> 
   <td> パブリックリソースの同期状態（列挙）。 使用可能な値は、「normal」（通常の実行）、「blacklist」（エラー404の場合はURLブラックリスト）、「spare」（既存の場合はスペアサーバでのファイルアップロード）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> normal<br /> </td> 
  </tr> 
  <tr> 
   <td> targetUrl<br /> </td> 
   <td> ターゲットページのURL:「Tomcatの設定 <a href="../../installation/using/configuring-campaign-server.md#configuring-tomcat" target="_blank">」を参照</a>。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> Maximum execution time (in seconds) of the request being relayed.<br /> </td> 
   <td> 長い<br /> </td> 
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

デフォルトの設定は次のとおりです。

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

各HTTPヘッ **ダーに対してWeb > relay > responseHeader** ノードを追加し、リレーに転送される応答に追加します。

詳しくは、「HTTPヘッダーの管理」を [参照してください](../../installation/using/configuring-campaign-server.md#managing-http-headers)。

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

デフォルトの設定は次のとおりです。

```
<responseHeader name="X-XSS-Protection" value="1; mode=block"/>
```

### redirection {#redirection}

web >リダイレクトノードの異なるパ **ラメーターを示します** 。 これはリダイレクトモジュールの構成です。

For additional information, refer to this [section](../../installation/using/deploying-an-instance.md#synchronizing-public-resources).

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
   <td> IMS organization identifier: unique organization identifier within the Adobe Marketing Cloud, used in particular for the VisitorID service and the IMS SSO. <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> P3PCompactPolicy<br /> </td> 
   <td> Value describing the policy used for permanent cookies (compliant with the P3P Compact Policy format). <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV'<br /> </td> 
  </tr> 
  <tr> 
   <td> cookieDomain<br /> </td> 
   <td> Comma separated list of domains to be configured to explicitly indicate your domain to set cookie. <br /> </td> 
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
   <td> 呼び出しによるログ数：メソッドGetTrackingLogsの呼び出し時にデフォルトで返されるログの数。<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> expirationURL<br /> </td> 
   <td> Page for expired redirections: URL of Web page used by default by the redirection server when redirection for a delivery action has expired.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxJobsInCache<br /> </td> 
   <td> 最大ジョブ数：キャッシュ内の配信アクションの最大数。 50以下にする必要があります。 <br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> Web tracking: creation of logs for the pages visited by unknown users. <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingPassword<br /> </td> 
   <td> リダイレクションサーバーが使用するパスワード.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

web > redirection > spareServerノードの異な **るパラメータを示します** 。

詳しくは、冗長トラッキングを参照 [してください](../../installation/using/configuring-campaign-server.md#redundant-tracking)。

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
   <td> 次の場合に考慮します。式がtrueを返す場合は、トラッキングサーバーが考慮されます。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> id<br /> </td> 
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

web/spamCheckノードの様々なパラ **メーターを示します** 。 これは、電子メールアンチスパムスコアリング評価パラメーターの設定です。

詳しくは、「スパムアサシンの設定」を [参照してください](../../installation/using/configuring-spamassassin.md)。

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
   <td> Command to execute to evaluate the anti-spam score of an email (e.g. 'perl spamcheck.pl').<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## wfserver {#wfserver}

wfserverノードの様々なパラメーターを次に **示します** 。 これは、ワークフロープロセスの設定です。

詳しくは、高可用性のワークフ [ローと親和性を参照してください](../../installation/using/configuring-campaign-server.md#high-availability-workflows-and-affinities)。

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataBasePoolPeriodSec<br /> </td> 
   <td> 期間<br /> </td> 
   <td> 長い<br /> </td> 
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
   <td> Memory consumption alert: alert concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> Memory consumption warning: warning concerning the amount of RAM consumed (in Mb) by a given process.<br /> </td> 
   <td> 長い<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：HostName：通知のリレーを有効にするポート。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間. 「自動プロ <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">セス再起動」を参照してくださ</a>い。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

