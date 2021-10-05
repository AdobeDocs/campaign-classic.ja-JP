---
product: campaign
title: Campaign サーバーの設定
description: Campaign サーバーの設定
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 46c8ed46-0947-47fb-abda-6541b12b6f0c
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 3%

---

# Campaign サーバー設定の概要{#gs-campaign-server-config}

![](../../assets/v7-only.svg)

この章では、ニーズや環境に特化した設定に合わせて実行できるサーバー側の設定について説明します。

## 制限事項

これらの手順は、オンプレミス **/** ハイブリッド **デプロイメントに限定され、管理権限が必要です。**

**ホストされた** デプロイメントの場合、サーバー側の設定はAdobeのみで構成できます。 ただし、IP のCampaign コントロールパネル管理や URL の権限など、[ キャンペーンの管理 ](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/key-features.html?lang=ja) 内で設定でき許可リストる設定もあります。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/ip-allow-listing-instance-access.html?lang=ja)。

詳しくは、次の節を参照してください。

* [コントロールパネルに関するドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)
* [ホスティングモデル](../../installation/using/hosting-models.md)
* [Campaign Classicオンプレミスとホスト機能のマトリックス](../../installation/using/capability-matrix.md)

## 設定ファイル

Campaign Classic設定ファイルは、Adobe Campaignインストールフォルダーの **conf** フォルダーに保存されます。 設定は、次の 2 つのファイルに分散されます。

* **serverConf.xml**:すべてのインスタンスの一般設定。このファイルは、Adobe Campaignサーバーの技術的なパラメーターを組み合わせたものです。これらはすべてのインスタンスで共有されます。 これらのパラメーターの一部の説明を以下に示します。 この [ 節 ](../../installation/using/the-server-configuration-file.md) に示す様々なノードとパラメータ。
* **config- `<instance>`.xml** (instance は **** インスタンスの名前 ):インスタンスの特定の設定。サーバーを複数のインスタンスで共有する場合は、各インスタンスに固有のパラメーターを関連するファイルに入力してください。

## 設定の範囲

ニーズと設定に応じて、Campaign サーバーを設定または調整します。 次をおこなうことができます。

* [ 内部識別子 ](#internal-identifier) を保護します。
* [ キャンペーンプロセス ](#enabling-processes) を有効にする
* [URL のアクセス許可 ](url-permissions.md) の設定
* [ セキュリティゾーン ](security-zones.md) を定義します
* [Tomcat の設定 ](configure-tomcat.md)
* [ 配信パラメーター ](configure-delivery-settings.md) のカスタマイズ
* [ 動的ページセキュリティとリレー ](#dynamic-page-security-and-relays) を定義
* [ 許可する外部コマンド ](#restricting-authorized-external-commands) のリストを制限
* [ 冗長トラッキング ](#redundant-tracking) の設定
* [ 高可用性とワークフローの親和性を管理 ](#high-availability-workflows-and-affinities)
* ファイル管理の設定 — [ 詳細 ](file-res-management.md)
   * アップロードファイル形式の制限
   * パブリックリソースへのアクセスを有効にする
   * プロキシ接続の設定
* [プロセスの自動再起動](#automatic-process-restart)


## 内部識別子 {#internal-identifier}

**内部** 識別子は、インストール、管理、メンテナンスの目的で使用する技術的なログインです。 このログインは、インスタンスに関連付けられていません。

このログインを使用して接続したオペレーターは、すべてのインスタンスに対してすべての権限を持ちます。 新規インストールの場合、このログインにはパスワードは含まれません。 このパスワードは手動で定義する必要があります。

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

## プロセスの有効化 {#enabling-processes}

サーバー上のAdobe Campaignプロセスは、**config-default.xml** ファイルと **`config-<instance>.xml`** ファイルを介して有効（および無効）になります。

これらのファイルに変更を適用するには、Adobe Campaignサービスが起動している場合に、 **nlserver config -reload** コマンドを実行する必要があります。

次の 2 つのタイプのプロセスがあります。複数インスタンスと単一インスタンスの両方を使用できます。

* **マルチインスタンス**:1 つのプロセスがすべてのインスタンスに対して開始されます。**web**、**syslogd**、および **trackinglogd** プロセスの場合です。

   イネーブルメントは、**config-default.xml** ファイルから設定できます。

   クライアントコンソールにアクセスし、リダイレクト（トラッキング）をおこなうためのAdobe Campaignサーバーの宣言：

   ```
   vi nl6/conf/config-default.xml
   <web args="-tomcat" autoStart="true"/>  
   <!-- to start if the machine is also a redirection server -->  
   <trackinglogd autoStart="true"/>
   ```

   この例では、Linux の **vi** コマンドを使用してファイルを編集します。 任意の **.txt** または **.xml** エディターを使用して編集できます。

* **モノラルインスタンス**:各インスタンス（モジュール）に対して 1 つのプロセスが開始されます。 **mta**、 **wfserver**、 **inMail**、smsand  **** stat ****)。

   イネーブルメントは、インスタンスの設定ファイルを使用して設定できます。

   ```
   config-<instance>.xml
   ```

   配信用のサーバーの宣言、ワークフローインスタンスの実行およびバウンスメールの復元：

   ```
   <mta autoStart="true" statServerAddress="localhost"/>
   <wfserver autoStart="true"/>  
   <inMail autoStart="true"/>
   <stat autoStart="true"/>
   ```

**Campaign データストレージ**

Adobe Campaignデータのストレージディレクトリ（**var** ディレクトリ）（ログ、ダウンロード、リダイレクトなど）を設定できます。 これをおこなうには、**XTK_VAR_DIR** システム変数を使用します。

* Windows の場合、**XTK_VAR_DIR** システム変数に次の値を入力します。

   ```
   D:\log\AdobeCampaign
   ```

* Linux では、**customer.sh** ファイルに移動し、次の情報を指定します。**export XTK_VAR_DIR=/app/log/AdobeCampaign**.

   詳しくは、[ パラメーターのパーソナライズ ](../../installation/using/installing-packages-with-linux.md#personalizing-parameters) を参照してください。


## 動的なページのセキュリティとリレー {#dynamic-page-security-and-relays}

デフォルトでは、すべての動的ページは、Web モジュールが起動したマシンの **ローカル** Tomcat サーバーに自動的に関連付けられます。 この設定は、**ServerConf.xml** ファイルのクエリリレー設定の **`<url>`** セクションに入力します。

動的ページの実行を **リモート** サーバーで中継できます。（コンピュータで Web モジュールがアクティブになっていない場合）。 これを行うには、**localhost** を、JSP および JSSP、Web アプリケーション、レポート、および文字列用のリモートコンピューターの名前に置き換える必要があります。

使用可能な様々なパラメーターについて詳しくは、**serverConf.xml** 設定ファイルを参照してください。

JSP ページのデフォルトの設定は次のとおりです。

```
<url relayHost="true" relayPath="true" targetUrl="http://localhost:8080" urlPath="*.jsp"/>
```

Adobe Campaignは次の JSP ページを使用します。

* /nl/jsp/**soaprouter.jsp**:クライアントコンソールと Web サービス接続 (SOAP API)
* /nl/jsp/**m.jsp**:ミラーページ、
* /nl/jsp/**logon.jsp**:レポートへの Web ベースのアクセスと、クライアントコンソールのデプロイメント
* /nl/jsp/**s.jsp** :バイラルマーケティング（スポンサーおよびソーシャルネットワーク）の使用。

モバイルアプリチャネルで使用される JSSP は次のとおりです。

* nms/mobile/1/registerIOS.jssp
* nms/mobile/1/registerAndroid.jssp

**例：**

外部からのクライアントマシンの接続を防ぐことができます。 これをおこなうには、**soapputer.jsp** の実行を制限し、ミラーページ、バイラルリンク、Web フォームおよびパブリックリソースの実行のみを許可します。

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

この例では、**`<IP_addresses>`** 値は、このマスクにリレーモジュールを使用する権限を持つ IP アドレスのリスト（コンマ区切り）と一致します。

>[!NOTE]
>
>値は、設定とネットワークの制約に従って適応する必要があります。特に、インストールに対して特定の設定が開発されている場合には、適応します。

### HTTP ヘッダーの管理 {#managing-http-headers}

デフォルトでは、すべての HTTP ヘッダーは中継されません。 リレーから送信された返信に、特定のヘッダーを追加できます。 手順は次のとおりです。

1. **serverConf.xml** ファイルに移動します。
1. **`<relay>`** ノードで、中継される HTTP ヘッダーのリストに移動します。
1. 次の属性を持つ **`<responseheader>`** 要素を追加します。

   * **名前**:ヘッダー名
   * **値**:値の名前。

   例：

   ```
   <responseHeader name="Strict-Transport-Security" value="max-age=16070400; includeSubDomains"/>
   ```

## 許可する外部コマンドの制限 {#restricting-authorized-external-commands}

ビルド 8780 以降、技術管理者はAdobe Campaignで使用できる承認済み外部コマンドのリストを制限できます。

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
>このリストが完全なものではありません。

サーバー設定ファイルの **exec** ノードで、**blacklistFile** 属性で、前に作成したファイルを参照する必要があります。

**Linux のみ**:サーバー設定ファイルでは、外部コマンドの実行専用のユーザーを指定して、セキュリティ設定を強化することをお勧めします。このユーザーは、設定ファイルの **exec** ノードに設定されます。 **serverConf.xml** で使用できるすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に記載されています。

>[!NOTE]
>
>ユーザーを指定しない場合、すべてのコマンドはAdobe Campaignインスタンスのユーザーコンテキストで実行されます。 ユーザーは、Adobe Campaignを実行しているユーザーとは異なる必要があります。

例：

```
<serverConf>
 <exec user="theUnixUser" blacklistFile="/pathtothefile/blacklist"/>
</serverConf>
```

このユーザーは、「neolane」Adobe Campaign演算子のスーダーリストに追加する必要があります。

>[!IMPORTANT]
>
>カスタムスードは使用しないでください。 標準のスードをシステムにインストールする必要があります。


## 冗長な追跡 {#redundant-tracking}

リダイレクトに複数のサーバーを使用する場合、リダイレクトする URL からの情報を共有するには、SOAP 呼び出しを介して相互に通信できる必要があります。 配信の開始時に、すべてのリダイレクションサーバーが使用可能とは限りません。したがって、同じレベルの情報を持たない可能性があります。

>[!NOTE]
>
>標準アーキテクチャまたはエンタープライズアーキテクチャを使用する場合、メインアプリケーションサーバーは、各コンピューターにトラッキング情報をアップロードする権限を持っている必要があります。

冗長サーバーの URL は、**serverConf.xml** ファイルを使用してリダイレクト設定で指定する必要があります。

**例：**

```
<spareserver enabledIf="$(hostname)!='front_srv1'" id="1" url="http://front_srv1:8080" />
<spareserver enabledIf="$(hostname)!='front_srv2'" id="2" url="http://front_srv2:8080" />
```

**enableIf** プロパティはオプションです（デフォルトでは空です）。結果が true の場合にのみ接続を有効にできます。 これにより、すべてのリダイレクションサーバーで同じ設定を取得できます。

コンピュータのホスト名を取得するには、次のコマンドを実行します。**hostname -s**。



## 高可用性のワークフローとアフィニティ {#high-availability-workflows-and-affinities}

複数のワークフローサーバー (wfserver) を設定し、2 つ以上のマシンに配布できます。 このタイプのアーキテクチャを選択する場合は、Adobe Campaignへのアクセスに応じてロードバランサーの接続モードを設定します。

Web からアクセスする場合は、**ロードバランサー** モードを選択して接続時間を制限します。

Adobe Campaignコンソールからアクセスする場合は、**hash** または **sticky ip** モードを選択します。 これにより、リッチクライアントとサーバー間の接続を維持し、例えば、インポートやエクスポートの操作中にユーザーセッションが中断されるのを防ぐことができます。

特定のマシンでのワークフローまたはワークフローアクティビティを強制的に実行するよう選択できます。 これをおこなうには、該当するワークフローまたはアクティビティに対して 1 つ以上のアフィニティを定義する必要があります。

1. 「**[!UICONTROL 親和性]**」フィールドに入力して、ワークフローまたはアクティビティの親和性を作成します。

   親和性の名前は任意に選択できますが、スペースや句読点を使用しないようにしてください。 異なるサーバーを使用する場合は、異なる名前を指定します。

   ![](assets/s_ncs_install_server_wf_affinity01.png)

   ![](assets/s_ncs_install_server_wf_affinity02.png)

   ドロップダウンリストには、以前に使用したアフィニティが含まれています。 時間の経過と共に、入力された値が異なります。

1. **nl6/conf/config-`<instance>.xml`** ファイルを開きます。
1. **[!UICONTROL wfserver]** モジュールに一致する行を次のように変更します。

   ```
   <wfserver autoStart="true" affinity="XXX,"/>
   ```

   複数のアフィニティを定義する場合は、スペースを含まないコンマで区切る必要があります。

   ```
   <wfserver autoStart="true" affinity="XXX,YYY,"/>
   ```

   アフィニティが定義されていないワークフローを実行するには、アフィニティの名前の後にコンマが続く必要があります。

   アフィニティが定義されたワークフローのみを実行する場合は、アフィニティのリストの最後にコンマを追加しないでください。 例えば、次のように行を変更します。

   ```
   <wfserver autoStart="true" affinity="XXX"/>
   ```

## 自動再起動 {#automatic-process-restart}

デフォルトでは、異なるAdobe Campaignプロセスは、毎日午前 6 時（サーバー時間）に自動的に再起動します。

ただし、この設定は変更できます。

これをおこなうには、インストール先の **conf** リポジトリにある **serverConf.xml** ファイルに移動します。

このファイルで設定された各プロセスには、**processRestartTime** 属性があります。 この属性の値を変更して、必要に応じて各プロセスの再開時間を調整できます。

>[!IMPORTANT]
>
>この属性は削除しないでください。 すべてのプロセスを毎日再起動する必要があります。
