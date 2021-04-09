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
source-git-commit: ae4f86f3703b9bfe7f08fd5c2580dd5da8c28cbd
workflow-type: tm+mt
source-wordcount: '1582'
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

## 構成範囲

ニーズと設定に応じて、キャンペーンサーバーを設定または調整します。 次の操作をおこなうことができます。

* [内部識別子](#internal-identifier)を保護します。
* [キャンペーンプロセス](#enabling-processes)を有効にする
* [URL権限](url-permissions.md)を設定
* [セキュリティゾーン](security-zones.md)の定義
* [Tomcat設定](configure-tomcat.md)を構成
* [配信パラメーター](configure-delivery-settings.md)のカスタマイズ
* [動的ページセキュリティを定義し、](#dynamic-page-security-and-relays)を中継します
* [許可する外部コマンド](#restricting-authorized-external-commands)のリストを制限
* [重複した追跡](#redundant-tracking)の設定
* [高可用性とワークフローのアフィニティを管理](#high-availability-workflows-and-affinities)
* ファイル管理の設定 — [詳細情報](file-res-management.md)
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
