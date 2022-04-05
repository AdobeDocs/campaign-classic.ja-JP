---
product: campaign
title: サーバー設定ファイル
description: サーバー設定ファイル
audience: installation
content-type: reference
topic-tags: appendices
exl-id: 70cd6a4b-c839-4bd9-b9a7-5a12e59c0cbf
source-git-commit: f4513834cf721f6d962c7c02c6c64b2171059352
workflow-type: tm+mt
source-wordcount: '7961'
ht-degree: 39%

---

# サーバー設定ファイル{#the-server-configuration-file}

![](../../assets/v7-only.svg)

************

>[!NOTE]
>
>Server-side configurations can only be performed by Adobe for deployments hosted by Adobe. [](../../installation/using/hosting-models.md)[](../../installation/using/capability-matrix.md)[](../../installation/using/hosting-models.md)

**** These are related to the instance. They are potentially used by all the nlserver commands (nlserver web, nlserver wfserver, etc.). The other sections are related to a specific nlserver sub-command.

****

* [認証](#authentication)
* [dataStore](#datastore)
* [dnsConfig](#dnsconfig)
* [exec](#exec)
* [htmlToPdf](#htmltopdf)
* [ims](#ims)
* [javaScript](#javascript)
* [mailExchanger](#mailexchanger)
* [module](#module)
* [monitoring](#monitoring)
* [ooconv](#ooconv)
* [proxyConfig](#proxyconfig)
* [threadPool](#threadpool)
* [urlPermission](#urlpermission)
* [xtkJobs](#xtkjobs)

****

* [archiving](#archiving)
* [inMail](#inmail)
* [interactiond](#interactiond)
* [MTA](#mta)
* [nmac](#nmac)
* [pipelined](#pipelined)
* [repair](#repair)
* [securityZone](#securityzone)
* [SMS](#sms)
* [stat](#stat)
* [syslogd](#syslogd)
* [tracking](#tracking)
* [trackinglogd](#trackinglogd)
* [Web](#web)
* [wfserver](#wfserver)

## 認証 {#authentication}

****

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
   <td> <br /> </td> 
   <td> IP アドレス検査を有効にする.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> デフォルトの識別モード.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'nl'<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1296000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
 </tbody> 
</table>

### XTK {#xtk}

****

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
   <td> <br /> </td> 
   <td> 内部アカウントのパスワード.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## dataStore {#datastore}

**** This is where the server data sources are defined.

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Form cache expiration delay: timeout in seconds after which a cache entry is invalidated. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> DNS masks: list of DNS masks that this instance serves (comma separated, can use * and ? <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '*'<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Interaction JSSP cache expiration delay: timeout in seconds after which a cache entry is invalidated. A negative value means that the cache is always invalidated. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Instance language (enumeration). <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 'en_US'<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> ダウンロードを許可されたファイル (「,」区切り)。この文字列は Java の有効な正規表現である必要があります。<a href="file-res-management.md" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.+' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Vault の秘密鍵のパス<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Vault トークンを含むファイルのローカルパス. <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> HashiCorp Vault の URL <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Validity period of view cache: timeout in seconds after which a cache entry is invalidated. A negative value means that the cache is always invalidated. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 作業ディレクトリの XPath。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> workingDirectory : XPath of the working directory. <br /> </td> 
  </tr> 
 </tbody> 
</table>

### proxyAdjust {#proxyadjust}

**** URLs matching the regular expression are regenerated based on the URL defined in urlBase.

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
   <td> <br /> </td> 
   <td> 外部 URL の生成時に使用するベース。例 : https://server.domain.com<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> URL を照合する正規表現。例 : http://server\.lan\.net.*<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

### dataSource {#datasource}

****

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
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> デフォルト<br /> </td> 
  </tr> 
 </tbody> 
</table>

****

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
   <td> <br /> </td> 
   <td> Unicode ストレージ<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> ワークスペース<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 暗号化されたパスワード<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> アカウント<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> パスワード<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> プロバイダー<br /> </td> 
   <td> Type (enumeration). <br /> </td> 
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
   <td> <br /> </td> 
   <td> <a href="../../installation/using/time-zone-management.md" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> データベースの Unicode データ<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <a href="../../installation/using/time-zone-management.md" target="_blank"></a><br /> </td> 
   <td> ブール値<br /> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

****

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
   <td> <br /> </td> 
   <td> 関数のプレフィックス<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

****

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
   <td> <br /> </td> 
   <td> 接続の有効性チェック処理間の遅延。<br /> </td> 
   <td> ショート<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> プールに保存されている空き接続数.<br /> </td> 
   <td> ショート<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 新しい接続を拒否する前に許可された接続の最大数。<a href="https://helpx.adobe.com/campaign/kb/how-to-increase-the-maximum-number-of-database-connections-from-.html"></a><br /> </td> 
   <td> ショート<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 接続の最大アイドル時間。0 はデフォルト値です.<br /> </td> 
   <td> ショート<br /> </td> 
  </tr> 
 </tbody> 
</table>

### virtualDir {#virtualdir}

**** This is the configuration of the virtual directory to real directory mapping.

[](file-res-management.md)

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
   <td> <br /> </td> 
   <td> 実際のディレクトリのフルパス<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

Here is the default configuration:

```
<virtualDir name="images" path="$(XTK_INSTALL_DIR)/var/res/img/"/>
<virtualDir name="formCache" path="$(XTK_INSTALL_DIR)/var/$(INSTANCE_NAME)/formCache/"/>
<virtualDir name="publicFileRes" path="$(XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)"/>
```

### preprocessCommand {#preprocesscommand}

**** These are the authorized commands for pre-processing of the &#39;Load file&#39; workflow activity.

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
   <td> <br /> </td> 
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

Here is the default configuration:

```
<preprocessCommand command="" label="None" name="none"/>
<preprocessCommand command="zcat &quot;$fileName&quot;" label="Decompression" name="zcat"/><preprocessCommand command="gpg --decrypt &quot;$fileName&quot;" label="Decrypt" name="gpg"/>
```

## dnsConfig {#dnsconfig}

****

[](../../installation/using/configuring-campaign-server.md)

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
   <td> <br /> </td> 
   <td> Domain name: default domain name. Used by the SMTP HELO command. <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> DNS server: comma separated list of domain name servers (DNS). <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> DNS クエリの再試行数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト<br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5000<br /> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>****
>parameters of the first network interface declared in Windows
>not defined in UNIX. Defines the domain name servers (DNS)
>used by the MTA to get the Mail Exchanger declared for
>a domain.
>
>If this value is not defined, the MTA seeks this information in the host network configuration. If several DNS are possible, the different DNS addresses must be separated by a comma (example: 212.155.207.1,212.155.207.2). If your delivery server has several network interfaces, the DNS list used by the MTA is the first one. ****

>[!CAUTION]
>
>If your network host configuration uses DHCP, the MTA will not find the DNS list provided by DHCP. In this case, we recommend specifying the DNS list in the network parameters of the Windows control panel.

## exec {#exec}

****

[](../../installation/using/configuring-campaign-server.md#restricting-authorized-external-commands)

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
   <td> <br /> </td> 
   <td> <br /> </td> 
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

**** This is the configuration of the service for converting web pages into PDF documents.

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 最大<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Tool to use for the conversion. <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト<br /> </td> 
   <td> Timeout for a conversion: maximum conversion time in seconds. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 120<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Delay when waiting for a process: delay in seconds, when all processes are used at the same time and when waiting for a process to free up. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
 </tbody> 
</table>

Example for phantomjs:

```
phantomjs - -ignore-ssl-errors=true '$(XTK_INSTALL_DIR)/bin/htmlToPdf.js' '-out:{outPdf}' '-post:{postFile}' '-url:{originUrl}' -sessiontoken:{sessiontoken} -format:{format} -orientation:{orientation} -marginTop:{marginTop} -marginLeft:{marginLeft} -marginRight:{marginRight} -marginBottom:{marginBottom}
```

## ims {#ims}

****[](../../integrations/using/about-adobe-id.md)

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
   <td> <br /> </td> 
   <td> クライアント ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 秘密鍵 (AES で暗号化)<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 承認コード (AES で暗号化)<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> IMS サーバー URL<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> テクニカルアカウントクライアント ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> テクニカルアカウント秘密鍵 (AES で暗号化)<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> テクニカルアカウント ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> テクニカルアカウント秘密鍵 (AES で暗号化)<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## JavaScript {#javascript}

**** This is the configuration of the JavaScript interpreter.

[](../../reporting/using/actions-on-reports.md#memory-allocation)

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 512 <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Size of each stack chunk in kilo octets. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
 </tbody> 
</table>

## mailExchanger {#mailexchanger}

**** This is the configuration of the SMTP server.

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> E メール転送に使用される SMTP サーバーの TCP ポート。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## module {#module}

**** This is the configuration for the namespaces restrictions module xtk.

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
   <td> <br /> </td> 
   <td> 新しいエンティティの作成時に使用されるデフォルトの名前空間.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## monitoring {#monitoring}

**** This is the monitoring service configuration.

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 監視サービスにより実行される Unix スクリプト.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 監視サービスにより実行される Windows スクリプト.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## ooconv {#ooconv}

**** This is the configuration of the document conversion server.

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
   <td> <br /> </td> 
   <td> OpenOffice サーバーでの実行が許可されたコンバージョンの最大数です。この数を超えると、サーバーは再起動されます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> OpenOffice サーバーが強制終了するまでの最大アイドル時間。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 7200<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> OpenOffice サーバーがリスニングしているポートの間隔.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 8101-8110<br /> </td> 
  </tr> 
  <tr> 
   <td> url<br /> </td> 
   <td> 文書変換サーバーの URL.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## proxyConfig {#proxyconfig}

**** This is the configuration of proxy parameters.

[](file-res-management.md)

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
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### HTTP Proxy / Secure proxy {#http-proxy---secure-proxy-}

****

[](file-res-management.md)

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
   <td> <br /> </td> 
   <td> プロキシサーバーのアドレス<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> プロキシサーバーに接続するためのログイン<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
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

****

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## urlPermission {#urlpermission}

**** This is the list of URLs that the Javascript code can access.

List of domains and regular expressions specifying whether a URL encountered in the Javascript code can or cannot be used by the Adobe Campaign server.

If the URL cannot be found, the default action is carried out, according to the default mode specified.

[](../../installation/using/configuring-campaign-server.md#url-permissions)

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
   <td> <br /> </td> 
   <td> Default action if the URL is not in the authorized list (enumeration). <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### url {#url}

****

[](../../installation/using/configuring-campaign-server.md#url-permissions)

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
   <td> <br /> </td> 
   <td> Domain name, or domain parent, concerned by the URL: all or part of the URL's domain to verify, to accelerate the verification. <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

********

For example, to authorize access to all of the URLs of the domain business.com, we can define two records:

&#42;

および 

&#42;

Here is the default configuration:

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

**** This is the configuration of the server jobs.

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
   <td> <br /> </td> 
   <td> サーバー処理のメモリステータスの更新期間 (ms).<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## archiving {#archiving}

**** This is the configuration of the executed archiving operations in the background.

[](../../installation/using/email-archiving.md#activating-email-archiving--on-premise-)

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
   <td> <br /> </td> 
   <td> 同時に処理する EML の数<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Archiving strategy of sent messages (enumeration). <br /> </td> 
   <td> バイト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 10000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Compression format used during archiving (enumeration). <br /> </td> 
   <td> バイト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 未処理の E メールが削除されるまでの日数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 7<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> アーカイブ SMTP サーバーへの接続数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> SMTP サーバーの IP ポート。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
 </tbody> 
</table>

## inMail {#inmail}

**** This is the configuration of the inbound Email management module.

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
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Ignore message size: is used to ignore the size of a message returned by POP3 servers. In this case, the module expects a '.' <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 20<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> POP3 セッションで読み取るメッセージの最大数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 200<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 読み取りメッセージのキューサイズ<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> ポーリングするアカウントのデータベース再読み込み頻度。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

### msgDump {#msgdump}

**** This is the configuration of the dump of processed messages.

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> メッセージダンプのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## interactiond {#interactiond}

**** This is the configuration of the write daemon for inbound Interaction events.

[](../../installation/using/interaction---data-buffer.md)

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
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 最大<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 最大<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 提案直後に並べ替えられ、統計用に保存される適格オファーの最大数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Aggregation duration in seconds for the response time statistics. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 最大<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 16<br /> </td> 
  </tr> 
 </tbody> 
</table>

## MTA {#mta}

**** This is the configuration of delivery agents.

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
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Dump directory:iIf not empty, copy MIME envelopes of sent mail messages in this directory. <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> エラー統計を生成してデータベースに保存します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> ログメッセージのレベルを表示します。Severity level of the logs written in the database. Log messages generated by the MTA are not all always written in the database. With this parameter, you can define the level from which you consider a message must be written in the database. If you define level 2, messages of level 1 and 0 are also written, whereas if you define level 1, only messages of level 1 and 0 are written. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> MTA プロセスが使用できる最大メモリサイズ (MB)。この制限を超えると MTA プロセスが再起動され、使用しているメモリはシステムに解放されます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 考慮する接続しきい値. errorPeriodSec で指定される期間の接続の合計数がしきい値よりも厳密に低い場合、エラー統計は指定のパスに対して生成されません。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 考慮するメッセージしきい値. errorPeriodSec で指定する期間に送信されたメッセージの合計数が厳密にはしきい値を下回る場合、指定されたパスに対するエラー統計は生成されません。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 15<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Enable the signature mechanism. <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr>
  <tr> 
   <td> <br /> </td> 
   <td> <code>[</code><code>]</code><a href="../../installation/using/email-deliverability.md#coordinates-of-the-statistics-server" target="_blank"></a><br /> 
     </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <a href="../../delivery/using/sending-with-enhanced-mta.md" target="_blank"></a><br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td>b 
  </tr>
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr>  
 </tbody> 
</table>

### cache {#cache}

**** This is the local file cache configuration.

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 244800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 最大キャッシュサイズ (MB)。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1024<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 3600<br /> </td> 
  </tr> 
 </tbody> 
</table>

### relay {#relay}

**** This is the configuration of the mail server for the message delivery.

The list will be handled in the same way as a list of MX returned by a MX DNS query, usually the first MX is used as long as it is available, then the next one is used, and so on.

[](../../installation/using/configuring-campaign-server.md#smtp-relay)

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
   <td> <br /> </td> 
   <td> <br /> </td> 
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

### master {#master}

**** This is the configuration of the main server.

[](../../installation/using/configuring-campaign-server.md#mta-child-processes)

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
   <td> <br /> </td> 
   <td> 配信するジョブに対するデータベースポーリング頻度。この値はデータベースのポーリング頻度 (秒) を示します。配信待ちのジョブのリストを取得するために、MTA は定期的にデータベースをポーリングします。待機中のジョブがない場合、ポーリング期間はこの値によって定義されます。待機中のジョブがあり、ジョブが子サーバーに転送された場合は、できるだけ早く新しいジョブを再び処理できるようにするために (つまりできるだけ早く子サーバーが再び利用可能になるように)、このポーリング期間は自動的に 1 秒に短縮されます。これは、子サーバーが再び利用可能になるまでデータベースクエリが毎秒実行されるということを意味しません。実際は、少なくとも 1 つの子サーバーが利用可能になった場合にのみデータベースアクセスがおこなわれます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> データベースへの接続の失敗後に待機する期間。通常、データベース接続が失敗する原因は、データベースサーバー自体にあります。例えば、サーバーは、メンテナンスのために停止されることもあります。データベース接続が失敗した場合に接続を再試行するまでの時間は、DataBaseRetryDelay パラメーターで定義します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 秘密鍵のキャッシュの有効期間 (DomainKeys)。DomainKeys の推奨事項 (http://antispam.yahoo.com/domainkeys) に従った E メールへの署名に使用される秘密鍵は、データベース内にオプションとして保存されます。domainKeysReloadPeriodSec パラメーターに、MTA がこれらの鍵をキャッシュに保持できる秒数を定義します。この時間が過ぎた後は、すべての鍵をデータベースから再度読み込む必要があります。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 子サーバーの最大数。実行しているサービスの最大数を表します。サーバーメモリリソースと互換性がある最適値で制限することをお勧めします。これは、配信中にチェックできます。使用されるメモリは、利用可能な物理メモリの 3 分の 1 以下にする必要があります。それ以上になると、スワップが使用されます。<a href="../../installation/using/configuring-campaign-server.md#mta-child-processes" target="_blank"></a><br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 子サーバーの最小数。MTA は少なくともこの数のサーバーが実行され続けるようにします。サーバーの数がこれよりも少ない場合は、この値に達するまで毎秒新しいサーバーを再起動します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 起動時の子サーバーの数。子サーバーの数が動的に監視されます。MTA の起動時に、この値で指定した最大数の子サーバーが作成されます。通常、子サーバーは、ホストリソースを保存するために、秒単位の 1 台のサーバーより速く開始することはできません。ただし、MTA を起動した場合、子サーバーができるだけ早く使用可能になるように、この制限は上書きされます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
 </tbody> 
</table>

### child {#child}

**** This is the configuration of child servers.

[](../../installation/using/email-deliverability.md#email-sending-optimization)

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
   <td> <br /> </td> 
   <td> オプションのコマンドライン引数 <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> アイドル状態の子サーバーが停止するまで中断。子サーバーのアイドル時間がこのパラメーターより大きい場合、自分自身を自動的に kill してホストのリソースを解放します。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 最大メッセージ保持時間。準備されたメッセージがスロットルによって送信されなかった場合やターゲット MTA に接続できなかった場合、メッセージは破棄され、次の再試行で処理されます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 各子サーバーによって開始された FCM に対する並列 HTTP リクエストの最大数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 8<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 子サーバーごとの最大メッセージ数。それぞれの MTA の子はこの数のメッセージを処理して終了します。MTA でのメモリまたはリソースリークが悪影響を及ぼさない程度の数を指定することが重要です (通常は数千)。MTA コード内に既知のメモリリークが存在していない場合でも、埋め込まれた JavaScript  および XSL エンジンは完全に信頼できるものではありません。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5000000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 128<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 配信コネクタの SOAP 接続が破棄されるまでのタイムアウト (秒)。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 常に最優先 MX で開始.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 再開時に連続して再試行する最大回数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 48<br /> </td> 
  </tr> 
 </tbody> 
</table>

**** This is the configuration of SMTP sessions.

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
   <td> <br /> </td> 
   <td> リモートサーバーでサポートされる場合、セーフモードで E メールの配信を有効化します (STARTTLS/SMTPS)。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> アイドルセッションがタイムアウトになりました。このパラメーターは、あるドメインに対して複数のメッセージを転送するためにセッションが再利用される場合にのみ使用されます。MTA によってメッセージの転送が完了した場合、使用していた SMTP セッションはシステム的にはクローズされません。この同じドメインへのメッセージの送信準備が整えば、同じ SMTP セッションが再利用されます。このため、セッションは自動的にクローズされません。パラメーター IdleSessionTimeout では、別のメッセージを待機するために SMTP セッションがアクティブな状態を維持できる時間を定義します。その時間が経過した後、セッションは自動的にクローズされます。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 接続を再試行する前の初期遅延. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 4<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 子サーバーによる SMTP セッションの最大数。メッセージを配信するために、この MTA は受信者 MTA との SMTP 接続を初期化します。1 台の子サーバーでのアクティブな同時 SMTP セッションの最大数はこの値によって制限されます。この値と maxSpareServers の値を乗算すると、1 台の子サーバーで同時に処理できるメッセージの最大数がわかります。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

**** This is the configuration of the management of affinities with IP addresses for optimized outgoing SMTP traffic.

[](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)[](../../installation/using/configuring-campaign-server.md#managing-outbound-smtp-traffic-with-affinities)

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
   <td> <br /> </td> 
   <td> Domain name: local domain name linked to the IP address. <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> name<br /> </td> 
   <td> Logical name: names linked to the affinity by users. <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

****

[](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 関連付けられたパブリックアドレス ID です。統計サーバーのキーとして使用されます。数値で指定する必要があります。<a href="../../installation/using/email-deliverability.md#managing-ip-addresses">こちら</a>を参照してください。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
  </tr> 
  <tr> 
   <td> 重み付け<br /> </td> 
   <td> この IP の使用頻度を他の IP に相対的に指定します (重みを大きくすると頻度が高くなります)。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 含めるドメインマスクのコンマ区切りリスト.<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 除外するドメインマスクのコンマ区切りのリスト.<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> IP アドレスにリンクされたコンピューター名です。SMTP HELO コマンドの発行時に使用します。<br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## nmac {#nmac}

**** This is the configuration of for push notification deliveries.

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
   <td> <br /> </td> 
   <td> 共有 / プロキシ HTTP で定義された HTTP プロキシを使用. <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### relay {#relay-1}

**** This configures the use of a relay for the message delivery (ios http2 connector).

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
   <td> <br /> </td> 
   <td> <br /> </td> 
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
   <td> <br /> </td> 
   <td> 証明書チェーン (PEM ファイル)。モックサーバー使用時に役立ちます.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

## pipelined {#pipelined}

**** This is the configuration of the event processing module for Pipeline Services.

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
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authGatewayEndpoint<br /> </td> 
   <td> ゲートウェイトークンを取得する URL.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> authPrivateKey<br /> </td> 
   <td> トークンを取得するための秘密鍵 (AES で XtkKey オプションを指定して暗号化).<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始 <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> disableAuth<br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> 2<br /> </td> 
  </tr> 
  <tr> 
   <td> discoverPipelineEndpoint<br /> </td> 
   <td> パイプラインサービス URL を検出するための URL.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> dumpStatePeriodSec<br /> </td> 
   <td> Status save period: frequency that the process's internal information is saved in a file. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 0<br /> </td> 
  </tr> 
  <tr> 
   <td> forcedPipelineEndpoint<br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> monitorServerPort<br /> </td> 
   <td> Status server port: HTTP server port allowing you to query the status of the process. <br /> </td> 
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
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
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
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## repair {#repair}

**** This is the configuration of the database repair module.

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
 </tbody> 
</table>

## securityZone {#securityzone}

****

[](../../installation/using/security-zones.md)

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
   <td> <br /> </td> 
   <td> Web アプリケーションのデバッグモードを許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> パスワードなしでアプリケーションを使用することをユーザーに許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> オペレーターのログオンに HTTP の使用を許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 式で SQLDATA の使用を承認.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> ユーザー / パスワードセッショントークンを許可.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> label<br /> </td> 
   <td> ラベル<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> name<br /> </td> 
   <td> 内部名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> セキュリティトークンを使用しない.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> エラーの詳細を表示<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

Here is the default configuration:

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

****

[](../../installation/using/security-zones.md)

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
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> マスクまたはアドレス<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> name<br /> </td> 
   <td> 内部名<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> このサブネットワークでインスタンスにアクセスするために使用されている (リバース) プロキシのマスクまたはアドレス。この場合、「X-Forwarded-For」ヘッダーがこのプロキシの代わりにテストされます。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> 127.0.0.1 <br /> </td> 
  </tr> 
 </tbody> 
</table>

## SMS {#sms}

**** This is the configuration of the inbound SMS management module.

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
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> SMPP コネクタで保持される作業ファイルの最大数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 60<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> SMPP 作業ファイルの最大サイズ (MB)。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 512<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Recurrence of the session continuity frame: max. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 25<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
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

****

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
 </tbody> 
</table>

## stat {#stat}

**** This is the configuration of the MTA statistics module.

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
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
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
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## syslogd {#syslogd}

**** This is the configuration of the Log management module.

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
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 保持する logins.log ファイルの最大数. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 365<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>

## tracking {#tracking}

**** This is the configuration of the tracking server.

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
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 統合期間<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 300<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> バイト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 2592000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> リモートトラッキングサーバーに対する呼び出しによってリクエストされたログの数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> API key for the Phishbowl Service Endpoint Integration. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Endpoint for the Phishbowl Service Endpoint Integration. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> バイト<br /> </td> 
   <td> 1<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 86400<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> ブラウザー識別子のキャッシュのサイズ<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
 </tbody> 
</table>

## trackinglogd {#trackinglogd}

**** This is the configuration of the tracking log writing daemon.

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
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Maximum log size: maximum space used by logs on disk (in MB). <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 500<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Maximum log count: maximum number of logs stored in shared memory. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 25000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Number of logs before purge: number of logs inserted before starting the purge of log files. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 50000<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 追加の Web トラッキングパラメーターの共有メモリに保存される最大文字数.<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 64<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Web {#web}

**** This is the configuration of the Web Module.

[](configuring-campaign-server.md#default-port-for-tomcat)

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
   <td> <br /> </td> 
   <td> 文字列として渡される JVM オプション。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> スレッドの最大数です。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 75<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> スレッドの最小数。<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 5<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <a href="configure-tomcat.md" target="_blank"></a><br /> </td> 
   <td> ショート<br /> </td> 
   <td> 8005<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <a href="configure-tomcat.md" target="_blank"></a><br /> </td> 
   <td> ショート<br /> </td> 
   <td> 8080<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 50<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> モジュールモードで SOAP ルーターを起動します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
 </tbody> 
</table>

### jsp {#jsp}

**** This is the configuration of the parameters used by the JSPs.

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
   <td> <br /> </td> 
   <td> デバッグモードで JSP を実行するかどうか.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> .fo ファイルのパス。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> SOAP ルーターの URL (http://myserver/xxx, http://jni or mailto:xxx).<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

**** Here is the default configuration:

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

**** This is the configuration of the parameters used by the JSSPs.

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
   <td> <br /> </td> 
   <td> 各クエリの後で JavaScript コンテキストのガベージコレクターを有効にします。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1000<br /> </td> 
  </tr> 
 </tbody> 
</table>

****

### relay {#relay-2}

**** This is the configuration of the relay for HTTP requests between two zones.

[](../../installation/using/deploying-an-instance.md#synchronizing-public-resources)

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
   <td> <br /> </td> 
   <td> Web サーバー内の HTTP リレーモジュールをデバッグモードで起動します.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '.?#@/:' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '?#/'<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> HTTP リレーモジュールを開始.<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
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

****

[](../../installation/using/configuring-campaign-server.md#dynamic-page-security-and-relays)[](../../installation/using/deploying-an-instance.md#synchronizing-public-resources)

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> これらの URL へのアクセスを拒否します (HTTP 403 エラーを返します)<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> ステータス<br /> </td> 
   <td> Synchronization status of a public resource (enumeration). <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <a href="configure-tomcat.md" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> タイムアウト<br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 中継する URL のマスク (例 : 「/nl*」、「*.jsp」)。<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

Here is the default configuration:

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

****

[](../../installation/using/configuring-campaign-server.md#managing-http-headers)

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

Here is the default configuration:

```
<responseHeader name="X-XSS-Protection" value="1; mode=block"/>
```

### redirection {#redirection}

**** This is the configuration of the redirection module.

[](../../installation/using/deploying-an-instance.md#synchronizing-public-resources)

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
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> P3PCompactPolicy<br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> トラッキングインスタンスに関連付けられたデータベース識別子.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 30<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> Maximum job count: maximum number of delivery actions in cache. <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 100<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> リダイレクトサービスを開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> モジュールモードでリダイレクトサービスを開始します。<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> true<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> リダイレクションサーバーが使用するパスワード.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
 </tbody> 
</table>

****

[](../../installation/using/configuring-campaign-server.md#redundant-tracking)

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
   <td> <br /> </td> 
   <td> <br /> </td> 
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

**** This is the configuration the Email anti-spam scoring evaluation parameters.

[](../../installation/using/configuring-spamassassin.md)

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
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
  </tr> 
 </tbody> 
</table>

## wfserver {#wfserver}

**** This is the workflow process configuration.

[](../../installation/using/configuring-campaign-server.md#high-availability-workflows-and-affinities)

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
   <td> <br /> </td> 
   <td> スタートアップパラメーター<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 自動で開始<br /> </td> 
   <td> ブール値<br /> </td> 
   <td> false<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 期間<br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 20<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理の開始時に実行する JavaScript の ID.<br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1800<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 長いテキスト<br /> </td> 
   <td> 1600<br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> <br /> </td> 
   <td> 文字列<br /> </td> 
   <td> <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 処理が自動的に再度開始される時間. <a href="../../installation/using/configuring-campaign-server.md#automatic-process-restart" target="_blank"></a><br /> </td> 
   <td> 文字列<br /> </td> 
   <td> '06:00:00' <br /> </td> 
  </tr> 
  <tr> 
   <td> <br /> </td> 
   <td> 開始時の優先順位. 優先順位の低いモジュールが最初に開始され、最後に停止されます。したがって、syslogd モジュールは優先順位 0 である必要があります。<br /> </td> 
   <td> ショート<br /> </td> 
   <td> 10<br /> </td> 
  </tr> 
 </tbody> 
</table>
