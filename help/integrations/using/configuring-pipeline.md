---
title: 統合の設定
seo-title: 統合の設定
description: 統合の設定
seo-description: null
page-status-flag: never-activated
uuid: e2db7bdb-8630-497c-aacf-242734cc0a72
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
discoiquuid: 1c20795d-748c-4f5d-b526-579b36666e8f
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0112d5bd052ad66169225073276d1da4f3c245d8
workflow-type: ht
source-wordcount: '937'
ht-degree: 100%

---


# パイプラインの設定 {#configuring-pipeline}

顧客 ID、秘密鍵、認証エンドポイントなどの認証パラメーターは、インスタンス設定ファイルで設定します。
処理されるトリガーのリストは、オプションで設定します。これは JSON 形式です。
トリガーは、JavaScript コードを使用して直ちに処理されます。これ以上処理をおこなうことなく、リアルタイムにデータベーステーブルに保存されます。
トリガーは、E メールを送信するキャンペーンワークフローでターゲティングに使用されます。キャンペーンは、両方のトリガーイベントを持つ顧客が E メールを受信するように設定されています。

## 前提条件 {#prerequisites}

Campaign で [!DNL Experience Cloud Triggers] を使用するには、以下が必要です。

* Adobe Campaign バージョン 6.11 ビルド 8705 以降。
* Adobe Analytics Ultimate、Premium、Foundation、OD、Select、Prime、Mobile Apps、Select または Standard。

前もって必要な設定は次のとおりです。

* 秘密鍵ファイルの作成と、その鍵に登録された OAuth アプリケーションの作成
* Adobe Analytics でのトリガーの設定

Adobe Analytics 設定は、このドキュメントの範囲外です。

Adobe Campaign には、Adobe Analytics から次の情報が必要です。

* OAuth アプリケーションの名前
* IMSOrgId（Experience Cloud 顧客の ID）
* Analytics で設定されたトリガーの名前
* マーケティングデータベースと紐付けするデータフィールドの名前と形式

この設定の一部はカスタム開発であり、以下が必要です。

* Adobe Campaign での JSON、XML および JavaScript の解析に関する実務知識
* QueryDef API および Writer API の実務知識
* 秘密鍵を使用した暗号化と認証に関する実務概念

>[!NOTE]
>
>JS コードの編集には技術スキルが必要なので、きちんと理解していない限り JS コードを編集しないでください。<br>トリガーは、データベーステーブルに保存されます。したがって、トリガーデータは、ターゲティングワークフローのマーケティングオペレーターで安全に使用できます。

## 認証および設定ファイル {#authentication-configuration}

パイプラインは Adobe Experience Cloud でホストされるので、認証が必要です。
マーケティングサーバーがオンプレミスでホストされている場合、マーケティングサーバーがパイプラインにログインする際に、安全に接続するために認証が必要です。
公開鍵と秘密鍵のペアが使用されます。このプロセスは、ユーザー／パスワードと同じ機能で、より安全になっています。

### IMSOrgId {#imsorgid}

IMSOrgId は、Adobe Experience Cloud 上の顧客の識別子です。
インスタンスの serverConf.xml ファイルで IMSOrgId 属性にこれを設定します。
例：

```
<redirection IMSOrgId="C5E715(…)98A4@AdobeOrg" (…)
```

### キーの生成 {#key-generation}

キーはファイルのペアです。RSA 形式で、4096 バイト長です。OpenSSL などのオープンソースツールで生成できます。ツールを実行するたびに、新しいキーがランダムに生成されます。
便宜上、次の手順に従います。

* ```openssl genrsa -out <private_key.pem> 4096```

* ```openssl rsa -pubout -in <private_key.pem> -out <public_key.pem>```

private_key.pem ファイルの例：

```
----BEGIN RSA PRIVATE KEY----
MIIEowIBAAKCAQEAtqcYzt5WGGABxUJSfe1Xy8sAALrfVuDYURpdgbBEmS3bQMDb
(…)
64+YQDOSNFTKLNbDd+bdAA+JoYwUCkhFyvrILlgvlSBvwAByQ2Lx
----END RSA PRIVATE KEY----
```

public_key.pem ファイルの例：

```
----BEGIN PUBLIC KEY----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtqcYzt5WGGABxUJSfe1X
(…)
EwIDAQAB
----END PUBLIC KEY----
```

>[!NOTE]
>
>PuttyGen でキーを生成しないでください。OpenSSL が最適な選択肢です。

### Adobe Experience Cloud での OAuth クライアントの作成 {#oauth-client-creation}

**[!UICONTROL 管理者]**／**[!UICONTROL ユーザー管理]**／**[!UICONTROL 旧来の OAuth アプリケーション]**&#x200B;で正しい組織アカウントで Adobe Analytics にログインして、JWT タイプのアプリケーションを作成する必要があります。

次の手順に従います。

1. 「**[!UICONTROL サービスアカウント (JWT アサーション)]**」を選択します。
1. 「**[!UICONTROL アプリケーション名]**」を入力します。
1. 「**[!UICONTROL 公開鍵]**」を登録します。
1. トリガーの「**[!UICONTROL スコープ]**」を選択します。

   ![](assets/triggers_5.png)

1. 「**[!UICONTROL 作成]**」をクリックし、作成した「**[!UICONTROL アプリケーション ID」と「]**」と「**[!UICONTROL アプリケーション秘密鍵]**」を確認します。

   ![](assets/triggers_6.png)

### Adobe Campaign Classic でのアプリ名の登録 {#application-name-registration}

作成する OAuth クライアントのアプリケーション ID は、Adobe Campaign で設定する必要があります。それには、インスタンス設定ファイル内の [!DNL pipelined] 要素（特に appName 属性）を編集します。

例：

```
<pipelined autoStart="true" appName="applicationID" authPrivateKey="@qQf146pexBksGvo0esVIDO(…)"/>
```

### キーの暗号化 {#key-encription}

[!DNL pipelined] で使用するには、秘密鍵を暗号化する必要があります。暗号化は JavaScript の cryptString 関数を使用しておこなわれ、[!DNL pipelined] と同じインスタンスで実行する必要があります。

JavaScript を使用した秘密鍵暗号化の例については、[こちら](../../integrations/using/pipeline-troubleshooting.md)を参照してください。

暗号化された秘密鍵は Adobe Campaign に登録する必要があります。それには、インスタンス設定ファイル内の [!DNL pipelined] 要素（特に authPrivateKey 属性）を編集します。

例：

```
<pipelined autoStart="true" appName="applicationID" authPrivateKey="@qQf146pexBksGvo0esVIDO(…)"/>
```

### パイプラインプロセスの自動開始 {#pipelined-auto-start}

[!DNL pipelined] プロセスは自動的に開始する必要があります。
それには、設定ファイル内の要素を autostart=&quot;true&quot; に設定します。

```
<pipelined autoStart="true" appName="applicationID" authPrivateKey="@qQf146pexBksGvo0esVIDO(…)"/>
```

### pipelined プロセスの再開 {#pipelined-restart}

コマンドラインを使用して、手動で起動することもできます。

```
nlserver start pipelined@instance
```

変更を有効にするには、再起動が必要です。

```
nlserver restart pipelined@instance
```

エラーが発生した場合は、標準出力（手動で起動した場合）または [!DNL pipelined] ログファイルでエラーを探します。問題の解決方法について詳しくは、このドキュメントの「トラブルシューティング」の節を参照してください。

### パイプライン設定オプション {#pipelined-configuration-options}

| オプション | 説明 |
|:-:|:-:|
| appName | （公開鍵がアップロードされた）Adobe Analytics に登録されている OAuth アプリケーションの ID（アプリケーション ID）：管理者／ユーザー管理／旧来の OAuth アプリケーション。[こちら](../../integrations/using/configuring-pipeline.md#oauth-client-creation)を参照してください。 |
| authGatewayEndpoint | 「ゲートウェイトークン」を取得するための URL。<br>デフォルト：https://api.omniture.com |
| authPrivateKey | 秘密鍵。公開部分は Adobe Analytics でアップロード済み（この節を参照）。XtkSecretKey オプションで暗号化された AES：xtk.session.EncryptPassword(&quot;PRIVATE_KEY&quot;); |
| disableAuth | 認証の無効化（ゲートウェイトークンを使用せずに接続することは、一部の開発パイプラインエンドポイントでのみ可能です） |
| discoverPipelineEndpoint | このテナントに使用するパイプラインサービスエンドポイントを検出するための URL です。デフォルト：https://producer-pipeline-pnw.adobe.net |
| dumpStatePeriodSec | var/INSTANCE/pipelined.json 内部状態におけるプロセス内部状態の 2 回のダンプ間の期間も、http://INSTANCE/pipelined/status（ポート 7781）でオンデマンドでアクセスできます。 |
| forcedPipelineEndpoint | PipelineServicesEndpoint の検出を無効にし、強制的におこないます |
| monitorServerPort | [!DNL pipelined] プロセスは、このポートでリッスンして、http://INSTANCE/pipelined/status（ポート 7781）でプロセス内部状態を提供します。 |
| pointerFlushMessageCount | この数のメッセージが処理されると、オフセットがデータベースに保存されます。デフォルトは 1000 です。 |
| pointerFlushPeriodSec | この期間を過ぎると、オフセットがデータベースに保存されます。デフォルトは 5（秒）です |
| processingJSThreads | カスタム JS コネクタを使用してメッセージを処理する専用スレッドの数。デフォルトは 4 です。 |
| processingThreads | 組み込みコードを使用してメッセージを処理する専用スレッドの数。デフォルトは 4 です。 |
| retryPeriodSec | 再試行間の遅延（処理エラーがある場合）。デフォルトは 30（秒）です |
| retryValiditySec | この期間が経過してもメッセージが正常に処理されない場合（再試行回数が多すぎる場合）、メッセージを破棄します。デフォルトは 300（秒）です |
