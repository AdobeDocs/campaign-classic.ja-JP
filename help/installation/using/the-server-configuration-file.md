---
product: campaign
title: サーバー設定ファイル
description: サーバー設定ファイル
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: appendices
exl-id: 70cd6a4b-c839-4bd9-b9a7-5a12e59c0cbf
TQID: https://experienceleague.adobe.com/BZ4rjzbXYikNoGAVHq4Gy7tY8OugKDgsmVLkKuIB9tw
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 8103
ht-degree: 8%

---

# サーバー設定ファイル{#the-server-configuration-file}

Adobe Campaignの全体的な設定は、インストールディレクトリの&#x200B;**conf** ディレクトリにある&#x200B;**serverConf.xml** ファイルで定義されます。 この節では、**serverConf.xml** ファイルの様々なノードとパラメーターをすべてリストします。

>[!NOTE]
>
>サーバーサイド設定は、Adobeでホストされているデプロイメントに対してのみ、Adobeで実行できます。 様々なデプロイメントについて詳しくは、[&#x200B; ホスティングモデル &#x200B;](../../installation/using/hosting-models.md) セクションまたは[このページ &#x200B;](../../installation/using/capability-matrix.md)を参照してください。 ホスト モデルとハイブリッド モデルのインストールと設定の手順については、この[&#x200B; セクション &#x200B;](../../installation/using/hosting-models.md)で説明します。

最初のパラメーターは、**共有** ノード内にあります。 これらはインスタンスに関連しています。 これらは、すべてのnlserver コマンド（nlserver web、nlserver wfserverなど）で使用される可能性があります。 その他のセクションは、特定のnlserver サブコマンドに関連しています。

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
* [相互作用](#interactiond)
* [MTA](#mta)
* [nmac](#nmac)
* [パイプライン化](#pipelined)
* [修復](#repair)
* [securityZone](#securityzone)
* [SMS](#sms)
* [統計](#stat)
* [syslogd](#syslogd)
* [tracking](#tracking)
* [trackinglogd](#trackinglogd)
* [Web](#web)
* [wfserver](#wfserver)

## 認証 {#authentication}

**認証** ノードの様々なパラメーターを次に示します。

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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> defaultMode<br /> </td> 
   <td> 既定の識別モード。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nl'<br /> </td> 
  </tr> 
  <tr> 
   <td> longSessionTimeOutSec<br /> </td> 
   <td> 長いセッションのタイムアウト （秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1296000<br /> </td> 
  </tr> 
  <tr> 
   <td> securityTimeOutSec<br /> </td> 
   <td> セキュリティ トークンのタイムアウト （秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionCacheSec<br /> </td> 
   <td> キャッシュ時間：セッション情報のキャッシュ （秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> sessionTimeOutSec<br /> </td> 
   <td> セッションのタイムアウト （秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
 </tbody> 
</table>

### XTK {#xtk}

**認証 / XTK** ノードの様々なパラメーターを次に示します。

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
   <td> 内部アカウント セキュリティ ゾーン：内部アカウントの承認済みゾーン。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'lan'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## dataStore {#datastore}

**dataStore** ノードの様々なパラメーターを次に示します。 ここでは、サーバーのデータソースが定義されます。

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
   <td> エクスポート ディレクトリ：エクスポートされたデータの宛先ディレクトリのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$（XTK_INSTALL_DIR）/var/$（INSTANCE_NAME）/export/' <br /> </td> 
  </tr> 
  <tr> 
   <td> extraSandboxedDirectories<br /> </td> 
   <td> 追加のサンドボックス化されたディレクトリ：サンドボックスに追加されるその他のパス （コマ区切り）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/home/customers/,/sftp/' <br /> </td> 
  </tr> 
  <tr> 
   <td> formCacheTimeToLive<br /> </td> 
   <td> フォームキャッシュの有効期限の遅延：キャッシュエントリが無効になるまでのタイムアウト秒数。 Oは、キャッシュ エントリが公開時にのみ更新されることを意味します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> ホスト <br /> </td> 
   <td> DNS マスク：このインスタンスが提供するDNS マスクのリスト（コンマ区切り、および*を使用できます）。 パターン）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '*'<br /> </td> 
  </tr> 
  <tr> 
   <td> interactionCacheTimeToLive<br /> </td> 
   <td> インタラクション JSSP キャッシュ有効期限の遅延：キャッシュエントリが無効化されるまでのタイムアウト秒数。 負の値は、キャッシュが常に無効化されることを意味します。 '0'、空または無効な値は60と見なされます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> lang<br /> </td> 
   <td> インスタンス言語（列挙）。 使用可能な値は、「fr_FR」（Français）、「en_GB」（英国）、「en_US」（英語（米国）、「de_DE」（ドイツ語）、「ja_JP」（日本語）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'en_US'<br /> </td> 
  </tr> 
  <tr> 
   <td> uploadDirectory<br /> </td> 
   <td> アップロードフォルダー：アップロードされたデータの宛先ディレクトリのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$（XTK_INSTALL_DIR）/var/$（INSTANCE_NAME）/upload/' <br /> </td> 
  </tr> 
  <tr> 
   <td> uploadAllowlist<br /> </td> 
   <td> ダウンロードを許可されたファイルは、「,」で区切られます。 文字列は、有効な正規のJava式である必要があります。 <a href="file-res-management.md" target="_blank"> アップロード可能なファイルの制限</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.+' <br /> </td> 
  </tr> 
  <tr> 
   <td> useVault<br /> </td> 
   <td> Vaultにシークレットを保存する：Hashicorp Vaultを使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultSecretPath<br /> </td> 
   <td> Vault<br />の秘密パス </td> 
   <td> 文字列<br /> </td> 
   <td> '/v1/secret/campaign/'<br /> </td> 
  </tr> 
  <tr> 
   <td> vaultTokenPath<br /> </td> 
   <td> Vault トークンを含むファイルのローカルパス。 $（HOME）はこのパスで使用できます（他の環境変数は使用できません）。<br /> </td> 
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
   <td> ビューのキャッシュの有効期間：キャッシュエントリが無効化されるまでのタイムアウト秒数。 負の値は、キャッシュが常に無効化されることを意味します。 '0'、空または無効な値は60と見なされます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> workingDirectory<br /> </td> 
   <td> 作業ディレクトリのXPath。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> workingDirectory：作業ディレクトリのXPath。 デフォルト：'$（XTK_INSTALL_DIR）/var/$（INSTANCE_NAME）/workspace/'<br /> </td> 
  </tr> 
 </tbody> 
</table>

### proxyAdjust {#proxyadjust}

**dataStore > proxyAdjust** ノードの様々なパラメーターを次に示します。 正規表現に一致するURLは、urlBaseで定義されたURLに基づいて再生成されます。

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
   <td> 外部URLを生成する際に使用するベース。 例：https://server.domain.com<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> urlRegEx<br /> </td> 
   <td> URLに一致させる正規表現。 例：http://server\.lan\.net.*<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

### dataSource {#datasource}

**dataStore > dataSource** ノードの様々なパラメーターを次に示します。

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
   <td> Data Source名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> デフォルト <br /> </td> 
  </tr> 
 </tbody> 
</table>

**dataStore > dataSource > dbcnx** ノードで、接続設定を行います。

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
   <td> Unicode ストレージ <br /> </td> 
   <td> ブール値<br /> </td> 
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
   <td> 暗号化されたパスワード <br /> </td> 
   <td> ブール値<br /> </td> 
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
   <td> プロバイダー<br /> </td> 
   <td> タイプ（列挙）。 指定可能な値は、「Oracle」、「MSSQL」（Microsoft SQL Server）、「PostgreSQL」（PostgreSQL）、「Teradata」、「MySQL」、「Netezza」、「AsterData」、「SAPHANA」（SAP HANA）、「RedShift」（Amazon Redshift）、「ODBC」（ODBC （Sybase ASE、Sybase IQ））、「リレー」（HTTP リレーリモートデータベース） <br />です。 </td> 
   <td> 文字列<br /> </td> 
   <td> 'Oracle'<br /> </td> 
  </tr> 
  <tr> 
   <td> サーバー<br /> </td> 
   <td> サーバー<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> タイムゾーン <br /> </td> 
   <td> タイムゾーン：<a href="../../installation/using/time-zone-management.md" target="_blank"> タイムゾーン管理</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> unicodeData<br /> </td> 
   <td> データベース <br />内のUnicode データ </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> useTimestampTZ<br /> </td> 
   <td> タイムゾーンを含む日付フィールド：<a href="../../installation/using/time-zone-management.md" target="_blank"> タイムゾーン管理</a>を参照してください。<br /> </td> 
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
   <td> 関数のプレフィックス <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

**dataStore > dataSource > pool** ノードで、関連付けられた接続プールのパラメーターを設定します。

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
   <td> 短い<br /> </td> 
  </tr> 
  <tr> 
   <td> freeCnx<br /> </td> 
   <td> プールに保持されている無料接続の数。<br /> </td> 
   <td> 短い<br /> </td> 
  </tr> 
  <tr> 
   <td> maxCnx<br /> </td> 
   <td> 新しい接続を拒否する前に許可された接続の最大数。 この<a href="https://helpx.adobe.com/jp/campaign/kb/how-to-increase-the-maximum-number-of-database-connections-from-.html"> テクニカルノート </a>を参照してください。<br /> </td> 
   <td> 短い<br /> </td> 
  </tr> 
  <tr> 
   <td> maxIdleDelaySec<br /> </td> 
   <td> 接続の最大アイドル時間。 0はデフォルト値を意味します。<br /> </td> 
   <td> 短い<br /> </td> 
  </tr> 
 </tbody> 
</table>

### virtualDir {#virtualdir}

**dataStore > virtualDir** ノードの様々なパラメーターを次に示します。 これは、仮想ディレクトリを実際のディレクトリにマッピングするための設定です。

詳しくは、[公開リソースの管理](file-res-management.md)を参照してください。

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
   <td> 仮想ディレクトリ <br />の名前 </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> パス <br /> </td> 
   <td> 実際のディレクトリ <br />の完全パス </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルト設定は次のとおりです。

```
<virtualDir name="images" path="$(XTK_INSTALL_DIR)/var/res/img/"/>
<virtualDir name="formCache" path="$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/formCache/"/>
<virtualDir name="publicFileRes" path="$(XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)"/>
```

### preprocessCommand {#preprocesscommand}

**dataStore > preprocessCommand** ノードの様々なパラメーターを次に示します。 これらは、「ファイルを読み込む」ワークフローアクティビティの事前処理に使用できる許可されたコマンドです。

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
   <td> コマンド ライン ラベル <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> 名前<br /> </td> 
   <td> コマンド ライン名<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルト設定は次のとおりです。

```
<preprocessCommand command="" label="None" name="none"/>
<preprocessCommand command="zcat &quot;$fileName&quot;" label="Decompression" name="zcat"/><preprocessCommand command="gpg --decrypt &quot;$fileName&quot;" label="Decrypt" name="gpg"/>
```

## dnsConfig {#dnsconfig}

**dnsConfig** （DNS設定）ノードの様々なパラメーターを次に示します。

詳細については、この[&#x200B; セクション &#x200B;](../../installation/using/configuring-campaign-server.md)を参照してください。

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
   <td> ドメイン名：デフォルトのドメイン名。 SMTP HELO コマンドで使用されます。 デフォルトでは、Windowsで宣言された最初のネットワークインターフェイスのネットワークパラメーターを使用するか、Linux （ドメインまたは検索エントリ）でfile/etc/resolv.confを解析します。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> nameServers<br /> </td> 
   <td> DNS サーバー：ドメイン名サーバー（DNS）のコンマ区切りリスト。 以下のメモを参照してください。<br /> </td> 
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
   <td> タイムアウト <br /> </td> 
   <td> DNS クエリのタイムアウト （ミリ秒単位）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5000<br /> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>**nameSevers**&#x200B;に関する注意：デフォルトでは、ネットワークが使用されます>windowsで宣言された最初のネットワークインターフェイスのパラメーター>UNIXでは定義されていません。 ドメイン ネーム サーバー（DNS）を定義します>mtaで使用される、メール交換器を取得するための宣言>ドメイン。
>
>この値が定義されていない場合、MTAはホスト ネットワーク設定でこの情報をシークします。 複数のDNSが可能な場合は、異なるDNS アドレスをコンマで区切る必要があります（例：212.155.207.1,212.155.207.2）。 配信サーバーに複数のネットワークインターフェイスがある場合、MTAで使用されるDNS リストが最初のものです。 この場合は、あいまいさを避けるために、**nameServer** パラメーターを指定することをお勧めします。

>[!CAUTION]
>
>ネットワークホストの設定でDHCPを使用している場合、MTAはDHCPが提供するDNS リストを見つけません。 この場合は、Windows コントロールパネルのネットワークパラメータでDNS リストを指定することをお勧めします。

## exec {#exec}

**exec** （コマンド実行）ノードの様々なパラメーターを次に示します。

詳細については、[承認済み外部コマンドの制限](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)を参照してください。

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
   <td> 追加するコマンドを含むファイルへのパスを指定します。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ユーザー<br /> </td> 
   <td> コマンドを別のユーザーとして実行します。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## htmlToPdf {#htmltopdf}

**htmlToPdf** ノードの様々なパラメーターを次に示します。 これは、web ページをPDF ドキュメントに変換するためのサービスの設定です。

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
   <td> 変換を実行するためのコマンドライン （「その他」モード）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessusCount<br /> </td> 
   <td> 最大 1台のコンピューターで一度に許可されている変換プロセスの数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> モード <br /> </td> 
   <td> コンバージョンに使用するツール。 使用可能な値は、phantomjs、wkhtmltopdf、other、disabled<br />です。 </td> 
   <td> 文字列<br /> </td> 
   <td> 'phantomjs' <br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト <br /> </td> 
   <td> コンバージョンのタイムアウト：最大コンバージョン時間（秒単位）。 このしきい値を超えると、変換プロセスは停止され、エラーが発生します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 120<br /> </td> 
  </tr> 
  <tr> 
   <td> 詳細<br /> </td> 
   <td> 詳細モード：発生する可能性のあるエラーを診断するために、詳細モードで開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> waitTime<br /> </td> 
   <td> プロセス待ちの場合の遅延：すべてのプロセスが同時に使用され、プロセスの解放を待つ場合の秒単位の遅延。 この遅延を超えると、変換は停止され、エラーが発生します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
 </tbody> 
</table>

phantomjsの例：

```
phantomjs - -ignore-ssl-errors=true '$(XTK_INSTALL_DIR)/bin/htmlToPdf.js' '-out:{outPdf}' '-post:{postFile}' '-url:{originUrl}' -sessiontoken:{sessiontoken} -format:{format} -orientation:{orientation} -marginTop:{marginTop} -marginLeft:{marginLeft} -marginRight:{marginRight} -marginBottom:{marginBottom}
```

## ims {#ims}

**ims** ノードの様々なパラメーターを次に示します。 これは、[IMS](../../integrations/using/about-adobe-id.md)を使用してCampaignが別のサービスに接続するための設定です。

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
   <td> 秘密鍵（AESで暗号化） <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSCode<br /> </td> 
   <td> 認証コード （AESで暗号化） <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSEndpoint<br /> </td> 
   <td> IMS サーバーURL<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://ims-na1.adobelogin.com'<br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSTAClientId<br /> </td> 
   <td> テクニカル アカウント クライアント ID <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSTAClientSecret<br /> </td> 
   <td> テクニカル アカウント秘密鍵（AESで暗号化） <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSTAId<br /> </td> 
   <td> テクニカル アカウント ID <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authIMSTAPrivateKey<br /> </td> 
   <td> テクニカルアカウントの秘密鍵（AESで暗号化） <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## JavaScript {#javascript}

**javaScript** ノードの様々なパラメーターを次に示します。 これは、JavaScript インタープリターの設定です。

詳細については、[&#x200B; レポートに関するドキュメント &#x200B;](../../reporting/using/actions-on-reports.md#memory-allocation)を参照してください。

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
   <td> ガベージコレクターを実行する前の最大サイズ （MB単位）です。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 512 <br /> </td> 
  </tr> 
  <tr> 
   <td> stackSizeKB<br /> </td> 
   <td> 各スタック チャンクのサイズ （キロオクテット）。 これは、ほとんどのユーザーが調整すべきではないメモリ管理チューニングパラメーターです。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
 </tbody> 
</table>

## mailExchanger {#mailexchanger}

**mailExchanger** ノードの様々なパラメーターを次に示します。 これはSMTP サーバーの設定です。

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
   <td> SMTP サーバー：電子メールの転送用SMTP サーバーのIP アドレス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> mxPort<br /> </td> 
   <td> 電子メール転送に使用されるSMTP サーバーのTCP ポート。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## モジュール {#module}

**モジュール** ノードの様々なパラメーターを次に示します。 これは、名前空間制限モジュール xtkの設定です。

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
   <td> 新しいエンティティの作成時に使用される既定の名前空間。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'cus'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 監視 {#monitoring}

**監視** ノードの様々なパラメーターを次に示します。 これが監視サービス設定です。

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
   <td> 最大準備時間：配信アクションが準備中でなくなるまでの秒単位。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
  <tr> 
   <td> unixScript<br /> </td> 
   <td> 監視サービスによって実行されたUnix スクリプト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> winScript<br /> </td> 
   <td> 監視サービスによって実行されるWindows スクリプト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## ooconv {#ooconv}

**ooconv** ノードの様々なパラメーターを次に示します。 これは、ドキュメント変換サーバーの設定です。

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
   <td> OpenOffice サーバーが実行できるコンバージョンの最大数です。 この番号を超えると、サーバーが再起動されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxServerIdleSec<br /> </td> 
   <td> 強制終了までのOpenOffice サーバーの最大アイドル時間です。<br /> </td> 
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
   <td> ドキュメント変換サーバーのURL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'http://localhost:8080/nl/jsp/ooconv.jsp'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## proxyConfig {#proxyconfig}

**proxyConfig** ノードの様々なパラメーターを次に示します。 これは、プロキシパラメーターの設定です。

詳細については、[&#x200B; プロキシ接続設定](file-res-management.md)を参照してください。

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
   <td> プロキシ サーバーを使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> 上書き<br /> </td> 
   <td> 例外：プロキシパラメーターを無視するアドレスのリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'localhost*' <br /> </td> 
  </tr> 
  <tr> 
   <td> useSingleProxy<br /> </td> 
   <td> 一意のプロキシ サーバー：すべての種類のプロキシに同じ構成を使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### HTTP プロキシ / セキュアプロキシ {#http-proxy---secure-proxy-}

**proxyConfig > HTTP Proxy / Secure proxy** ノードで、次のパラメーターを設定します。

詳細については、[&#x200B; プロキシ接続設定](file-res-management.md)を参照してください。

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
   <td> プロキシ サーバー<br />のアドレス </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ログイン <br /> </td> 
   <td> プロキシサーバー<br />への接続にログインします </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> パスワード <br /> </td> 
   <td> プロキシ サーバー<br />との接続のパスワード </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> プロキシ サーバーのポート <br /> </td> 
   <td> 短い<br /> </td> 
  </tr> 
 </tbody> 
</table>

## threadPool {#threadpool}

**threadPool** ノードの様々なパラメーターを次に示します。

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
   <td> Long<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## urlPermission {#urlpermission}

**urlPermission** ノードの様々なパラメーターを次に示します。 これは、Javascript コードがアクセスできるURLのリストです。

Javascript コードで見つかったURLをAdobe Campaign サーバーで使用できるか使用できないかを指定するドメインと正規表現のリスト。

URLが見つからない場合は、指定されたデフォルトモードに従って、デフォルトアクションが実行されます。

詳細については、[送信接続保護](../../installation/using/configuring-campaign-server.md#url-permissions)を参照してください。

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
   <td> URLが承認済みリスト（列挙）にない場合のデフォルトアクション。 指定できる値は、「無視」（警告メッセージなしで認証します。これには保護を無効にする必要があります）、「警告」（警告メッセージを承認して発行します）、「拒否」（URLへのアクセスを禁止します）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 拒否<br /> </td> 
  </tr> 
  <tr> 
   <td> debugTrace<br /> </td> 
   <td> URL選択メカニズムのトレースをデバッグしています。URL確認プロセス中に追加のメッセージを発行します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

## cusHeaders {#cusheaders}

このノードを使用すると、外部サーバーからファイルをアップロードする際に実行されるリクエストに特定のヘッダーを追加できます。 コンテンツ配信ネットワーク（CND）は、依頼者を信頼するために、特定のヘッダーを要求できます。 これらのヘッダーは、特に配信実行ステップで受信者ごとにパーソナライズされたドキュメントをダウンロードする際に、Campaign リクエストに対する信頼を向上するために使用できます。 大量のリソースダウンロード要求は、DDos攻撃と解釈できます。 dnsPatternを使用すると、ドメイン名に基づいて、異なるCDNの特定のヘッダー名と値を設定できます。

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

URLごとに、次のパラメーターを含む&#x200B;**url** ノードを追加します。

詳細については、[送信接続保護](../../installation/using/configuring-campaign-server.md#url-permissions)を参照してください。

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
   <td> ドメイン名、またはドメインの親は、URLに関係する：検証するURLのドメインの全部または一部を検証し、検証を高速化します。 URLは、ドメインにdsnSuffixが含まれている場合にのみ、正規表現に関して検証されます。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> urlRegEx<br /> </td> 
   <td> このドメインに属するURLの検証を絞り込む正規表現：dnsSuffixに対応する場合は、URLが検証する必要がある正規表現。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

レコードが&#x200B;**dnsSuffix**&#x200B;を満たしたが&#x200B;**urlRegEx**&#x200B;を満たさない場合、次のレコードが調べられます。

例えば、ドメイン business.comのすべてのURLへのアクセスを許可するには、次の2つのレコードを定義できます。

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;http://.&#42;&quot;

かつ

dnsSuffix=&quot;business.com&quot; urlRegEx=&quot;https://.&#42;&quot;

デフォルト設定は次のとおりです。

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

**xtkJobs** ノードの様々なパラメーターを次に示します。 これは、サーバージョブの設定です。

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
   <td> サーバー処理のメモリ状態の更新期間（ミリ秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## アーカイブ {#archiving}

**アーカイブ** ノードの様々なパラメーターを次に示します。 これは、バックグラウンドで実行されるアーカイブ操作の設定です。

詳しくは、[電子メールアーカイブのアクティブ化（オンプレミス） &#x200B;](../../installation/using/email-archiving.md#activating-email-archiving--on-premise-)を参照してください。

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
   <td> 同時に処理するEMLの数<br /> </td> 
   <td> Long<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> archivingType<br /> </td> 
   <td> 送信メッセージのアーカイブ戦略（列挙）。 指定可能な値は、'0' （アーカイブなし）および'1' （送信されたメッセージのアーカイブをSMTP サーバーに転送）です。<br /> </td> 
   <td> バイト <br /> </td> 
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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> compressBatchSize<br /> </td> 
   <td> 圧縮アーカイブのサイズ：圧縮アーカイブ内のファイルの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 10000<br /> </td> 
  </tr> 
  <tr> 
   <td> compressionFormat<br /> </td> 
   <td> アーカイブ中に使用される圧縮形式（列挙）。 指定できる値は、'0' （圧縮なし）および'1' （送信されたメッセージをzip形式で圧縮する）です。<br /> </td> 
   <td> バイト <br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> expirationDelay<br /> </td> 
   <td> 未処理の電子メールの自動アーカイブまでの遅延時間：未処理の電子メールがアーカイブされるまでの日数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptのID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollDelay<br /> </td> 
   <td> 各更新イベント間の遅延（秒単位）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeArchivesDelay<br /> </td> 
   <td> 未処理の電子メールが削除されるまでの日数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 7<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> smtpBccAddress<br /> </td> 
   <td> ターゲットの宛先をアーカイブ中<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> smtpEnableTLS<br /> </td> 
   <td> SMTPS サポートの有効化：リモート サーバーでサポートされている場合、メールの配信をセーフモード （STARTTLS/SMTPS）で有効化します。<br /> </td> 
   <td> ブール値<br /> </td> 
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
   <td> 使用するSMTP リレーのDNS名またはIP アドレスのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> smtpRelayPort<br /> </td> 
   <td> SMTP サーバーのIP ポート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## inMail {#inmail}

**inMail** ノードの様々なパラメーターを次に示します。 これは、インバウンドメール管理モジュールの設定です。

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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> checkInstanceName<br /> </td> 
   <td> インスタンス名の確認：trueの場合、Message-ID ヘッダーに含まれるAdobe Campaign インスタンスの名前は、現在のインスタンスと同じである必要があります。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> defaultForwardAddress<br /> </td> 
   <td> 転送アドレス：デフォルトのメール転送アドレスは、ルールで処理されません。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> errorForwardAddress<br /> </td> 
   <td> エラーのアドレス：無効なメールの転送に使用されるデフォルトのアドレス（不正なMIME エンコーディング）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ignoreSize<br /> </td> 
   <td> メッセージサイズを無視：POP3 サーバーから返されるメッセージのサイズを無視するために使用されます。 この場合、モジュールはメッセージの最後に「。」を想定します。<br /> </td> 
   <td> ブール値<br /> </td> 
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
   <td> プロセスの開始時に実行するJavaScriptのID。<br /> </td> 
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
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
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
   <td> 読み取りメッセージのキューのサイズ <br /> </td> 
   <td> Long<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> popTimeoutSec<br /> </td> 
   <td> POP3 サーバーとの通信がタイムアウトしました。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriodSec<br /> </td> 
   <td> ポーリングするアカウントのデータベースのリロード頻度。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

### msgDump {#msgdump}

**inMail > msgDump** ノードで、次のパラメーターを設定します。 これは、処理済みメッセージのダンプの設定です。

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
   <td> すべてのインバウンドメッセージをテキスト形式で保存します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> msgPath<br /> </td> 
   <td> メッセージダンプパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '/tmp/inMail'<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 相互作用 {#interactiond}

**対話型** ノードの様々なパラメーターを次に示します。 これは、インバウンドインタラクションイベントの書き込みデーモンの設定です。

詳細については、[&#x200B; インタラクション – データバッファー](../../installation/using/interaction-data-buffer.md)を参照してください。

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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> callDataSize<br /> </td> 
   <td> 最大 通話データの共有メモリに保存されている文字数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセス開始時に実行するJavaScriptのID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedEntries<br /> </td> 
   <td> 最大 共有メモリに保存されているイベントの数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> nextOffersSize<br /> </td> 
   <td> 統計用に保存される、提案の直後に並べ替えられる対象オファーの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> statsPeriod<br /> </td> 
   <td> 応答時間統計の集計期間（秒）。 0は、統計ストレージが非アクティブ化されたことを意味します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> targetKeySize<br /> </td> 
   <td> 最大 個人を識別するために共有メモリに保存されている文字数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 16<br /> </td> 
  </tr> 
 </tbody> 
</table>

## MTA {#mta}

**mta** ノードの様々なパラメーターを次に示します。 これは、配信エージェントの設定です。

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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataLogPath<br /> </td> 
   <td> 送信されたメールのパスを保存：空でない場合、送信されたメールのすべてのソースファイルが保存されるパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> debugPath<br /> </td> 
   <td> ダンプディレクトリ：i空でない場合は、このディレクトリに送信されたメールメッセージのMIME エンベロープをコピーします。 トラブル撮影に使用されます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> dnsRequestLogDelayMs<br /> </td> 
   <td> DNS クエリ ログの遅延：ログを表示するまでの時間（ミリ秒単位）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> errorPeriodSec<br /> </td> 
   <td> エラー統計の頻度：統計の生成とデータベース内のストレージの間の時間。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptのID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> logEmailErrors<br /> </td> 
   <td> エラー統計を生成し、データベースに保存します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> logLevel<br /> </td> 
   <td> ログメッセージのレベルを表示します。 データベースに書き込まれたログの重大度レベル。 MTAによって生成されたログメッセージは、必ずしもデータベースに書き込まれるわけではありません。 このパラメーターを使用すると、メッセージをデータベースに書き込む必要があると考えるレベルを定義できます。 レベル 2を定義すると、レベル 1と0のメッセージも書き込まれます。一方、レベル 1を定義すると、レベル 1と0のメッセージのみが書き込まれます。 使用可能な値は、0 （エラー）、1 （警告）、2 （情報） <br />です </td> 
   <td> Long<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMemoryMb<br /> </td> 
   <td> Mta プロセスで使用できる最大メモリ サイズ （MB単位）。 この制限を超えると、使用するメモリがシステムに解放されるように、プロセスが再開されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> minConnectionsToLog<br /> </td> 
   <td> 考慮に入れるべき接続しきい値。 errorPeriodSecで指定された期間の合計接続数がしきい値よりも厳密に低い場合、特定のパスに対してエラー統計は生成されません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> minErrorsToLog<br /> </td> 
   <td> 考慮するエラーのしきい値：errorPeriodSecで指定された期間のエラーの合計数がしきい値よりも厳密に低い場合、特定のパスに対してエラー統計は生成されません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> minMessagesToLog<br /> </td> 
   <td> 考慮に入れるべきメッセージのしきい値。 errorPeriodSecで指定された期間に送信されたメッセージの合計数がしきい値よりも厳密に低い場合、特定のパスに対してエラー統計は生成されません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：通知のリレーに使用されるHostName:Port。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeDataLogDelay<br /> </td> 
   <td> アーカイブされた電子メールが削除されるまでの遅延時間：dataLogPathで指定されたディレクトリ内のアーカイブされた電子メールがパージされるまでの日数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
  <tr> 
   <td> retryLostMessages<br /> </td> 
   <td> 失ったメッセージの再試行：子プロセスが停止した場合、配信の一部が再試行されます。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> signEmailLinks<br /> </td> 
   <td> 署名メカニズムを有効にします。 これにより、電子メール内のトラッキングリンクのセキュリティが強化されます。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr>
  <tr> 
   <td> statServerAddress<br /> </td> 
   <td> 配信統計サーバーのアドレス。次のように指定します 
    &lt;dnsまたはip&gt; 
      <code>&lbrack;</code>: 
     &lt;port&gt; 
       <code>&rbrack;</code>. 参照 
      <a href="../../installation/using/email-deliverability.md#coordinates-of-the-statistics-server" target="_blank">統計サーバーの座標</a>。 
      <br /> 
     </td> 
   <td> 文字列<br /> </td> 
   <td> 定義されていない場合、既定のポートは7777です。<br /> </td> 
  </tr> 
  <tr> 
   <td> statServerTLSSupport<br /> </td> 
   <td> ドメイン別TLSを有効にする：MXで設定可能なTLSを有効にします（最新の統計サーバーが必要です）。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true <br /> </td> 
  </tr> 
  <!--
  tr> 
   <td> statServerVersion<br /> </td> 
   <td> Protocol version used: communication protocol version (1 for a v5.11 and 6.0.2 server, 2 for a v6.1 server).<br /> </td> 
   <td> String<br /> </td> 
   <td> If undefined, the latest version is used. <br /> </td> 
  </tr
  --> 
  <tr> 
   <td> useMomentum<br /> </td> 
   <td> 「true」に設定すると、インスタンスは<a href="../../delivery/using/sending-with-enhanced-mta.md" target="_blank">拡張MTA</a>.<br />を使用しています </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td>b 
  </tr>
  <tr> 
   <td> verifyMode<br /> </td> 
   <td> 検証モード：検証モードをアクティブ化します（メッセージの物理的な送信はありません。シミュレーションとテストに使用されます）。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> workingPath<br /> </td> 
   <td> 作業ディレクトリ：MTAが子プロセスとの通信に使用する一時ファイルの場所。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '$（XTK_INSTALL_DIR）/var/$（INSTANCE_NAME）/mta/' <br /> </td> 
  </tr> 
  <tr> 
   <td> xMailer<br /> </td> 
   <td> X-Mailer フィールド：SMTP メールヘッダーのフィールド 'X-Mailer'の値。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nlserver, ビルド $（PRODUCT_VERSION）'<br /> </td> 
  </tr>  
 </tbody> 
</table>

### キャッシュ {#cache}

**cache** ノードで、次のパラメーターを設定します。 これはローカルファイルキャッシュ設定です。

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
   <td> 後に再利用されます。保存容量を再利用するために、ファイルがキャッシュから自動的に削除されるまでの時間を秒単位で表します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 244800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSizeOnDiskMb<br /> </td> 
   <td> 最大キャッシュ サイズ （Mb）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> purgePeriodSec<br /> </td> 
   <td> パージ頻度：キャッシュ パージ メカニズムの実行間隔を秒単位で指定します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リレー {#relay}

**mta > relay** ノードで、次のパラメーターを設定します。 これは、メッセージ配信のためのメールサーバーの設定です。

リストは、MX DNS クエリによって返されるMXのリストと同じように処理されます。通常、最初のMXは使用可能な限り使用され、次のMXは使用されます。

詳細については、[SMTP リレー](../../installation/using/configuring-campaign-server.md#smtp-relay)を参照してください。

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
   <td> 使用するSMTP リレーのDNS名またはIP アドレスのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> SMTP サーバーのIP ポート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

### マスター {#master}

**mta > master** ノードで、次のパラメーターを設定します。 これはメインサーバーの設定です。

詳細については、この[&#x200B; セクション &#x200B;](../../installation/using/configuring-campaign-server.md#mta-child-processes)を参照してください。

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
   <td> 配信するジョブに対するデータベースポーリング頻度。 この値は、データベースのポーリング頻度（秒単位）を示します。 配信を待っているジョブのリストを取得するために、MTAはデータベースを定期的にポーリングします。 ジョブ待ちがない場合、ポーリング期間はこの値で定義されます。 そうでなければ、ジョブが子サーバーに転送された場合、このポーリング時間は自動的に1秒に短縮され、新しいジョブをできるだけ早く、つまり子サーバーが再び利用可能になるとすぐに再処理できます。 これは、子サーバーが再び利用可能になるまで、データベースクエリが1秒ごとに実行されることを意味しません。 実際、データベース アクセスは、少なくとも1つの子サーバーが使用可能になった場合にのみ実行されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> dataBaseRetryDelaySec<br /> </td> 
   <td> データベースへの接続の失敗後に待機する期間。 データベース接続の障害は、通常、データベース・サーバ自体が原因で発生します。 また、サーバーは、たとえばメンテナンス目的で停止することもできます。 DataBaseRetryDelay パラメーターは、データベース接続に失敗した場合の2回の接続試行間の期間を定義します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> domainKeysReloadPeriodSec<br /> </td> 
   <td> 秘密鍵のキャッシュの有効期間 (DomainKeys)。 DomainKeysの推奨事項（http://antispam.yahoo.com/domainkeys）に従って電子メールに署名するために使用される秘密鍵は、データベースにオプションとして保存されます。 domainKeysReloadPeriodSec パラメーターは、MTAがこれらのキーをキャッシュに保持できる秒数を定義します。 この遅延後、すべてのキーをデータベースから再読み込みする必要があります。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSpareServers<br /> </td> 
   <td> 子サーバーの最大数。 実行中のサーバーの最大数を表します。 この数は、サーバーメモリリソースとの最適な互換性で制限することをお勧めします。 これは配信中に確認できます。 使用されるメモリは、利用可能な物理メモリの3分の1を超えてはなりません。そうしないと、スワップが使用されます。 <a href="../../installation/using/configuring-campaign-server.md#mta-child-processes" target="_blank">MTA子プロセス </a>を参照してください。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> minSpareServers<br /> </td> 
   <td> 子サーバーの最小数。 MTAは、少なくともこの数のサーバーを稼働させようとしています。 少ない場合は、この値に達するまで、毎秒新しいサーバーを再起動します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> startSpareServers<br /> </td> 
   <td> 起動時の子サーバーの数。 子サーバーの数は動的に監視されます。MTAが開始されると、この値で示される数の子サーバーが作成されます。 通常、ホストリソースを保存するために、1秒あたり1台のサーバーよりも高速に子サーバーを起動することはできません。 ただし、MTAが開始されると、この制限は無効になり、できるだけ早く子サーバーを利用できるようになります。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
 </tbody> 
</table>

### 子 {#child}

**mta > child** ノードで、次のパラメーターを設定します。 これは子サーバーの設定です。

詳細については、[&#x200B; メール送信の最適化](../../installation/using/email-deliverability.md#email-sending-optimization)を参照してください。

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
   <td> オプションのコマンドライン引数<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> idleChildTimeoutSec<br /> </td> 
   <td> アイドル状態の子サーバーが停止するまで中断。 子サーバーのアイドル時間がこのパラメーターより大きい場合、ホスト リソースを解放するために自動的に自分自身を強制終了します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> maxAgeSec<br /> </td> 
   <td> 最大メッセージ保持時間。 調整が原因で準備されたメッセージを送信できなかったか、ターゲット MTAに接続できなかった場合、メッセージは破棄され、次の再試行時に処理されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxGCMConnectPerChild<br /> </td> 
   <td> 各子サーバーが開始したFCMに対する並列Http要求の最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
  <tr> 
   <td> maxMsgPerChild<br /> </td> 
   <td> 子サーバーごとの最大メッセージ数。 各MTAの子はこの数のメッセージを処理し、死ぬ。 MTA内のメモリまたはリソースのリークが無害である（通常は数千）ように数を指定することが重要です。 MTA コードに既知のメモリ リークがない場合でも、組み込まれたJavaScriptとXSL エンジンは完全に信頼できません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5000000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWaitingMessages<br /> </td> 
   <td> 保留中のメッセージ：メモリ内で配信を待機しているメッセージの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 2000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxWorkingSetMb<br /> </td> 
   <td> 子プロセスで使用できる最大メモリ サイズ （MB単位）。 この制限を超えると、プロセスは停止され、使用するメモリがシステムに解放されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 128<br /> </td> 
  </tr> 
  <tr> 
   <td> soapConnectorTimeoutSec<br /> </td> 
   <td> 配信コネクタのSOAP接続が破棄されるまでのタイムアウト （秒単位）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> startWithFirstMX<br /> </td> 
   <td> 常に最も優先度の高いMXで開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> timeToLive<br /> </td> 
   <td> 再開時の連続試行回数の最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 48<br /> </td> 
  </tr> 
 </tbody> 
</table>

**mta / 子 / smtp** ノードで、次のパラメーターを設定します。 これはSMTP セッションの設定です。

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
   <td> リモート サーバーでサポートされている場合、メールの配信をセーフモード （STARTTLS/SMTPS）でアクティブにします。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> idleSessionTimeoutSec<br /> </td> 
   <td> アイドルセッションがタイムアウトになりました。 このパラメーターは、セッションが特定のドメインに複数のメッセージを送信するために再利用される場合にのみ使用されます。 MTAがメッセージ送信を完了した場合、使用したSMTP セッションは体系的にクローズされません。 同じドメインにメッセージを送信する準備ができている場合、同じSMTP セッションが再利用されます。そのため、セッションは自動的に閉じません。 パラメーターIdleSessionTimeout パラメーターを使用すると、SMTP セッションが別のメッセージを待ってアクティブな状態を維持できる時間を定義できます。 期間が経過すると、セッションは自動的に閉じられます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> initialDelaySec<br /> </td> 
   <td> 接続を再試行する前の最初の遅延。 接続が失敗するたびに、この遅延は2倍になります。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSessionsPerChild<br /> </td> 
   <td> 子サーバーによる SMTP セッションの最大数。 メッセージを配信するために、MTAは受信者MTAとのSMTP接続を初期化します。 特定の子サーバーの同時SMTP セッションとアクティブ SMTP セッションの最大数は、この値によって制限されます。 この値にmaxSpareServersを掛けると、指定された子サーバーが同時に処理できるメッセージの最大数が得られます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

**mta / 子 / smtp / IPAffinity** ノードで、次のパラメーターを設定します。 これは、最適化された送信SMTP トラフィックのIP アドレスとのアフィニティの管理の設定です。

詳細については、[使用するIP アドレスのリスト &#x200B;](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)および[&#x200B; アフィニティを使用した送信SMTP トラフィックの管理](../../installation/using/configuring-campaign-server.md#managing-outbound-smtp-traffic-with-affinities)を参照してください。

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
   <td> 名前<br /> </td> 
   <td> 論理名：ユーザーによって親和性にリンクされた名前。 名前はセミコロンで区切られます。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

**mta / 子 / smtp / IP** ノードで、次のパラメーターを設定します。

詳しくは、[使用するIP アドレスのリスト &#x200B;](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)を参照してください。

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
   <td> 関連する物理アドレス。 例：'192.168.0.1'<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> publicId<br /> </td> 
   <td> 関連付けられた公開アドレス ID。 統計サーバーのキーとして使用されます。 数値にする必要があります。 この<a href="../../installation/using/email-deliverability.md#managing-ip-addresses"> セクション </a>を参照してください。<br /> </td> 
   <td> Long<br /> </td> 
  </tr> 
  <tr> 
   <td> 重み付け<br /> </td> 
   <td> このIPの使用頻度を他のIPに対して指定します（重みが大きいほど使用頻度が高くなります）。<br /> </td> 
   <td> Long<br /> </td> 
  </tr> 
  <tr> 
   <td> includeDomains<br /> </td> 
   <td> 含めるドメイン マスクのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> excludeDomains<br /> </td> 
   <td> 除外するドメイン マスクのコンマ区切りリスト。<br /> </td> 
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

**nmac** ノードの様々なパラメーターを次に示します。 これは、プッシュ通知配信の設定です。

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
   <td> shared/proxyHTTPで定義されたHTTP プロキシを使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### リレー {#relay-1}

**nmac > relay** ノードの様々なパラメーターを次に示します。 これにより、メッセージ配信にリレー（ios http2 コネクタ）を使用するように設定されます。

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
   <td> 使用するリレーのDNS アドレスまたは名前。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> リレーポート <br /> </td> 
   <td> Long<br /> </td> 
   <td> 443<br /> </td> 
  </tr> 
  <tr> 
   <td> trustedCertsChain<br /> </td> 
   <td> 証明書チェーン （PEM ファイル）。 モックサーバーを使用する場合に便利です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## パイプライン化 {#pipelined}

**パイプライン化された** ノードの様々なパラメーターを次に示します。 これは、パイプラインサービスのイベント処理モジュールの設定です。

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
   <td> 公開鍵の保存時にDeveloper接続で生成されるアプリケーションの名前。<br /> </td> 
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
   <td> ゲートウェイ トークンを取得するURL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://api.omniture.com' <br /> </td> 
  </tr> 
  <tr> 
   <td> authPrivateKey<br /> </td> 
   <td> トークンを取得するための秘密鍵（XtkKey オプションを使用してAESで暗号化）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> autoStart<br /> </td> 
   <td> 自動開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> disableAuth<br /> </td> 
   <td> 認証を無効にする：認証なしでPipeline Servicesに接続します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> discoverPipelineEndpoint<br /> </td> 
   <td> パイプラインサービス URLを検索するURL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'https://producer-pipeline-pnw.adobe.net'<br /> </td> 
  </tr> 
  <tr> 
   <td> dumpStatePeriodSec<br /> </td> 
   <td> ステータス保存期間：プロセスの内部情報がファイルに保存される頻度。 0. <br />の場合は非アクティブ </td> 
   <td> Long<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> forcedPipelineEndpoint<br /> </td> 
   <td> リスニング URL: パイプラインサービスのリスニング URLを強制的に指定します。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptのID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> monitorServerPort<br /> </td> 
   <td> ステータスサーバーポート：プロセスのステータスをクエリできるHTTP サーバーポート。 0.<br />の場合は非アクティブ </td> 
   <td> Long<br /> </td> 
   <td> 7781<br /> </td> 
  </tr> 
  <tr> 
   <td> pointerFlushMessageCount<br /> </td> 
   <td> このメッセージ数が処理されるたびに、ポインターがデータベースに保存されます。<br /> </td> 
   <td> <br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> pointerFlushPeriodSec<br /> </td> 
   <td> ポインターを保存するまでの遅延時間：ポインターはこの期間に少なくとも1回はデータベースに保存されます（アクティビティが少ない場合に便利です）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> processingJSThreads<br /> </td> 
   <td> パーソナライズされたJavaScript コネクタを使用したイベント処理のスレッド数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> processingThreads<br /> </td> 
   <td> イベント処理のスレッド数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> retryPeriodSec<br /> </td> 
   <td> エラーが発生した場合の処理の間の遅延。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> retryValiditySec<br /> </td> 
   <td> この期間の後に破棄：この期間の後も処理が失敗している場合は、イベントを放棄します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 修復 {#repair}

**修復** ノードの様々なパラメーターを次に示します。 これは、データベース修復モジュールの設定です。

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
   <td> 配信アクション修復モジュール：配信アクションを修復モジュールで処理できるまでの遅延（分単位）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
 </tbody> 
</table>

## securityZone {#securityzone}

**securityZone** ノードの様々なパラメーターを次に示します。

詳細については、[&#x200B; セキュリティゾーンの定義](../../installation/using/security-zones.md)を参照してください。

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
   <td> Web アプリケーションのデバッグモードを承認します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowEmptyPassword<br /> </td> 
   <td> パスワードなしでアプリケーションを使用することをユーザーに許可します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowHTTP<br /> </td> 
   <td> オペレーターのログオンにHTTPを使用することを許可します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowSQLInjection<br /> </td> 
   <td> 式でのSQLDATAの使用を許可します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> allowUserPassword<br /> </td> 
   <td> ユーザー/パスワード セッション トークンを承認します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> ラベル <br /> </td> 
   <td> ラベル <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewLabel （） <br /> </td> 
  </tr> 
  <tr> 
   <td> 名前<br /> </td> 
   <td> 内部名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewName （） <br /> </td> 
  </tr> 
  <tr> 
   <td> sessionTokenOnly<br /> </td> 
   <td> セキュリティ トークンを使用しないでください。<br /> </td> 
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

デフォルト設定は次のとおりです。

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

**securityZone > subNetwork** ノードの様々なパラメーターを次に示します。

詳細については、[&#x200B; セキュリティゾーンの定義](../../installation/using/security-zones.md)を参照してください。

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
   <td> 名前<br /> </td> 
   <td> 内部名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> NewName （） <br /> </td> 
  </tr> 
  <tr> 
   <td> プロキシ <br /> </td> 
   <td> このサブネットワークがインスタンスにアクセスするために使用する（逆方向）プロキシのマスクまたはアドレス。 この場合、このプロキシの代わりに'X-Forwarded-For' ヘッダーがテストされます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 127.0.0.1 <br /> </td> 
  </tr> 
 </tbody> 
</table>

## SMS {#sms}

**sms** ノードの様々なパラメーターを次に示します。 これは、インバウンド SMS管理モジュールの設定です。

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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> dataRetentionDays<br /> </td> 
   <td> SMPP コネクタによって保存されているファイルを操作する最大日数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> dataSizeMo<br /> </td> 
   <td> SMPP作業ファイルの最大サイズ （MB）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 512<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptのID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> keepAlivePeriod<br /> </td> 
   <td> セッション継続性フレームの繰り返し：最大。 受信セッションがまだ有効であることを通知するための2つのフレーム間の期間（秒単位）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> pollPeriod<br /> </td> 
   <td> 検索頻度：SMS アカウントのアンケート期間。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> reloadPeriod<br /> </td> 
   <td> アカウント リロード頻度：ポーリングするアカウントのデータベース リロード頻度。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> srReadDelay<br /> </td> 
   <td> SR処理の遅延秒数：現在の時刻より前の回復日を持つSRのみが、srReadDelayによって指定された秒数を差し引きます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト <br /> </td> 
   <td> SMS ゲートウェイとの通信がタイムアウトしました。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
 </tbody> 
</table>

### netsize {#netsize}

**sms > netsize** ノードの様々なパラメーターを次に示します。

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
   <td> Netsizeとの接続を確立する際のタイムアウト （秒）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 統計 {#stat}

**stat** ノードの様々なパラメーターを次に示します。 これは、MTA統計モジュールの設定です。

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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptのID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> ポート <br /> </td> 
   <td> サーバーリスニングポート。 この<a href="../../installation/using/email-deliverability.md#definition-of-the-server-port"> セクション </a>を参照してください。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## syslogd {#syslogd}

**syslogd** ノードの様々なパラメーターを次に示します。 これは、ログ管理モジュールの設定です。

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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptのID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxFileSizeMb<br /> </td> 
   <td> ログファイルの最大サイズ （Mb）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> maxNumberOfLoginsFiles<br /> </td> 
   <td> 保持するlogins.log ファイルの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 365<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## tracking {#tracking}

**トラッキング** ノードの様々なパラメーターを次に示します。 これはトラッキングサーバーの設定です。

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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> blockRedirectForUnsignedTrackingLink<br /> </td> 
   <td> 以前のビルドから生成された形式が正しくないURLを無効にします。<br /> </td> 
   <td> ブール値<br /> </td> 
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
   <td> 重複しない開封：重複する開封トラッキングログを削除して、Outlookなどのメールリーダーでのメールプレビューの影響を制限します。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePercent<br /> </td> 
   <td> エラーの最大X%を無視：まだ考慮されていない仕訳の比率がこの値に達しない限り、トラッキングインジケーターを更新しないでください。<br /> </td> 
   <td> バイト <br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> errorIgnorePeriod<br /> </td> 
   <td> エラーインジケーターの更新：エラーインジケーターが再計算されるまでの最大期間。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> indicatorsDuration<br /> </td> 
   <td> 計算中の指標：配信の有効期間が終了した後、統合指標が計算されなくなった期間。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 2592000<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセス <br />の開始時に実行するJavaScriptのID </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> logCountPerRequest<br /> </td> 
   <td> リモート トラッキング サーバーへの呼び出しによって要求されたログの数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> phishbowlServiceAPIKey<br /> </td> 
   <td> Phishbowl サービスエンドポイント統合用のAPI キー。 これにより、古いビルドから生成された形式が正しくないURLのリダイレクトが保護されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> phishbowlServiceEndpoint<br /> </td> 
   <td> Phishbowl サービスエンドポイント統合のエンドポイント。 これにより、古いビルドから生成された形式が正しくないURLのリダイレクトが保護されます。<br /> </td> 
   <td> Long<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePercent<br /> </td> 
   <td> トラッキングの最大X%を無視：まだ考慮されていない仕訳の比率がこの値に達しない限り、トラッキング指標を更新しません。<br /> </td> 
   <td> バイト <br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingIgnorePeriod<br /> </td> 
   <td> トラッキングインジケーターの更新：トラッキングインジケーターが再計算されるまでの最大期間。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> userAgentCacheSize<br /> </td> 
   <td> ブラウザー識別子キャッシュのサイズ。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## trackinglogd {#trackinglogd}

**trackinglogd** ノードの様々なパラメーターを次に示します。 これは、トラッキングログ書き込みデーモンの設定です。

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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセス <br />の開始時に実行するJavaScriptのID </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxCreateFileRetry<br /> </td> 
   <td> 書き込み再試行の最大数：ログファイルに書き込みエラーが発生した場合に作成できるファイルの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> maxLogsSizeOnDiskMb<br /> </td> 
   <td> 最大ログサイズ：ディスク上のログで使用される最大容量（MB単位）。 100 MB未満である可能性があります。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> maxSharedLogs<br /> </td> 
   <td> 最大ログ数：共有メモリに保存されるログの最大数。 10000未満にすることはできません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> purgeLogsPeriod<br /> </td> 
   <td> パージ前のログ数：ログファイルのパージを開始する前に挿入されたログの数。 50000<br />より小さくすることはできません </td> 
   <td> Long<br /> </td> 
   <td> 50000<br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> webTrackingParamSize<br /> </td> 
   <td> 追加のWeb トラッキング パラメーター用に共有メモリに保存できる最大文字数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 64<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Web {#web}

**web** ノードの様々なパラメーターを次に示します。 これは、Web モジュールの設定です。

詳細については、この[&#x200B; セクション &#x200B;](configuring-campaign-server.md#default-port-for-tomcat)を参照してください。

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
   <td> 文字列として渡されたJVMのオプション。<br /> </td> 
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
   <td> 最小スレッド数。<br /> </td> 
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
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> controlPort<br /> </td> 
   <td> Tomcat リスニング制御ポート：<a href="configure-tomcat.md" target="_blank">Tomcatの設定</a>を参照してください。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 8005<br /> </td> 
  </tr> 
  <tr> 
   <td> httpPort<br /> </td> 
   <td> Tomcat HTTP リスニングポート：<a href="configure-tomcat.md" target="_blank">Tomcatの設定</a>を参照してください。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 8080<br /> </td> 
  </tr> 
  <tr> 
   <td> initScript<br /> </td> 
   <td> プロセスの開始時に実行するJavaScriptのID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxDeliveryQueueSize<br /> </td> 
   <td> SubmitDelivery呼び出しのキューのサイズ：キューに追加できるSubmitDelivery SOAP呼び出しの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 50<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：HostName:Portで通知のリレーを有効にしています。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> startSoapRouterInModule<br /> </td> 
   <td> SOAP ルータをモジュールモードで起動します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### jsp {#jsp}

**web > jsp** ノードの様々なパラメーターを次に示します。 これは、JSPで使用されるパラメーターの設定です。

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
   <td> デバッグモードでJSPを実行するかどうか。<br /> </td> 
   <td> ブール値<br /> </td> 
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
   <td> SOAP ルーターのURL （http://myserver/xxx、http://jniまたはmailto:xxx）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'http://jni'<br /> </td> 
  </tr> 
 </tbody> 
</table>

**web > jsp > classpath** ノードには、JVMの起動時に使用するすべてのクラスパスのリストが含まれています。 デフォルト設定は次のとおりです。

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

**web > jssp** ノードの様々なパラメーターを次に示します。 これは、JSSPで使用されるパラメーターの設定です。

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
   <td> 各クエリの後に、JavaScript コンテキストのガベージコレクターを有効にします。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> timeToLive<br /> </td> 
   <td> JavaScript コンテキストで提供されるページの最大数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

**web > jsp > classpath** ノードには、JVMの起動時に使用するすべてのクラスパスのリストが含まれています。

### リレー {#relay-2}

**web > リレー** ノードの様々なパラメーターを次に示します。 これは、2つのゾーン間のHTTP リクエストのリレーの設定です。

詳細については、この[&#x200B; セクション &#x200B;](../../installation/using/deploying-an-instance.md#synchronizing-public-resources)を参照してください。

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
   <td> Web サーバー内のHTTP リレーモジュールをデバッグモードで開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInAuthority<br /> </td> 
   <td> 禁止されている文字（ドメイン）: URIの「権限」セクション内の禁止されている文字のリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.?#@/:' <br /> </td> 
  </tr> 
  <tr> 
   <td> forbiddenCharsInPath<br /> </td> 
   <td> 禁止されている文字（パス）: URIの「パス」セクション内の禁止されている文字のリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '?#/'<br /> </td> 
  </tr> 
  <tr> 
   <td> modDir<br /> </td> 
   <td> 「mod_dir」モジュールオプションの値：フォルダー上のクエリ中に使用されるファイルのリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'index.md' <br /> </td> 
  </tr> 
  <tr> 
   <td> startRelay<br /> </td> 
   <td> HTTP リレーモジュールを開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> startRelayInModule<br /> </td> 
   <td> Web サーバー内でHTTP リレーモジュールを開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト <br /> </td> 
   <td> 禁止されたURLを削除するまでの待機時間です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '60'<br /> </td> 
  </tr> 
 </tbody> 
</table>

次のパラメーターを使用して、リレー（順序を挿入して優先順位を定義）するURLごとに&#x200B;**web/リレー/url** ノードを追加します。

詳細については、[動的ページセキュリティおよびリレー](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays)および[&#x200B; セクション &#x200B;](../../installation/using/deploying-an-instance.md#synchronizing-public-resources)を参照してください。

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
   <td> 承認済みIP：このマスクにリレーを使用できるソース IP アドレスのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> 拒否<br /> </td> 
   <td> これらのURLへのアクセスを拒否します（HTTP 403 エラーを返します） <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> hostMask<br /> </td> 
   <td> リレーするDNS エイリアス：リレーするDNS エイリアス マスクのコンマ区切りリスト （例：'*.adobe.com'）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> httpAllowed<br /> </td> 
   <td> セキュリティゾーン（webAppsなど）に関係なく、HTTP アクセスが許可されています。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayHost<br /> </td> 
   <td> 元のホストを追加：リレー時に元のリクエストのHTTP 'Host' ヘッダーを使用します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> relayPath<br /> </td> 
   <td> 最初のURL パスを追加：ターゲットページのURLにリレーするURLの完全なパスを追加します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ステータス <br /> </td> 
   <td> パブリックリソースの同期ステータス（列挙）。 使用可能な値は、「normal」（通常の実行）、「blacklist」（エラー404の場合はURLがブロックリストに追加）、「spare」（既存の場合は予備サーバーにファイルアップロード）です。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 標準<br /> </td> 
  </tr> 
  <tr> 
   <td> targetUrl<br /> </td> 
   <td> ターゲットページのURL: <a href="configure-tomcat.md" target="_blank">Tomcatの設定</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト <br /> </td> 
   <td> リレー中のリクエストの最大実行時間（秒単位）。<br /> </td> 
   <td> Long<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> urlPath<br /> </td> 
   <td> 中継するURLのマスク （例：'/nl*'、'*.jsp'）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルト設定は次のとおりです。

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

各HTTP ヘッダーに&#x200B;**web/リレー/responseHeader** ノードを追加して、リレーに転送される返信に追加します。

詳細については、[HTTP ヘッダーの管理](../../installation/using/configuring-campaign-server.md#managing-http-headers)を参照してください。

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
   <td> ヘッダー値<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

デフォルト設定は次のとおりです。

```
<responseHeader name="X-XSS-Protection" value="1; mode=block"/>
```

### リダイレクト {#redirection}

**web > リダイレクト** ノードの様々なパラメーターを次に示します。 これは、リダイレクトモジュールの設定です。

詳細については、この[&#x200B; セクション &#x200B;](../../installation/using/deploying-an-instance.md#synchronizing-public-resources)を参照してください。

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
   <td> 組織ID: Adobe Experience Cloud内の一意の組織ID。特にVisitorID サービスとIMS SSOに使用されます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> P3PCompactPolicy<br /> </td> 
   <td> 永続的なCookieに使用されるポリシーを表す値（P3P コンパクトポリシー形式に準拠）。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'CAO DSP COR CURa DEVa TAIa OUR BUS IND UNI COM NAV'<br /> </td> 
  </tr> 
  <tr> 
   <td> cookieDomain<br /> </td> 
   <td> Cookieを設定するドメインを明示的に示すように設定するドメインのコンマ区切りリスト。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> databaseId<br /> </td> 
   <td> トラッキングインスタンスに関連付けられているデータベース ID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> defLogCount<br /> </td> 
   <td> 呼び出しによるログ数：メソッド GetTrackingLogsの呼び出し時にデフォルトで返されるログの数。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> 有効期限URL<br /> </td> 
   <td> 期限切れリダイレクトのページ：配信アクションのリダイレクトが期限切れになったときに、リダイレクションサーバーがデフォルトで使用するWeb ページのURL。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxJobsInCache<br /> </td> 
   <td> 最大ジョブ数：キャッシュ内の配信アクションの最大数。 50より小さくすることはできません。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> showSourceIP<br /> </td> 
   <td> falseに設定すると、r/testによって返される応答のsourceIPの値は空の文字列になります。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> startRedirection<br /> </td> 
   <td> リダイレクト サービスを開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> startRedirectionInModule<br /> </td> 
   <td> モジュールモードでリダイレクションサービスを開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> trackWebVisitors<br /> </td> 
   <td> Web トラッキング：未知のユーザーが訪問したページのログの作成。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> trackingPassword<br /> </td> 
   <td> リダイレクト サーバーで使用されるパスワード。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

**web/リダイレクト/spareServer** ノードの様々なパラメーターを次に示します。

詳細については、[冗長トラッキング &#x200B;](../../installation/using/configuring-campaign-server.md#redundant-tracking)を参照してください。

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
   <td> 次の場合に考慮します。式がtrueを返す場合、トラッキングサーバーが考慮されます。<br /> </td> 
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
   <td> 追加リダイレクションサーバーURL <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

### spamCheck {#spamcheck}

**web > spamCheck** ノードの様々なパラメーターを次に示します。 これは、メールの迷惑メールスコアリング対策の評価パラメーターの設定です。

詳細については、[SpamAssassinの設定](../../installation/using/configuring-spamassassin.md)を参照してください。

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
   <td> 電子メールのスパム対策スコアを評価するために実行するコマンド （例：'perl spamcheck.pl'）。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## wfserver {#wfserver}

**wfserver** ノードの様々なパラメーターを次に示します。 これはワークフロープロセスの設定です。

詳細については、[高可用性ワークフローと親和性](../../installation/using/configuring-campaign-server.md#high-availability-workflows-and-affinities)を参照してください。

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
   <td> 親和性<br /> </td> 
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
   <td> ブール値<br /> </td> 
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
   <td> プロセスの開始時に実行するJavaScriptのID。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryAlertMb<br /> </td> 
   <td> メモリ消費アラート：特定のプロセスで消費されたRAMの量（Mb）に関するアラート。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> maxProcessMemoryWarningMb<br /> </td> 
   <td> メモリ消費に関する警告：特定のプロセスで消費されるRAMの量（Mb）に関する警告。<br /> </td> 
   <td> Long<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> notifRelay<br /> </td> 
   <td> 通知リレー：HostName:Portで通知のリレーを有効にしています。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> processRestartTime<br /> </td> 
   <td> プロセスが自動的に再起動される時刻。 <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank">自動プロセス再起動</a>を参照してください。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> runLevel<br /> </td> 
   <td> 開始時の優先度。 優先度の低いモジュールは、最初に開始され、最後に停止されます。 したがって、syslogd モジュールの優先度は0である必要があります。<br /> </td> 
   <td> 短い<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>
