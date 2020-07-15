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
source-wordcount: '1152'
ht-degree: 2%

---


# Triggers イベント {#events}

## JavaScriptでの処理イベント {#events-javascript}

### JavaScriptファイル {#file-js}

パイプラインはJavaScript関数を使用して各メッセージを処理します。 この関数はユーザー定義です。

これは、「JSConnector」属性の下の **[!UICONTROL NmsPipeline_Config]** オプションで設定されます。 このjavascriptは、イベントを受信するたびに呼び出されます。 プロセスで実行され [!DNL pipelined] ます。

サンプルのJSファイルは、cus:triggers.jsです。

### JavaScript 関数 {#function-js}

JavaScript [!DNL pipelined] は、特定の関数と開始する必要があります。

この関数は、イベントごとに1回呼び出されます。

```
function processPipelineMessage(xmlTrigger) {}
```

次のように返されます。

```
<undefined/>
```

JSを編集 [!DNL pipelined] した後、再起動します。

### トリガーデータの形式 {#trigger-format}

データがJS関数に渡され [!DNL trigger] ます。 XML形式です。

* @triggerId **[!UICONTROL 属性には、の名前が含まれ]**[!DNL trigger]ます。
* JSON形式の **エンリッチメント** 要素には、Analyticsによって生成されたデータが含まれ、トリガーに添付されます。
* **[!UICONTROL @offset]** は、メッセージへの「ポインタ」です。 キュー内のメッセージの順序を示します。
* **[!UICONTROL @partition]**nは、キュー内のメッセージのコンテナです。 オフセットは、パーティションを基準とした相対位置です。 <br>キューには約15のパーティションがあります。

例：

```
<trigger offset="1500435" partition="4" triggerId="LogoUpload_1_Visits_from_specific_Channel_or_ppp">
 <enrichments>{"analyticsHitSummary":{"dimensions":{" eVar01":{"type":"string","data":["PI4INE1ETDF6UK35GO13X7HO2ITLJHVH"],"name":" eVar01","source":"session summary"}, "timeGMT":{"type":"int","data":[1469164186,1469164195],"name":"timeGMT","source":"session summary"}},"products":{}}}</enrichments>
 <aliases/>
 </trigger>
```

### エンリッチメントデータ形式 {#enrichment-format}

>[!NOTE]
>
>これは、様々な実装から得られる具体的な例です。

コンテンツは、各トリガーに対してAnalyticsで定義されます。 JSON形式です。
例えば、LogoUpload_uploading_Visitsをトリガーする場合：

* **[!UICONTROL eVar01]** には、キャンペーン受信者との調整に使用される買い物客IDを含めることができます。 文字列形式です。 <br>主キーである買い物客IDを見つけるには調整する必要があります。

* **[!UICONTROL timeGMT]** :Analytics側のトリガーの時間を含めることができます。 UTCエポック形式です（01/01/1970 UTCからの秒数）。

例：

```
{
 "analyticsHitSummary": {
 "dimensions": {
 "eVar01": {
 "type": "string",
 "data": ["PI4INE1ETDF6UK35GO13X7HO2ITLJHVH"],
 "name": " eVar01",
 "source": "session summary"
 },
 "timeGMT": {
 "type": "int",
 "data": [1469164186, 1469164195],
 "name": "timeGMT",
 "source": "session summary"
 }
 },
 "products": {}
 }
 }
```

### イベント処理の順序 {#order-events}

イベントは、オフセット順に1つずつ処理されます。 各スレッドは異なるパーティションを [!DNL pipelined] 処理します。

最後に取得したイベントの「オフセット」がデータベースに格納されます。 したがって、プロセスが停止すると、最後のメッセージから再開されます。 このデータは組み込みスキーマxtk:pipelineOffsetに格納されます。

このポインタは、各インスタンスと各コンシューマに固有です。 したがって、多くのインスタンスが異なるコンシューマーを使用して同じパイプラインにアクセスする場合、すべてのメッセージが同じ順序で取得されます。

パイプラインオプションの「consumer」パラメータは、呼び出し元のインスタンスを識別します。

現在、「staging」や「dev」などの別々の環境に異なるキューを置く方法はありません。

### ログとエラー処理 {#logging-error-handling}

logInfo()などのログはログに送られ [!DNL pipelined] ます。 logError()などのエラーはログに書き込まれ、イベントが再試行キューに入れら [!DNL pipelined] れます。 パイプラインログを確認します。
エラーのメッセージは、 [!DNL pipelined] オプションで設定された時間内に複数回再試行されます。

デバッグおよび監視の目的で、完全なトリガーデータがトリガーテーブルに書き込まれます。 XML形式の「data」フィールドです。 または、トリガーデータを含むlogInfo()も同じ目的で使用します。

### データの解析 {#data-parsing}

このサンプルJSコードは、エンリッチメント内のeVar01を解析します。

```
function processPipelineMessage(xmlTrigger)
 {
 (…)
 var shopper_id = ""
 if (xmlTrigger.enrichments.length() > 0)
 {
 if (xmlTrigger.enrichments.toString().match(/eVar01/) != undefined)
 {
 var enrichments = JSON.parse(xmlTrigger.enrichments.toString())
 shopper_id = enrichments.analyticsHitSummary.dimensions. eVar01.data[0]
 }
 }
 (…)
 }
```

エラーを回避するために解析を行う場合は注意が必要です。
このコードはすべてのトリガーに使用されるので、ほとんどのデータは不要です。 したがって、存在しない場合は空のままにすることができます。

### トリガーの格納 {#storing-triggers-js}

>[!NOTE]
>
>これは、様々な実装から得られる具体的な例です。

このサンプルJSコードは、トリガーをデータベースに保存します。

```
function processPipelineMessage(xmlTrigger)
 {```
 (…)
 var event = 
 <pipelineEvent
 xtkschema = "cus:pipelineEvent"
 _operation = "insert"
 created = {timeNow}
 lastModified = {timeNow}
 triggerType = {triggerType}
 timeGMT = {timeGMT}
 shopper_id = {shopper_id}
 data = {xmlTrigger.toXMLString()}
 />
 xtk.session.Write(event)
 return <undef/>; 
 }
```

### 制約 {#constraints}

このコードは高周波で動作するので、パフォーマンスは最適である必要があります。 他のマーケティングアクティビティには悪影響が出る可能性があります。 特に、1時間に100万を超える処理が行われると、マーケティングサーバーでイベントがトリガーされます。 または適切に調整されていない場合は、

このJavaScriptのコンテキストは制限されます。 APIの一部の機能を使用できるわけではありません。 例えば、getOption()やgetCurrentdate()は機能しません。

処理を高速化するために、このスクリプトの複数のスレッドが同時に実行されます。 コードはスレッドセーフである必要があります。

## イベントの保存 {#store-events}

>[!NOTE]
>
>これは、様々な実装から得られる具体的な例です。

### パイプラインイベントスキーマ {#pipeline-event-schema}

イベントは、データベーステーブルに格納されます。 ターゲットの顧客に対するマーケティングキャンペーンや、トリガーを使用した電子メールの拡充に使用されます。
各トリガーは異なるデータ構造を持つことができますが、すべてのトリガーは単一のテーブルに保持できます。
triggerTypeフィールドは、データの送信元を識別します。

次に、この表のスキーマコードの例を示します。

| 属性 | タイプ | ラベル | 説明 |
|:-:|:-:|:-:|:-:|
| pipelineEventId | 長い | プライマリキー | トリガーの内部主キー。 |
| data | メモ | トリガーデータ | XML形式のトリガーデータの完全な内容。 デバッグおよび監査の目的で使用します。 |
| triggerType | 文字列50 | TriggerType | トリガーの名前。 Webサイト上での顧客の行動を識別します。 |
| shopper_id | 文字列32 | shopper_id | 買い物客の内部識別子。 調整ワークフローによって設定されます。 0の場合、キャンペーンが不明であることを意味します。 |
| shopper_key | 長い | shopper_key | Analyticsによってキャプチャされた買い物客の外部識別子。 |
| created | 日時 | 作成済み | イベントがキャンペーンで作成された時刻。 |
| lastModified | 日時 | 最終変更日時 | イベントが最後にアドビで変更されたとき。 |
| timeGMT | 日時 | Timestamp | イベントがAnalyticsで発生した時刻。 |

### イベントの表示 {#display-events}

イベントは、イベントスキーマに基づく単純なフォームで表示できます。

>[!NOTE]
>
>パイプラインイベントノードは組み込まれておらず、追加する必要があります。また、関連するフォームをキャンペーンで作成する必要があります。 これらの操作は、エキスパートユーザーにのみ制限されます。 この点について詳しくは、次の節を参照してください。 [ナビゲーション階層](../../configuration/using/about-navigation-hierarchy.md) 、 [フォームの](../../configuration/using/editing-forms.md)編集。

![](assets/triggers_7.png)

## イベントの処理 {#processing-the-events}

### 調整ワークフロー {#reconciliation-workflow}

調整とは、顧客をAnalyticsからキャンペーンデータベースに照合するプロセスです。 例えば、照合の条件はshopper_idにできます。

パフォーマンス上の理由から、照合はワークフローによってバッチモードで行う必要があります。
ワークロードを最適化するには、頻度を15分に設定する必要があります。 その結果、Adobe Campaignでのイベントの受信とマーケティングワークフローによる処理との間の遅延は、最大15分です。

### JavaScriptでの単位調整のオプション {#options-unit-reconciliation}

理論的には、JavaScriptの各トリガーに対して調整クエリを実行できます。 パフォーマンスへの影響が高く、結果が速くなります。 反応性が必要な場合に特定の使用例に対して必要となる場合があります。

shopper_idにインデックスが設定されていない場合は、実行が困難になる場合があります。 マーケティングサーバーとは別のデータベースサーバー上に条件がある場合は、データベースリンクが使用されますが、パフォーマンスが低下します。

### ワークフローの削除 {#purge-workflow}

トリガーは1時間以内に処理されるので、長時間トリガーを保持する理由はありません。 1時間あたり約100万トリガーをボリュームに含めることができます。 これは、パージワークフローを導入する必要がある理由を説明します。 削除を行うと、3日を超えて1日に1回実行されるすべてのトリガーが削除されます。

### キャンペーンワークフロー {#campaign-workflow}

トリガーキャンペーンのワークフローは、多くの場合、以前に使用した他の定期キャンペーンと同様です。
例えば、トリガーに関するクエリと開始して、最終日に特定のイベントを探すことができます。 そのターゲットは電子メールの送信に使用されます。 エンリッチメントやデータはトリガーから取得できます。 設定は不要なので、マーケティングで安全に使用できます。
