---
title: パイプラインの設定
description: パイプラインの設定方法
page-status-flag: never-activated
uuid: e2db7bdb-8630-497c-aacf-242734cc0a72
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
discoiquuid: 1c20795d-748c-4f5d-b526-579b36666e8f
translation-type: tm+mt
source-git-commit: f3caef21a269cf57624a07bfe1b4bf1e241061a6
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 19%

---


# パイプラインの設定 {#configuring-pipeline}

顧客 ID、秘密鍵、認証エンドポイントなどの認証パラメーターは、インスタンス設定ファイルで設定します。
処理されるトリガーのリストは、JSON形式のオプションで設定されます。
トリガーは、E メールを送信するキャンペーンワークフローでターゲティングに使用されます。キャンペーンは、両方のトリガーイベントを持つ顧客が E メールを受信するように設定されています。

>[!CAUTION]
>
>ハイブリッド展開の場合は、パイプラインが中間インスタンスに設定されていることを確認します。

## 前提条件 {#prerequisites}

この設定を開始する前に、次の点を確認してください。

* 最新Adobe Campaign:19.1.8または20.2.1以降のビルド、
* Adobe Analytics Standard版

また、次の情報も必要です。

* AdobeI/Oプロジェクト認証
* 有効なIMSOrgID。Adobe Analyticsが追加したExperience Cloud顧客のID
* IMS組織への開発者アクセス
* adobe analyticsで行われたトリガー設定

## 認証および設定ファイル {#authentication-configuration}

パイプラインはAdobe Experience Cloudでホストされるので、認証が必要です。
公開鍵と秘密鍵のペアが使用されます。このプロセスは、ユーザー/パスワードと同じ機能を持ちますが、セキュリティは高くなります。
認証は、AdobeI/Oプロジェクトを介したMarketing Cloudに対してサポートされます。

## 手順1:AdobeI/Oプロジェクトの作成/更新 {#creating-adobe-io-project}

ホストされるお客様の場合は、カスタマーケアチケットを作成して、Triggers統合のためのAdobeI/Oテクニカルアカウントトークンを組織で有効にすることができます。

オンプレミスのお客様の場合は、「Adobe Experience CloudトリガーのAdobeI/O [の設定](../../integrations/using/configuring-adobe-io.md) 」ページを参照してください。 AdobeI/O秘密鍵証明書にAPIを追加する際に **[!UICONTROL Adobe Analytics]** を選択する必要があることに注意してください。

## 手順2:NmsPipeline_Configパイプラインオプションの設定 {#configuring-nmspipeline}

認証が設定されると、パイプラインはイベントを取得します。 Adobe Campaignで設定されたトリガーのみが処理されます。 トリガーは、Adobe Analyticsから生成され、Adobe Campaignで設定されたトリガーのみを処理するパイプラインに送られる必要があります。
また、名前に関係なく、すべてのトリガーを取得するために、ワイルドカードを使用してオプションを設定することもできます。

1. Adobe Campaignで、 **[!UICONTROL 管理]** / **[!UICONTROL プラットフォーム]** / **[!UICONTROL オプションの下にあるオプションメニュー(]** Explorer )にアクセス ****&#x200B;します。

1. NmsPipeline_Config **[!UICONTROL オプションを選択します]** 。

1. 「 **[!UICONTROL 値（長いテキスト）]** 」フィールドに、2つのトリガーを指定する次のJSONコードを貼り付けることができます。 コメントは必ず削除する必要があります。

   ```
   {
   "topics": [ // list of "topics" that the pipelined is listening to.
      {
           "name": "triggers", // Name of the first topic: triggers.
           "consumer": "customer_dev", // Name of the instance that listens.  This value can be found on the monitoring page of Adobe Campaign.
           "triggers": [ // Array of triggers.
               {
                   "name": "3e8a2ba7-fccc-49bb-bdac-33ee33cf02bf", // TriggerType ID from Analytics 
                   "jsConnector": "cus:triggers.js" // Javascript library holding the processing function.
               }, {
                   "name": "2da3fdff-13af-4c51-8ed0-05802a572e94", // Second TriggerType ID 
                   "jsConnector": "cus:triggers.js" // Can use the same JS for all.
               },
           ]
       }
   ]
   }
   ```

1. また、すべてのトリガーを取得する次のJSONコードを貼り付けることもできます。

   ```
   {
   "topics": [
     {
       "name": "triggers",
       "consumer":  "customer_dev",
       "triggers": [
         {
           "name": "*",
           "jsConnector": "cus:pipeline.js"
         }
       ]
     }
   ]
   }
   ```

### The Consumer parameter {#consumer-parameter}

パイプラインは、サプライヤーや消費者モデルのように機能します。 メッセージは、個々の消費者に対してのみ使用されます。消費者はそれぞれ、メッセージのコピーを取得します。

The **Consumer** parameter identifies the instance as one of these consumers. インスタンスのIDがパイプラインを呼び出します。 クライアントコンソールの[監視]ページにあるインスタンス名を入力できます。

パイプラインサービスは、各コンシューマーが取得したメッセージを追跡します。異なるインスタンスに異なるコンシューマーを使用すると、すべてのメッセージを各インスタンスに送信するようにできます。

### パイプラインオプションの推奨 {#pipeline-option-recommendation}

パイプラインオプションを設定するには、次の推奨事項に従う必要があります。

* または **[!UICONTROL Triggersの下でトリガーを追加編集する場合は、残りのトリガーを編集しないでください]**。
* JSONが有効であることを確認します。 JSONバリデーターを使用できます。例えば、この [Webサイト](http://jsonlint.com/) を参照してください。
* &quot;name&quot;は、トリガーIDに対応します。 ワイルドカード「*」は、すべてのトリガーをキャッチします。
* &quot;consumer&quot;は、呼び出し元のインスタンスまたはアプリケーションの名前に対応します。
* パイプラインでは、「エイリアス」トピックもサポートされています。
* 変更を行った後は、必ずパイプラインで再起動する必要があります。

## 手順3:オプション設定 {#step-optional}

一部の内部パラメータは、必要な読み込み量に応じて変更できますが、実稼働環境に組み込む前に必ずテストしてください。

オプションのパラメーターのリストは次のとおりです。

| オプション | 説明 |
|:-:|:-:|
| appName（レガシー） | 公開鍵がアップロードされた従来のOAuthアプリケーションに登録されたOAuthアプリケーションのAppID。 詳しくは、この[ページ](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md.)を参照してください。 |
| authGatewayEndpoint（レガシ） | ゲートウェイトークンを取得するURL。 デフォルト: ```https://api.omniture.com``` |
| authPrivateKey（レガシー） | 秘密鍵、従来のOathアプリケーションにアップロードされた公開鍵、XtkKeyオプションで暗号化されたAES。 ```cryptString("PRIVATE_KEY")``` |
| disableAuth(Legacy) | 認証を無効にし、ゲートウェイトークンなしで接続すると、一部の開発パイプラインエンドポイントでのみ受け入れられます。 |
| discoverPipelineEndpoint | このテナントに使用するパイプラインサービスエンドポイントを検索するURLです。 デフォルト: ```https://producer-pipeline-pnw.adobe.net``` |
| dumpStatePeriodSec | 内部状態での内部状態プロセスの2つのダンプ間の期間も、 ```var/INSTANCE/pipelined.json.```<br> オンデマンドでアクセスできます。 ```http://INSTANCE:7781/pipelined/status``` |
| forcedPipelineEndpoint | PipelineServicesEndpointの検出を無効にして、PipelineServicesEndpointを強制的に検出します |
| monitorServerPort | パイプラインプロセスは、このポートでリッスンして内部状態プロセスを提供します。 ```http://INSTANCE:PORT/pipelined/status```. <br>デフォルトは 7781 です。 |
| pointerFlushMessageCount | この数のメッセージが処理されると、オフセットはデータベースに保存されます。 <br>デフォルトは 1000 です。 |
| pointerFlushPeriodSec | この期間を過ぎると、オフセットがデータベースに保存されます。<br>デフォルトは 5（秒）です |
| processingJSThreads | カスタム JS コネクタを使用してメッセージを処理する専用スレッドの数。<br>デフォルトは 4 です。 |
| processingThreads | 組み込みコードを使用してメッセージを処理する専用スレッドの数。<br>デフォルトは 4 です。 |
| retryPeriodSec | 処理エラーの場合の再試行間の遅延。 <br>デフォルトは 30（秒）です |
| retryValiditySec | この期間が経過してもメッセージが正常に処理されない場合（再試行回数が多すぎる場合）、メッセージを破棄します。<br>デフォルトは 300（秒）です |

### パイプラインプロセスの自動開始 {#pipelined-process-autostart}

パイプラインプロセスは自動的に開始する必要があります。

この場合、設定ファイルの&lt; pipelined >要素をautostart=&quot;true&quot;に設定します。

```
 <pipelined autoStart="true" ... "/>
```

### pipelined プロセスの再開 {#pipelined-process-restart}

変更を有効にするには、再起動が必要です。

```
nlserver restart pipelined@instance
```

## 手順4:検証 {#step-validation}

プロビジョニングのパイプライン設定を検証するには、次の手順に従います。

* Make sure the [!DNL pipelined] process is running.
* パイプライン接続ログのpipelined.logを確認します。
* 接続を確認し、pingを受け取ったかどうかを確認します。 ホスト対象のお客様は、クライアントコンソールから監視を使用できます。
