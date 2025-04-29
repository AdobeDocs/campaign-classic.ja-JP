---
product: campaign
title: パイプラインの設定
description: Campaign とトリガーの統合用にパイプラインを設定する方法について説明します
feature: Triggers
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
level: Intermediate, Experienced
exl-id: 2d214c36-8429-4b2b-b1f5-fe2730581bba
source-git-commit: 2bfcec5eaa1145cfb88adfa9c8b2f72ee3cd9469
workflow-type: ht
source-wordcount: '843'
ht-degree: 100%

---

# パイプラインの設定 {#configuring-pipeline}

顧客 ID、秘密鍵、認証エンドポイントなどの認証パラメーターは、インスタンス設定ファイルで設定します。

処理されるトリガーのリストは、JSON フォーマットでオプションに設定されます。

トリガーは、メールを送信するキャンペーンワークフローでターゲティングに使用されます。キャンペーンは、両方のトリガーイベントを持つ顧客がメールを受信するように設定されています。

## 前提条件 {#prerequisites}

この設定を開始する前に、以下があることを確認してください。

* Adobe Developer プロジェクト
* 有効な組織 ID - 組織 ID を見つけるには、[このページ](https://experienceleague.adobe.com/ja/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255){_blank}を参照してください。
* 組織への開発者のアクセス
* Adobe Analytics での有効なトリガー設定

パイプラインは Adobe Experience Cloud でホストされるので、認証が必要です。Adobe Developer プロジェクト経由でサポートされている認証を使用します。

## 手順 1：Adobe Developer プロジェクトを作成／更新 {#creating-adobe-io-project}

トリガー統合用の Adobe Developer アカウントトークンを使用して、組織を有効にする必要があります。

アドビのテクニカルアカウントの作成方法については、[このページ](../../integrations/using/oauth-technical-account.md)を参照してください。Adobe Developer 資格情報に API を追加する際に、「**[!UICONTROL Adobe Analytics]**」を選択する必要があります。

## 手順 2：パイプラインオプションを設定 {#configuring-nmspipeline}

認証が設定されると、パイプラインはイベントを取得します。Adobe Campaign で設定されたトリガーのみが処理されます。トリガーは、Adobe Analytics から生成され、Adobe Campaign で設定されたトリガーのみを処理するパイプラインに送られる必要があります。

また、名前に関係なく、すべてのトリガーを取得するように、ワイルドカードを使用して設定することもできます。

1. Adobe Campaign の&#x200B;**[!UICONTROL エクスプローラー]**&#x200B;で、**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL オプション]**&#x200B;のオプションメニューにアクセスします。

1. **[!UICONTROL 「NmsPipeline_Config]**」オプションを選択します。

1. 「**[!UICONTROL 値 (長いテキスト)]**」フィールドに、次の JSON コードを貼り付けることができます。このコードは、2 つのトリガーを指定します。コメントは必ず削除してください。

   ```json
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

1. また、次のすべてのトリガーを取得する JSON コードを貼り付けることもできます。

   ```json
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

### Consumer パラメーターを設定 {#consumer-parameter}

パイプラインは、「サプライヤーとコンシューマー」モデルのように機能します。メッセージは、個々のコンシューマーによってのみ消費されます。コンシューマーはそれぞれ、メッセージのコピーを取得します。

**Consumer** パラメーターは、インスタンスをこれらのコンシューマーの 1 つとして識別します。インスタンスの ID がパイプラインを呼び出します。クライアントコンソールの監視ページにあるインスタンス名を入力できます。

パイプラインサービスは、各コンシューマーが取得したメッセージを追跡します。異なるインスタンスに異なるコンシューマーを使用すると、すべてのメッセージを各インスタンスに送信するようにできます。

### パイプラインオプションのレコメンデーション {#pipeline-option-recommendation}

パイプラインオプションを設定するには、次のレコメンデーションに従う必要があります。

* **[!UICONTROL トリガー]**&#x200B;でトリガーを追加または編集します。
* JSON が有効であることを確認します。
* **Name** パラメーターは、トリガー ID に対応します。ワイルドカード「*」は、すべてのトリガーを取得します。
* **Consumer** パラメーターは、呼び出し元のインスタンスまたはアプリケーションの名前に対応します。
* `pipelined` プロセスでは、「aliases」トピックもサポートしています。
* 変更を加えた後は、必ず `pipelined` プロセスをやり直す必要があります。

## （オプション）手順 3：追加の設定 {#step-optional}

一部の内部パラメーターは、必要な読み込み量に応じて変更できますが、実稼動環境に適用する前に必ずテストする必要があります。

オプションのパラメーターのリストを以下に示します。

| オプション | 説明 |
|:-:|:-:|
| appName(Legacy) | 公開鍵がアップロードされた OAuth レガシーアプリケーションに登録されている OAuth アプリケーションの App ID。詳しくは、この[ページ](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md)を参照してください。 |
| authGatewayEndpoint（レガシー） | ゲートウェイトークンを取得するための URL。デフォルト：```https://api.omniture.com``` |
| authPrivateKey（レガシー） | 秘密鍵、OAuth レガシーアプリケーションにアップロードされた公開部分、XtkKey オプション「```cryptString("PRIVATE_KEY")```」で暗号化された AES。 |
| disableAuth（レガシー） | 認証の無効化（ゲートウェイトークンを使用せずに接続することは、一部の開発パイプラインエンドポイントでのみ可能）。 |
| discoverPipelineEndpoint | このテナントに使用するパイプラインサービスエンドポイントを見つけるための URL。デフォルト：```https://producer-pipeline-pnw.adobe.net``` |
| dumpStatePeriodSec | ```var/INSTANCE/pipelined.json.``` での内部ステートプロセスの 2 つのダンプ間の期間<br>内部ステートはオンデマンドで ```http://INSTANCE:7781/pipelined/status``` でもアクセスできます。 |
| forcedPipelineEndpoint | PipelineServicesEndpoint の検出を無効にし、強制的におこないます。 |
| monitorServerPort | パイプライン化されたプロセスは、このポートでリッスンして内部ステートプロセスを ```http://INSTANCE:PORT/pipelined/status``` で提供します。<br>デフォルトは 7781 です。 |
| pointerFlushMessageCount | この数のメッセージが処理されると、オフセットがデータベースに保存されます。<br>デフォルトは 1000 です。 |
| pointerFlushPeriodSec | この期間を過ぎると、オフセットがデータベースに保存されます。<br>デフォルトは 5（秒）です。 |
| processingJSThreads | カスタム JS コネクタを使用してメッセージを処理する専用スレッドの数。<br>デフォルトは 4 です。 |
| processingThreads | ビルトインコードを使用してメッセージを処理する専用スレッドの数。<br>デフォルトは 4 です。 |
| retryPeriodSec | 処理エラーの場合の再試行間の遅延。<br>デフォルトは 30（秒）です。 |
| retryValiditySec | この期間が経過してもメッセージが正常に処理されない場合（再試行回数が多すぎる場合）、メッセージを破棄します。<br>デフォルトは 300（秒）です。 |

### パイプライン化されたプロセスの自動開始 {#pipelined-process-autostart}

`pipelined` プロセスは自動的に開始する必要があります。

この場合、設定ファイルの `<`pipelined`>` 要素を「autostart=&quot;true&quot;」に設定します。

```sql
 <pipelined autoStart="true" ... "/>
```

### パイプライン化されたプロセスの再起動 {#pipelined-process-restart}

変更を有効にするには、再起動が必要です。

```sql
nlserver restart pipelined@instance
```

## 手順 4：検証 {#step-validation}

プロビジョニングのパイプライン設定を検証するには、次の手順に従います。

* `pipelined` プロセスが実行中であることを確認します。
* パイプライン接続ログの `pipelined.log` を確認します。
* 接続を確認し、ping を受け取ったかどうかを確認します。ホスト型の顧客は、クライアントコンソールから「監視」を使用できます。
