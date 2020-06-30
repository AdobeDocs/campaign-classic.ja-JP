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
translation-type: tm+mt
source-git-commit: 39d6da007d69f81da959660b24b56ba2558a97ba
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 1%

---


# パイプラインの設定 {#configuring-pipeline}

顧客ID、秘密鍵、認証エンドポイントなどの認証パラメーターは、インスタンス設定ファイルで設定します。
処理されるトリガーのリストは、オプションで設定します。 JSON形式です。
トリガーは、JavaScriptコードを使用して直ちに処理されます。 これ以上の処理をリアルタイムに行うことなく、データベーステーブルに保存されます。
トリガーは、電子メールを送信するキャンペーンワークフローでのターゲティングに使用されます。 キャンペーンは、両方のトリガーイベントを持つ顧客が電子メールを受信できるように設定されています。

## 前提条件 {#prerequisites}

キャンペーン [!DNL Experience Cloud Triggers] での使用には、次が必要です。

* Adobe Campaignバージョン6.11ビルド8705以降。
* Adobe Ultimate、Premium、Foundation、OD、Select、Prime、Mobile Apps、SelectまたはStandard。

前提条件の設定は次のとおりです。

* 秘密鍵ファイルを作成し、その鍵に登録されたoAuthアプリケーションを作成します。
* アドビAnalyticsでのトリガーの設定。

アドビのAnalytics設定は、このドキュメントの範囲外です。

Adobe Campaignには、アドビのAnalyticsから次の情報が必要です。

* oAuthアプリケーションの名前。
* IMSOrgId。Experience Cloud顧客のIDです。
* Analyticsで設定されたトリガーの名前。
* マーケティングデータベースと調整するデータフィールドの名前と形式です。

この設定の一部はカスタム開発であり、以下が必要です。

* Adobe CampaignでのJSON、XMLおよびJavaScriptの解析に関する実用的な知識
* QueryDef APIおよびWriter APIの実用的な知識
* 秘密鍵を使用した暗号化と認証の機能に関する概念。

>[!NOTE]
>
>JSコードの編集には技術的なスキルが必要なので、適切な理解が得られない限りJSコードを編集しないでください。 <br>トリガーは、データベーステーブルに保存されます。 したがって、トリガーデータは、ターゲティングワークフローのマーケティング演算子で安全に使用できます。

## 認証および設定ファイル {#authentication-configuration}

パイプラインはAdobe Experience Cloudでホストされるので、認証が必要です。
Marketingサーバーがオンプレミスでホストされている場合、Marketingサーバーがパイプラインにログインする際に、安全な接続を持つために認証が必要です。
公開鍵と秘密鍵のペアを使用します。 このプロセスは、ユーザー/パスワードと同じ機能で、より安全です。

### IMSOrgId {#imsorgid}

IMSOrgIdは、Adobe Experience Cloud上の顧客の識別子です。
IMSOrgId属性の下のインスタンスserverConf.xmlファイルに設定します。
例：

```
<redirection IMSOrgId="C5E715(…)98A4@AdobeOrg" (…)
```

### 鍵の生成 {#key-generation}

鍵はファイルのペアです。 RSA形式で、4096バイト長です。 OpenSSLなどのオープンソースツールを使用して生成できます。 ツールを実行するたびに、新しいキーがランダムに生成されます。
便宜上、次の手順を行います。

* ```openssl genrsa -out <private_key.pem> 4096```

* ```openssl rsa -pubout -in <private_key.pem> -out <public_key.pem>```

private_key.pemファイルの例：

```
----BEGIN RSA PRIVATE KEY----
MIIEowIBAAKCAQEAtqcYzt5WGGABxUJSfe1Xy8sAALrfVuDYURpdgbBEmS3bQMDb
(…)
64+YQDOSNFTKLNbDd+bdAA+JoYwUCkhFyvrILlgvlSBvwAByQ2Lx
----END RSA PRIVATE KEY----
```

public_key.pemファイルの例：

```
----BEGIN PUBLIC KEY----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtqcYzt5WGGABxUJSfe1X
(…)
EwIDAQAB
----END PUBLIC KEY----
```

>[!NOTE]
>
>PuttyGenではキーを生成しないでください。OpenSSLが最適な選択肢です。

### Adobe Experience CloudでのAuthクライアントの作成 {#oauth-client-creation}

タイプJWTのアプリケーションは、 **[!UICONTROL 管理者]** / **[!UICONTROL ユーザー管理]** / ****&#x200B;従来のOathアプリケーションの下にある正しい組織アカウントでアドビのAnalyticsにログインして作成する必要があります。

次の手順に従います。

1. 「 **[!UICONTROL サービスアカウント(JWT Assertion)」を選択し]**&#x200B;ます。
1. 「 **[!UICONTROL Application Name]**」を入力します。
1. **[!UICONTROL 公開鍵を登録します]**。
1. トリガーの **[!UICONTROL スコープを選択します]**。

   ![](assets/triggers_5.png)

1. 「 **[!UICONTROL 作成]** 」をクリックし、 **[!UICONTROL 作成したアプリケーション ID]** と **** アプリケーション秘密鍵を確認します。

   ![](assets/triggers_6.png)

### Adobe Campaignクラシックでのアプリ名の登録 {#application-name-registration}

作成するoAuthクライアントのアプリケーション IDは、Adobe Campaignで構成する必要があります。 これを行うには、パイプライン要素（特にappName属性）のインスタンス設定ファイルを編集します。

例：

```
<pipelined autoStart="true" appName="applicationID" authPrivateKey="@qQf146pexBksGvo0esVIDO(…)"/>
```

### 鍵の暗号化 {#key-encription}

パイプラインで使用するには、秘密鍵を暗号化する必要があります。 暗号化はJavaScriptのcryptString関数を使用して行われ、パイプラインと同じインスタンスで実行する必要があります。

JavaScriptを使用した秘密鍵暗号化の例をこの [ページで紹介します](../../integrations/using/pipeline-troubleshooting.md)。

暗号化された秘密鍵はAdobe Campaignに登録する必要があります。 これを行うには、パイプライン要素（特にauthPrivateKey属性）のインスタンス設定ファイルを編集します。

例：

```
<pipelined autoStart="true" appName="applicationID" authPrivateKey="@qQf146pexBksGvo0esVIDO(…)"/>
```

### パイプラインプロセスの自動開始 {#pipelined-auto-start}

パイプラインプロセスは自動的に開始する必要があります。
これを行うには、設定ファイル内の要素をautostart=&quot;true&quot;に設定します。

```
<pipelined autoStart="true" appName="applicationID" authPrivateKey="@qQf146pexBksGvo0esVIDO(…)"/>
```

### パイプラインプロセスの再開 {#pipelined-restart}

コマンドラインを使用して、手動で起動することもできます。

```
nlserver start pipelined@instance
```

変更を有効にするには、再起動が必要です。

```
nlserver restart pipelined@instance
```

エラーが発生した場合は、標準出力（手動で起動した場合）またはパイプライン付きログファイルでエラーを探します。 問題の解決方法の詳細については、このドキュメントの「トラブルシューティング」の項を参照してください。

### パイプライン構成オプション {#pipelined-configuration-options}

| オプション | 説明 |
|:-:|:-:|
| appName | （公開鍵がアップロードされた）AdobeAnalyticsに登録されているOAuthアプリケーション(アプリケーション ID)のID: 管理者/ユーザー管理/レガシーのOathアプリケーション。 Refer to this [section](../../integrations/using/configuring-pipeline.md#oauth-client-creation). |
| authGatewayEndpoint | 「ゲートウェイトークン」を取得するURL。 <br> デフォルト：https://api.omniture.com |
| authPrivateKey | 秘密鍵(公開パーツはAdobeAnalyticsにアップロードされました（この節を参照）。 XtkSecretKeyオプションで暗号化されたAES: xtk.session.EncryptPassword(&quot;PRIVATE_KEY&quot;); |
| disableAuth | 認証の無効化（ゲートウェイトークンを使用しない接続は、一部の開発パイプラインエンドポイントでのみ受け入れられます） |
| discoverPipelineEndpoint | このテナントに使用するパイプラインサービスエンドポイントを検出するURLです。 デフォルト：https://producer-pipeline-pnw.adobe.net |
| dumpStatePeriodSec | var/INSTANCE/pipelined.json内部状態のプロセス内部状態の2ダンプ間の期間も、http://INSTANCE/pipelined/statusでオンデマンドでアクセスできます（ポート7781）。 |
| forcedPipelineEndpoint | PipelineServicesEndpointの検出を無効にし、強制的に行います |
| monitorServerPort | パイプラインプロセスは、このポートをリッスンして、http://INSTANCE/pipelined/status（ポート7781）でプロセス内部状態を提供します。 |
| pointerFlushMessageCount | この数のメッセージが処理されると、オフセットはデータベースに保存されます。 初期設定は1000です。 |
| pointerFlushPeriodSec | この期間を過ぎると、オフセットはデータベースに保存されます。 初期設定は5（秒）です |
| processingJSThreads | カスタムJSコネクタを使用してメッセージを処理する専用スレッドの数。 初期設定は4です。 |
| processingThreads | 組み込みコードを含むメッセージを処理する専用スレッドの数。 初期設定は4です。 |
| retryPeriodSec | 再試行間の遅延（処理エラーがある場合） 初期設定は30（秒）です |
| retryValiditySec | この期間後に正常に処理されない場合(再試行数が多すぎる場合)、メッセージを破棄します。 初期設定は300（秒）です |
