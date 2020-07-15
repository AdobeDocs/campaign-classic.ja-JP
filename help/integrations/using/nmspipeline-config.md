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
source-git-commit: 0112d5bd052ad66169225073276d1da4f3c245d8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 3%

---


# パイプラインオプション NmsPipeline_Config {#nmspipeline_config}

認証が機能したら、 [!DNL pipelined] イベントを取得して処理できます。 Adobe Campaignで設定されたトリガーのみを処理し、他のトリガーは無視します。 トリガーは、事前にAnalyticsから生成され、パイプラインに押し込まれている必要があります。
また、名前に関係なく、すべてのトリガーを取得するワイルドカードを使用して設定することもできます。

トリガーの設定は、 **[!UICONTROL 管理]** / **[!UICONTROL Platform]** / **[!UICONTROL オプションで行います]**。 オプション名は **[!UICONTROL NmsPipeline_Config]**&#x200B;です。 データタイプがJSON形式の「long text」です。

次の例では、2つのトリガーを指定します。

このテンプレートのJSONコードをオプション値に貼り付けます。 コメントは必ず削除してください。

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

次の2つ目の例は、すべてのトリガーを取得します。

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
>Analyticsインターフェイスの特定のトリガー名の [!DNL Trigger] UID値は、TriggersインターフェイスのURLクエリ文字列パラメーターの一部として見つかります。 triggerType UIDはパイプラインデータストリームで渡され、コードをpipeline.JSに記述して、トリガーUIDをユーザーにわかりやすいラベルにマップし、pipelineEventsスキーマのTrigger Name列に格納できます。

## consumerパラメーター {#consumer-parameter}

このパイプラインは、「サプライヤーと消費者」モデルと連携しています。 同じキューには多くのコンシューマーが存在する可能性があります。 メッセージは、個々の消費者に対してのみ「消費」されます。 消費者はそれぞれ、メッセージの「コピー」を取得します。

「consumer」パラメーターは、インスタンスをこれらのコンシューマーの1つとして識別します。 これは、パイプラインを呼び出しているインスタンスのIDです。 インスタンス名を入力できます。 パイプラインサービスは、各コンシューマーが取得したメッセージを追跡します。 異なるインスタンスに異なるコンシューマーを使用すると、すべてのメッセージが各インスタンスに送信されます。

## パイプラインオプションの設定方法 {#configure-pipeline-option}

「トリガー」追加配列の下のExperience Cloudトリガーを編集する。 残りの部分は編集しないでください。
この [Webサイトの助けを借りて、JSONが有効であることを確認してください](http://jsonlint.com/)。

* 「name」はトリガーIDです。 ワイルドカード「*」は、すべてのトリガーをキャッチします。
* 「コンシューマー」は、nlserverインスタンスを一意に識別する一意の文字列です。 通常は、インスタンス名自体を指定できます。 複数の環境（開発/ステージ/実稼動環境）の場合、各インスタンスがメッセージのコピーを受け取るように、各ユーザーに対して一意であることを確認してください。
* [!DNL Pipelined] は、「エイリアス」トピックもサポートしています。

変更 [!DNL pipelined] を行った後、再起動します。
