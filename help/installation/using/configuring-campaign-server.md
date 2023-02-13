---
product: campaign
title: Campaign サーバーの設定
description: Campaign サーバーの設定
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 46c8ed46-0947-47fb-abda-6541b12b6f0c
source-git-commit: 294309239bc476669e9e017c27bd1b51a0bdaf8c
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 3%

---

# Campaign サーバー設定の概要{#gs-campaign-server-config}

![](../../assets/v7-only.svg)

この章では、ニーズや環境特有の状況に合わせて実行できるサーバー側の設定について説明します。

## 制限事項

これらの手順は、次の操作に制限されます。 **オンプレミス**/**ハイブリッド** のデプロイメントおよび管理権限が必要です。

の場合 **ホスト** デプロイメント、サーバー側の設定は、Adobeのみで構成できます。 ただし、一部の設定は、 [キャンペーンCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/key-features.html?lang=ja):IP アクセス権許可リストの管理や URL アクセス権など。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/ip-allow-listing-instance-access.html?lang=ja)。

詳しくは、次の節を参照してください。

* [コントロールパネルに関するドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)
* [ホスティングモデル](../../installation/using/hosting-models.md)
* [Campaign Classicオンプレミス/ホスト機能マトリックス](../../installation/using/capability-matrix.md)

## 設定ファイル

Campaign Classic設定ファイルは、 **conf** Adobe Campaignインストールフォルダーのフォルダー。 設定は、次の 2 つのファイルに分散されます。

* **serverConf.xml**:すべてのインスタンスの一般的な設定。 このファイルは、Adobe Campaignサーバーの技術的パラメーターを組み合わせたものです。これらはすべてのインスタンスで共有されます。 これらのパラメーターのいくつかの説明を以下に示します。 様々なノードおよびパラメーターと、このリスト [セクション](../../installation/using/the-server-configuration-file.md).
* **config-`<instance>`.xml** ( **インスタンス** は、インスタンスの名前です )。インスタンスの特定の設定。 複数のインスタンスでサーバーを共有する場合は、各インスタンスに固有のパラメーターを関連するファイルに入力してください。

## 設定範囲

ニーズと設定に応じて、Campaign サーバーを設定または調整します。 以下を行うことができます。

* を保護します。 [内部識別子](#internal-identifier)
* 有効にする [キャンペーンプロセス](#enabling-processes)
* 設定 [URL へのアクセス権限](url-permissions.md)
* 定義 [セキュリティゾーン](security-zones.md)
* 設定 [Tomcat 設定](configure-tomcat.md)
* カスタマイズ [配信パラメーター](configure-delivery-settings.md)
* 定義 [動的ページのセキュリティとリレー](#dynamic-page-security-and-relays)
* リストを制限 [許可される外部コマンド](#restricting-authorized-external-commands)
* 設定 [重複した追跡](#redundant-tracking)
* 管理 [高可用性とワークフローの親和性](#high-availability-workflows-and-affinities)
* ファイル管理の設定 — [詳細情報](file-res-management.md)
   * アップロードファイル形式の制限
   * パブリックリソースへのアクセスを有効にする
   * プロキシ接続を設定
* [自動プロセス再起動](#automatic-process-restart)


## 内部識別子 {#internal-identifier}

この **内部** identifier は、インストール、管理、メンテナンスの目的で使用する技術的なログインです。 このログインはインスタンスに関連付けられていません。

このログインを使用して接続したオペレーターは、すべてのインスタンスに対するすべての権限を持ちます。 新規インストールの場合、このログインにはパスワードが含まれません。 このパスワードは手動で定義する必要があります。

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

サーバー上のAdobe Campaignプロセスは、 **config-default.xml** および **`config-<instance>.xml`** ファイル。

これらのファイルに変更を適用するには、Adobe Campaignサービスが起動している場合に、 **nlserver config -reload** コマンドを使用します。

プロセスには次の 2 つのタイプがあります。マルチインスタンスとシングルインスタンスの両方に対応しています。

* **マルチインスタンス**:すべてのインスタンスに対して 1 つの単一プロセスが開始されます。 これは **web**, **syslogd** および **trackinglogd** プロセス。

   有効化は、 **config-default.xml** ファイル。

   クライアントコンソールにアクセスし、リダイレクト（トラッキング）をおこなうAdobe Campaignサーバーを宣言する場合：

   ```
   vi nl6/conf/config-default.xml
   <web args="-tomcat" autoStart="true"/>  
   <!-- to start if the machine is also a redirection server -->  
   <trackinglogd autoStart="true"/>
   ```

   この例では、ファイルは **vi** 」コマンドを使用します。 任意の **.txt** または **.xml** 編集者。

* **モノインスタンス**:各インスタンス（モジュール）に対して 1 つのプロセスが開始されます。 **mta**, **wfserver**, **inMail**, **sms** および **stat**) をクリックします。

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

ストレージディレクトリ (**var** Adobe Campaignデータ（ログ、ダウンロード、リダイレクトなど）のディレクトリ内にあること。 これをおこなうには、 **XTK_VAR_DIR** システム変数：

* Windows の場合、 **XTK_VAR_DIR** システム変数

   ```
   D:\log\AdobeCampaign
   ```

* Linux の場合、 **customer.sh** ファイルを開き、次のように指定します。 **export XTK_VAR_DIR=/app/log/AdobeCampaign**.

   詳しくは、 [パラメーターをパーソナライズ](../../installation/using/installing-packages-with-linux.md#personalizing-parameters).


## 動的ページのセキュリティとリレー {#dynamic-page-security-and-relays}

デフォルトでは、すべての動的ページは、 **ローカル** Web モジュールが起動したマシンの Tomcat サーバー。 この設定は、 **`<url>`** のセクションに含まれています。 **ServerConf.xml** ファイル。

動的ページの実行を **リモート** server;コンピュータ上で Web モジュールがアクティブになっていない場合。 これをおこなうには、 **localhost** JSP および JSSP、Web アプリケーション、レポート、および文字列用のリモートコンピュータの名前を使用します。

使用可能な様々なパラメーターについて詳しくは、 **serverConf.xml** 設定ファイル。

JSP ページの場合、デフォルトの設定は次のようになります。

```
<url relayHost="true" relayPath="true" targetUrl="http://localhost:8080" urlPath="*.jsp"/>
```

Adobe Campaignは次の JSP ページを使用します。

* /nl/jsp/**soaproter.jsp**:クライアントコンソールと Web サービスの接続 (SOAP API)
* /nl/jsp/**m.jsp**:ミラーページ、
* /nl/jsp/**logon.jsp**:レポートへの Web ベースのアクセスと、クライアントコンソールのデプロイメント
* /nl/jsp/**s.jsp** :バイラルマーケティング（スポンサーおよびソーシャルネットワーク）の使用。

モバイルアプリチャネルで使用される JSSP は次のとおりです。

* nms/mobile/1/registerIOS.jssp
* nms/mobile/1/registerAndroid.jssp

**例：**

クライアントマシンが外部から接続されるのを防ぐことができます。 これをおこなうには、 **soaproter.jsp** ミラーページ、バイラルリンク、web フォーム、パブリックリソースの実行のみを許可します。

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

この例では、 **`<IP_addresses>`** の値は、このマスクにリレーモジュールを使用する権限を持つ IP アドレスのリスト（coma で区切られる）と一致します。

>[!NOTE]
>
>値は、設定とネットワークの制約に従って調整する必要があります。特に、インストールに対して特定の設定が開発されている場合は、この制約に従って調整します。

### HTTP ヘッダーの管理 {#managing-http-headers}

デフォルトでは、すべての HTTP ヘッダーは中継されません。 リレーから送信される返信に特定のヘッダーを追加できます。 手順は次のとおりです。

1. 次に移動： **serverConf.xml** ファイル。
1. 内 **`<relay>`** ノードで、リレーされた HTTP ヘッダーのリストに移動します。
1. を追加します。 **`<responseheader>`** 要素に次の属性を追加します。

   * **名前**:ヘッダー名
   * **値**:値の名前。

   例：

   ```
   <responseHeader name="Strict-Transport-Security" value="max-age=16070400; includeSubDomains"/>
   ```

## 許可する外部コマンドの制限 {#restricting-authorized-external-commands}

ビルド 8780 以降、技術管理者は、Adobe Campaignで使用できる承認済みの外部コマンドのリストを制限できます。

これをおこなうには、次のように、使用を禁止するコマンドのリストを含むテキストファイルを作成する必要があります。

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

内 **exec** サーバー設定ファイルのノードで、以前に作成したファイルを **blacklistFile** 属性。

**Linux のみ**:サーバー設定ファイルで、セキュリティ設定を強化する外部コマンドの実行専用のユーザーを指定することをお勧めします。 このユーザーは、 **exec** 設定ファイルのノード。 次の **serverConf.xml** を [セクション](../../installation/using/the-server-configuration-file.md).

>[!NOTE]
>
>ユーザーを指定しない場合、すべてのコマンドはAdobe Campaignインスタンスのユーザーコンテキストで実行されます。 ユーザーは、Adobe Campaignを実行しているユーザーとは異なる必要があります。

例：

```
<serverConf>
 <exec user="theUnixUser" blacklistFile="/pathtothefile/blacklist"/>
</serverConf>
```

このユーザーは、「neolane」Adobe Campaign演算子のスーダーリストに追加されている必要があります。

>[!IMPORTANT]
>
>カスタムスードは使用しないでください。 標準の sudo をシステムにインストールする必要があります。


## 重複した追跡 {#redundant-tracking}

リダイレクトに複数のサーバーを使用する場合、リダイレクトする URL からの情報を共有するには、SOAP 呼び出しを介して相互に通信できる必要があります。 配信の開始時に、一部のリダイレクションサーバーが使用できるとは限りません。したがって、同じレベルの情報を持っていない可能性があります。

>[!NOTE]
>
>標準アーキテクチャまたはエンタープライズアーキテクチャを使用する場合、メインアプリケーションサーバーは、各コンピューターにトラッキング情報をアップロードする権限を持っている必要があります。

冗長サーバーの URL は、 **serverConf.xml** ファイル。

**例：**

```
<spareserver enabledIf="$(hostname)!='front_srv1'" id="1" url="http://front_srv1:8080" />
<spareserver enabledIf="$(hostname)!='front_srv2'" id="2" url="http://front_srv2:8080" />
```

この **enableIf** プロパティはオプション（デフォルトでは空）で、結果が true の場合にのみ接続を有効にできます。 これにより、すべてのリダイレクトサーバーで同じ設定を取得できます。

コンピューターのホスト名を取得するには、次のコマンドを実行します。 **hostname -s**.



## 高可用性のワークフローとアフィニティ {#high-availability-workflows-and-affinities}

複数のワークフローサーバー (wfserver) を設定し、2 台以上のマシンに配布することができます。 このタイプのアーキテクチャを選択する場合は、Adobe Campaignへのアクセスに応じて、ロードバランサーの接続モードを設定します。

Web からアクセスする場合は、 **ロードバランサー** 接続時間を制限するモードです。

Adobe Campaignコンソールからにアクセスする場合は、「 **ハッシュ** または **共通 ip** モード。 これにより、リッチクライアントとサーバー間の接続を維持し、例えば、インポートまたはエクスポート操作中にユーザーセッションが中断されるのを防ぐことができます。

特定のマシン上でのワークフローまたはワークフローアクティビティの実行を強制するよう選択できます。 これをおこなうには、該当するワークフローまたはアクティビティに対して 1 つ以上のアフィニティを定義する必要があります。

1. ワークフローまたはアクティビティのアフィニティを作成するには、 **[!UICONTROL アフィニティ]** フィールドに入力します。

   親和性の名前は任意に選択できますが、スペースや句読点を使用しないようにしてください。 異なるサーバーを使用する場合は、異なる名前を指定します。

   ![](assets/s_ncs_install_server_wf_affinity01.png)

   ![](assets/s_ncs_install_server_wf_affinity02.png)

   ドロップダウンリストには、以前に使用したアフィニティが含まれています。 入力された値が異なる状態で、時間の経過と共に完了します。

1. を開きます。 **nl6/conf/config-`<instance>.xml`** ファイル。
1. 次に一致する行を変更 **[!UICONTROL wfserver]** モジュールの説明：

   ```
   <wfserver autoStart="true" affinity="XXX,"/>
   ```

   複数のアフィニティを定義する場合は、スペースを含まないコンマで区切る必要があります。

   ```
   <wfserver autoStart="true" affinity="XXX,YYY,"/>
   ```

   アフィニティが定義されていないワークフローを実行するには、アフィニティ名の後にあるコンマが必要です。

   アフィニティが定義されているワークフローのみを実行する場合は、アフィニティのリストの最後にコンマを追加しないでください。 例えば、次のように行を変更します。

   ```
   <wfserver autoStart="true" affinity="XXX"/>
   ```

## 自動再起動 {#automatic-process-restart}

デフォルトでは、異なるAdobe Campaignプロセスは、毎日午前 6 時（サーバー時間）に自動的に再起動します。

ただし、この設定は変更できます。

これをおこなうには、 **serverConf.xml** ファイルの場所は、 **conf** インストールのリポジトリ。

このファイルで設定された各プロセスには、 **processRestartTime** 属性。 この属性の値を変更し、必要に応じて各プロセスの再起動時間を調整できます。

>[!IMPORTANT]
>
>この属性は削除しないでください。 すべてのプロセスは毎日再起動する必要があります。
