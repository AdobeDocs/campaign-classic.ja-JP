---
product: campaign
title: Campaign サーバーの設定
description: Campaign サーバーの設定
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 46c8ed46-0947-47fb-abda-6541b12b6f0c
source-git-commit: 1be1528d657537786c430ea9c8bdb3aad58ba20d
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 2%

---

# Campaign サーバー設定の基本を学ぶ{#gs-campaign-server-config}



この章では、ニーズや環境の特性に合わせて実行できるサーバーサイド設定について詳しく説明します。

## 制限

これらの手順は、**オンプレミス**/**ハイブリッド** デプロイメントに制限され、管理権限が必要です。

**ホスト** デプロイメントの場合、サーバーサイドの設定はAdobeでのみ指定できます。 ただし、IPCampaign コントロールパネル許可リストに加えるや URL 権限など、一部の設定は [ キャンペーン管理 ](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/key-features.html?lang=ja) 内で設定できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/ip-allow-listing-instance-access.html?lang=ja)。

詳しくは、次の節を参照してください。

* [コントロールパネルに関するドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)
* [ホスティングモデル](../../installation/using/hosting-models.md)
* [Campaign Classicオンプレミスおよびホスト環境の機能マトリックス](../../installation/using/capability-matrix.md)

## 設定ファイル

Campaign Classic設定ファイルは、Adobe Campaign インストールフォルダーの **conf** フォルダーに保存されます。 設定は、次の 2 つのファイルに分散されています。

* **serverConf.xml**：すべてのインスタンスの一般設定。 このファイルには、Adobe Campaign サーバーの技術的なパラメーターが組み合わされています。これらのパラメーターは、すべてのインスタンスで共有されます。 これらのパラメーターの一部について、以下で詳しく説明します。 様々なノードとパラメーター、およびこの [ 節 ](../../installation/using/the-server-configuration-file.md) で示します。
* **config-`<instance>`.xml** （**instance** はインスタンスの名前）：インスタンスの特定の設定。 複数のインスタンスでサーバーを共有する場合は、関連するファイルに各インスタンスに固有のパラメーターを入力してください。

## 設定スコープ

ニーズと設定に応じて、Campaign サーバーを設定または調整します。 以下を行うことができます。

* [ 内部識別子 ](#internal-identifier) を保護します
* [ キャンペーンプロセス ](#enabling-processes) を有効にする
* [URL 権限 ](url-permissions.md) の設定
* [ セキュリティゾーン ](security-zones.md) を定義
* 設定 [Tomcat 設定 ](configure-tomcat.md)
* カスタマイズ [ 配信パラメーター ](configure-delivery-settings.md)
* [ 動的ページセキュリティとリレー ](#dynamic-page-security-and-relays) の定義
* [ 許可される外部コマンド ](#restricting-authorized-external-commands) のリストの制限
* [ 冗長トラッキング ](#redundant-tracking) の設定
* 管理 [ 高可用性とワークフローアフィニティ ](#high-availability-workflows-and-affinities)
* ファイル管理の設定 – [ 詳細情報 ](file-res-management.md)
   * アップロードファイル形式を制限
   * パブリックリソースへのアクセスを有効にする
   * プロキシ接続の設定
* [プロセスの自動再起動](#automatic-process-restart)


## 内部識別子 {#internal-identifier}

**内部** 識別子は、インストール、管理、メンテナンスに使用されるテクニカルログインです。 このログインはインスタンスに関連付けられていません。

このログインを使用して接続したオペレーターは、すべてのインスタンスに対するすべての権限を持ちます。 新しいインストールの場合、このログインにパスワードは含まれません。 このパスワードは手動で定義する必要があります。

次のコマンドを使用します。

```sql
nlserver config -internalpassword
```

次の情報が表示されます。 パスワードを入力し、確認します。

```sql
17:33:57 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
Enter the current password.
Password:
Enter the new password.
Password: XXXX
Confirmation: XXXX
17:34:02 >   Password successfully changed for account 'internal' (authentication mode 'nl')
```

## プロセスの有効化 {#enabling-processes}

サーバー上のAdobe Campaign プロセスは、**config-default.xml** および **`config-<instance>.xml`** ファイルを介して有効（および無効）になります。

これらのファイルに変更内容を適用するには、Adobe Campaign サービスが起動されている場合は、**nlserver config -reload** コマンドを実行する必要があります。

プロセスには、マルチインスタンスとシングルインスタンスの 2 つのタイプがあります。

* **マルチインスタンス**：すべてのインスタンスに対して 1 つのプロセスが開始されます。 これは、**web**、**syslogd** および **trackinglogd** プロセスの場合です。

  イネーブルメントは、**config-default.xml** ファイルから設定できます。

  クライアントコンソールにアクセスするためのAdobe Campaign サーバーの宣言とリダイレクト（トラッキング）:

  ```
  vi nl6/conf/config-default.xml
  <web args="-tomcat" autoStart="true"/>  
  <!-- to start if the machine is also a redirection server -->  
  <trackinglogd autoStart="true"/>
  ```

  この例では、Linux で **vi** コマンドを使用してファイルを編集します。 任意の **.txt** エディターまたは **.xml** エディターを使用して編集できます。

* **mono-instance**：インスタンスごとに 1 つのプロセスが開始されます（モジュール：**mta**、**wfserver**、**inMail**、**sms** および **stat**）。

  イネーブルメントは、インスタンスの設定ファイルを使用して設定できます。

  ```
  config-<instance>.xml
  ```

  配信のためのサーバーの宣言、ワークフローインスタンスの実行、バウンスメールの復元：

  ```
  <mta autoStart="true" statServerAddress="localhost"/>
  <wfserver autoStart="true"/>  
  <inMail autoStart="true"/>
  <stat autoStart="true"/>
  ```

**Campaign データストレージ**

Adobe Campaign データ（ログ、ダウンロード、リダイレクトなど）のストレージディレクトリ（**var** ディレクトリ）を設定できます。 それには、システム変数 **XTK_VAR_DIR** を使用します。

* Windows では、**XTK_VAR_DIR** システム変数に次の値を指定します

  ```
  D:\log\AdobeCampaign
  ```

* Linux の場合、**customer.sh** ファイルに移動して、**export XTK_VAR_DIR=/app/log/AdobeCampaign** と指定します。

  詳しくは、[ パラメーターのパーソナライズ ](../../installation/using/installing-packages-with-linux.md#personalizing-parameters) を参照してください。


## 動的ページセキュリティとリレー {#dynamic-page-security-and-relays}

デフォルトでは、すべての動的ページは、Web モジュールが起動されたマシンの **ローカル** Tomcat サーバーに自動的に関連付けられます。 この設定は、**ServerConf.xml** ファイルのクエリリレー設定の **`<url>`** セクションに入力されます。

**リモート** サーバーで動的ページの実行をリレーできます。コンピューターで web モジュールがアクティブ化されていない場合は。 これを行うには、**localhost** を JSP および JSSP、web アプリケーション、レポートおよび文字列用のリモートコンピューターの名前に置き換える必要があります。

使用可能な様々なパラメーターについて詳しくは、**serverConf.xml** 設定ファイルを参照してください。

JSP ページの場合、デフォルトの設定はです。

```
<url relayHost="true" relayPath="true" targetUrl="http://localhost:8080" urlPath="*.jsp"/>
```

Adobe Campaignでは、次の JSP ページを使用します。

* /nl/jsp/**soaprouter.jsp**：クライアントコンソールおよび web サービス接続（SOAP API）
* /nl/jsp/**m.jsp**：ミラーページ、
* /nl/jsp/**logon.jsp**: レポートおよびクライアントコンソールのデプロイメントへの Web ベースのアクセス
* /nl/jsp/**s.jsp**：バイラルマーケティング（スポンサーおよびソーシャルネットワーク）を使用します。

モバイルアプリチャネルで使用される JSSP は次のとおりです。

* nms/mobile/1/registerIOS.jssp
* nms/mobile/1/registerAndroid.jssp

**例：**

外部からのクライアントマシン接続を防ぐことができます。 これをおこなうには、**soaprouter.jsp** の実行を制限し、ミラーページ、バイラルリンク、web フォーム、パブリックリソースの実行のみを許可します。

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

この例では、**`<IP_addresses>`** の値は、このマスクのリレーモジュールの使用が許可されている IP アドレスのリスト （コンマ区切り）と一致します。

>[!NOTE]
>
>特に、インストール用に特定の設定が開発されている場合、値は設定とネットワークの制約に応じて適応する必要があります。

### HTTP ヘッダーの管理 {#managing-http-headers}

デフォルトでは、すべての HTTP ヘッダーが中継されません。 リレーで送信される返信に特定のヘッダーを追加できます。 手順は次のとおりです。

1. **serverConf.xml** ファイルに移動します。
1. **`<relay>`** ノードで、リレーされた HTTP ヘッダーのリストに移動します。
1. 次の属性を持つ **`<responseheader>`** 要素を追加します。

   * **name**: ヘッダー名
   * **value**：値の名前。

   例：

   ```
   <responseHeader name="Strict-Transport-Security" value="max-age=16070400; includeSubDomains"/>
   ```

## 許可された外部コマンドの制限 {#restricting-authorized-external-commands}

ビルド 8780 以降、技術管理者は、Adobe Campaignで使用できる承認済みの外部コマンドのリストを制限できます。

それには、の使用を禁止するコマンドのリストを含んだテキストファイルを作成する必要があります。次に例を示します。

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
>このリストは網羅的ではありません。

サーバー設定ファイルの **exec** ノードで、前に作成した **blacklistFile** 属性のファイルを参照する必要があります。

**Linux のみ**：サーバー設定ファイルでは、外部コマンドの実行専用のユーザーを指定して、セキュリティ設定を強化することをお勧めします。 このユーザーは、設定ファイルの **exec** ノードに設定されます。 **serverConf.xml** で使用可能なすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に一覧表示されます。

>[!NOTE]
>
>ユーザーが指定されていない場合、すべてのコマンドはAdobe Campaign インスタンスのユーザーコンテキストで実行されます。 ユーザーは、Adobe Campaignを実行しているユーザーとは異なる必要があります。

例：

```
<serverConf>
 <exec user="theUnixUser" blacklistFile="/pathtothefile/blacklist"/>
</serverConf>
```

このユーザーは、「neolane」Adobe Campaign演算子のソースリストに追加される必要があります。

>[!IMPORTANT]
>
>ユーザー設定の sudo を使用しないでください。 システムに標準の sudo をインストールする必要があります。


## 冗長トラッキング {#redundant-tracking}

複数のサーバーをリダイレクトに使用する場合は、リダイレクト先の URL の情報を共有するために、SOAP呼び出しを介して相互に通信できる必要があります。 配信の開始時に、すべてのリダイレクトサーバーが利用できるわけではなく、同じレベルの情報が存在しない可能性があります。

>[!NOTE]
>
>標準またはエンタープライズアーキテクチャを使用する場合、メインアプリケーションサーバーは、各コンピューターにトラッキング情報をアップロードする権限を持っている必要があります。

冗長サーバーの URL は、**serverConf.xml** ファイルを介してリダイレクト設定で指定する必要があります。

**例：**

```
<spareserver enabledIf="$(hostname)!='front_srv1'" id="1" url="http://front_srv1:8080" />
<spareserver enabledIf="$(hostname)!='front_srv2'" id="2" url="http://front_srv2:8080" />
```

**enableIf** プロパティはオプション（デフォルトでは空）で、結果が true の場合にのみ接続を有効にできます。 これにより、すべてのリダイレクトサーバーで同一の設定を取得できます。

コンピューターのホスト名を取得するには、次のコマンドを実行します：**hostname -s**。



## 高可用性のワークフローとアフィニティ {#high-availability-workflows-and-affinities}

複数のワークフローサーバー（wfserver）を設定し、それらを 2 台以上のマシンに配布できます。 このタイプのアーキテクチャを選択する場合は、Adobe Campaign アクセスに応じてロードバランサーの接続モードを設定します。

Web からのアクセスの場合は、「**ロードバランサー**」モードを選択して接続時間を制限します。

Adobe Campaign コンソールを使用してアクセスする場合は、「**ハッシュ** または **スティッキー ip** モードを選択します。 これにより、リッチクライアントとサーバー間の接続を維持し、例えばインポートまたはエクスポートの操作中にユーザーセッションが中断されるのを防ぐことができます。

特定のマシン上でワークフローまたはワークフローアクティビティを強制的に実行するように選択できます。 それには、関係するワークフローまたはアクティビティに 1 つ以上のアフィニティを定義する必要があります。

1. **[!UICONTROL アフィニティ]** フィールドに入力して、ワークフローまたはアクティビティのアフィニティを作成します。

   任意のアフィニティ名を選択できますが、スペースや句読点を使用しないでください。 別のサーバーを使用する場合は、別の名前を指定してください。

   ![](assets/s_ncs_install_server_wf_affinity01.png)

   ![](assets/s_ncs_install_server_wf_affinity02.png)

   ドロップダウンリストには、以前使用したアフィニティが含まれます。 この処理は、時間の経過と共に、様々な入力値で完了します。

1. **nl6/conf/config-`<instance>.xml`** ファイルを開きます。
1. **[!UICONTROL wfserver]** モジュールに一致する行を次のように変更します。

   ```
   <wfserver autoStart="true" affinity="XXX,"/>
   ```

   複数のアフィニティを定義する場合は、スペースを入れずにコンマで区切る必要があります。

   ```
   <wfserver autoStart="true" affinity="XXX,YYY,"/>
   ```

   アフィニティが定義されていないワークフローを実行するには、アフィニティ名の後のコンマが必要です。

   アフィニティが定義されているワークフローのみを実行する場合は、アフィニティのリストの最後にコンマを追加しないでください。 例えば、以下のように行を変更します。

   ```
   <wfserver autoStart="true" affinity="XXX"/>
   ```

## 自動再起動 {#automatic-process-restart}

デフォルトでは、様々なAdobe Campaign プロセスが毎日午前 6 時（サーバー時間）に自動的に再起動します。

ただし、この設定は変更できます。

これをおこなうには、インストールの **conf** リポジトリにある **serverConf.xml** ファイルに移動します。

このファイルで設定された各プロセスには、**processRestartTime** 属性があります。 この属性の値を変更して、必要に応じて各プロセスの再起動時間を調整できます。

>[!IMPORTANT]
>
>この属性は削除しないでください。 すべてのプロセスを毎日再起動する必要があります。
