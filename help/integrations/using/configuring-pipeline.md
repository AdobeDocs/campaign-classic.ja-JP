---
product: campaign
title: パイプラインを設定
description: Campaign とトリガーの統合用にパイプラインを設定する方法を学ぶ
feature: Triggers
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
exl-id: 2d214c36-8429-4b2b-b1f5-fe2730581bba
source-git-commit: 271e0f9fde0cbfb016e201c8390b26673d8fc696
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 63%

---

# パイプラインを設定 {#configuring-pipeline}

顧客 ID、秘密鍵、認証エンドポイントなどの認証パラメーターは、インスタンス設定ファイルで設定します。

処理されるトリガーのリストは、JSON 形式のオプションで設定されます。

トリガーは、メールを送信するキャンペーンワークフローでターゲティングに使用されます。キャンペーンは、両方のトリガーイベントを持つ顧客がメールを受信するように設定されています。

## 前提条件 {#prerequisites}

この設定を開始する前に、以下の点を確認してください。

* Adobe Developer プロジェクト
* 有効な組織 ID – 組織 ID を見つけるには、 [このページ](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255){_blank}
* 組織への開発者のアクセス
* Adobe Analyticsの有効なトリガー設定

## 認証および設定ファイル {#authentication-configuration}

パイプラインはAdobe Experience Cloudでホストされているので、認証が必要です。 公開鍵と秘密鍵のペアが使用されます。このプロセスは、ユーザー/パスワードと同じ機能を持ちますが、より安全です。 Adobe Developer プロジェクトを介したMarketing Cloudでは、認証がサポートされます。

## 手順 1：Adobe Developer プロジェクトを作成／更新 {#creating-adobe-io-project}

ホステッド環境のお客様の場合は、Adobe担当者/ カスタマーケアと協力して、Adobe Developer アカウントトークンでトリガー統合を有効にします。

オンプレミス/ハイブリッドのお客様の場合は、を参照してください。 [Adobe Experience Cloud Triggers用のAdobe I/Oの設定](../../integrations/using/configuring-adobe-io.md) ページ。 を選択する必要があります。 **[!UICONTROL Adobe Analytics]** Adobe Developer資格情報への API の追加中。

## 手順 2：パイプラインオプションの設定 {#configuring-nmspipeline}

認証が設定されると、パイプラインはイベントを取得します。Adobe Campaign で設定されたトリガーのみが処理されます。トリガーは、Adobe Analyticsから生成され、パイプラインにプッシュされている必要があります。パイプラインは、Adobe Campaignで設定されたトリガーのみを処理します。

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

### Consumer パラメーターの設定 {#consumer-parameter}

パイプラインは、「サプライヤーとコンシューマー」モデルのように機能します。メッセージは、個々のコンシューマーによってのみ消費されます。コンシューマーはそれぞれ、メッセージのコピーを取得します。

**Consumer** パラメーターは、インスタンスをこれらのコンシューマーの 1 つとして識別します。インスタンスの ID がパイプラインを呼び出します。クライアントコンソールの監視ページにあるインスタンス名を入力できます。

パイプラインサービスは、各コンシューマーが取得したメッセージを追跡します。異なるインスタンスに異なるコンシューマーを使用すると、すべてのメッセージを各インスタンスに送信するようにできます。

### パイプラインオプションのレコメンデーション {#pipeline-option-recommendation}

パイプラインオプションを設定するには、次のレコメンデーションに従う必要があります。

* の下でトリガーを追加または編集 **[!UICONTROL トリガー]**.
* JSON が有効であることを確認します。
* この **名前** パラメーターはトリガー ID に対応しています。 ワイルドカード「*」は、すべてのトリガーを取得します。
* この **消費者** パラメーターは、呼び出し元のインスタンスまたはアプリケーションの名前に対応します。
* この `pipelined`プロセスでは、「エイリアス」トピックもサポートしています。
* 必ずを再起動してください `pipelined`変更後のプロセス。

## 手順 3：オプション設定 {#step-optional}

一部の内部パラメーターは負荷要件に応じて変更できますが、実稼動環境に適用する前に必ずテストしてください。

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

この `pipelined` プロセスは自動的に開始する必要があります。

そのためには、 `<`パイプライン化`>` 構成ファイル内の要素を autostart=&quot;true&quot;に設定します。

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
* を確認します `pipelined.log` （パイプライン接続ログ用）。
* 接続を確認し、ping を受け取ったかどうかを確認します。ホスト型の顧客は、クライアントコンソールから「監視」を使用できます。
