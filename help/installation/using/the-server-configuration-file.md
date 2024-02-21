---
product: campaign
title: サーバー設定ファイル
description: サーバー設定ファイル
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: installation
content-type: reference
topic-tags: appendices
exl-id: 70cd6a4b-c839-4bd9-b9a7-5a12e59c0cbf
source-git-commit: 668cee663890fafe27f86f2afd3752f7e2ab347a
workflow-type: tm+mt
source-wordcount: '8075'
ht-degree: 6%

---

# サーバー設定ファイル{#the-server-configuration-file}



Adobe Campaignの全体的な設定は、 **serverConf.xml** ファイルの場所は、 **conf** インストールディレクトリのディレクトリ。 このセクションでは、 **serverConf.xml** ファイル。

>[!NOTE]
>
>サーバー側設定は、Adobeがホストするデプロイメントの場合、Adobeでのみ実行できます。 様々なデプロイメントについて詳しくは、 [ホスティングのモデル](../../installation/using/hosting-models.md) セクションまたは [このページ](../../installation/using/capability-matrix.md). ホストモデルおよびハイブリッドモデルのインストールおよび設定手順については、次のセクションで説明します [セクション](../../installation/using/hosting-models.md).

最初のパラメーターは、 **共有** ノード。 これらはインスタンスに関連しています。 これらは、すべての nlserver コマンド（nlserver web、nlserver wfserver など）で使用される可能性があります。 その他のセクションは、特定の nlserver サブコマンドに関連しています。

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
* [相互作用する](#interactiond)
* [MTA](#mta)
* [nmac](#nmac)
* [パイプラインの](#pipelined)
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

次に、 **認証** ノード：

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
   <td> Boolean<br /> </td> 
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
   <td> 長いセッションのタイムアウト（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1296000<br /> </td> 
  </tr> 
  <tr> 
   <td> securityTimeOutSec<br /> </td> 
   <td> セキュリティトークンのタイムアウト（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionCacheSec<br /> </td> 
   <td> キャッシュ時間：セッション情報のキャッシュ（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionTimeOutSec<br /> </td> 
   <td> セッションタイムアウト（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
 </tbody> 
</table>

### XTK {#xtk}

次に、 **認証 > XTK** ノード：

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
   <td> 内部アカウントのセキュリティゾーン：内部アカウントの認証済みゾーン。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'lan'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## dataStore {#datastore}

次に、 **dataStore** ノード。 サーバーのデータソースが定義される場所です。

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
   <td> Export directory：エクスポートされたデータの保存先ディレクトリのパス。<br /> </td> 
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
   <td> フォームキャッシュの有効期限の遅延：キャッシュエントリが無効になるまでのタイムアウト（秒）。 つまり、キャッシュエントリはパブリッシュ時にのみ更新されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> ホスト<br /> </td> 
   <td> DNS マスク：このインスタンスが提供する DNS マスクのリスト（コンマ区切り、*および？を使用可能） パターン )。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '*'<br /> </td> 
  </tr> 
  <tr> 
   <td> interactionCacheTimeToLive<br /> </td> 
   <td> インタラクション JSSP キャッシュの有効期限の遅延：キャッシュエントリが無効になるまでのタイムアウト（秒）。 負の値は、キャッシュが常に無効化されることを意味します。 「0」、空または無効な値は 60 と見なされます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> lang<br /> </td> 
   <td> インスタンスの言語（列挙）。 指定できる値は、「fr_FR」(Français)、「en_GB」( 英語 (UK))、「en_US」( 英語（米国）)、「de_DE」(Deutsch)、「ja_JP」（日本語）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'en_US'<br /> </td> 
  </tr> 
  <tr> 
   <td> uploadDirectory<br /> </td> 
   <td> アップロードフォルダー：アップロードされたデータの保存先ディレクトリのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/upload/' <br /> </td> 
  </tr> 
  <tr> 
   <td> uploadAllowlist<br /> </td> 
   <td> ダウンロードを許可されたファイル（「,」区切り）。 文字列は、有効な正規の Java 式である必要があります。 詳しくは、 <a href="file-res-management.md" target="_blank">アップロード可能なファイルの制限</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.+' <br /> </td> 
  </tr> 
  <tr> 
   <td> useVault<br /> </td> 
   <td> Vault に秘密鍵を保存する：Hashicorp Vault を使用します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultSecretPath<br /> </td> 
   <td> Vault 内の秘密パス<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/v1/secret/campaign/'<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultTokenPath<br /> </td> 
   <td> Vault トークンを含むファイルのローカルパス。 このパスでは$(HOME) を使用できます（他の環境変数は使用できません）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(HOME)/.vaulttoken'<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultUrl<br /> </td> 
   <td> Hashicorp Vault の URL <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> viewCacheTimeToLive<br /> </td> 
   <td> 表示キャッシュの有効期間：キャッシュエントリが無効になるまでのタイムアウト（秒）。 負の値は、キャッシュが常に無効化されることを意味します。 「0」、空または無効な値は 60 と見なされます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> workingDirectory<br /> </td> 
   <td> 作業ディレクトリの XPath。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> workingDirectory ：作業ディレクトリの XPath。 デフォルト： 「$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/workspace/」<br /> </td> 
  </tr> 
 </tbody> 
</table>

### proxyAdjust {#proxyadjust}

次に、 **dataStore > proxyAdjust** ノード。 正規表現に一致する URL は、urlBase で定義された URL に基づいて再生成されます。

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
   <td> 外部 URL の生成時に使用するベース。 例： https://server.domain.com<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> urlRegEx<br /> </td> 
   <td> URL に一致させる正規表現。 例： http://server\.lan\.net.*<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

### dataSource {#datasource}

次に、 **dataStore > dataSource** ノード。

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
   <td> 名前<br /> </td> 
   <td> データソース名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> デフォルト<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Analytics の **dataStore > dataSource > dbcnx** ノードで、接続設定を指定します。

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
   <td> Boolean<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> dbSchema<br /> </td> 
   <td> Workspace<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> 暗号化<br /> </td> 
   <td> 暗号化されたパスワード<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> ログイン<br /> </td> 
   <td> アカウント<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> パスワード<br /> </td> 
   <td> パスワード<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> プロバイダー<br /> </td> 
   <td> タイプ（列挙）。 指定できる値は、「Oracle」、「MSSQL」(Microsoft SQL Server)、「PostgreSQL」(PostgreSQL)、「Teradata」、「DB2」、「Netezza」、「AsterData」、「SAPHANA」(SAP HANA)、「RedShift」(Amazon Redshift)、ODBC です「 」(ODBC(Sybase ASE、Sybase IQ)、「リレー」（リモートデータベースへの HTTP リレー）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'ORACLE'<br /> </td> 
  </tr> 
  <tr> 
   <td> server<br /> </td> 
   <td> サーバー<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> timezone<br /> </td> 
   <td> タイムゾーン：詳しくは、 <a href="../../installation/using/time-zone-management.md" target="_blank">タイムゾーン管理</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> unicodeData<br /> </td> 
   <td> データベース内の Unicode データ<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> useTimestampTZ<br /> </td> 
   <td> タイムゾーンを持つ日付フィールド：詳しくは、 <a href="../../installation/using/time-zone-management.md" target="_blank">タイムゾーン管理</a>.<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Analytics の **dataStore > dataSource > sqlParams** ノードで、SQL パラメーターを設定します。

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

Adobe Analytics の **dataStore > dataSource > pool** ノードに、関連する接続プールのパラメータを構成します。

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
   <td> Short<br /> </td> 
  </tr> 
  <tr> 
   <td> freeCnx<br /> </td> 
   <td> プールに保持されている空き接続の数。<br /> </td> 
   <td> Short<br /> </td> 
  </tr> 
  <tr> 
   <td> maxCnx<br /> </td> 
   <td> 新しい接続を拒否する前に許可される接続の最大数。 詳しくは、 <a href="https://helpx.adobe.com/campaign/kb/how-to-increase-the-maximum-number-of-database-connections-from-.html">技術者</a>.<br /> </td> 
   <td> Short<br /> </td> 
  </tr> 
  <tr> 
   <td> maxIdleDelaySec<br /> </td> 
   <td> 接続の最大アイドル時間。 0 はデフォルト値を意味します。<br /> </td> 
   <td> Short<br /> </td> 
  </tr> 
 </tbody> 
</table>

### virtualDir {#virtualdir}

次に、 **dataStore > virtualDir** ノード。 これは、仮想ディレクトリと実ディレクトリのマッピングの設定です。

詳しくは、 [パブリックリソースの管理](file-res-management.md).

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
   <td> 名前<br /> </td> 
   <td> 仮想ディレクトリの名前 <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> パス<br /> </td> 
   <td> 実際のディレクトリのフルパス<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

次にデフォルトの設定を示します。

```
<virtualDir name="images" path="$(XTK_INSTALL_DIR)/var/res/img/"/>
<virtualDir name="formCache" path="$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/formCache/"/>
<virtualDir name="publicFileRes" path="$(XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)"/>
```

### preprocessCommand {#preprocesscommand}

次に、 **dataStore > preprocessCommand** ノード。 これらは、「ファイル読み込み」ワークフローアクティビティの前処理に許可されたコマンドです。

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
   <td> ラベル<br /> </td> 
   <td> コマンドラインラベル<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> 名前<br /> </td> 
   <td> コマンドライン名<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

次にデフォルトの設定を示します。

```
<preprocessCommand command="" label="None" name="none"/>
<preprocessCommand command="zcat &quot;$fileName&quot;" label="Decompression" name="zcat"/><preprocessCommand command="gpg --decrypt &quot;$fileName&quot;" label="Decrypt" name="gpg"/>
```

## dnsConfig {#dnsconfig}

次に、 **dnsConfig** （DNS 設定）ノード。

詳しくは、 [セクション](../../installation/using/configuring-campaign-server.md).

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
   <td> ドメイン名：デフォルトのドメイン名。 SMTP HELO コマンドで使用されます。 デフォルトでは、は Windows で宣言された最初のネットワークインターフェイスのネットワークパラメーターを使用するか、Linux のfile/etc/resolv.conf （ドメインまたは検索エントリ）を解析します。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> nameServers<br /> </td> 
   <td> DNS サーバー：ドメインネームサーバー (DNS) のコンマ区切りリスト。 以下のメモを参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 再試行<br /> </td> 
   <td> DNS クエリの再試行回数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> DNS クエリのタイムアウト（ミリ秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5000<br /> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>メモ： **nameSevers**：デフォルトでは、はネットワークを使用します
>Windows で宣言された最初のネットワークインターフェイスのパラメーター
>UNIX では定義されていません。 ドメインネームサーバー (DNS) を定義します
>MTA が、次の用に宣言されたメールエクスチェンジャを取得するために使用
>1 つのドメイン。
>
>この値を定義しない場合、MTA はホストネットワーク設定でこの情報を探します。 複数の DNS が可能な場合は、異なる DNS アドレスをコンマで区切る必要があります（例： 212.155.207.1,212.155.207.2）。 配信サーバーに複数のネットワークインターフェイスがある場合、MTA が使用する DNS リストが最初のものになります。 この場合、 **nameServer** パラメーターを使用して、曖昧さを回避します。

>[!CAUTION]
>
>ネットワークホストの設定で DHCP を使用している場合、MTA は DHCP から提供される DNS リストを見つけられません。 この場合、Windows コントロールパネルのネットワークパラメーターで DNS リストを指定することをお勧めします。

## exec {#exec}

次に、 **exec** （コマンド実行）ノードに設定します。

詳しくは、 [許可された外部コマンドの制限](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands).

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
   <td> に追加するコマンドを含むファイルのパ許可リストに加えるス。 <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ユーザー<br /> </td> 
   <td> 別のユーザーとしてコマンドを実行します。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## htmlToPdf {#htmltopdf}

次に、 **htmlToPdf** ノード。 これは、Web ページを変換ドキュメントに変換するサービスのPDFです。

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
   <td> （「その他」モードで）変換を実行するためのコマンドライン。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessusCount<br /> </td> 
   <td> 最大1 台のマシン上で一度に許可されるコンバージョンプロセスの数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> mode<br /> </td> 
   <td> 変換に使用するツール。 使用可能な値は、phantomjs、wkhtmltopdf、other、disabled です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'phantomjs' <br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> 変換のタイムアウト：最大変換時間（秒）。 このしきい値を超えると、変換プロセスが停止し、エラーが発生します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 120<br /> </td> 
  </tr> 
  <tr> 
   <td> verbove<br /> </td> 
   <td> 詳細モード：可能性のあるエラーを診断するために、詳細モードで開始します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> waitTime<br /> </td> 
   <td> プロセス待機時の遅延：すべてのプロセスが同時に使用されたとき、およびプロセスが解放されるのを待っているときの遅延（秒単位）。 この遅延を超えると、変換が停止し、エラーが発生します。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
 </tbody> 
</table>

phantomjs の例：

```
phantomjs - -ignore-ssl-errors=true '$(XTK_INSTALL_DIR)/bin/htmlToPdf.js' '-out:{outPdf}' '-post:{postFile}' '-url:{originUrl}' -sessiontoken:{sessiontoken} -format:{format} -orientation:{orientation} -marginTop:{marginTop} -marginLeft:{marginLeft} -marginRight:{marginRight} -marginBottom:{marginBottom}
```

## ims {#ims}

次に、 **ims** ノード。 これは、次を使用して別のサービスに接続する Campaign の設定です。 [IMS](../../integrations/using/about-adobe-id.md).

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
   <td> 秘密鍵（AES で暗号化）<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSCode<br /> </td> 
   <td> 認証コード（AES で暗号化）<br /> </td> 
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
   <td> テクニカルアカウント秘密鍵（AES で暗号化）<br /> </td> 
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
   <td> テクニカルアカウント秘密鍵（AES で暗号化）<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## JavaScript {#javascript}

次に、 **javaScript** ノード。 これは JavaScript インタープリターの設定です。

詳しくは、 [レポートドキュメント](../../reporting/using/actions-on-reports.md#memory-allocation).

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
   <td> ガベージコレクターを実行する前の最大サイズ (MB)。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 512 <br /> </td> 
  </tr> 
  <tr> 
   <td> stackSizeKB<br /> </td> 
   <td> 各スタックチャンクのサイズ（キロオクテット）。 これは、ほとんどのユーザが調整すべきでないメモリ管理チューニングパラメータです。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
 </tbody> 
</table>

## mailExchanger {#mailexchanger}

次に、 **mailExchanger** ノード。 これは SMTP サーバーの設定です。

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
   <td> SMTP server:E メール転送用の SMTP サーバーの IP アドレス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> mxPort<br /> </td> 
   <td> E メール転送に使用する SMTP サーバーの TCP ポート。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## モジュール {#module}

次に、 **モジュール** ノード。 これは、名前空間制限モジュール xtk の設定です。

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

次に、 **監視** ノード。 これは、監視サービスの設定です。

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
   <td> 最大準備時間：配信アクションを準備中でなくなるまでの時間（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
  <tr> 
   <td> unixScript<br /> </td> 
   <td> 監視サービスによって実行される UNIX スクリプト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> winScript<br /> </td> 
   <td> 監視サービスで実行される Windows スクリプト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## ooconv {#ooconv}

次に、 **ooconv** ノード。 これは、ドキュメント変換サーバーの設定です。

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
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxServerIdleSec<br /> </td> 
   <td> 強制終了前の OpenOffice サーバーの最大アイドル時間。<br /> </td> 
   <td> Long<br /> </td> 
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

次に、 **proxyConfig** ノード。 これはプロキシパラメーターの設定です。

詳しくは、 [プロキシ接続の設定](file-res-management.md).

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
   <td> プロキシサーバーを使用します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> 上書き<br /> </td> 
   <td> 例外：プロキシパラメーターを無視するアドレスのリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 「localhost*」 <br /> </td> 
  </tr> 
  <tr> 
   <td> useSingleProxy<br /> </td> 
   <td> 一意のプロキシサーバー：すべてのタイプのプロキシに同じ設定を使用します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### HTTP プロキシ/セキュアプロキシ {#http-proxy---secure-proxy-}

Adobe Analytics の **proxyConfig > HTTP Proxy / Secure proxy** ノードで、次のパラメーターを設定します。

詳しくは、 [プロキシ接続の設定](file-res-management.md).

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
   <td> 住所<br /> </td> 
   <td> プロキシサーバーのアドレス<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ログイン<br /> </td> 
   <td> プロキシサーバーへの接続にログインします<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> パスワード<br /> </td> 
   <td> プロキシサーバーとの接続用のパスワード<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> プロキシサーバーポート<br /> </td> 
   <td> Short<br /> </td> 
  </tr> 
 </tbody> 
</table>

## threadPool {#threadpool}

次に、 **threadPool** ノード。

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
   <td> プール内のスレッドの最大数。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## urlPermission {#urlpermission}

次に、 **urlPermission** ノード。 これは、JavaScript コードがアクセスできる URL のリストです。

JavaScript コードで検出された URL をAdobe Campaignサーバーで使用できるかどうかを指定するドメインと正規表現のリストです。

URL が見つからない場合は、指定されたデフォルトのモードに従って、デフォルトのアクションが実行されます。

詳しくは、 [発信接続の保護](../../installation/using/configuring-campaign-server.md#url-permissions).

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
   <td> アクション<br /> </td> 
   <td> URL が許可リスト（列挙）にない場合のデフォルトのアクション。 値には、「無視」（警告メッセージなしで許可、保護の無効化が必要）、「警告」（許可して警告メッセージを発行）、「拒否」（URL へのアクセスを禁止）があります。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 拒否<br /> </td> 
  </tr> 
  <tr> 
   <td> debugTrace<br /> </td> 
   <td> URL 選択メカニズムのデバッグトレース：URL 検証プロセス中に追加のメッセージを発行します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

## cusHeaders {#cusheaders}

このノードを使用すると、外部サーバーからファイルをアップロードする際に実行されるリクエストに、特定のヘッダーを追加できます。 コンテンツ配信ネットワーク (CND) は、リクエスターを信頼するために特定のヘッダーを要求できます。 これらのヘッダーを使用すると、特に、配信の実行手順で各受信者にパーソナライズされたドキュメントをダウンロードする際に、Campaign の要求に対する信頼性を高めることができます。 リソースのダウンロードリクエストが多数ある場合、DDos 攻撃と解釈できます。 dnsPattern を使用すると、ドメイン名に基づいて様々な CDN に特定のヘッダー名と値を設定できます。

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

URL ごとに、 **url** ノードに次のパラメーターを追加します。

詳しくは、 [発信接続の保護](../../installation/using/configuring-campaign-server.md#url-permissions).

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
   <td> URL に関係するドメイン名またはドメインの親。検証する URL のドメインのすべてまたは一部。検証を高速化するために使用されます。 URL のドメインに dsnSuffix が含まれている場合にのみ、URL が正規表現に関して検証されます。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> urlRegEx<br /> </td> 
   <td> このドメインに属する URL の検証を絞り込むための正規表現：URL が dnsSuffix に対応する場合は、URL が検証する必要がある正規表現。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

レコードが満たす場合 **dnsSuffix** しかし、 **urlRegEx**&#x200B;に続く記録を調べた。

例えば、business.comドメインのすべての URL へのアクセスを承認するには、2 つのレコードを定義します。

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;http://.&#42;&quot;

かつ

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;https://.&#42;&quot;

次にデフォルトの設定を示します。

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

次に、 **xtkJobs** ノード。 これは、サーバージョブの設定です。

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
   <td> サーバー処理のメモリステータス更新期間（ミリ秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## アーカイブ {#archiving}

次に、 **アーカイブ** ノード。 これは、バックグラウンドで実行されたアーカイブ操作の設定です。

詳しくは、 [電子メールアーカイブのアクティブ化（オンプレミス）](../../installation/using/email-archiving.md#activating-email-archiving--on-premise-).

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
   <td> Long<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> archivingType<br /> </td> 
   <td> 送信済みメッセージのアーカイブ方法（列挙）。 可能な値は、「0」（アーカイブなし）と「1」（送信されたメッセージのアーカイブを SMTP サーバーに転送）です。<br /> </td> 
   <td> Byte<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> compressBatchSize<br /> </td> 
   <td> 圧縮アーカイブのサイズ：圧縮アーカイブ内の最大ファイル数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 10000<br /> </td> 
  </tr> 
  <tr> 
   <td> compressionFormat<br /> </td> 
   <td> アーカイブ中に使用される圧縮形式（列挙）。 指定できる値は、「0」（圧縮なし）と「1」（送信されたメッセージを zip 形式で圧縮）です。<br /> </td> 
   <td> Byte<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> expirationDelay<br /> </td> 
   <td> 未処理の E メールが自動アーカイブされるまでの遅延：未処理の E メールがアーカイブされるまでの日数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollDelay<br /> </td> 
   <td> 各更新イベント間の遅延（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeArchivesDelay<br /> </td> 
   <td> 未処理の E メールが削除されるまでの日数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 7<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpBccAddress<br /> </td> 
   <td> ターゲット宛先のアーカイブ<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> smtpEnableTLS<br /> </td> 
   <td> SMTPS サポートを有効化：リモートサーバーでサポートされている場合に、セーフモード (STARTTLS/SMTPS) での E メールの配信を有効化します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpNbConnection<br /> </td> 
   <td> アーカイブ SMTP サーバーへの接続数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpRelayAddress<br /> </td> 
   <td> 使用する SMTP リレーの DNS 名または IP アドレスのコンマ区切りリスト。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> smtpRelayPort<br /> </td> 
   <td> SMTP サーバーの IP ポート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## inMail {#inmail}

次に、 **inMail** ノード。 これは、インバウンド E メール管理モジュールの設定です。

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
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> checkInstanceName<br /> </td> 
   <td> インスタンス名の検証： true の場合、Message-ID ヘッダーに含まれるAdobe Campaignインスタンスの名前は、現在のインスタンスと同じである必要があります。 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> defaultForwardAddress<br /> </td> 
   <td> 転送アドレス：ルールで処理されないデフォルトの E メール転送アドレスです。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> errorForwardAddress<br /> </td> 
   <td> エラーのアドレス：無効な E メール（無効な MIME エンコーディング）の転送に使用されるデフォルトのアドレス。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ignoreSize<br /> </td> 
   <td> 無視メッセージサイズ：POP3 サーバーから返されるメッセージのサイズを無視する場合に使用します。 この場合、モジュールは「。」を想定しています。 を送信します。 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> inMailPeriodSec<br /> </td> 
   <td> メッセージ読み取り期間：メッセージキューのポーリング頻度。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxBroadLog<br /> </td> 
   <td> 更新するログの最大数：データベースを更新する前にメモリに保持するログメッセージの最大数を定義します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 20<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMsgPerSession<br /> </td> 
   <td> POP3 セッション中に読み取るメッセージの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 200<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSessionTTLSec<br /> </td> 
   <td> セッション時間：メッセージ処理セッションの最大時間。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> popMailPeriodSec<br /> </td> 
   <td> POP3 ポーリング期間<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> popQueueSize<br /> </td> 
   <td> 読み取りメッセージのキューサイズ<br /> </td> 
   <td> Long<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> popTimeoutSec<br /> </td> 
   <td> POP3 サーバーとの通信タイムアウト。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriodSec<br /> </td> 
   <td> ポーリングするアカウントのデータベース再読み込み頻度。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

### msgDump {#msgdump}

Adobe Analytics の **inMail > msgDump** ノードで、次のパラメーターを設定します。 これは、処理されたメッセージのダンプの設定です。

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
   <td> すべての受信メッセージをテキスト形式で保存します。 <br /> </td> 
   <td> Boolean<br /> </td> 
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

## 相互作用する {#interactiond}

次に、 **相互作用する** ノード。 これは、インバウンドインタラクションイベントの書き込みデーモンの設定です。

詳しくは、 [インタラクション — データバッファ](../../installation/using/interaction-data-buffer.md).

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
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> callDataSize<br /> </td> 
   <td> 最大呼び出しデータ用に共有メモリに保存される文字数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedEntries<br /> </td> 
   <td> 最大共有メモリに保存されるイベントの数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> nextOffersSize<br /> </td> 
   <td> 提案直後に並べ替えられ、統計用に保存される適格なオファーの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> statsPeriod<br /> </td> 
   <td> 応答時間統計の集計期間（秒）。 0 は、統計の保存が無効化されたことを意味します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> targetKeySize<br /> </td> 
   <td> 最大個人を識別するために共有メモリに保存される文字の数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 16<br /> </td> 
  </tr> 
 </tbody> 
</table>

## MTA {#mta}

次に、 **mta** ノード。 これは、配信エージェントの設定です。

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
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '-tracefilter:nlmta' <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataLogPath<br /> </td> 
   <td> 送信済み電子メールのパス：空でない場合、送信済み電子メールのすべてのソースファイルが保存されるパス。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> debugPath<br /> </td> 
   <td> ダンプディレクトリ：空でない場合は、このディレクトリに送信メールメッセージの MIME エンベロープをコピーします。 トラブルシューティングに使用されます。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> dnsRequestLogDelayMs<br /> </td> 
   <td> DNS クエリログの遅延：ログを表示する時間（ミリ秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> errorPeriodSec<br /> </td> 
   <td> エラー統計頻度：統計の生成からデータベースのストレージまでの時間。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> logEmailErrors<br /> </td> 
   <td> エラー統計を生成し、データベースに保存します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> logLevel<br /> </td> 
   <td> ログメッセージのレベルを表示します。 データベースに書き込まれたログの重大度レベル。 MTA で生成されるログメッセージは、必ずしもデータベースに書き込まれるわけではありません。 このパラメーターを使用して、メッセージをデータベースに書き込む必要があると考えるレベルを定義できます。 レベル 2 を定義すると、レベル 1 と 0 のメッセージも書き込まれ、レベル 1 を定義すると、レベル 1 と 0 のメッセージのみが書き込まれます。 値は 0（エラー）、1（警告）、2（情報）です。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMemoryMb<br /> </td> 
   <td> MTA プロセスが使用できる最大メモリサイズ（MB 単位）。 この制限を超えると、プロセスは再起動され、使用するメモリがシステムに解放されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> minConnectionsToLog<br /> </td> 
   <td> 考慮する接続しきい値。 errorPeriodSec で指定された期間の接続の総数がしきい値より厳密に低い場合、指定されたパスに対するエラー統計は生成されません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> minErrorsToLog<br /> </td> 
   <td> 考慮するエラーしきい値：errorPeriodSec で指定された期間のエラーの合計数がしきい値より厳密に低い場合、指定されたパスに対してエラー統計は生成されません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> minMessagesToLog<br /> </td> 
   <td> 考慮するメッセージのしきい値。 errorPeriodSec で指定された期間に送信されたメッセージの総数がしきい値より厳密に低い場合、指定されたパスに対するエラー統計は生成されません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：通知のリレーに使用する HostName:Port。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeDataLogDelay<br /> </td> 
   <td> アーカイブされた E メールが削除されるまでの遅延：dataLogPath で指定されたディレクトリにアーカイブされた E メールがパージされるまでの日数です。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
  <tr> 
   <td> retryLostMessages<br /> </td> 
   <td> 失われたメッセージを再試行：子プロセスが無効になった場合、配信の一部が再試行されます。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> signEmailLinks<br /> </td> 
   <td> 署名メカニズムを有効にします。 これにより、E メール内のリンクの追跡に関するセキュリティが向上します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> true<br /> </td> 
  </tr>
  <tr> 
   <td> statServerAddress<br /> </td> 
   <td> 配信統計サーバーのアドレス（指定名： ） 
    &lt;dns or="" ip=""&gt; 
      <code>[</code>: 
     &lt;port&gt; 
       <code>]</code>. 詳しくは、 
      <a href="../../installation/using/email-deliverability.md#coordinates-of-the-statistics-server" target="_blank">統計サーバーの座標</a>. 
      <br /> 
     </td> 
   <td> 文字列<br /> </td> 
   <td> 定義されていない場合、デフォルトのポートは 7777 です。<br /> </td> 
  </tr> 
  <tr> 
   <td> statServerTLSSupport<br /> </td> 
   <td> ドメインごとに TLS を有効にする：MX ごとに設定可能な TLS を有効にします（最新の統計サーバーが必要です）。<br /> </td> 
   <td> Boolean<br /> </td> 
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
   <td> "true"に設定した場合、インスタンスは <a href="../../delivery/using/sending-with-enhanced-mta.md" target="_blank">拡張 MTA</a>.<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> <br /> </td>b 
  </tr>
  <tr> 
   <td> verifyMode<br /> </td> 
   <td> 検証モード：検証モードを有効にします（メッセージは物理的に送信されません。シミュレーションとテストに使用されます）。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> workingPath<br /> </td> 
   <td> 作業ディレクトリ：子プロセスとの通信に MTA が使用する一時ファイルの場所。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/mta/' <br /> </td> 
  </tr> 
  <tr> 
   <td> xMailer<br /> </td> 
   <td> X-Mailer フィールド： SMTP メールヘッダーの「X-Mailer」フィールドの値。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nlserver，ビルド$(PRODUCT_VERSION)'<br /> </td> 
  </tr>  
 </tbody> 
</table>

### キャッシュ {#cache}

Adobe Analytics の **キャッシュ** ノードで、次のパラメーターを設定します。 これは、ローカルファイルキャッシュ設定です。

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
   <td> 次の期間後にリサイクルされます。期間（秒単位）で表されます。その後、ストレージを再利用するためにファイルがキャッシュから自動的に削除されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 244800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSizeOnDiskMb<br /> </td> 
   <td> 最大キャッシュサイズ (MB)。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> purgePeriodSec<br /> </td> 
   <td> パージ頻度：キャッシュパージメカニズムの実行間隔（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リレー {#relay}

Adobe Analytics の **mta > リレー** ノードで、次のパラメーターを設定します。 これは、メッセージ配信用のメールサーバーの設定です。

リストは、MX DNS クエリが返す MX のリストと同じ方法で処理されます。通常、最初の MX は使用可能な限り使用され、次の MX が使用されるなどと同様に、最初の MX が使用されます。

詳しくは、 [SMTP リレー](../../installation/using/configuring-campaign-server.md#smtp-relay).

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
   <td> 住所<br /> </td> 
   <td> 使用する SMTP リレーの DNS 名または IP アドレスのコンマ区切りリスト。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> SMTP サーバーの IP ポート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

### プライマリ {#master}

Adobe Analytics の **mta > master** ノードで、次のパラメーターを設定します。 これはメインサーバーの設定です。

詳しくは、 [セクション](../../installation/using/configuring-campaign-server.md#mta-child-processes).

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
   <td> 配信するジョブのデータベースポーリング頻度。 この値は、データベースのポーリング頻度（秒）を示します。MTA は、配信を待機しているジョブのリストを取得するために、データベースを定期的にポーリングします。待機中のジョブがない場合、ポーリング期間はこの値で定義されます。ジョブが子サーバーに転送された場合、このポーリング期間は自動的に 1 秒に短縮され、新しいジョブをできるだけ早く（子サーバーが再利用可能になるとすぐに）再処理できます。これは、子サーバーが再び使用可能になるまで、データベースクエリが 1 秒ごとに実行されるという意味ではありません。 実際、データベースへのアクセスは、少なくとも 1 つの子サーバーが使用可能になった場合にのみ行われます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> dataBaseRetryDelaySec<br /> </td> 
   <td> データベース接続の失敗からの待機期間。 データベース接続の失敗は、通常、データベースサーバー自体が原因で発生します。サーバーは、メンテナンスの目的などで停止する場合もあります。 DataBaseRetryDelay パラメーターは、データベース接続に失敗した場合に 2 回の接続試行の間隔を定義します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> domainKeysReloadPeriodSec<br /> </td> 
   <td> 秘密鍵のキャッシュの有効期間 (DomainKeys)。 DomainKeys レコメンデーション (http://antispam.yahoo.com/domainkeys) に従って E メールの署名に使用する秘密鍵は、オプションとしてデータベースに保存されます。domainKeysReloadPeriodSec パラメーターは、MTA がこれらのキーをキャッシュに保持できる秒数を定義します。 この遅延の後、すべてのキーをデータベースから再読み込みする必要があります。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSpareServers<br /> </td> 
   <td> 子サーバーの最大数。 実行中のサーバーの最大数を表します。この数は、サーバーのメモリリソースと最適な互換性を持つように制限することをお勧めします。これは、配信中に確認できます。 使用メモリは、使用可能な物理メモリの 3 分の 1 を超えてはなりません。そうしないと、スワップが使用されます。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#mta-child-processes" target="_blank">MTA 子プロセス</a>.<br /> </td> 
   <td> Long<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> minSpareServers<br /> </td> 
   <td> 子サーバーの最小数。 MTA は、少なくともこの数のサーバーを実行し続けようとします。 サーバー数が少ない場合は、この値に達するまで 1 秒ごとに新しいサーバーを再起動します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> startSpareServers<br /> </td> 
   <td> 起動時の子サーバーの数。 子サーバーの数は動的に監視されます。MTA の開始時には、この値で示される数の子サーバーが作成されます。通常、ホストリソースを節約するために、1 秒あたり 1 台のサーバより高速に子サーバを起動することはできません。 ただし、MTA が開始すると、子サーバーをできるだけ早く使用できるように、この制限が無効になります。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 子 {#child}

Adobe Analytics の **mta > child** ノードで、次のパラメーターを設定します。 子サーバーの設定です。

詳しくは、 [E メール送信の最適化](../../installation/using/email-deliverability.md#email-sending-optimization).

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
   <td> アイドル状態の子サーバーが停止するまで中断。子サーバのアイドル時間がこのパラメータより長い場合は、自動的にキルしてホストリソースを解放します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> maxAgeSec<br /> </td> 
   <td> 最大メッセージ保持時間。 準備済みメッセージがスロットルのために送信されなかった場合、またはターゲット MTA に接続できなかった場合、メッセージは破棄され、次の再試行時に処理されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxGCMConnectPerChild<br /> </td> 
   <td> 各子サーバーが開始した FCM に対する並列 HTTP リクエストの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMsgPerChild<br /> </td> 
   <td> 子サーバーごとの最大メッセージ数。 各 MTA の子は、この数のメッセージと死を処理します。MTA 内のメモリやリソースのリークが無害（通常は数千）になるように数を指定することが重要です。 MTA コードに既知のメモリリークがなくても、埋め込み JavaScript エンジンと XSL エンジンは完全に信頼できません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5000000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWaitingMessages<br /> </td> 
   <td> 保留中のメッセージ：メモリ内で配信を待機しているメッセージの最大数。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 2000 年<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWorkingSetMb<br /> </td> 
   <td> 子プロセスが使用できる最大メモリサイズ（MB 単位）。 この制限を超えると、プロセスは停止し、使用するメモリがシステムに解放されます。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 128<br /> </td> 
  </tr> 
  <tr> 
   <td> soapConnectorTimeoutSec<br /> </td> 
   <td> 配信コネクタの SOAP 接続が中断されるまでのタイムアウト（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> startWithFirstMX<br /> </td> 
   <td> 常に最も優先度の高い MX から開始します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> timeToLive<br /> </td> 
   <td> 再開時の連続試行の最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 48<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Analytics の **mta > child > smtp** ノードで、次のパラメーターを設定します。 これは SMTP セッションの設定です。

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
   <td> リモートサーバーでサポートされている場合に、セーフモード (STARTTLS/SMTPS) での E メールの配信を有効化します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> idleSessionTimeoutSec<br /> </td> 
   <td> アイドルセッションのタイムアウト。 このパラメーターは、特定のドメインに複数のメッセージを送信するためにセッションが再利用される場合にのみ使用されます。MTA がメッセージの送信を完了した場合、使用した SMTP セッションはシステム的に閉じられません。この同じドメインに対してメッセージを送信する準備が整った場合は、同じ SMTP セッションが再利用されるので、セッションは自動的に閉じられません。パラメーター IdleSessionTimeout を使用すると、SMTP セッションが別のメッセージを待機中にアクティブなままになる時間を定義できます。 期間が経過すると、セッションは自動的に閉じられます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> initialDelaySec<br /> </td> 
   <td> 接続を再試行する前の初期遅延。 この遅延は、接続に失敗するたびに 2 倍になります。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSessionsPerChild<br /> </td> 
   <td> 子サーバーによる SMTP セッションの最大数。 メッセージを配信するために、MTA は受信者 MTA との SMTP 接続を初期化します。特定の子サーバーに対する同時およびアクティブな SMTP セッションの最大数は、この値によって制限されます。 この値に maxSpareServers を掛けると、指定した子サーバで同時に処理できるメッセージの最大数が得られます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Analytics の **mta > child > smtp > IPAffinity** ノードで、次のパラメーターを設定します。 これは、最適化された送信 SMTP トラフィックの IP アドレスを使用したアフィニティの管理の設定です。

詳しくは、 [使用する IP アドレスのリスト](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use) および [アフィニティを使用したアウトバウンド SMTP トラフィックの管理](../../installation/using/configuring-campaign-server.md#managing-outbound-smtp-traffic-with-affinities).

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
   <td> 名前<br /> </td> 
   <td> 論理名：ユーザーによるアフィニティにリンクされた名前。 名前はセミコロンを使用して区切られます。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

Adobe Analytics の **mta > child > smtp > IP** ノードで、次のパラメーターを設定します。

詳しくは、 [使用する IP アドレスのリスト](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use).

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
   <td> 住所<br /> </td> 
   <td> 関連する物理アドレス。 例： '192.168.0.1'<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> publicId<br /> </td> 
   <td> 関連付けられたパブリックアドレス ID。統計サーバーのキーとして使用されます。 数値である必要があります。 詳しくは、 <a href="../../installation/using/email-deliverability.md#managing-ip-addresses">セクション</a>.<br /> </td> 
   <td> Long<br /> </td> 
  </tr> 
  <tr> 
   <td> 重み<br /> </td> 
   <td> 他の IP と比較して、この IP の使用頻度を指定します（重みを大きくすると頻度が高くなります）。<br /> </td> 
   <td> Long<br /> </td> 
  </tr> 
  <tr> 
   <td> includeDomains<br /> </td> 
   <td> 含めるドメインマスクのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> excludeDomains<br /> </td> 
   <td> 除外するドメインマスクのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> heloHost<br /> </td> 
   <td> IP アドレスにリンクされたコンピューター名。 SMTP HELO コマンドを発行する際に使用します。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## nmac {#nmac}

次に、 **nmac** ノード。 これは、プッシュ通知配信のの設定です。

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
   <td> shared/proxyHTTP で定義された HTTP プロキシを使用します。 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リレー {#relay-1}

次に、 **nmac > リレー** ノード。 これにより、メッセージ配信（ios http2 コネクタ）にリレーを使用するように設定します。

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
   <td> 住所<br /> </td> 
   <td> 使用するリレーの DNS アドレスまたは名前。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> リレーポート<br /> </td> 
   <td> Long<br /> </td> 
   <td> 443<br /> </td> 
  </tr> 
  <tr> 
   <td> trustedCertsChain<br /> </td> 
   <td> 証明書チェーン（PEM ファイル）。 モックサーバーを使用する場合に役立ちます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## パイプラインの {#pipelined}

次に、 **パイプラインの** ノード。 これは、パイプラインサービスのイベント処理モジュールの設定です。

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
   <td> 公開鍵が保存されたときに Developer Connection で生成されたアプリケーションの名前。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authGatewayEndpoint<br /> </td> 
   <td> ゲートウェイトークンを取得する URL です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://api.omniture.com' <br /> </td> 
  </tr> 
  <tr> 
   <td> authPrivateKey<br /> </td> 
   <td> トークンを取得するための秘密鍵（AES で XtkKey オプションを使用して暗号化）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> disableAuth<br /> </td> 
   <td> 認証を無効にする：認証なしでパイプラインサービスに接続します。 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> discoverPipelineEndpoint<br /> </td> 
   <td> パイプラインサービス URL を検出する URL です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://producer-pipeline-pnw.adobe.net'<br /> </td> 
  </tr> 
  <tr> 
   <td> dumpStatePeriodSec<br /> </td> 
   <td> ステータス保存期間：プロセスの内部情報がファイルに保存される頻度。 0 の場合は非アクティブです。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> forcedPipelineEndpoint<br /> </td> 
   <td> リスニング URL：パイプラインサービスのリスニング URL を強制的に使用します。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> monitorServerPort<br /> </td> 
   <td> ステータスサーバーポート：プロセスのステータスを問い合わせるための HTTP サーバーポート。 0 の場合は非アクティブです。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 7781<br /> </td> 
  </tr> 
  <tr> 
   <td> pointerFlushMessageCount<br /> </td> 
   <td> この数のメッセージが処理されるたびに、ポインターがデータベースに保存されます。<br /> </td> 
   <td> <br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> pointerFlushPeriodSec<br /> </td> 
   <td> ポインターが格納されるまでの遅延：この期間中に、ポインターが少なくとも 1 回データベースに格納されます（低アクティビティの場合に役立ちます）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> processingJSThreads<br /> </td> 
   <td> パーソナライズされた JavaScript コネクタを使用したイベント処理のスレッド数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> processingThreads<br /> </td> 
   <td> イベント処理用のスレッドの数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> retryPeriodSec<br /> </td> 
   <td> エラーが発生した場合の処理間の遅延。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> retryValiditySec<br /> </td> 
   <td> この期間の後に離脱：この期間が過ぎても処理が失敗する場合は、イベントを破棄します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 修理 {#repair}

次に、 **修理** ノード。 これは、データベース修復モジュールの設定です。

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
   <td> 配信アクション修復モジュール：修復モジュールで配信アクションを処理できるまでの遅延（分単位）です。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
 </tbody> 
</table>

## securityZone {#securityzone}

次に、 **securityZone** ノード。

詳しくは、 [セキュリティゾーンの定義](../../installation/using/security-zones.md).

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
   <td> Web アプリケーションのデバッグモードを許可します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowEmptyPassword<br /> </td> 
   <td> パスワードなしでのアプリケーションの使用をユーザーに許可します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowHTTP<br /> </td> 
   <td> オペレーターのログオンに HTTP の使用を許可します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowSQLInjection<br /> </td> 
   <td> 式での SQLDATA の使用を許可します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowUserPassword<br /> </td> 
   <td> ユーザー/パスワードセッショントークンを許可します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> ラベル<br /> </td> 
   <td> ラベル<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewLabel()<br /> </td> 
  </tr> 
  <tr> 
   <td> 名前<br /> </td> 
   <td> 内部名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewName() <br /> </td> 
  </tr> 
  <tr> 
   <td> sessionTokenOnly<br /> </td> 
   <td> セキュリティトークンは使用しないでください。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> showErrors<br /> </td> 
   <td> エラーの詳細を表示<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

次にデフォルトの設定を示します。

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

次に、 **securityZone > subNetwork** ノード。

詳しくは、 [セキュリティゾーンの定義](../../installation/using/security-zones.md).

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
   <td> ラベル<br /> </td> 
   <td> ラベル<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewLabel()<br /> </td> 
  </tr> 
  <tr> 
   <td> マスク<br /> </td> 
   <td> マスクまたはアドレス<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 名前<br /> </td> 
   <td> 内部名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewName() <br /> </td> 
  </tr> 
  <tr> 
   <td> プロキシ<br /> </td> 
   <td> このサブネットワークがインスタンスにアクセスするために使用する（リバース）プロキシのマスクまたはアドレス。 この場合、このプロキシの代わりに「X-Forwarded-For」ヘッダーがテストされます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 127.0.0.1 <br /> </td> 
  </tr> 
 </tbody> 
</table>

## SMS {#sms}

次に、 **sms** ノード。 これは、インバウンド SMS 管理モジュールの設定です。

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
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataRetentionDays<br /> </td> 
   <td> SMPP コネクタが保持する作業ファイルの最大日数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> dataSizeMo<br /> </td> 
   <td> SMPP 作業ファイルの最大サイズ (MB)。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 512<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> keepAlivePeriod<br /> </td> 
   <td> セッション連続フレームの繰り返し： max. 受信セッションが引き続き有効であることを通知する 2 つのフレーム間の時間（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollPeriod<br /> </td> 
   <td> 検索頻度： SMS アカウントのポーリング期間。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriod<br /> </td> 
   <td> アカウント再読み込み頻度：ポーリングするアカウントのデータベース再読み込み頻度。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> srReadDelay<br /> </td> 
   <td> SR 処理の遅延秒数：現在の時刻から srReadDelay を引いた時間（秒）よりも前の復元日を持つ SR のみ。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> SMS ゲートウェイとの通信がタイムアウトしました。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
 </tbody> 
</table>

### netsize {#netsize}

次に、 **sms > netsize** ノード。

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
   <td> Long<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
 </tbody> 
</table>

## stat {#stat}

次に、 **stat** ノード。 これは、MTA 統計モジュールの設定です。

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
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> ポート<br /> </td> 
   <td> サーバーリスニングポート。 詳しくは、 <a href="../../installation/using/email-deliverability.md#definition-of-the-server-port">セクション</a>.<br /> </td> 
   <td> Short<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## syslogd {#syslogd}

次に、 **syslogd** ノード。 これは、ログ管理モジュールの設定です。

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
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxFileSizeMb<br /> </td> 
   <td> ログファイルの最大サイズ (MB)。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> maxNumberOfLoginsFiles<br /> </td> 
   <td> 保持する logins.log ファイルの最大数。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 365<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## tracking {#tracking}

次に、 **tracking** ノード。 これはトラッキングサーバーの設定です。

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
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> blockRedirectForUnsignedTrackingLink<br /> </td> 
   <td> 以前のビルドで生成された、形式の正しくない URL を無効にします。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> consolidationPeriodSec<br /> </td> 
   <td> 連結期間<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> dedupOpenPeriodMin<br /> </td> 
   <td> 開封数の重複を排除：重複した開封数のトラッキングログを削除して、Outlook などのメールリーダーでのメールプレビューの効果を制限します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePercent<br /> </td> 
   <td> エラーの最大 X%を無視：まだ考慮に入れていないジャーナルの割合がこの値に達しない限り、トラッキング指標を更新しません。 <br /> </td> 
   <td> Byte<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePeriod<br /> </td> 
   <td> エラー指標を更新：エラー指標が再計算されるまでの最大時間。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> indicatorsDuration<br /> </td> 
   <td> 指標の計算期間：配信の有効期間後の期間。その後、統合指標は計算されなくなります。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 2592000<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> logCountPerRequest<br /> </td> 
   <td> リモートトラッキングサーバーへの呼び出しによってリクエストされたログの数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> phishbowlServiceAPIKey<br /> </td> 
   <td> Phishbowl サービスエンドポイント統合の API キー。 これにより、古いビルドから生成された不正な URL のリダイレクトが保護されます。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> phishbowlServiceEndpoint<br /> </td> 
   <td> Phishbowl サービスエンドポイント統合のエンドポイントです。 これにより、古いビルドから生成された不正な URL のリダイレクトが保護されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePercent<br /> </td> 
   <td> 最大 X%の追跡を無視：まだ考慮に入れていないジャーナルの割合がこの値に達しない限り、追跡指標を更新しません。<br /> </td> 
   <td> Byte<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePeriod<br /> </td> 
   <td> トラッキング指標を更新：トラッキング指標が再計算されるまでの最大期間。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> userAgentCacheSize<br /> </td> 
   <td> ブラウザー識別子のキャッシュのサイズ。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## trackinglogd {#trackinglogd}

次に、 **trackinglogd** ノード。 これは、トラッキングログ書き込みデーモンの設定です。

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
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxCreateFileRetry<br /> </td> 
   <td> 最大書き込み再試行数：ログファイルへの書き込みに失敗した場合に作成できるファイルの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> maxLogsSizeOnDiskMb<br /> </td> 
   <td> ログの最大サイズ：ディスク上のログが使用する最大容量（MB 単位）。 100 MB 以上にする必要があります。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedLogs<br /> </td> 
   <td> 最大ログ数：共有メモリに保存されるログの最大数。 10000より小さい値は指定できません。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeLogsPeriod<br /> </td> 
   <td> パージ前のログ数：ログファイルのパージを開始する前に挿入されたログの数。 50000以下にする必要があります。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 50000<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> webTrackingParamSize<br /> </td> 
   <td> 追加の Web トラッキングパラメーター用に共有メモリに保存される最大文字数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 64<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Web {#web}

次に、 **web** ノード。 これは、Web モジュールの設定です。

詳しくは、 [セクション](configuring-campaign-server.md#default-port-for-tomcat).

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
   <td> 文字列として渡される JVM のオプション。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> MaxThreads<br /> </td> 
   <td> スレッドの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 75<br /> </td> 
  </tr> 
  <tr> 
   <td> MinSpareThreads<br /> </td> 
   <td> スレッドの最小数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> controlPort<br /> </td> 
   <td> Tomcat のリッスン制御ポート：を参照してください。 <a href="configure-tomcat.md" target="_blank">Tomcat の設定</a>.<br /> </td> 
   <td> Short<br /> </td> 
   <td> 8005<br /> </td> 
  </tr> 
  <tr> 
   <td> httpPort<br /> </td> 
   <td> Tomcat HTTP リスニングポート：を参照してください。 <a href="configure-tomcat.md" target="_blank">Tomcat の設定</a>.<br /> </td> 
   <td> Short<br /> </td> 
   <td> 8080<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxDeliveryQueueSize<br /> </td> 
   <td> SubmitDelivery 呼び出し用のキューのサイズ：キューに格納できる SubmitDelivery SOAP 呼び出しの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 50<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告<br /> </td> 
   <td> Long<br /> </td> 
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
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> startSoapRouterInModule<br /> </td> 
   <td> SOAP ルーターをモジュールモードで起動します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### jsp {#jsp}

次に、 **web > jsp** ノード。 これは、JSP で使用されるパラメータの設定です。

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
   <td> デバッグ<br /> </td> 
   <td> デバッグモードでの JSP の実行。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> downloadPath<br /> </td> 
   <td> ダウンロードフォルダー：クライアントコンソール用のインストールプログラムのダウンロードパス。<br /> </td> 
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
   <td> SOAP ルーターの URL (http://myserver/xxx、http://jni、mailto:xxx)。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'http://jni'<br /> </td> 
  </tr> 
 </tbody> 
</table>

The **web > jsp > classpath** ノードには、JVM の起動時に使用するすべてのクラスパスのリストが含まれます。 次にデフォルトの設定を示します。

```
'$(XTK_INSTALL_DIR)/tomcat-8/bin/bootstrap.jar
          $(XTK_INSTALL_DIR)/tomcat-8/bin/tomcat-juli.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/tomcat-coyote.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/tomcat-util.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/tomcat-api.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/servlet-api.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/jsp-api.jar
          $(XTK_INSTALL_DIR)/tomcat-8/lib/el-api.jar
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

次に、 **web > jssp** ノード。 これは、JSSP で使用されるパラメーターの設定です。

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
   <td> 各クエリの後に JavaScript コンテキストのガベージコレクターを有効にします。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> timeToLive<br /> </td> 
   <td> JavaScript コンテキストで提供されるページの最大数。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

The **web > jsp > classpath** ノードには、JVM の起動時に使用するすべてのクラスパスのリストが含まれます。

### リレー {#relay-2}

次に、 **web > リレー** ノード。 これは、2 つのゾーン間の HTTP 要求のリレーの設定です。

詳しくは、 [セクション](../../installation/using/deploying-an-instance.md#synchronizing-public-resources).

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
   <td> Web サーバー内で HTTP リレーモジュールをデバッグモードで起動します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInAuthority<br /> </td> 
   <td> 禁止文字（ドメイン）:URI の「authority」セクションで禁止されている文字のリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.?#@/:' <br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInPath<br /> </td> 
   <td> 禁止文字（パス）:URI の「パス」セクションで禁止されている文字のリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '?#/'<br /> </td> 
  </tr> 
  <tr> 
   <td> modDir<br /> </td> 
   <td> 「mod_dir」モジュールオプションの値：フォルダーに対するクエリ中に使用されるファイルのリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'index.md' <br /> </td> 
  </tr> 
  <tr> 
   <td> startRelay<br /> </td> 
   <td> HTTP リレーモジュールを起動します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> startRelayInModule<br /> </td> 
   <td> Web サーバー内で HTTP リレーモジュールを起動します。 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> 禁止された URL を削除するまでの待機時間。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '60'<br /> </td> 
  </tr> 
 </tbody> 
</table>

を追加します。 **web /リレー/ url** 中継する URL ごとにノード（挿入順序は優先度を定義します）を次のパラメーターで指定します。

詳しくは、 [動的ページのセキュリティとリレー](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays) および [セクション](../../installation/using/deploying-an-instance.md#synchronizing-public-resources).

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
   <td> 許可された IP：このマスクのリレーの使用が許可されているソース IP アドレスのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 拒否<br /> </td> 
   <td> これらの URL へのアクセスを拒否します（HTTP 403 エラーを返します）<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> hostMask<br /> </td> 
   <td> リレーする DNS エイリアス：リレーする DNS エイリアスマスクのコンマ区切りリスト（例： '*.adobe.com'）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> httpAllowed<br /> </td> 
   <td> セキュリティゾーン（WebApps など）に関係なく、HTTP アクセスが許可されます。 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayHost<br /> </td> 
   <td> 元のホストを追加：リレー時に元のリクエストの HTTP「Host」ヘッダーを使用します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayPath<br /> </td> 
   <td> 初期 URL パスの追加：リレーする URL の完全パスをターゲットページの URL に追加します。 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ステータス<br /> </td> 
   <td> パブリックリソースの同期ステータス（列挙）。 指定できる値は、「normal」（通常の実行）、「blacklist」（エラー 404 の場合はに追加される URL）、「spare」（既存の場合はスペアサーバー上のファイルアップロード）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 標準<br /> </td> 
  </tr> 
  <tr> 
   <td> targetUrl<br /> </td> 
   <td> ターゲットページの URL：を参照してください。 <a href="configure-tomcat.md" target="_blank">Tomcat の設定</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> timeout<br /> </td> 
   <td> 中継されるリクエストの最大実行時間（秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> urlPath<br /> </td> 
   <td> リレーする URL のマスク（例：「/nl*」、「*.jsp」）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

次にデフォルトの設定を示します。

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

を追加します。 **web > リレー > responseHeader** リレーに転送される返信に追加する HTTP ヘッダーごとのノード。

詳しくは、 [HTTP ヘッダーの管理](../../installation/using/configuring-campaign-server.md#managing-http-headers).

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
   <td> 名前<br /> </td> 
   <td> ヘッダー名<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> 値<br /> </td> 
   <td> ヘッダー値 <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

次にデフォルトの設定を示します。

```
<responseHeader name="X-XSS-Protection" value="1; mode=block"/>
```

### リダイレクト {#redirection}

次に、 **web /リダイレクト** ノード。 これは、リダイレクトモジュールの設定です。

詳しくは、 [セクション](../../installation/using/deploying-an-instance.md#synchronizing-public-resources).

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
   <td> 組織 ID:Adobe Experience Cloud内の一意の組織識別子。特に VisitorID サービスと IMS SSO で使用されます。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> P3PCompactPolicy<br /> </td> 
   <td> 永続的な Cookie に使用するポリシーを記述する値（P3P Compact Policy 形式に準拠）。 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV'<br /> </td> 
  </tr> 
  <tr> 
   <td> cookieDomain<br /> </td> 
   <td> Cookie を設定するドメインを明示的に示すために設定する、ドメインのコンマ区切りリスト。 <br /> </td> 
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
   <td> 呼び出し別のログ数：メソッド GetTrackingLogs の呼び出し時にデフォルトで返されるログの数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> expirationURL<br /> </td> 
   <td> 期限切れリダイレクトのページ：配信アクションのリダイレクトの期限が切れた場合にリダイレクションサーバーがデフォルトで使用する Web ページの URL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxJobsInCache<br /> </td> 
   <td> 最大ジョブ数：キャッシュ内の配信アクションの最大数。 50 以下にする必要があります。 <br /> </td> 
   <td> Long<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> showSourceIP<br /> </td> 
   <td> false に設定した場合、r/test から返される応答の sourceIP の値は空の文字列になります。 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> startRedirection<br /> </td> 
   <td> リダイレクトサービスを開始します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> startRedirectionInModule<br /> </td> 
   <td> モジュールモードでリダイレクトサービスを開始します。<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> trackWebVisitors<br /> </td> 
   <td> Web トラッキング：不明なユーザーが訪問したページのログの作成。 <br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingPassword<br /> </td> 
   <td> リダイレクションサーバーが使用するパスワード。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

次に、 **web > リダイレクト > spareServer** ノード。

詳しくは、 [重複した追跡](../../installation/using/configuring-campaign-server.md#redundant-tracking).

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
   <td> 次の場合に考慮：式が true を返した場合は、トラッキングサーバーが考慮されます。 <br /> </td> 
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
   <td> 追加のリダイレクトサーバー URL<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

### spamCheck {#spamcheck}

次に、 **web > spamCheck** ノード。 これは、 E メールスパム対策スコアリング評価パラメーターの設定です。

詳しくは、 [SpamAssassin の設定](../../installation/using/configuring-spamassassin.md).

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
   <td> E メールのスパム対策スコアを評価するために実行するコマンド（例：「perl spamcheck.pl」）。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## wfserver {#wfserver}

次に、 **wfserver** ノード。 これは、ワークフロープロセスの設定です。

詳しくは、 [高可用性のワークフローとアフィニティ](../../installation/using/configuring-campaign-server.md#high-availability-workflows-and-affinities).

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
   <td> 親和性<br /> </td> 
   <td> アフィニティ<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> args<br /> </td> 
   <td> 起動パラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> Boolean<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataBasePoolPeriodSec<br /> </td> 
   <td> 期間<br /> </td> 
   <td> Long<br /> </td> 
   <td> 20<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行する JavaScript の ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費量アラート：特定のプロセスが消費した RAM の量（MB 単位）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費量警告：特定のプロセスで消費された RAM の量（MB 単位）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
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
   <td> プロセスが自動的に再開される時刻。 詳しくは、 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールが最初に開始され、最後に停止されます。 したがって、syslogd モジュールは、優先度 0 を持つ必要があります。<br /> </td> 
   <td> Short<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>
