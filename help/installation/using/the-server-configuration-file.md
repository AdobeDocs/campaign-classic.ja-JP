---
product: campaign
title: サーバー設定ファイル
description: サーバー設定ファイル
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: appendices
exl-id: 70cd6a4b-c839-4bd9-b9a7-5a12e59c0cbf
source-git-commit: f032ed3bdc0b402c8281bc34e6cb29f3c575aaf9
workflow-type: tm+mt
source-wordcount: '8067'
ht-degree: 6%

---

# サーバー設定ファイル{#the-server-configuration-file}

Adobe Campaignの全体的な設定は、インストールディレクトリの **conf** ディレクトリにある **serverConf.xml** ファイルで定義されています。 この節では、**serverConf.xml** ファイルのすべてのノードとパラメーターを示します。

>[!NOTE]
>
>サーバーサイド設定は、Adobeがホストするデプロイメントに対してのみ、Adobeが実行できます。 様々なデプロイメントの詳細については、[ モデルのホスティング ](../../installation/using/hosting-models.md) の節または [ このページ ](../../installation/using/capability-matrix.md) を参照してください。 ホストモデルとハイブリッドモデルのインストールと設定の手順については、この [ 節 ](../../installation/using/hosting-models.md) を参照してください。

最初のパラメーターは **shared** ノード内にあります。 これらはインスタンスに関連しています。 すべての nlserver コマンド（nlserver web、nlserver wfserver など）で使用される可能性があります。 その他のセクションは、特定の nlserver サブコマンドに関連しています。

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
* [ooconv](#ooconv)
* [proxyConfig](#proxyconfig)
* [threadPool](#threadpool)
* [urlPermission](#urlpermission)
* [cusHeaders](#cusheaders)
* [xtkJobs](#xtkjobs)

**その他のパラメーター**

* [アーカイブ](#archiving)
* [inMail](#inmail)
* [interactiond](#interactiond)
* [MTA](#mta)
* [nmac](#nmac)
* [パイプライン化](#pipelined)
* [修理](#repair)
* [securityZone](#securityzone)
* [SMS](#sms)
* [統計](#stat)
* [syslogd](#syslogd)
* [tracking](#tracking)
* [trackinglogd](#trackinglogd)
* [Web](#web)
* [wfserver](#wfserver)

## 認証 {#authentication}

**authentication** ノードの様々なパラメーターを次に示します。

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
   <td> IP アドレスの確認を有効にします。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> defaultMode<br /> </td> 
   <td> デフォルトの識別モード。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nl'<br /> </td> 
  </tr> 
  <tr> 
   <td> longSessionTimeOutSec<br /> </td> 
   <td> 長いセッションのタイムアウト （秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1296000<br /> </td> 
  </tr> 
  <tr> 
   <td> securityTimeOutSec<br /> </td> 
   <td> セキュリティトークンのタイムアウト （秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionCacheSec<br /> </td> 
   <td> キャッシュ時間：セッション情報のキャッシュ （秒） <br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionTimeOutSec<br /> </td> 
   <td> セッションタイムアウト （秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
 </tbody> 
</table>

### XTK {#xtk}

**認証/XTK** ノードには、様々なパラメーターがあります。

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
   <td> 内部アカウントのパスワード。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> internalSecurityZone<br /> </td> 
   <td> 内部アカウントのセキュリティゾーン：内部アカウント用の承認済みゾーン。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'lan'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## dataStore {#datastore}

**dataStore** ノードの様々なパラメーターは次のとおりです。 サーバーデータソースは、ここで定義します。

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
   <td> エクスポートディレクトリ：書き出されたデータの宛先ディレクトリのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$（XTK_INSTALL_DIR）/var/$（INSTANCE_NAME）/export/' <br /> </td> 
  </tr> 
  <tr> 
   <td> extraSandboxedDirectories<br /> </td> 
   <td> 追加のサンドボックス化されたディレクトリ：サンドボックスに追加されるその他のパス（コンマ区切り）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/home/customers/,/sftp/' <br /> </td> 
  </tr> 
  <tr> 
   <td> formCacheTimeToLive<br /> </td> 
   <td> フォームキャッシュの有効期限の遅延：キャッシュエントリが無効になるまでのタイムアウト（秒単位）。 つまり、キャッシュエントリは公開時にのみ更新されます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> ホスト <br /> </td> 
   <td> DNS マスク：このインスタンスが提供する DNS マスクのリスト （コンマ区切り。*および？が使用可能） パターン）.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '*'<br /> </td> 
  </tr> 
  <tr> 
   <td> interactionCacheTimeToLive<br /> </td> 
   <td> インタラクション JSSP キャッシュの有効期限の遅延：キャッシュエントリが無効になるまでのタイムアウト （秒単位）。 負の値は、キャッシュが常に無効化されることを意味します。 「0」、空の値または無効な値は 60 と見なされます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> lang<br /> </td> 
   <td> インスタンス言語（列挙）。 使用できる値は、「fr_FR」（Français）、「en_GB」（English （UK））、「en_US」（English （US））、「de_DE」（Deutsch）、「ja_JP」（Japanese）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'en_US'<br /> </td> 
  </tr> 
  <tr> 
   <td> uploadDirectory<br /> </td> 
   <td> アップロードフォルダー：アップロードしたデータの保存先ディレクトリのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$（XTK_INSTALL_DIR）/var/$（INSTANCE_NAME）/upload/' <br /> </td> 
  </tr> 
  <tr> 
   <td> uploadAllowlist<br /> </td> 
   <td> ダウンロードを許可されたファイル （「,」区切り）。 文字列は、有効な Java 正規表現である必要があります。 <a href="file-res-management.md" target="_blank"> アップロード可能ファイルの制限 </a>.<br /> を参照してください。 </td> 
   <td> 文字列<br /> </td> 
   <td> 「。+」 <br /> </td> 
  </tr> 
  <tr> 
   <td> useVault<br /> </td> 
   <td> 秘密鍵を Vault に保存：Hashicorp Vault.<br /> を使用します </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultSecretPath<br /> </td> 
   <td> Vault の秘密鍵パス <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/v1/secret/campaign/'<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultTokenPath<br /> </td> 
   <td> Vault トークンを含むファイルのローカルパス。 $（HOME）はこのパスで使用できます（他の環境変数では使用できません）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$（HOME）/.vaulttoken'<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultUrl<br /> </td> 
   <td> Hashicorp Vault URL <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> viewCacheTimeToLive<br /> </td> 
   <td> ビューキャッシュの有効期間：キャッシュエントリが無効になるまでのタイムアウト （秒）。 負の値は、キャッシュが常に無効化されることを意味します。 「0」、空の値または無効な値は 60 と見なされます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> workingDirectory<br /> </td> 
   <td> 作業ディレクトリの XPath。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> workingDirectory：作業ディレクトリの XPath。 デフォルト：'$（XTK_INSTALL_DIR）/var/$（INSTANCE_NAME）/workspace/'<br /> </td> 
  </tr> 
 </tbody> 
</table>

### proxyAdjust {#proxyadjust}

**dataStore/proxyAdjust** ノードのパラメーターは様々です。 正規表現に一致する URL が、urlBase で定義された URL に基づいて再生成されます。

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
   <td> 外部 URL の生成時に使用するベース。 例：https://server.domain.com<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> urlRegEx<br /> </td> 
   <td> URL に一致する正規表現。 例：http://server\.lan\.net.*<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

### dataSource {#datasource}

**dataStore/dataSource** ノードの様々なパラメーターを次に示します。

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
   <td> 名前 <br /> </td> 
   <td> データSource名 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> デフォルト <br /> </td> 
  </tr> 
 </tbody> 
</table>

**dataStore/dataSource/dbcnx** ノードで、接続設定を指定します。

<table> 
 <thead> 
  <tr> 
   <th> パラメーター </th> 
   <th> 説明 </th> 
   <th> タイプ </th> 
   <th> デフォルト値 <br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> NChar<br /> </td> 
   <td> Unicode ストレージ <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> dbSchema<br /> </td> 
   <td> Workspace<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 暗号化 <br /> </td> 
   <td> 暗号化されたパスワード <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> ログイン <br /> </td> 
   <td> アカウント <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> パスワード <br /> </td> 
   <td> パスワード <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> プロバイダ <br /> </td> 
   <td> タイプ（列挙）。 'Oracle'、'MSSQL' （Microsoft SQL Server）、'PostgreSQL' （PostgreSQL）、'Teradata'、'MySQL'、'Netezza'、'AsterData'、'SAPHANA' （SAP HANA）、'RedShift' （Amazon Redshift）、'ODBC' （ODBC （Sybase ASE、Sybase IQ）、'リレー' （リモートデータベースへの HTTP リレー）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'Oracle'<br /> </td> 
  </tr> 
  <tr> 
   <td> サーバー <br /> </td> 
   <td> サーバー <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> タイムゾーン <br /> </td> 
   <td> タイムゾーン：<a href="../../installation/using/time-zone-management.md" target="_blank"> タイムゾーンの管理 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> unicodeData<br /> </td> 
   <td> データベースの Unicode データ <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> useTimestampTZ<br /> </td> 
   <td> タイムゾーンを含む日付フィールド：<a href="../../installation/using/time-zone-management.md" target="_blank"> タイムゾーンの管理 </a> を参照してください。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**dataStore/dataSource/sqlParams** ノードで、SQL パラメーターを設定します。

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
   <td> 関数のプレフィックス <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

**dataStore/dataSource/pool** ノードで、関連付けられた接続プールのパラメーターを設定します。

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
   <td> 接続の有効性チェック間の遅延。<br /> </td> 
   <td> 短い <br /> </td> 
  </tr> 
  <tr> 
   <td> freeCnx<br /> </td> 
   <td> プールに保持されている空き接続数。<br /> </td> 
   <td> 短い <br /> </td> 
  </tr> 
  <tr> 
   <td> maxCnx<br /> </td> 
   <td> 新しい接続を拒否する前に許可された最大接続数。 この <a href="https://helpx.adobe.com/campaign/kb/how-to-increase-the-maximum-number-of-database-connections-from-.html"> テクニカルノート </a> を参照してください <br />。 </td> 
   <td> 短い <br /> </td> 
  </tr> 
  <tr> 
   <td> maxIdleDelaySec<br /> </td> 
   <td> 接続の最大アイドル時間。 0 はデフォルト値を意味します。<br /> </td> 
   <td> 短い <br /> </td> 
  </tr> 
 </tbody> 
</table>

### virtualDir {#virtualdir}

**dataStore/virtualDir** ノードの様々なパラメーターを次に示します。 これは、仮想ディレクトリから実際のディレクトリへのマッピングの設定です。

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
   <td> 名前 <br /> </td> 
   <td> 仮想ディレクトリ <br /> の名前 </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> パス <br /> </td> 
   <td> 実際のディレクトリのフルパス <br /> </td> 
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

**dataStore/preprocessCommand** ノードの様々なパラメーターを次に示します。 「ファイルを読み込み」ワークフローアクティビティの前処理に使用できる承認済みコマンドです。

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
   <td> コマンド <br /> </td> 
   <td> コマンドライン <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ラベル <br /> </td> 
   <td> コマンドラインラベル <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> 名前 <br /> </td> 
   <td> コマンドライン名 <br /> </td> 
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

**dnsConfig** （DNS 設定）ノードの様々なパラメーターを次に示します。

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
   <td> ドメイン名：デフォルトのドメイン名です。 SMTP HELO コマンドで使用されます。 デフォルトでは、Windows で宣言されている最初のネットワークインターフェイスのネットワークパラメーターを使用します。または、Linux ではfile/etc/resolv.confを解析します（domain または search エントリ）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> nameServers<br /> </td> 
   <td> DNS サーバー：ドメインネームサーバー（DNS）のコンマ区切りリスト。 以下のメモを参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 再試行 <br /> </td> 
   <td> DNS クエリの再試行回数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト <br /> </td> 
   <td> DNS クエリのタイムアウト （ミリ秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 5000<br /> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>**nameSevers** に関する注意：デフォルトでは、ネットワークを使用します
>windows で宣言された最初のネットワーク インターフェイスのパラメーター
>UNIX では定義されていません。 ドメインネームサーバー（DNS）を定義します。
>のメール交換機を宣言するために MTA で使用されます
>ドメイン。
>
>この値が定義されていない場合、MTA はホスト ネットワーク構成でこの情報をシークします。 複数の DNS が使用可能な場合は、異なる DNS アドレスをコンマで区切る必要があります（例：212.155.207.1,212.155.207.2）。 配信サーバーに複数のネットワークインターフェイスがある場合は、MTA が使用する DNS リストが最初のインターフェイスです。 この場合は、曖昧さを避けるために **nameServer** パラメーターを指定することをお勧めします。

>[!CAUTION]
>
>ネットワーク ホスト構成で DHCP が使用されている場合、MTA は DHCP から提供された DNS リストを見つけることができません。 この場合、Windows コントロールパネルのネットワークパラメータで DNS リストを指定することをお勧めします。

## exec {#exec}

**exec** （コマンド実行）ノードの様々なパラメーターを次に示します。

詳しくは、[ 承認済みの外部コマンドの制限 ](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands) を参照してください。

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
   <td> 許可リストに追加するコマンドを含むファイルへのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ユーザー <br /> </td> 
   <td> 別のユーザーとしてコマンドを実行します。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## htmlToPdf {#htmltopdf}

**htmlToPdf** ノードの様々なパラメーターは次のとおりです。 これは、web ページをPDFドキュメントに変換するためのサービスの設定です。

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
   <td> コマンド <br /> </td> 
   <td> コンバージョンを（「その他」モードで）実行するためのコマンドライン。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessusCount<br /> </td> 
   <td> 最大1 台のマシンで一度に実行できるコンバージョンプロセスの数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> モード <br /> </td> 
   <td> 変換に使用するツール。 使用可能な値：phantomjs、wkhtmltopdf、other、disabled<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'phantomjs' <br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト <br /> </td> 
   <td> コンバージョンのタイムアウト：最大コンバージョン時間（秒）。 このしきい値を超えると、変換プロセスが停止し、エラーが発生します。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 120<br /> </td> 
  </tr> 
  <tr> 
   <td> 詳細 <br /> </td> 
   <td> 詳細モード：可能性のあるエラーを診断するために詳細モードで開始します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> waitTime<br /> </td> 
   <td> プロセス待機時の遅延：すべてのプロセスが同時に使用される場合と、プロセスの解放を待機している場合の秒単位の遅延。 この遅延を超えると、変換が停止され、エラーが発生します。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
 </tbody> 
</table>

phantomjs の例：

```
phantomjs - -ignore-ssl-errors=true '$(XTK_INSTALL_DIR)/bin/htmlToPdf.js' '-out:{outPdf}' '-post:{postFile}' '-url:{originUrl}' -sessiontoken:{sessiontoken} -format:{format} -orientation:{orientation} -marginTop:{marginTop} -marginLeft:{marginLeft} -marginRight:{marginRight} -marginBottom:{marginBottom}
```

## ims {#ims}

**ims** ノードの様々なパラメーターを次に示します。 これは、[IMS](../../integrations/using/about-adobe-id.md) を使用して別のサービスに接続する Campaign の設定です。

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
   <td> 秘密鍵（AES で暗号化） <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSCode<br /> </td> 
   <td> 認証コード （AES で暗号化） <br /> </td> 
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
   <td> テクニカルアカウント秘密鍵（AES で暗号化） <br /> </td> 
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
   <td> テクニカルアカウント秘密鍵（AES で暗号化） <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## JavaScript {#javascript}

**javaScript** ノードの様々なパラメーターを次に示します。 これは、JavaScript インタープリターの設定です。

詳しくは、[ レポートドキュメント ](../../reporting/using/actions-on-reports.md#memory-allocation) を参照してください。

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
   <td> ガベージコレクターを実行する前の最大サイズ （メガバイト）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 512<br /> </td> 
  </tr> 
  <tr> 
   <td> stackSizeKB<br /> </td> 
   <td> 各スタックチャンクのサイズ （キロオクテット単位）。 これは、ほとんどのユーザーが調整すべきでないメモリ管理の調整パラメーターです。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
 </tbody> 
</table>

## mailExchanger {#mailexchanger}

**mailExchanger** ノードのパラメーターは次のとおりです。 これは、SMTP サーバーの設定です。

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
   <td> SMTP サーバー：メール転送用の SMTP サーバーの IP アドレス。<br /> </td> 
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

**module** ノードの様々なパラメーターを次に示します。 これは、名前空間制限モジュール xtk の設定です。

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
   <td> 新しいエンティティの作成時に使用されるデフォルトの名前空間。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'cus'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 監視 {#monitoring}

**monitoring** ノードのパラメーターは次のとおりです。 これは監視サービスの設定です。

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
   <td> 最大準備時間：配信アクションが準備から外れるまでの時間（秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
  <tr> 
   <td> unixScript<br /> </td> 
   <td> 監視サービスによって実行される Unix スクリプト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> winScript<br /> </td> 
   <td> 監視サービスによって実行される Windows スクリプト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## ooconv {#ooconv}

**ooconv** ノードのパラメーターは次のとおりです。 これは、ドキュメント変換サーバーの設定です。

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
   <td> OpenOffice サーバーが実行できるコンバージョンの最大数。 この数を超えると、サーバーは再起動されます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxServerIdleSec<br /> </td> 
   <td> OpenOffice サーバーが強制終了するまでの最大アイドル時間です。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 7200<br /> </td> 
  </tr> 
  <tr> 
   <td> portRange<br /> </td> 
   <td> OpenOffice サーバーがリッスンしているポートの間隔。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 8101-8110<br /> </td> 
  </tr> 
  <tr> 
   <td> url<br /> </td> 
   <td> ドキュメント変換サーバーの URL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'http://localhost:8080/nl/jsp/ooconv.jsp'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## proxyConfig {#proxyconfig}

**proxyConfig** ノードのパラメーターは次のとおりです。 プロキシパラメーターの設定です。

詳しくは、[ プロキシ接続設定 ](file-res-management.md) を参照してください。

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
   <td> 有効 <br /> </td> 
   <td> プロキシサーバーを使用します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> オーバーライド <br /> </td> 
   <td> 例外：プロキシパラメーターを無視するアドレスのリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'localhost*' <br /> </td> 
  </tr> 
  <tr> 
   <td> useSingleProxy<br /> </td> 
   <td> 一意のプロキシサーバー：すべてのタイプのプロキシに同じ設定を使用します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### HTTP プロキシ/セキュアプロキシ {#http-proxy---secure-proxy-}

**proxyConfig/HTTP プロキシ/セキュアプロキシ** ノードで、次のパラメーターを設定します。

詳しくは、[ プロキシ接続設定 ](file-res-management.md) を参照してください。

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
   <td> 住所 <br /> </td> 
   <td> プロキシサーバーのアドレス <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ログイン <br /> </td> 
   <td> プロキシサーバーに接続するためのログイン <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> パスワード <br /> </td> 
   <td> プロキシサーバーへの接続用パスワード <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> プロキシサーバーポート <br /> </td> 
   <td> 短い <br /> </td> 
  </tr> 
 </tbody> 
</table>

## threadPool {#threadpool}

**threadPool** ノードの様々なパラメーターは次のとおりです。

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
   <td> プール内のスレッドの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## urlPermission {#urlpermission}

**urlPermission** ノードの様々なパラメーターを次に示します。 これは、JavaScript コードがアクセスできる URL のリストです。

Javascript コードで検出された URL がAdobe Campaign サーバーで使用できるか使用できないかを指定するドメインと正規表現のリスト。

URL が見つからない場合は、指定されたデフォルトモードに従って、デフォルトのアクションが実行されます。

詳細については、「[ 発信接続保護 ](../../installation/using/configuring-campaign-server.md#url-permissions)」を参照してください。

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
   <td> アクション <br /> </td> 
   <td> URL が許可リスト（列挙）に含まれていない場合のデフォルトのアクション。 取り得る値は、「ignore」（警告メッセージなしで許可する。これには保護の無効化が必要です）、「warn」（警告メッセージを許可して発行）、「deny」（URL へのアクセスを禁止）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 拒否 <br /> </td> 
  </tr> 
  <tr> 
   <td> debugTrace<br /> </td> 
   <td> URL 選択メカニズムのデバッグトレース：URL 検証プロセス中に追加のメッセージを発行します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

## cusHeaders {#cusheaders}

このノードを使用すると、外部サーバーからファイルをアップロードする際に実行されるリクエストに特定のヘッダーを追加できます。 コンテンツ配信ネットワーク（CND）は、要求者を信頼するために、特定のヘッダーを要求できます。 これらのヘッダーは、特に、配信実行手順で各受信者のパーソナライズされたドキュメントをダウンロードする際に、Campaign リクエストの信頼を向上するために使用できます。 多数のリソースダウンロードリクエストが DDos 攻撃と解釈される可能性があります。 dnsPattern を使用すると、ドメイン名に基づいて様々な CDN に特定のヘッダー名と値を設定できます。

```
  <!-- List of custom headers added to request. 
         -->
    <cusHeaders>

    <!-- Pattern of DNS name or domain 
         value :  dnsPattern: All or part of the URL's domain to verify, * is a wild card Default:  -->
      <dnsPattern value="">

    <!-- Header Name and Value 
           headerName :  Header Name 
           headerValue :  Header Value -->
        <headerDef headerName="" headerValue=""/>

      </dnsPattern>

    </cusHeaders> 
```

### URL {#url}

各 URL に対して、次のパラメーターを持つ **url** ノードを追加します。

詳細については、「[ 発信接続保護 ](../../installation/using/configuring-campaign-server.md#url-permissions)」を参照してください。

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
   <td> URL に関係するドメイン名またはドメインの親：検証を高速化するために、検証する URL のドメインのすべてまたは一部。 URL は、ドメインに dsnSuffix.<br /> が含まれている場合にのみ、正規表現に関して検証されます。 </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> urlRegEx<br /> </td> 
   <td> このドメインに属する URL の検証を絞り込むための正規表現：URL が dnsSuffix.<br /> に対応する場合に検証する必要がある正規表現 </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

レコードが **urlRegEx** ではなく **dnsSuffix** を満たす場合、次のレコードが調べられます。

例えば、ドメイン business.comのすべての URL へのアクセスを許可するには、次の 2 つのレコードを定義します。

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;http://.&#42;&quot;

かつ

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;https://.&#42;&quot;

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
<url dnsSuffix="localhost"                               urlRegEx="http://localhost:8080/nms/jsp/.*"              />
<url dnsSuffix="localhost"                               urlRegEx="http://localhost:8080/nl/jsp/.*"               />
<url dnsSuffix="localhost"                               urlRegEx="http://localhost:8080/xtk/jsp/.*"              />
```

## xtkJobs {#xtkjobs}

**xtkJobs** ノードの様々なパラメーターは次のとおりです。 これは、サーバージョブの設定です。

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
   <td> サーバー処理のメモリステータスの更新期間（ミリ秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## アーカイブ {#archiving}

**アーカイブ** ノードの様々なパラメーターを次に示します。 これは、バックグラウンドで実行されるアーカイブ操作の設定です。

詳しくは、[ メールアーカイブのアクティブ化（オンプレミス） ](../../installation/using/email-archiving.md#activating-email-archiving--on-premise-) を参照してください。

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
   <td> 同時に処理する EML の数 <br /> </td> 
   <td> 長い <br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> archivingType<br /> </td> 
   <td> 送信済みメッセージのアーカイブ方法（列挙）。 有効な値は、「0」（アーカイブなし）と「1」（送信済みメッセージのアーカイブを SMTP サーバーに転送）です。<br /> </td> 
   <td> バイト <br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> compressBatchSize<br /> </td> 
   <td> 圧縮されたアーカイブのサイズ：圧縮されたアーカイブの最大ファイル数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 10000<br /> </td> 
  </tr> 
  <tr> 
   <td> compressionFormat<br /> </td> 
   <td> アーカイブ時に使用される圧縮形式（列挙）。 有効な値は、「0」（圧縮なし）および「1」（zip 形式を使用して送信済みメッセージを圧縮）です。<br /> </td> 
   <td> バイト <br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> expirationDelay<br /> </td> 
   <td> 未処理の E メールが自動的にアーカイブされるまでの遅延時間：未処理の E メールがアーカイブされるまでの日数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollDelay<br /> </td> 
   <td> 各更新イベント間の遅延（秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeArchivesDelay<br /> </td> 
   <td> 未処理の E メールが削除されるまでの日数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 7<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpBccAddress<br /> </td> 
   <td> ターゲットのアーカイブ先 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> smtpEnableTLS<br /> </td> 
   <td> SMTPS サポートを有効化：リモートサーバーでサポートされる場合、セーフモードでメールの配信を有効化します（STARTTLS/SMTPS）。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpNbConnection<br /> </td> 
   <td> アーカイブ SMTP サーバーへの接続数。<br /> </td> 
   <td> 長い <br /> </td> 
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
   <td> 長い <br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## inMail {#inmail}

**inMail** ノードの様々なパラメーターを次に示します。 これは、受信メール管理モジュールの設定です。

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
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> checkInstanceName<br /> </td> 
   <td> インスタンス名を確認：true の場合、Message-ID ヘッダーに含まれるAdobe Campaign インスタンス名は現在のインスタンスと同じである必要があります。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> defaultForwardAddress<br /> </td> 
   <td> 転送アドレス：ルールによって処理されないデフォルトのメール転送アドレス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> errorForwardAddress<br /> </td> 
   <td> エラーのアドレス：無効なメール（不正な MIME エンコーディング）を転送するために使用するデフォルトのアドレスです。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ignoreSize<br /> </td> 
   <td> メッセージサイズを無視：POP3 サーバーから返されるメッセージのサイズを無視するために使用されます。 この場合、モジュールは「。」を想定します。 メッセージの最後に。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> inMailPeriodSec<br /> </td> 
   <td> メッセージ読み取り期間：メッセージキューのポーリング頻度。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxBroadLog<br /> </td> 
   <td> 更新するログの最大数：データベースを更新する前にメモリに保持するログメッセージの最大数を定義します。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 20<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMsgPerSession<br /> </td> 
   <td> POP3 セッション中に読み取るメッセージの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 200<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSessionTTLSec<br /> </td> 
   <td> セッション時間：メッセージ処理セッションの最大継続時間。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> popMailPeriodSec<br /> </td> 
   <td> POP3 ポーリング期間 <br /> </td> 
   <td> 長い <br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> popQueueSize<br /> </td> 
   <td> 読み取りメッセージのキューサイズ <br /> </td> 
   <td> 長い <br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> popTimeoutSec<br /> </td> 
   <td> POP3 サーバーとの通信タイムアウト。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriodSec<br /> </td> 
   <td> ポーリングするアカウントのデータベース再読み込み頻度。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

### msgDump {#msgdump}

**inMail / msgDump** ノードで、次のパラメーターを設定します。 これは、処理されたメッセージのダンプの設定です。

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
   <td> ダンプ <br /> </td> 
   <td> すべての受信メッセージをテキストフォーマットで保存します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> msgPath<br /> </td> 
   <td> メッセージダンプのパス <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/tmp/inMail'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## interactiond {#interactiond}

**interactiond** ノードの様々なパラメーターを次に示します。 これは、インバウンドインタラクションイベントの書き込みデーモンの設定です。

詳しくは、[ インタラクション – データバッファー ](../../installation/using/interaction-data-buffer.md) を参照してください。

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
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> callDataSize<br /> </td> 
   <td> 最大呼び出しデータの共有メモリに保存される文字数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedEntries<br /> </td> 
   <td> 最大共有メモリに保存されているイベントの数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> nextOffersSize<br /> </td> 
   <td> 提案直後に並べ替えられ、統計用に保存される適格オファーの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> statsPeriod<br /> </td> 
   <td> 応答時間統計の集計期間（秒）。 0 は、統計ストレージが非アクティブ化されたことを意味します。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> targetKeySize<br /> </td> 
   <td> 最大共有メモリに保存される、個人を識別するための文字数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 16<br /> </td> 
  </tr> 
 </tbody> 
</table>

## MTA {#mta}

**mta** ノードの様々なパラメーターは次のとおりです。 これは、配信エージェントの設定です。

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
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '-tracefilter:nlmta' <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataLogPath<br /> </td> 
   <td> 送信されたメールのパスを保存：空でない場合、送信済みメールのすべてのソースファイルが保存されるパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> debugPath<br /> </td> 
   <td> ディレクトリのダンプ：i 空でない場合は、このディレクトリに送信済みメールメッセージの MIME エンベロープをコピーします。 トラブルシューティングに使用します。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> dnsRequestLogDelayMs<br /> </td> 
   <td> DNS クエリログの遅延：ログを表示する時間（ミリ秒単位）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> errorPeriodSec<br /> </td> 
   <td> エラー統計の頻度：統計が生成されてからデータベースに保存されるまでの時間。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> logEmailErrors<br /> </td> 
   <td> エラー統計を生成してデータベースに保存します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> logLevel<br /> </td> 
   <td> ログメッセージのレベルを表示します。 データベースに書き込まれるログの重大度レベル。 MTA で生成されるログメッセージは、必ずしもすべてがデータベースに書き込まれるわけではありません。 このパラメーターを使用すると、メッセージをデータベースに書き込む必要があると考えるレベルを定義できます。 レベル 2 を定義した場合は、レベル 1 と 0 のメッセージも書き込まれます。一方、レベル 1 を定義した場合は、レベル 1 と 0 のメッセージのみが書き込まれます。 使用可能な値：0 （エラー）、1 （警告）、2 （情報） <br /> </td> 
   <td> 長い <br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMemoryMb<br /> </td> 
   <td> Mta プロセスが使用できる最大メモリサイズ （MB 単位）。 この制限を超えると、プロセスは再起動され、使用しているメモリはシステムに解放されます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> minConnectionsToLog<br /> </td> 
   <td> 考慮する接続しきい値。 errorPeriodSec で指定された期間の接続の合計数が厳密にはしきい値を下回る場合、指定されたパスのエラー統計は生成されません。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> minErrorsToLog<br /> </td> 
   <td> 考慮するエラーしきい値：errorPeriodSec で指定された期間のエラー総数がしきい値よりも厳密に低い場合、指定されたパスのエラー統計は生成されません。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> minMessagesToLog<br /> </td> 
   <td> 考慮するメッセージしきい値。 errorPeriodSec で指定された期間に送信されたメッセージの合計数が厳密にはしきい値を下回る場合、指定されたパスのエラー統計は生成されません。<br /> </td> 
   <td> 長い <br /> </td> 
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
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeDataLogDelay<br /> </td> 
   <td> アーカイブした E メールが削除されるまでの遅延：dataLogPath で指定したディレクトリにアーカイブした E メールがパージされるまでの日数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
  <tr> 
   <td> retryLostMessages<br /> </td> 
   <td> 失われたメッセージを再試行：子プロセスが無効になった場合、配信の一部が再試行されます。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> signEmailLinks<br /> </td> 
   <td> 署名メカニズムを有効にします。 これにより、メール内のトラッキングリンクのセキュリティが向上します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true<br /> </td> 
  </tr>
  <tr> 
   <td> statServerAddress<br /> </td> 
   <td> 配信統計サーバーのアドレス（指定は次のとおりです） 
    &lt;dns または ip&gt; 
      <code>&lbrack;</code>: 
     &lt;port&gt; 
       <code>&rbrack;</code>。 参照： 
      <a href="../../installation/using/email-deliverability.md#coordinates-of-the-statistics-server" target="_blank"> 統計サーバーの座標 </a>。 
      <br /> 
     </td> 
   <td> 文字列<br /> </td> 
   <td> 定義されていない場合、デフォルトのポートは 7777.<br /> です </td> 
  </tr> 
  <tr> 
   <td> statServerTLSSupport<br /> </td> 
   <td> ドメイン別に TLS を有効にする：MX ごとに設定可能な TLS を有効にします（最新の統計サーバーが必要です）。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true <br /> </td> 
  </tr> 
  <!--tr> 
   <td> statServerVersion<br /> </td> 
   <td> Protocol version used: communication protocol version (1 for a v5.11 and 6.0.2 server, 2 for a v6.1 server).<br /> </td> 
   <td> String<br /> </td> 
   <td> If undefined, the latest version is used. <br /> </td> 
  </tr--> 
  <tr> 
   <td> useMomentum<br /> </td> 
   <td> 「true」に設定した場合、インスタンスは <a href="../../delivery/using/sending-with-enhanced-mta.md" target="_blank">Enhanced MTA</a>.<br /> を使用しています </td> 
   <td> ブール値 <br /> </td> 
   <td> <br /> </td>b 
  </tr>
  <tr> 
   <td> verifyMode<br /> </td> 
   <td> 検証モード：検証モードを有効化します（メッセージを物理的に送信しません。シミュレーションおよびテストに使用します）。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> workingPath<br /> </td> 
   <td> 作業ディレクトリ：MTA が子プロセスと通信するために使用する一時ファイルの場所。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$（XTK_INSTALL_DIR）/var/$（INSTANCE_NAME）/mta/' <br /> </td> 
  </tr> 
  <tr> 
   <td> xMailer<br /> </td> 
   <td> X-Mailer フィールド：SMTP メールヘッダーの「X-Mailer」フィールドの値 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nlserver, ビルド $（PRODUCT_VERSION）'<br /> </td> 
  </tr>  
 </tbody> 
</table>

### キャッシュ {#cache}

**cache** ノードで、次のパラメーターを設定します。 これはローカルファイルキャッシュの設定です。

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
   <td> 次の期間でリサイクル：ストレージを再利用するためにキャッシュからファイルが自動的に削除される期間（秒単位）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 244800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSizeOnDiskMb<br /> </td> 
   <td> 最大キャッシュサイズ （Mb）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> purgePeriodSec<br /> </td> 
   <td> パージ頻度：キャッシュパージメカニズムの実行間隔（秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リレー {#relay}

**mta/リレー** ノードで、次のパラメーターを設定します。 これは、メッセージ配信用メールサーバーの設定です。

リストは、MX DNS クエリによって返される MX のリストと同じ方法で処理されます。通常、最初の MX が使用可能な限り使用され、次の MX が使用されます。

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
   <td> 住所 <br /> </td> 
   <td> 使用する SMTP リレーの DNS 名または IP アドレスのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> SMTP サーバーの IP ポート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

### master {#master}

**mta/master** ノードで、次のパラメーターを設定します。 これはメインサーバーの設定です。

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
   <td> databasePoolPeriodSec<br /> </td> 
   <td> 配信するジョブに対するデータベースポーリング頻度。 この値は、データベースのポーリング頻度（秒）を示します。配信待ちのジョブのリストを取得するために、MTA は定期的にデータベースをポーリングします。待機中のジョブがない場合、ポーリング期間はこの値によって定義されます。それ以外の場合、ジョブが子サーバーに転送された場合、このポーリング時間は自動的に 1 秒に短縮され、新しいジョブをできるだけ早く（例えば、子サーバーが再び使用可能になるとすぐに）再処理できるようになります。これは、子サーバーが再び使用可能になるまで、データベースクエリが 1 秒ごとに実行されるわけではありません。 実際、データベースアクセスは、少なくとも 1 つの子サーバーが使用可能になった場合にのみ実行されます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> databaseRetryDelaySec<br /> </td> 
   <td> データベース接続の失敗後の待機期間。 通常、データベース接続の失敗は、データベースサーバー自体が原因で発生します。サーバーは、メンテナンスなどの目的で停止する場合もあります。 DataBaseRetryDelay パラメーターは、データベース接続が失敗した場合に接続を再試行するまでの時間を定義します。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> domainKeysReloadPeriodSec<br /> </td> 
   <td> 秘密鍵のキャッシュの有効期間（DomainKeys）。 DomainKeys の推奨事項（http://antispam.yahoo.com/domainkeys）に従ったメールへの署名に使用される秘密鍵は、データベースにオプションとして保存されます。domainKeysReloadPeriodSec パラメーターは、MTA がこれらのキーをキャッシュに保持できる秒数を定義します。 この遅延の後は、すべてのキーをデータベースから再読み込みする必要があります。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSpareServers<br /> </td> 
   <td> 子サーバーの最大数。 実行されているサーバーの最大数を表します。この数は、サーバーのメモリリソースと互換性のある最適な値に制限することをお勧めします。配信中に確認できます。 使用されるメモリは、使用可能な物理メモリの 3 分の 1 以下にする必要があります。そうしないと、スワップが使用されます。 <a href="../../installation/using/configuring-campaign-server.md#mta-child-processes" target="_blank">MTA 子プロセス </a> を参照してください。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> minSpareServers<br /> </td> 
   <td> 子サーバーの最小数。 MTA は少なくともこの数のサーバーが実行され続けるようにします。 サーバー数が少ない場合は、この値に達するまで毎秒新しいサーバーを再起動します。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> startSpareServers<br /> </td> 
   <td> 起動時の子サーバーの数。 子サーバーの数は動的に監視されます。MTA が起動すると、この値で示されるとおりの数の子サーバーが作成されます。通常、ホストのリソースを節約するために、子サーバーを 1 秒あたり 1 サーバーよりも高速に起動することはできません。 ただし、MTA が起動すると、子サーバーができるだけ早く使用可能になるように、この制限が無効になります。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 子 {#child}

**mta /子** ノードで、次のパラメーターを設定します。 これは、子サーバーの設定です。

詳しくは、[ メール送信の最適化 ](../../installation/using/email-deliverability.md#email-sending-optimization) を参照してください。

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
   <td> アイドル状態の子サーバーが停止するまで中断。子サーバーのアイドル時間がこのパラメーターより大きい場合は、自動的に kill してホストリソースを解放します。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> maxAgeSec<br /> </td> 
   <td> 最大メッセージ保持時間。 準備されたメッセージがスロットルによって送信されなかった場合やターゲット MTA に接続できなかった場合、メッセージは破棄され、次の再試行で処理されます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxGCMConnectPerChild<br /> </td> 
   <td> 各子サーバーによって開始された FCM に対する並列 HTTP リクエストの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMsgPerChild<br /> </td> 
   <td> 子サーバーごとの最大メッセージ数。 各 MTA の子はこの数のメッセージを処理して終了します。MTA でのメモリまたはリソースリークが無害であるように数を指定することが重要です（通常は数千）。 MTA コードに既知のメモリリークがない場合でも、埋め込まれたJavaScriptおよび XSL エンジンは完全には信頼できません。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 5000000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWaitingMessages<br /> </td> 
   <td> 保留中のメッセージ：メモリ内で配信待ちのメッセージの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 2000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWorkingSetMb<br /> </td> 
   <td> 子プロセスが使用できる最大メモリサイズ （MB 単位）。 この制限を超えるとプロセスは停止し、使用しているメモリはシステムに解放されます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 128<br /> </td> 
  </tr> 
  <tr> 
   <td> soapConnectorTimeoutSec<br /> </td> 
   <td> 配信コネクタのSOAP接続が破棄されるまでのタイムアウト （秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> startWithFirstMX<br /> </td> 
   <td> 常に最優先 MX.<br /> で開始 </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> timeToLive<br /> </td> 
   <td> 再開時に連続して再試行する最大回数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 48<br /> </td> 
  </tr> 
 </tbody> 
</table>

**mta /子/ smtp** ノードで、次のパラメーターを設定します。 これは、SMTP セッションの設定です。

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
   <td> リモートサーバーでサポートされる場合、セーフモードで E メールの配信を有効化します（STARTTLS/SMTPS）。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> idleSessionTimeoutSec<br /> </td> 
   <td> アイドル セッション タイムアウト。 このパラメーターは、セッションが特定のドメインに複数のメッセージを送信するために再利用される場合にのみ使用されます。MTA がメッセージの送信を完了した後、使用した SMTP セッションが体系的に閉じられていません。メッセージを同じドメインに送信する準備ができている場合は、同じ SMTP セッションが再利用されるため、セッションが自動的に閉じません。IdleSessionTimeout パラメーターを使用すると、SMTP セッションが別のメッセージを待機しながらアクティブである期間を定義できます。 期間が経過すると、セッションは自動的に閉じられます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> initialDelaySec<br /> </td> 
   <td> 接続を再試行する前の初期遅延。 この遅延は、接続が失敗するたびに 2 倍になります。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSessionsPerChild<br /> </td> 
   <td> 子サーバーによる SMTP セッションの最大数。 メッセージを配信するために、MTA は受信者 MTA との SMTP 接続を初期化します。特定の子サーバーに対する同時およびアクティブな SMTP セッションの最大数は、この値によって制限されます。 この値に maxSpareServers を乗算すると、特定の子サーバーで同時に処理できるメッセージの最大数が取得されます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

**mta /子/ smtp / IPAffinity** ノードで、次のパラメーターを設定します。 これは、最適化された送信 SMTP トラフィックに対する IP アドレスとの親和性の管理の設定です。

詳しくは、[ 使用する IP アドレスのリスト ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use) および [ アフィニティを使用した送信 SMTP トラフィックの管理 ](../../installation/using/configuring-campaign-server.md#managing-outbound-smtp-traffic-with-affinities) を参照してください。

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
   <td> ドメイン名：IP アドレスにリンクされたローカルドメイン名。 SMTP HELO コマンドの発行時に使用されます。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> 名前 <br /> </td> 
   <td> 論理名：ユーザーによってアフィニティにリンクされた名前。 名前はセミコロンで区切ります。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

**mta /子/ smtp / IP** ノードで、次のパラメーターを設定します。

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
   <td> 住所 <br /> </td> 
   <td> 関連付けられた物理アドレス。 例：'192.168.0.1'<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> publicId<br /> </td> 
   <td> 関連付けられたパブリックアドレス ID。統計サーバーのキーとして使用します。 数値である必要があります。 詳しくは、<a href="../../installation/using/email-deliverability.md#managing-ip-addresses"> 節 </a> を参照してください <br />。 </td> 
   <td> 長い <br /> </td> 
  </tr> 
  <tr> 
   <td> 重み <br /> </td> 
   <td> この IP の使用頻度を他の IP に相対的に指定します（重みを大きくすると頻度が高くなります）。<br /> </td> 
   <td> 長い <br /> </td> 
  </tr> 
  <tr> 
   <td> includeDomains<br /> </td> 
   <td> 含めるドメインマスクのコンマ区切りのリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> excludeDomains<br /> </td> 
   <td> 除外するドメインマスクのコンマ区切りのリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> heloHost<br /> </td> 
   <td> IP アドレスにリンクされたコンピューター名。 SMTP HELO コマンドの発行時に使用されます。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## nmac {#nmac}

**nmac** ノードの様々なパラメーターを次に示します。 これは、プッシュ通知配信用のの設定です。

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
   <td> shared/proxyHTTP で定義された HTTP プロキシを使用します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リレー {#relay-1}

**nmac/relay** ノードの様々なパラメーターを次に示します。 メッセージ配信にリレーを使用するように設定します（ios http2 コネクタ）。

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
   <td> 住所 <br /> </td> 
   <td> 使用するリレーの DNS アドレスまたは名前。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> リレーポート <br /> </td> 
   <td> 長い <br /> </td> 
   <td> 443<br /> </td> 
  </tr> 
  <tr> 
   <td> trustedCertsChain<br /> </td> 
   <td> 証明書チェーン （PEM ファイル）。 モックサーバーを使用する場合に役立ちます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## パイプライン化 {#pipelined}

**pipelined** ノードの様々なパラメーターを次に示します。 これは、パイプラインサービスのイベント処理モジュールの設定です。

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
   <td> 公開鍵が保存されるときに Developer Connection で生成されるアプリケーションの名前。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authGatewayEndpoint<br /> </td> 
   <td> ゲートウェイトークンを取得する URL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://api.omniture.com' <br /> </td> 
  </tr> 
  <tr> 
   <td> authPrivateKey<br /> </td> 
   <td> トークンを取得するための秘密鍵（AES で XtkKey オプションを指定して暗号化）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> disableAuth<br /> </td> 
   <td> 認証を無効にする：認証なしでパイプラインサービスに接続します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> discoverPipelineEndpoint<br /> </td> 
   <td> パイプラインサービス URL を検出するための URL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://producer-pipeline-pnw.adobe.net'<br /> </td> 
  </tr> 
  <tr> 
   <td> dumpStatePeriodSec<br /> </td> 
   <td> ステータス保存期間：プロセスの内部情報がファイルに保存される頻度。 0 の場合は非アクティブ。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> forcedPipelineEndpoint<br /> </td> 
   <td> リスニング URL: パイプラインサービスのリスニング URL を強制的に使用します。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> monitorserverport<br /> </td> 
   <td> ステータスサーバーポート：プロセスのステータスのクエリが可能な HTTP サーバーポート。 0.<br /> の場合は非アクティブ </td> 
   <td> 長い <br /> </td> 
   <td> 7781<br /> </td> 
  </tr> 
  <tr> 
   <td> pointerFlushMessageCount<br /> </td> 
   <td> この数のメッセージが処理されるたびに、ポインターがデータベースに格納されます。<br /> </td> 
   <td> <br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> pointerFlushPeriodSec<br /> </td> 
   <td> ポインターを保存するまでの遅延時間：ポインターは、この期間中に 1 回以上データベースに保存されます（低アクティビティの場合に役立ちます）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> processingJSThreads<br /> </td> 
   <td> パーソナライズされたJavaScript コネクタによるイベント処理のスレッド数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> processingThreads<br /> </td> 
   <td> イベント処理用のスレッドの数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> retryPeriodSec<br /> </td> 
   <td> エラーが発生した場合の処理間の遅延。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> retryValiditySec<br /> </td> 
   <td> この期間の後に中断：この期間の後も処理が失敗する場合は、イベントを中断します。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 修理 {#repair}

**repair** ノードの様々なパラメーターは次のとおりです。 これは、データベース修復モジュールの構成です。

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
   <td> 配信アクション修復モジュール：修復モジュールで配信アクションを処理できるようになるまでの遅延（分）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
 </tbody> 
</table>

## securityZone {#securityzone}

**securityZone** ノードのパラメーターは次のとおりです。

詳細については、[ セキュリティ ゾーンの定義 ](../../installation/using/security-zones.md) を参照してください。

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
   <td> Web アプリケーションのデバッグ モードを承認します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowEmptyPassword<br /> </td> 
   <td> パスワードなしでアプリケーションを使用することをユーザーに許可します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowHTTP<br /> </td> 
   <td> オペレーターのログオンに HTTP を使用することを許可します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowSQLInjection<br /> </td> 
   <td> 式での SQLDATA の使用を承認します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowUserPassword<br /> </td> 
   <td> ユーザー/パスワードセッショントークンを許可。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> ラベル <br /> </td> 
   <td> ラベル <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewLabel （） <br /> </td> 
  </tr> 
  <tr> 
   <td> 名前 <br /> </td> 
   <td> 内部名 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> （） </td> 
  </tr> 
  <tr> 
   <td> sessionTokenOnly<br /> </td> 
   <td> セキュリティトークンは使用しないでください。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> showErrors<br /> </td> 
   <td> エラーの詳細を表示 <br /> </td> 
   <td> ブール値 <br /> </td> 
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

**securityZone/subNetwork** ノードのパラメーターは次のとおりです。

詳細については、[ セキュリティ ゾーンの定義 ](../../installation/using/security-zones.md) を参照してください。

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
   <td> ラベル <br /> </td> 
   <td> ラベル <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewLabel （） <br /> </td> 
  </tr> 
  <tr> 
   <td> マスク <br /> </td> 
   <td> マスクまたはアドレス <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 名前 <br /> </td> 
   <td> 内部名 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> （） </td> 
  </tr> 
  <tr> 
   <td> プロキシ <br /> </td> 
   <td> このサブネットワークでインスタンスへのアクセスに使用される（リバース） プロキシのマスクまたはアドレス。 この場合、「X-Forwarded-For」ヘッダーがこのプロキシの代わりにテストされます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 127.0.0.1 <br /> </td> 
  </tr> 
 </tbody> 
</table>

## SMS {#sms}

**sms** ノードの様々なパラメーターは次のとおりです。 これは、インバウンド SMS 管理モジュールの設定です。

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
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataRetentionDays<br /> </td> 
   <td> SMPP コネクタで保持される作業ファイルの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> dataSizeMo<br /> </td> 
   <td> SMPP 作業ファイルの最大サイズ （MB）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 512<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> keepAlivePeriod<br /> </td> 
   <td> セッション継続フレームの繰り返し：最大 受信セッションが引き続き有効であることを通知するための 2 つのフレーム間の期間（秒）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollPeriod<br /> </td> 
   <td> 検索頻度：SMS アカウントのポーリング期間。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriod<br /> </td> 
   <td> アカウント再読み込み頻度：ポーリングされるアカウントのデータベース再読み込み頻度です。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> srReadDelay<br /> </td> 
   <td> SR 処理の遅延秒数：現在の時間から srReadDelay で指定された期間（秒）を引いた日付より前の復元日を持つ SR のみ。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト <br /> </td> 
   <td> SMS ゲートウェイでの通信タイムアウト。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
 </tbody> 
</table>

### netsize {#netsize}

**sms/netsize** ノードの様々なパラメーターを次に示します。

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
   <td> Netsize.<br /> との接続を確立する場合のタイムアウト （秒） </td> 
   <td> 長い <br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 統計 {#stat}

**stat** ノードの様々なパラメーターを次に示します。 MTA 統計モジュールの設定です。

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
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> サーバーリスニングポート。 詳しくは、<a href="../../installation/using/email-deliverability.md#definition-of-the-server-port"> 節 </a> を参照してください <br />。 </td> 
   <td> 短い <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## syslogd {#syslogd}

**syslogd** ノードのパラメーターは次のとおりです。 これは、ログ管理モジュールの設定です。

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
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxFileSizeMb<br /> </td> 
   <td> ログファイルの最大サイズ（MB 単位）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> maxNumberOfLoginsFiles<br /> </td> 
   <td> 保持する logins.log ファイルの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 365<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## tracking {#tracking}

**トラッキング** ノードの様々なパラメーターを次に示します。 これは、トラッキングサーバーの設定です。

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
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> blockRedirectForUnsignedTrackingLink<br /> </td> 
   <td> 以前のビルドから生成された不正な形式の URL を無効にします。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> consolidationPeriodSec<br /> </td> 
   <td> 統合期間 <br /> </td> 
   <td> 長い <br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> dedupOpenPeriodMin<br /> </td> 
   <td> 開封の重複排除：重複した開封トラッキングログを削除して、Outlook などのメールリーダーでのメールプレビューの影響を制限します。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePercent<br /> </td> 
   <td> エラーの最大 X% を無視：まだ考慮に入れていないログの割合がこの値に達しない限り、トラッキング指標を更新しません。<br /> </td> 
   <td> バイト <br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePeriod<br /> </td> 
   <td> エラー指標の更新：エラー指標を再計算するまでの最大期間です。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> indicatorsDuration<br /> </td> 
   <td> 次の期間に指標を計算：配信の有効期限からの期間（それ以降、統合指標が計算されなくなる）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 2592000<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセス <br /> ークフローの開始時に実行するJavaScriptの ID </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> logcountPerRequest<br /> </td> 
   <td> リモートトラッキングサーバーへの呼び出しによってリクエストされたログの数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> phishbowlServiceAPIKey<br /> </td> 
   <td> Phishbowl サービスエンドポイント統合用の API キー。 これにより、古いビルドから生成された不正な形式の URL のリダイレクトが保護されます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> phishbowlServiceEndpoint<br /> </td> 
   <td> Phishbowl サービスエンドポイント統合のエンドポイント。 これにより、古いビルドから生成された不正な形式の URL のリダイレクトが保護されます。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePercent<br /> </td> 
   <td> 最大 X% のトラッキングを無視：まだ考慮に入れていないログの割合がこの値に達しない限り、トラッキング指標を更新しません。<br /> </td> 
   <td> バイト <br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePeriod<br /> </td> 
   <td> トラッキング指標を更新：トラッキング指標の再計算までの最大期間。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> userAgentCacheSize<br /> </td> 
   <td> ブラウザー識別子キャッシュのサイズ。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## trackinglogd {#trackinglogd}

**trackinglogd** ノードの様々なパラメーターは次のとおりです。 これは、トラッキングログ書き込みデーモンの設定です。

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
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセス <br /> ークフローの開始時に実行するJavaScriptの ID </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxCreateFileRetry<br /> </td> 
   <td> 最大書き込み再試行：ログファイルへの書き込みに失敗した場合に作成できるファイルの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> maxLogsSizeOnDiskMb<br /> </td> 
   <td> 最大ログサイズ：ディスク上のログに使用される最大領域（MB）。 100 MB 以上である必要があります。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedLogs<br /> </td> 
   <td> 最大ログ数：共有メモリに保存されるログの最大数。 10000 よりも小さい値にすることはできません。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeLogsPeriod<br /> </td> 
   <td> パージ前のログ数：ログファイルのパージを開始する前に挿入したログの数。 50000.<br /> よりも小さい値にすることはできません </td> 
   <td> 長い <br /> </td> 
   <td> 50000<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> webTrackingParamSize<br /> </td> 
   <td> 追加の Web トラッキングパラメーターの共有メモリに保存される最大文字数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 64<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Web {#web}

**web** ノードの様々なパラメーターは次のとおりです。 これは、web モジュールの設定です。

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
   <td> スレッドの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 75<br /> </td> 
  </tr> 
  <tr> 
   <td> MinSpareThreads<br /> </td> 
   <td> スレッドの最小数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> controlPort<br /> </td> 
   <td> Tomcat のリスニングコントロールポート：<a href="configure-tomcat.md" target="_blank">Tomcat の設定 </a> を参照してください。<br /> </td> 
   <td> 短い <br /> </td> 
   <td> 8005<br /> </td> 
  </tr> 
  <tr> 
   <td> httpPort<br /> </td> 
   <td> Tomcat HTTP リスニングポート：<a href="configure-tomcat.md" target="_blank">Tomcat の設定 </a> を参照してください。<br /> </td> 
   <td> 短い <br /> </td> 
   <td> 8080<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxdeliveryQueueSize<br /> </td> 
   <td> SubmitDelivery 呼び出し用のキューのサイズ：キューに格納できる SubmitDelivery SOAP呼び出しの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 50<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費警告：特定のプロセスが消費する RAM の量（MB）に関する警告 <br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：通知のリレーを有効にする HostName:Port。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> startSoapRouterInModule<br /> </td> 
   <td> モジュールモードでSOAP ルーターを起動します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### jsp {#jsp}

**web/jsp** ノードの様々なパラメーターを次に示します。 これは、JSP によって使用されるパラメーターの設定です。

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
   <td> デバッグ <br /> </td> 
   <td> デバッグモードで JSP を実行するかどうか。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> downloadPath<br /> </td> 
   <td> ダウンロードフォルダー：クライアントコンソールのインストールプログラムのダウンロードパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$（XTK_INSTALL_DIR）/datakit/nl/eng/jsp'<br /> </td> 
  </tr> 
  <tr> 
   <td> foFileName<br /> </td> 
   <td> .fo ファイルのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> soapRouter<br /> </td> 
   <td> SOAP ルーターの URL （http://myserver/xxx, http://jni or mailto:xxx）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'http://jni'<br /> </td> 
  </tr> 
 </tbody> 
</table>

**web/jsp/クラスパス** ノードには、JVM の起動時に使用するすべてのクラスパスのリストが含まれています。 デフォルトの設定は次のとおりです。

```
'$(XTK_INSTALL_DIR)/tomcat-X/bin/bootstrap.jar
          $(XTK_INSTALL_DIR)/tomcat-X/bin/tomcat-juli.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/tomcat-coyote.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/tomcat-util.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/tomcat-api.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/servlet-api.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/jsp-api.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/el-api.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/annotations-api.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/catalina.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/websocket-api.jar
          $(XTK_INSTALL_DIR)/tomcat-X/lib/tomcat7-websocket.jar
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

**web/jssp** ノードの様々なパラメーターを次に示します。 これは、JSSP が使用するパラメーターの設定です。

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
   <td> 各クエリの後でJavaScript コンテキストのガベージコレクターを有効にします。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> timeToLive<br /> </td> 
   <td> JavaScript コンテキストで提供されたページの最大数。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

**web/jsp/クラスパス** ノードには、JVM の起動時に使用するすべてのクラスパスのリストが含まれています。

### リレー {#relay-2}

**web/リレー** ノードの様々なパラメーターを次に示します。 これは、2 つのゾーン間の HTTP リクエスト用リレーの設定です。

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
   <td> Web サーバー内の HTTP リレーモジュールをデバッグモードで起動します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInAuthority<br /> </td> 
   <td> 禁止されている文字（ドメイン）: URI の「authority」セクションで禁止されている文字のリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.?#@/:' <br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInPath<br /> </td> 
   <td> 禁止文字（パス） : URI の「パス」セクションで禁止されている文字のリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '?#/'<br /> </td> 
  </tr> 
  <tr> 
   <td> modDir<br /> </td> 
   <td> 「mod_dir」モジュールオプションの値：フォルダーに対するクエリ中に使用されるファイルのリスト <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'index.md' <br /> </td> 
  </tr> 
  <tr> 
   <td> startRelay<br /> </td> 
   <td> HTTP リレーモジュールを開始します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> startRelayInModule<br /> </td> 
   <td> Web サーバー内で HTTP リレーモジュールを開始します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト <br /> </td> 
   <td> 禁止された URL を削除するまでの待機時間です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '60'<br /> </td> 
  </tr> 
 </tbody> 
</table>

次のパラメーターを使用して、リレーする URL ごとに **web/リレー/URL** ノードを追加します（挿入順で優先度を定義します）。

詳しくは、[ 動的ページセキュリティとリレー ](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays) および [ 節 ](../../installation/using/deploying-an-instance.md#synchronizing-public-resources) を参照してください。

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
   <td> 承認済み IP：このマスクのリレーを使用できるソース IP アドレスのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 拒否 <br /> </td> 
   <td> これらの URL へのアクセスを拒否します（HTTP 403 エラーを返します） <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> hostMask<br /> </td> 
   <td> リレーする DNS エイリアス：リレーする DNS エイリアスマスクのコンマ区切りリスト （例：'*.adobe.com'）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> httpAllowed<br /> </td> 
   <td> セキュリティゾーン （webApps など）に関係なく、HTTP アクセスが許可されました。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayHost<br /> </td> 
   <td> 元のホストを追加：リレー時に元のリクエストの HTTP 「ホスト」ヘッダーを使用します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayPath<br /> </td> 
   <td> 初期 URL パスを追加：中継する URL の完全パスをターゲットページの URL に追加します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ステータス <br /> </td> 
   <td> パブリックリソースの同期ステータス （列挙）。 ブロックリストに加える取り得る値は、'normal' （通常の実行）、'blacklist' （url added to case of error 404）、'spare' （file upload on spare server if existing）.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 標準 <br /> </td> 
  </tr> 
  <tr> 
   <td> targetUrl<br /> </td> 
   <td> ターゲットページの URL:<a href="configure-tomcat.md" target="_blank">Tomcat の設定 </a> を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト <br /> </td> 
   <td> リレーされているリクエストの最大実行時間（秒単位）。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> urlPath<br /> </td> 
   <td> 中継する URL のマスク （例：'/nl*', '*.jsp'）。<br /> </td> 
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

各 HTTP ヘッダーに **web/リレー/responseHeader** ノードを追加して、リレーに転送される返信に追加します。

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
   <td> 名前 <br /> </td> 
   <td> ヘッダー名 <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> 値 <br /> </td> 
   <td> ヘッダー値 <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルトの設定は次のとおりです。

```
<responseHeader name="X-XSS-Protection" value="1; mode=block"/>
```

### リダイレクト {#redirection}

**web/リダイレクト** ノードの様々なパラメーターを次に示します。 これは、リダイレクトモジュールの設定です。

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
   <td> 組織 ID:Adobe Experience Cloud内の組織の一意の識別子。特に VisitorID サービスと IMS SSO で使用されます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> P3PCompactPolicy<br /> </td> 
   <td> 永続 Cookie に使用されるポリシーを表す値（P3P Compact Policy 形式に準拠）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV'<br /> </td> 
  </tr> 
  <tr> 
   <td> cookieDomain<br /> </td> 
   <td> 設定するドメインのコンマ区切りのリストで、Cookie を設定するドメインを明示的に示します。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> databaseId<br /> </td> 
   <td> トラッキングインスタンスに関連付けられたデータベース識別子。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> defLogCount<br /> </td> 
   <td> 呼び出しによるログ数：メソッド GetTrackingLogs.<br /> の呼び出し時にデフォルトで返されるログの数 </td> 
   <td> 長い <br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> expirationURL<br /> </td> 
   <td> 期限切れリダイレクト用のページ：配信アクションのリダイレクトの有効期限が切れた場合にリダイレクトサーバーでデフォルトで使用される web ページの URL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxJobInCache<br /> </td> 
   <td> 最大ジョブ数：キャッシュ内の配信アクションの最大数。 50 以上である必要があります。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> showSourceIP<br /> </td> 
   <td> false に設定した場合、r/test から返される応答の sourceIP の値は空の文字列です。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> startRedirection<br /> </td> 
   <td> リダイレクトサービスを開始します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> startRedirectionInModule<br /> </td> 
   <td> モジュールモードでリダイレクトサービスを開始します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> trackWebVisitors<br /> </td> 
   <td> Web トラッキング：不明なユーザーが訪問したページのログを作成します。<br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingPassword<br /> </td> 
   <td> リダイレクトサーバーが使用するパスワード。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

**web/リダイレクト/spareServer** ノードのパラメーターは様々です。

詳しくは、[ 冗長トラッキング ](../../installation/using/configuring-campaign-server.md#redundant-tracking) を参照してください。

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
   <td> 考慮する条件：式が true を返した場合、トラッキングサーバーが考慮されます。<br /> </td> 
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

**web/spamCheck** ノードの様々なパラメーターを次に示します。 これは、E メールスパム対策のスコア付け評価パラメーターの設定です。

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
   <td> コマンド <br /> </td> 
   <td> E メールのスパム対策スコアを評価するために実行するコマンド （「perl spamcheck.pl」など）。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## wfserver {#wfserver}

**wfserver** ノードの様々なパラメーターを次に示します。 これは、ワークフロープロセスの設定です。

詳しくは、[ 高可用性ワークフローとアフィニティ ](../../installation/using/configuring-campaign-server.md#high-availability-workflows-and-affinities) を参照してください。

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
   <td> 親和性 <br /> </td> 
   <td> アフィニティ <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> スタートアップパラメーター <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 自動開始 <br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> ブール値 <br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> databasePoolPeriodSec<br /> </td> 
   <td> 期間 <br /> </td> 
   <td> 長い <br /> </td> 
   <td> 20<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptの ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスによる RAM の消費量（MB）に関するアラート。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費の警告：特定のプロセスが消費する RAM の量（MB）に関する警告。<br /> </td> 
   <td> 長い <br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：通知のリレーを有効にする HostName:Port。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> 処理が自動的に再度開始される時間。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"> プロセスの自動再起動 </a> を参照してください <br />。 </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先順位の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先順位は 0.<br /> でなければなりません </td> 
   <td> 短い <br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>
