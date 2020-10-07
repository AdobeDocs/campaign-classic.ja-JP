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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 100%

---


# パイプラインオプション NmsPipeline_Config {#nmspipeline_config}

認証が機能したら、[!DNL pipelined] でイベントを取得して処理できます。Adobe Campaign で設定されたトリガーのみを処理し、他のトリガーは無視します。トリガーは、事前に Analytics から生成され、パイプラインに追加されている必要があります。
また、名前に関係なく、すべてのトリガーを取得するように、ワイルドカードを使用して設定することもできます。

トリガーの設定は、**[!UICONTROL 管理]**／**[!UICONTROL Platform]**／**[!UICONTROL オプション]**&#x200B;でおこないます。オプション名は **[!UICONTROL NmsPipeline_Config]** です。データタイプは JSON 形式の「長いテキスト」です。

次の例では、2 つのトリガーを指定しています。

このテンプレートの JSON コードをオプション値に貼り付けます。コメントは必ず削除してください。

```
{
    "topics": [ // list of "topics" that the pipelined is listening to.
        {
            "name": "triggers", // Name of the first topic: triggers.
            "consumer": "customer_dev", // Name of the instance that listens. 
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

次の 2 つ目の例では、すべてのトリガーを取得しています。

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

>[!NOTE]
>
>Analytics インターフェイスでの特定のトリガー名に対する [!DNL Trigger] UID 値は、Triggers インターフェイスでは URL クエリー文字列パラメーターの一部として含まれます。triggerType UID はパイプラインデータストリームで渡します。コードを pipeline.JS に記述して、トリガー UID をユーザーにわかりやすいラベルにマッピングし、pipelineEvents スキーマの Trigger Name 列に格納できます。

## コンシューマーパラメーター {#consumer-parameter}

パイプラインは、「サプライヤーとコンシューマー」モデルで機能します。同じキューには多くのコンシューマーが存在する可能性があります。メッセージは、個々のコンシューマーに対してのみ「消費」されます。各コンシューマーは、メッセージの独自の「コピー」を取得します。

「consumer」パラメーターは、インスタンスをこれらのコンシューマーの 1 つとして識別します。これは、パイプラインを呼び出しているインスタンスの ID になります。このパラメーターにはインスタンス名を入力できます。パイプラインサービスは、各コンシューマーが取得したメッセージを追跡します。異なるインスタンスに異なるコンシューマーを使用することで、すべてのメッセージが各インスタンスに送信されます。

## パイプラインオプションの設定方法 {#configure-pipeline-option}

「triggers」配列内の Experience Cloud トリガーを追加または編集します。残りの部分は編集しないでください。
この [Web サイト](http://jsonlint.com/)で、JSON が有効であることを確認してください。

* 「name」はトリガー ID です。ワイルドカード「*」を指定すると、すべてのトリガーが取得されます。
* 「consumer」は、nlserver インスタンスを一意に識別する一意の文字列です。通常は、インスタンス名自体を指定できます。複数の環境（開発／ステージ／実稼動環境）の場合は、各インスタンスがメッセージのコピーを取得するように、環境ごとに一意になるようにしてください。
* [!DNL Pipelined] では、「aliases」トピックもサポートしています。

変更をおこなった後、[!DNL pipelined] を再起動します。
