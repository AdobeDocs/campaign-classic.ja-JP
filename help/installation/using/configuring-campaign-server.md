---
solution: Campaign Classic
product: campaign
title: Campaign サーバーの設定
description: Campaign サーバーの設定
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 46c8ed46-0947-47fb-abda-6541b12b6f0c
translation-type: tm+mt
source-git-commit: b0a1e0596e985998f1a1d02236f9359d0482624f
workflow-type: tm+mt
source-wordcount: '2577'
ht-degree: 2%

---

# キャンペーンサーバー構成の使用を開始する{#gs-campaign-server-config}

この章では、お客様のニーズと環境の特定性に合わせて実行できるサーバー側の設定について説明します。

## 制限事項

これらの手順は、**オンプレミス**/**ハイブリッド**&#x200B;のデプロイメントに制限され、管理権限が必要です。

**ホストされる**&#x200B;デプロイメントの場合、Adobe側の設定はサーバーでのみ構成できます。 ただし、IP許可リスト管理やURL権限など、[キャンペーンCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/key-features.html)内で設定できる設定もあります。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/ip-allow-listing-instance-access.html)。

詳しくは、次の節を参照してください。

* [コントロールパネルのドキュメント](https://docs.adobe.com/content/help/ja-JP/control-panel/using/control-panel-home.html)
* [モデルのホスティング](../../installation/using/hosting-models.md)
* [Campaign Classicオンプレミスおよびホステッド機能マトリックス](../../installation/using/capability-matrix.md)

## 設定ファイル

Campaign Classic構成ファイルは、Adobe Campaignのインストールフォルダーの&#x200B;**conf**&#x200B;フォルダーに保存されます。 設定は2つのファイルに分かれています。

* **serverConf.xml**:すべてのインスタンスの一般設定。このファイルは、Adobe Campaignサーバーの技術的なパラメーターを組み合わせたものです。これらはすべてのインスタンスで共有されます。 これらのパラメーターの一部については、以下で詳しく説明します。 この[セクション](../../installation/using/the-server-configuration-file.md)に示す、様々なノードとパラメーター。
* **config-`<instance>`.xml** ( **** instanceはインスタンスの名前):インスタンスの特定の設定。サーバを複数のインスタンス間で共有する場合は、各インスタンスに固有のパラメータを関連ファイルに入力してください。

一般的なサーバ設定のガイドラインは、[キャンペーンサーバ設定](../../installation/using/configuring-campaign-server.md)で詳しく説明しています。


## 構成範囲

ニーズと設定に応じて、キャンペーンサーバーを設定または調整します。 次の操作をおこなうことができます。

* [内部識別子](#internal-identifier)を保護します。
* [キャンペーンプロセス](#enabling-processes)を有効にする
* [URL権限](url-permissions.md)を設定
* [セキュリティゾーン](security-zones.md)の定義
* [Tomcat設定](configure-tomcat.md)を構成
* [配信パラメーター](#delivery-settings)のカスタマイズ
* [動的ページセキュリティを定義し、](#dynamic-page-security-and-relays)を中継します
* [許可する外部コマンド](#restricting-authorized-external-commands)のリストを制限
* [重複した追跡](#redundant-tracking)の設定
* [高可用性とワークフローのアフィニティを管理](#high-availability-workflows-and-affinities)
* ファイル管理の設定 — [詳細情報](#file-and-resmanagement)
   * アップロードファイルの形式の制限
   * パブリックリソースへのアクセスを有効にする
   * プロキシ接続の設定
* [自動プロセス再開](#automatic-process-restart)


## 内部識別子{#internal-identifier}

**internal**&#x200B;識別子は、インストール、管理、メンテナンスの目的で使用する技術的なログインです。 このログインは、インスタンスに関連付けられていません。

このログインを使用して接続されたオペレーターは、すべてのインスタンスに対してすべての権限を持ちます。 新たにインストールした場合、このログインにはパスワードがありません。 このパスワードは手動で定義する必要があります。

次のコマンドを使用します。

```
nlserver config -internalpassword
```

次の情報が表示されます。 パスワードを入力して確認します。

```
17:33:57 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
Enter the current password.
Password:
Enter the new password.
Password: XXXX
Confirmation: XXXX
17:34:02 >   Password successfully changed for account 'internal' (authentication mode 'nl')
```

## プロセスを有効にする{#enabling-processes}

サーバー上のAdobe Campaignプロセスは、**config-default.xml**&#x200B;ファイルと&#x200B;**`config-<instance>.xml`**&#x200B;ファイルを介して有効（および無効）になります。

これらのファイルに変更を適用するには、Adobe Campaignサービスが起動している場合、**nlserver config -reload**&#x200B;コマンドを実行する必要があります。

プロセスには次の2種類があります。マルチインスタンスとシングルインスタンスの両方を追加します。

* **マルチインスタンス**:すべてのインスタンスに対して1つの単一プロセスが開始されます。**web**、**syslogd**、**trackinglogd**&#x200B;の各プロセスは、このように処理されます。

   有効化は、**config-default.xml**&#x200B;ファイルから設定できます。

   クライアントコンソールにアクセスし、リダイレクト（トラッキング）を行うAdobe Campaignサーバーの宣言：

   ```
   vi nl6/conf/config-default.xml
   <web args="-tomcat" autoStart="true"/>  
   <!-- to start if the machine is also a redirection server -->  
   <trackinglogd autoStart="true"/>
   ```

   この例では、Linuxでは&#x200B;**vi**&#x200B;コマンドを使用してファイルを編集します。 **.txt**&#x200B;または&#x200B;**.xml**&#x200B;エディターを使用して編集できます。

* **モノラルインスタンス**:各インスタンスに対して1つのプロセスが開始されます(モジュール： **mta**, wfserver **,** inMail **, sand** stat  ****  **** smt)

   有効化は、インスタンスの設定ファイルを使用して設定できます。

   ```
   config-<instance>.xml
   ```

   配信用のサーバーの宣言、ワークフローインスタンスの実行、バウンスメールの回復：

   ```
   <mta autoStart="true" statServerAddress="localhost"/>
   <wfserver autoStart="true"/>  
   <inMail autoStart="true"/>
   <stat autoStart="true"/>
   ```

**キャンペーンデータストレージ**

Adobe Campaignデータ（ログ、ダウンロード、リダイレクトなど）のストレージディレクトリ（**var**&#x200B;ディレクトリ）を設定できます。 これを行うには、**XTK_VAR_DIR**&#x200B;システム変数を使用します。

* Windowsの場合、**XTK_VAR_DIR**&#x200B;システム変数に次の値を指定します

   ```
   D:\log\AdobeCampaign
   ```

* Linuxでは、**customer.sh**&#x200B;ファイルに移動し、次のことを示します。**XTK_VAR_DIR=/app/log/AdobeCampaign**&#x200B;をエクスポートします。

   詳しくは、[パーソナライズパラメーター](../../installation/using/installing-packages-with-linux.md#personalizing-parameters)を参照してください。

## 配信設定を構成{#delivery-settings}

配信パラメーターは、**serverConf.xml**&#x200B;フォルダーで設定する必要があります。

* **DNS構成**:以 **`<dnsconfig>`** 降のMTAモジュールが行うMX型DNSクエリに応答するために使用するDNSサーバーの配信ドメインとIPアドレス（またはホスト）を指定します。

   >[!NOTE]
   >
   >**nameServers**&#x200B;パラメーターは、Windowsでのインストールに必須です。 Linuxでのインストールの場合は、空のままにしておく必要があります。

   ```
   <dnsConfig localDomain="domain.com" nameServers="192.0.0.1,192.0.0.2"/>
   ```

また、ニーズや設定に応じて、次の設定を行うこともできます。[SMTPリレー](#smtp-relay)を構成し、[MTA子プロセス](#mta-child-processes)の数を調整します。[送信SMTPトラフィックの管理](#managing-outbound-smtp-traffic-with-affinities)。

### SMTPリレー{#smtp-relay}

MTAモジュールは、SMTPブロードキャスト用のネイティブメール転送エージェント（ポート25）として機能する。

ただし、セキュリティポリシーで必要な場合は、リレーサーバーで置き換えることができます。 その場合、グローバルスループットは、中継サーバのスループットがAdobe Campaignのスループットより低い場合に限り、中継サーバのスループットとなります。

この場合、これらのパラメーターは&#x200B;**`<relay>`**&#x200B;セクションでSMTPサーバーを設定することで設定されます。 メールの転送に使用するSMTPサーバーのIPアドレス（またはホスト）と、それに関連付けられたポート（デフォルトで25）を指定する必要があります。

```
<relay address="192.0.0.3" port="25"/>
```

>[!IMPORTANT]
>
>この動作モードは、中継サーバ固有の性能（待ち時間、帯域など）が原因でスループットが大幅に低下する可能性があるので、配信に対する重大な制限を意味します。 また、（SMTPトラフィックの分析で検出される）同期配信エラーを認定する能力も限られ、中継サーバが使用できない場合は送信はできません。

### MTA子プロセス{#mta-child-processes}

サーバのCPU電力と使用可能なネットワークリソースに応じてブロードキャストパフォーマンスを最適化するために、子プロセスの数（デフォルトではmaxSpareServers）を制御できます。 この設定は、各コンピュータのMTA設定の&#x200B;**`<master>`**&#x200B;セクションで行います。

```
<master dataBasePoolPeriodSec="30" dataBaseRetryDelaySec="60" maxSpareServers="2" minSpareServers="0" startSpareServers="0">
```

[Eメール送信の最適化](../../installation/using/email-deliverability.md#email-sending-optimization)も参照してください。

### アフィニティ{#managing-outbound-smtp-traffic-with-affinities}で送信SMTPトラフィックを管理

>[!IMPORTANT]
>
>アフィニティの設定は、サーバ間で一貫している必要があります。 構成の変更はMTAを実行するすべてのアプリケーションサーバーに複製される必要があるので、アフィニティ設定についてはAdobeにお問い合わせください。

IPアドレスを持つアフィニティを介した送信SMTPトラフィックを改善できます。

それには、次の手順に従います。

1. **serverConf.xml**&#x200B;ファイルの&#x200B;**`<ipaffinity>`**&#x200B;セクションにアフィニティを入力します。

   1つのアフィニティには、複数の異なる名前を付けることができます。区切るには、**;**&#x200B;文字を使用します。

   例：

   ```
    IPAffinity name="mid.Server;WWserver;local.Server">
             <IP address="XX.XXX.XX.XX" heloHost="myserver.us.campaign.net" publicId="123" excludeDomains="neo.*" weight="5"/
   ```

   関連するパラメーターを表示するには、**serverConf.xml**&#x200B;ファイルを参照してください。

1. ドロップダウンリストでアフィニティを選択できるようにするには、**IPAffinity**&#x200B;定義済みリストにアフィニティ名を追加する必要があります。

   ![](assets/ipaffinity_enum.png)

   >[!NOTE]
   >
   >定義済みリストの詳細は[このドキュメント](../../platform/using/managing-enumerations.md)に記載されています。

   次に示すように、タイポロジに使用するアフィニティを選択できます。

   ![](assets/ipaffinity_typology.png)

   >[!NOTE]
   >
   >[配信サーバの設定](../../installation/using/email-deliverability.md#delivery-server-configuration)も参照できます。



## 動的なページセキュリティとリレー{#dynamic-page-security-and-relays}

デフォルトでは、すべての動的ページは、Webモジュールが起動したマシンの&#x200B;**ローカル** Tomcatサーバーに自動的に関連付けられます。 この設定は、**ServerConf.xml**&#x200B;ファイルのクエリリレー設定の&#x200B;**`<url>`**&#x200B;セクションに入力されます。

動的ページの実行を&#x200B;**リモート**&#x200B;サーバー上で中継できます。を返します。 これを行うには、**localhost**&#x200B;を、JSPおよびJSSP、Web アプリケーション、レポート、文字列用のリモートコンピューターの名前に置き換える必要があります。

使用可能な様々なパラメーターの詳細については、**serverConf.xml**&#x200B;設定ファイルを参照してください。

JSPページの場合、デフォルト設定は次のとおりです。

```
<url relayHost="true" relayPath="true" targetUrl="http://localhost:8080" urlPath="*.jsp"/>
```

Adobe Campaignでは、次のJSPページを使用します。

* /nl/jsp/**soaprouter.jsp**:クライアントコンソールとWebサービス接続(SOAP API)、
* /nl/jsp/**m.jsp**:ミラーページ、
* /nl/jsp/**logon.jsp**:レポートへのWebベースのアクセスとクライアントコンソールのデプロイメント、
* /nl/jsp/**s.jsp** :クチコミマーケティング（スポンサーおよびソーシャルネットワーク）の使用を参照してください。

Mobile Appチャネルで使用されるJSSPは次のとおりです。

* nms/mobile/1/registerIOS.jssp
* nms/mobile/1/registerAndroid.jssp

**例：**

外部からのクライアントマシン接続を防ぐことができます。 これを行うには、**soaprouter.jsp**&#x200B;の実行を制限し、ミラーページ、クチコミリンク、Webフォームおよびパブリックリソースの実行のみを許可します。

パラメーターは次のとおりです。

```
<url IPMask="<IP_addresses>" deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="*.jsp"/>
<url IPMask="<IP_addresses>" deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="*.jssp"/> 
<url IPMask=""               deny=""     hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080" timeout="" urlPath="m.jsp"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080" timeout="" urlPath="s.jsp"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080" timeout="" urlPath="webForm.jsp"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="/webApp/pub*"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="/jssp/pub*"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="/strings/pub*"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="/interaction/pub*"/>
<url IPMask=""               deny="true" hostMask="" relayHost="false" relayPath="false" targetUrl="http://localhost:8080" timeout="" urlPath="*.jsp"/>
<url IPMask=""               deny="true" hostMask="" relayHost="false" relayPath="false" targetUrl="http://localhost:8080" timeout="" urlPath="*.jssp"/>
```

この例では、**`<IP_addresses>`**&#x200B;値は、このマスクに中継モジュールを使用する権限を持つIPアドレス（comaで区切られたもの）のリストと一致します。

>[!NOTE]
>
>値は、設定とネットワークの制約に従って適合する必要があります。特に、お客様の設置に対して特定の設定が開発されている場合には、その設定が必要です。

### HTTPヘッダーの管理{#managing-http-headers}

デフォルトでは、すべてのHTTPヘッダーは再生されません。 リレーから送信される返信に、特定のヘッダーを追加できます。 手順は次のとおりです。

1. **serverConf.xml**&#x200B;ファイルに移動します。
1. **`<relay>`**&#x200B;ノードで、中継されたHTTPヘッダーのリストに移動します。
1. 追加次の属性を持つ&#x200B;**`<responseheader>`**&#x200B;要素：

   * **name**:header name
   * **value**:値の名前。

   例：

   ```
   <responseHeader name="Strict-Transport-Security" value="max-age=16070400; includeSubDomains"/>
   ```

## 許可された外部コマンドを制限{#restricting-authorized-external-commands}

ビルド8780から、技術管理者は、Adobe Campaignで使用できる認証済みの外部コマンドのリストを制限できます。

そのためには、次のように、使用を禁止するコマンドのリストを含むテキストファイルを作成する必要があります。

```
ln
dd
openssl
curl
wget
python
python3
perl
ruby
sh
```

>[!IMPORTANT]
>
>このリストは完全なものではありません。

サーバー設定ファイルの&#x200B;**exec**&#x200B;ノードで、**blacklistFile**&#x200B;属性で、以前に作成したファイルを参照する必要があります。

**Linuxの場合のみ**:サーバー構成ファイルで、セキュリティ構成を強化するために、外部コマンドの実行専用のユーザーを指定するように再コマンドします。このユーザーは、設定ファイルの&#x200B;**exec**&#x200B;ノードに設定されます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

>[!NOTE]
>
>ユーザーを指定しない場合、すべてのコマンドはAdobe Campaignインスタンスのユーザーコンテキストで実行されます。 ユーザーは、Adobe Campaignを実行しているユーザーとは異なる必要があります。

例：

```
<serverConf>
 <exec user="theUnixUser" blacklistFile="/pathtothefile/blacklist"/>
</serverConf>
```

このユーザーは、「neolane」Adobe Campaign演算子のsudoerリストに追加する必要があります。

>[!IMPORTANT]
>
>カスタムsudoは使用しないでください。 標準のsudoをシステムにインストールする必要があります。


## 重複した追跡{#redundant-tracking}

リダイレクトに複数のサーバーを使用する場合、リダイレクトするURLからの情報を共有するには、SOAP呼び出しを介して相互に通信できる必要があります。 配信の開始アップ時に、すべてのリダイレクトサーバーが利用できるとは限りません。したがって、同じレベルの情報を持つことはないかもしれません。

>[!NOTE]
>
>標準アーキテクチャまたはエンタープライズアーキテクチャを使用する場合、メインアプリケーションサーバーは、各コンピューター上で追跡情報をアップロードする権限を持っている必要があります。

冗長サーバーのURLは、**serverConf.xml**&#x200B;ファイルを介して、リダイレクト構成で指定する必要があります。

**例：**

```
<spareserver enabledIf="$(hostname)!='front_srv1'" id="1" url="http://front_srv1:8080" />
<spareserver enabledIf="$(hostname)!='front_srv2'" id="2" url="http://front_srv2:8080" />
```

**enableIf**&#x200B;プロパティはオプションです（デフォルトでは空）。結果がtrueの場合にのみ接続を有効にできます。 これにより、すべてのリダイレクトサーバーで同じ構成を取得できます。

コンピューターのホスト名を取得するには、次のコマンドを実行します。**hostname -s**.

## ファイルとリソースの管理{#file-and-resmanagement}

### アップロードファイル形式の制限{#limiting-uploadable-files}

**uploadWhiteList**&#x200B;属性を使用して、Adobe Campaignサーバーでアップロードできるファイルの種類を制限します。

この属性は、**serverConf.xml**&#x200B;ファイルの&#x200B;**dataStore**&#x200B;要素内で使用できます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

この属性のデフォルト値は&#x200B;**です。+**&#x200B;を追加し、任意のファイルタイプをアップロードできます。

使用可能な形式を制限するには、有効なJava正規式で属性値を置き換えます。 複数の値をコンマで区切って入力できます。

次に例を示します。**uploadWhiteList=&quot;.*.png,.*.jpg&quot;**&#x200B;を使用すると、PNG形式とJPG形式をサーバにアップロードできます。 その他の形式は使用できません。

>[!NOTE]
>
>Internet Explorerでは、完全なファイルパスを正規式で検証する必要があります。

また、Webサーバーを設定して、重要なファイルがアップロードされないようにすることもできます。 [詳細情報](web-server-configuration.md)

### プロキシ接続の構成{#proxy-connection-configuration}

例えば、**ファイル転送**&#x200B;ワークフローアクティビティを使用して、キャンペーンサーバーをプロキシ経由で外部システムに接続できます。 これを行うには、特定のコマンドを使用して&#x200B;**serverConf.xml**&#x200B;ファイルの&#x200B;**proxyConfig**&#x200B;セクションを設定する必要があります。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

次のプロキシ接続が可能です。HTTP、HTTPS、FTP、SFTP。 20.2キャンペーンリリース以降、HTTPおよびHTTPSプロトコルのパラメーターは&#x200B;**使用できなくなりました**。 これらのパラメーターは、9032を含む以前のビルドで引き続き使用できるので、以下に説明します。

>[!CAUTION]
>
>基本認証モードのみがサポートされています。 NTLM認証はサポートされていません。
>
>SOCKSプロキシはサポートされていません。


次のコマンドを使用できます。

```
nlserver config -setproxy:[protocol]/[serverIP]:[port]/[login][:‘https’|'http’]
```

プロトコルのパラメータには、「http」、「https」、「ftp」のいずれかを使用できます。

HTTP/HTTPSトラフィックと同じポートにFTPを設定する場合は、次を使用できます。

```
nlserver config -setproxy:http/198.51.100.0:8080/user
```

「http」および「https」オプションは、プロトコルパラメータが「ftp」の場合にのみ使用され、指定したポートでのトンネリングがHTTPSまたはHTTPを使用して実行されるかどうかを示します。

プロキシサーバー経由のFTP/SFTPとHTTP/HTTPSトラフィックに異なるポートを使用する場合は、「ftp」プロトコルパラメーターを設定する必要があります。


例：

```
nlserver config -setproxy:ftp/198.51.100.0:8080/user:’http’
```

次に、パスワードを入力します。

HTTP接続は、proxyHTTPパラメーターで定義します。

```
<proxyConfig enabled=“1” override=“localhost*” useSingleProxy=“0”>
<proxyHTTP address=“198.51.100.0" login=“user” password=“*******” port=“8080”/>
</proxyConfig>
```

HTTPS接続は、proxyHTTPSパラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyHTTPS address=“198.51.100.0” login=“user” password=“******” port=“8080"/>
</proxyConfig>
```

FTP/FTPS接続は、proxyFTPパラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyFTP address=“198.51.100.0” login=“user” password=“******” port=“5555" https=”true”/>
</proxyConfig>
```

複数の接続タイプで同じプロキシを使用する場合、proxyHTTPのみがuseSingleProxyを&quot;1&quot;または&quot;true&quot;に設定して定義されます。

プロキシを経由する必要がある内部接続がある場合は、それらをoverrideパラメーターに追加します。

プロキシ接続を一時的に無効にする場合は、有効なパラメーターを「false」または「0」に設定します。

### パブリックリソースの管理{#managing-public-resources}

公開されるようにするには、キャンペーンにリンクされた電子メールやパブリックリソースで使用される画像が、外部からアクセス可能なサーバー上に存在する必要があります。 その後、外部の受信者や演算子で使用できます。 [詳細情報](../../installation/using/deploying-an-instance.md#managing-public-resources)。

パブリックリソースは、Adobe Campaignインストールディレクトリの&#x200B;**/var/res/instance**&#x200B;ディレクトリに保存されます。

一致するURLは次のとおりです。**http://server/res/instance**&#x200B;ここで&#x200B;**instance**&#x200B;は、トラッキングインスタンスの名前です。

別のディレクトリを指定するには、**conf-`<instance>`.xml**&#x200B;ファイルにノードを追加して、サーバー上のストレージを設定します。 これは、次の行を追加することを意味します。

```
<serverconf>
  <shared>
    <dataStore hosts="media*" lang="fra">
      <virtualDir name="images" path="/var/www/images"/>
     <virtualDir name="publicFileRes" path="$(XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)/"/>
    </dataStore>
  </shared>
</serverconf>
```

この場合、デプロイメントウィザードのウィンドウ上部に表示されるパブリックリソースの新しいURLは、このフォルダーを指す必要があります。

## 高可用性ワークフローとアフィニティ{#high-availability-workflows-and-affinities}

複数のワークフローサーバー(wfserver)を設定し、2台以上のマシンに配布できます。 この種のアーキテクチャを選択する場合は、Adobe Campaignアクセスに応じてロードバランサーの接続モードを設定します。

Webからのアクセスの場合は、**ロードバランサー**&#x200B;モードを選択して接続時間を制限します。

Adobe Campaignコンソールからアクセスする場合は、**ハッシュ**&#x200B;または&#x200B;**スティッキーip**&#x200B;モードを選択します。 これにより、リッチクライアントとサーバー間の接続を維持し、例えばインポート操作やエクスポート操作中にユーザーセッションが中断されるのを防ぐことができます。

特定のマシン上でワークフローまたはワークフローアクティビティを強制的に実行するよう選択できます。 これを行うには、関連するワークフローまたはアクティビティに対して1つ以上のアフィニティを定義する必要があります。

1. ワークフローまたはアクティビティのアフィニティを作成するには、**[!UICONTROL アフィニティ]**&#x200B;フィールドに入力します。

   任意のアフィニティ名を選択できますが、スペースや句読点を使用しないようにしてください。 別のサーバーを使用する場合は、別の名前を指定します。

   ![](assets/s_ncs_install_server_wf_affinity01.png)

   ![](assets/s_ncs_install_server_wf_affinity02.png)

   ドロップダウンリストには、以前に使用したアフィニティが含まれています。 時間の経過と共に異なる入力値で完了します。

1. **nl6/conf/config-`<instance>.xml`**&#x200B;ファイルを開きます。
1. **[!UICONTROL wfserver]**&#x200B;モジュールに一致する行を次のように変更します。

   ```
   <wfserver autoStart="true" affinity="XXX,"/>
   ```

   複数のアフィニティを定義する場合は、コンマで区切ってスペースを入れないでください。

   ```
   <wfserver autoStart="true" affinity="XXX,YYY,"/>
   ```

   アフィニティが定義されていないワークフローを実行するには、アフィニティ名の後のカンマが必要です。

   アフィニティが定義されているワークフローのみを実行する場合は、アフィニティのリストの最後にカンマを追加しないでください。 例えば、次のように行を変更します。

   ```
   <wfserver autoStart="true" affinity="XXX"/>
   ```

## 自動再起動{#automatic-process-restart}

デフォルトでは、異なるAdobe Campaignプロセスは、毎日午前6時（サーバー時間）に自動的に再起動します。

ただし、この設定は変更できます。

これを行うには、インストール先の&#x200B;**conf**&#x200B;リポジトリにある&#x200B;**serverConf.xml**&#x200B;ファイルに移動します。

このファイルに設定された各プロセスには、**processRestartTime**&#x200B;属性があります。 この属性の値を変更して、各プロセスの再開時間をニーズに合わせて調整できます。

>[!IMPORTANT]
>
>この属性は削除しないでください。 すべてのプロセスは毎日再起動する必要があります。
