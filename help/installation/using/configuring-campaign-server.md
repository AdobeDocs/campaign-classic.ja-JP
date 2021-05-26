---
solution: Campaign Classic
product: campaign
title: Campaign サーバーの設定
description: Campaign サーバーの設定
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 46c8ed46-0947-47fb-abda-6541b12b6f0c
source-git-commit: bce114f36d1ec4582fc79e750d48155ba0d7cd1f
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 2%

---

# Campaignサーバー設定の概要{#gs-campaign-server-config}

この章では、ニーズや環境に特化した設定に合わせて実行できるサーバー側の設定について説明します。

## 制限事項

これらの手順は、オンプレミス&#x200B;**/**&#x200B;ハイブリッド&#x200B;**デプロイメントに制限され、管理権限が必要です。**

**ホストされる**&#x200B;デプロイメントの場合、サーバー側の設定はAdobeのみで設定できます。 ただし、IPCampaign コントロールパネル管理やURL権限など、[キャンペーン管理](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/key-features.html)内で設定でき許可リストる設定もあります。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/ip-allow-listing-instance-access.html)。

詳しくは、次の節を参照してください。

* [コントロールパネルのドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)
* [ホスティングのモデル](../../installation/using/hosting-models.md)
* [Campaign Classicオンプレミスとホスト機能のマトリックス](../../installation/using/capability-matrix.md)

## 設定ファイル

Campaign Classic設定ファイルは、Adobe Campaignインストールフォルダーの&#x200B;**conf**&#x200B;フォルダーに保存されます。 設定は、次の2つのファイルに分散されます。

* **serverConf.xml**:すべてのインスタンスの一般的な設定。このファイルは、Adobe Campaignサーバーの技術的パラメーターを組み合わせたものです。これらはすべてのインスタンスで共有されます。 これらのパラメーターの一部の説明を以下に示します。 この[節](../../installation/using/the-server-configuration-file.md)に示す様々なノードおよびパラメーター。
* **config-`<instance>`.xml** (instanceはイ **** ンスタンスの名前):インスタンスの特定の設定。複数のインスタンスでサーバーを共有する場合は、各インスタンスに固有のパラメーターを関連するファイルに入力してください。

## 設定の範囲

ニーズと設定に応じて、Campaignサーバーを設定または調整します。 次の操作をおこなうことができます。

* [内部識別子](#internal-identifier)を保護します。
* [キャンペーンプロセス](#enabling-processes)を有効にする
* [URLの権限](url-permissions.md)の設定
* [セキュリティゾーン](security-zones.md)を定義します
* [Tomcatの設定](configure-tomcat.md)を構成します。
* [配信パラメーター](configure-delivery-settings.md)のカスタマイズ
* [動的ページセキュリティとリレー](#dynamic-page-security-and-relays)を定義します
* [許可される外部コマンド](#restricting-authorized-external-commands)のリストを制限します
* [冗長トラッキング](#redundant-tracking)を設定します
* [高可用性とワークフローの親和性を管理](#high-availability-workflows-and-affinities)
* ファイル管理の設定 — [詳細](file-res-management.md)
   * アップロードファイル形式の制限
   * パブリックリソースへのアクセスを有効にする
   * プロキシ接続の設定
* [プロセスの自動再起動](#automatic-process-restart)


## 内部識別子{#internal-identifier}

**内部**&#x200B;識別子は、インストール、管理、メンテナンスの目的で使用される技術的なログインです。 このログインは、インスタンスに関連付けられていません。

このログインを使用して接続したオペレーターは、すべてのインスタンスに対してすべての権限を持ちます。 新規インストールの場合、このログインにはパスワードが含まれません。 このパスワードは手動で定義する必要があります。

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

## プロセス{#enabling-processes}を有効にする

サーバー上のAdobe Campaignプロセスは、**config-default.xml**&#x200B;ファイルと&#x200B;**`config-<instance>.xml`**&#x200B;ファイルを介して有効（および無効）になります。

これらのファイルに変更を適用するには、Adobe Campaignサービスが起動している場合に、 **nlserver config -reload**&#x200B;コマンドを実行する必要があります。

次の2種類のプロセスがあります。マルチインスタンスとシングルインスタンスの両方に対応しています。

* **マルチインスタンス**:すべてのインスタンスに対して1つのプロセスが開始されます。**web**、**syslogd**、**trackinglogd**&#x200B;プロセスの場合です。

   イネーブルメントは、**config-default.xml**&#x200B;ファイルから設定できます。

   クライアントコンソールにアクセスし、リダイレクト（トラッキング）をおこなうためのAdobe Campaignサーバーの宣言：

   ```
   vi nl6/conf/config-default.xml
   <web args="-tomcat" autoStart="true"/>  
   <!-- to start if the machine is also a redirection server -->  
   <trackinglogd autoStart="true"/>
   ```

   この例では、Linuxの&#x200B;**vi**&#x200B;コマンドを使用してファイルを編集します。 任意の&#x200B;**.txt**&#x200B;または&#x200B;**.xml**&#x200B;エディターを使用して編集できます。

* **モノラルインスタンス**:各インスタンス（以下のモジュール）に対して1つのプロセスが開始されます。 **mta**、 **wfserver**、 **inMail**、smsand  **** stat ****)。

   有効化は、インスタンスの設定ファイルを使用して設定できます。

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

**Campaignデータストレージ**

Adobe Campaignデータのストレージディレクトリ（**var**&#x200B;ディレクトリ）（ログ、ダウンロード、リダイレクトなど）を設定できます。 これをおこなうには、システム変数&#x200B;**XTK_VAR_DIR**&#x200B;を使用します。

* Windowsの場合、**XTK_VAR_DIR**&#x200B;システム変数に次の値を入力します。

   ```
   D:\log\AdobeCampaign
   ```

* Linuxの場合、**customer.sh**&#x200B;ファイルに移動し、次の情報を入力します。**XTK_VAR_DIR=/app/log/AdobeCampaign**&#x200B;を書き出します。

   詳しくは、[パラメーターのパーソナライズ](../../installation/using/installing-packages-with-linux.md#personalizing-parameters)を参照してください。


## 動的ページのセキュリティとリレー{#dynamic-page-security-and-relays}

デフォルトでは、すべての動的ページは、Webモジュールが起動したマシンの&#x200B;**ローカル** Tomcatサーバーに自動的に関連付けられます。 この設定は、**ServerConf.xml**&#x200B;ファイルのクエリリレー設定の&#x200B;**`<url>`**&#x200B;セクションに入力します。

動的ページの実行を&#x200B;**リモート**&#x200B;サーバー上でリレーできます。（Webモジュールがコンピューター上で有効になっていない場合）。 これをおこなうには、**localhost**&#x200B;を、JSPおよびJSSP、Webアプリケーション、レポートおよび文字列用のリモートコンピューターの名前に置き換える必要があります。

使用可能な様々なパラメーターについて詳しくは、**serverConf.xml**&#x200B;設定ファイルを参照してください。

JSPページの場合、デフォルトの設定は次のとおりです。

```
<url relayHost="true" relayPath="true" targetUrl="http://localhost:8080" urlPath="*.jsp"/>
```

Adobe Campaignは次のJSPページを使用します。

* /nl/jsp/**soaprouter.jsp**:クライアントコンソールとWebサービス接続(SOAP API)
* /nl/jsp/**m.jsp**:ミラーページ、
* /nl/jsp/**logon.jsp**:レポートへのWebベースのアクセスと、クライアントコンソールのデプロイメント
* /nl/jsp/**s.jsp** :バイラルマーケティング（スポンサーとソーシャルネットワーク）の使用。

モバイルアプリチャネルで使用されるJSSPは次のとおりです。

* nms/mobile/1/registerIOS.jssp
* nms/mobile/1/registerAndroid.jssp

**例：**

クライアントマシンの外部からの接続を防ぐことができます。 これを行うには、**soapprouter.jsp**&#x200B;の実行を制限し、ミラーページ、バイラルリンク、Webフォームおよびパブリックリソースの実行のみを許可します。

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

この例では、**`<IP_addresses>`**&#x200B;値は、このマスクにリレーモジュールを使用する権限を持つIPアドレスのリスト（コマで区切られたリスト）に一致します。

>[!NOTE]
>
>値は、設定とネットワークの制約に従って適応する必要があります。特に、インストール用に特定の設定が開発されている場合は、適応します。

### HTTPヘッダーの管理{#managing-http-headers}

デフォルトでは、すべてのHTTPヘッダーは中継されません。 リレーで送信される返信に、特定のヘッダーを追加できます。 手順は次のとおりです。

1. **serverConf.xml**&#x200B;ファイルに移動します。
1. **`<relay>`**&#x200B;ノードで、中継されるHTTPヘッダーのリストに移動します。
1. 次の属性を持つ&#x200B;**`<responseheader>`**&#x200B;要素を追加します。

   * **名前**:ヘッダー名
   * **値**:値の名前。

   例：

   ```
   <responseHeader name="Strict-Transport-Security" value="max-age=16070400; includeSubDomains"/>
   ```

## 許可された外部コマンドを制限する{#restricting-authorized-external-commands}

ビルド8780以降、技術管理者は、Adobe Campaignで使用できる許可済みの外部コマンドのリストを制限できます。

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

サーバー設定ファイルの&#x200B;**exec**&#x200B;ノードで、**blacklistFile**&#x200B;属性で、前に作成したファイルを参照する必要があります。

**Linuxの場合のみ**:サーバー設定ファイルで、セキュリティ設定を強化するために、外部コマンドの実行専用のユーザーを指定するコマンドを再実行します。このユーザーは、設定ファイルの&#x200B;**exec**&#x200B;ノードに設定されます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に記載されています。

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
>カスタムスードは使用しないでください。 標準のsudoをシステムにインストールする必要があります。


## 重複した追跡{#redundant-tracking}

リダイレクトに複数のサーバーを使用する場合、リダイレクトするURLからの情報を共有するには、SOAP呼び出しを介して相互に通信できる必要があります。 配信の開始時に、すべてのリダイレクションサーバーが使用可能とは限りません。したがって、同じレベルの情報を持たない可能性があります。

>[!NOTE]
>
>標準アーキテクチャまたはエンタープライズアーキテクチャを使用する場合、メインアプリケーションサーバーに、各コンピューター上のトラッキング情報をアップロードする権限が必要です。

冗長サーバーのURLは、**serverConf.xml**&#x200B;ファイルを使用して、リダイレクト設定で指定する必要があります。

**例：**

```
<spareserver enabledIf="$(hostname)!='front_srv1'" id="1" url="http://front_srv1:8080" />
<spareserver enabledIf="$(hostname)!='front_srv2'" id="2" url="http://front_srv2:8080" />
```

**enableIf**&#x200B;プロパティはオプションです（デフォルトでは空です）。結果がtrueの場合にのみ接続を有効にできます。 これにより、すべてのリダイレクションサーバーで同じ設定を取得できます。

コンピューターのホスト名を取得するには、次のコマンドを実行します。**hostname -s**.



## 高可用性のワークフローとアフィニティ{#high-availability-workflows-and-affinities}

複数のワークフローサーバー(wfserver)を設定し、2つ以上のマシンに配布できます。 このタイプのアーキテクチャを選択する場合は、Adobe Campaignへのアクセスに応じてロードバランサーの接続モードを設定します。

Webからのアクセスの場合は、**ロードバランサー**&#x200B;モードを選択して接続時間を制限します。

Adobe Campaignコンソールからアクセスする場合は、**hash**&#x200B;または&#x200B;**sticky ip**&#x200B;モードを選択します。 これにより、リッチクライアントとサーバー間の接続を維持し、例えば、インポートまたはエクスポート操作中にユーザーセッションが中断されるのを防ぐことができます。

特定のマシン上でのワークフローまたはワークフローアクティビティの実行を強制するよう選択できます。 これをおこなうには、該当するワークフローまたはアクティビティに対して1つ以上のアフィニティを定義する必要があります。

1. 「**[!UICONTROL 親和性]**」フィールドに入力して、ワークフローまたはアクティビティのアフィニティを作成します。

   アフィニティ名は任意に選択できますが、スペースや句読点を使用しないようにしてください。 異なるサーバーを使用する場合は、異なる名前を指定します。

   ![](assets/s_ncs_install_server_wf_affinity01.png)

   ![](assets/s_ncs_install_server_wf_affinity02.png)

   ドロップダウンリストには、以前に使用したアフィニティが含まれています。 入力された値が異なり、時間の経過と共に完了します。

1. **nl6/conf/config-`<instance>.xml`**&#x200B;ファイルを開きます。
1. **[!UICONTROL wfserver]**&#x200B;モジュールに一致する行を次のように変更します。

   ```
   <wfserver autoStart="true" affinity="XXX,"/>
   ```

   複数のアフィニティを定義する場合は、スペースを含まないコンマで区切る必要があります。

   ```
   <wfserver autoStart="true" affinity="XXX,YYY,"/>
   ```

   アフィニティが定義されていないワークフローを実行するには、アフィニティ名の後にコンマが続く必要があります。

   アフィニティが定義されているワークフローのみを実行する場合は、アフィニティのリストの最後にコンマを追加しないでください。 例えば、次のように行を変更します。

   ```
   <wfserver autoStart="true" affinity="XXX"/>
   ```

## 自動再起動{#automatic-process-restart}

デフォルトでは、様々なAdobe Campaignプロセスは、毎日午前6時（サーバー時間）に自動的に再起動します。

ただし、この設定は変更できます。

これをおこなうには、インストール先の&#x200B;**conf**&#x200B;リポジトリにある&#x200B;**serverConf.xml**&#x200B;ファイルに移動します。

このファイルで設定された各プロセスには、**processRestartTime**&#x200B;属性があります。 この属性の値を変更して、必要に応じて各プロセスの再開時間を調整できます。

>[!IMPORTANT]
>
>この属性は削除しないでください。 すべてのプロセスは毎日再起動する必要があります。
