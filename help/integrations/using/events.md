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
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '1152'
ht-degree: 100%

---


# Triggers イベント {#events}

## JavaScript でのイベント処理 {#events-javascript}

### JavaScript ファイル {#file-js}

パイプラインでは JavaScript 関数を使用して各メッセージを処理します。この関数はユーザー定義関数です。

これは、「JSConnector」属性の下の **[!UICONTROL NmsPipeline_Config]** オプションで設定します。この JavaScript は、イベントを受信するたびに呼び出されます。[!DNL pipelined] プロセスで実行されます。

サンプルの JS ファイルは、cus:triggers.js です。

### JavaScript 関数 {#function-js}

[!DNL pipelined] JavaScript は、特定の関数で起動する必要があります。

この関数は、イベントごとに 1 回呼び出されます。

```
function processPipelineMessage(xmlTrigger) {}
```

次のように返されます。

```
<undefined/>
```

JS を編集した後、[!DNL pipelined] を再起動します。

### トリガーデータフォーマット {#trigger-format}

[!DNL trigger] データが JS 関数に渡されます。XML 形式です。

* **[!UICONTROL @triggerId]** 属性には [!DNL trigger] の名前が含まれています。
* JSON 形式の **enrichments** 要素は、Analytics で生成されたデータを含んでおり、トリガーに添付されます。
* **[!UICONTROL @offset]** は、メッセージへの「ポインタ」です。キュー内のメッセージの順序を示します。
* **[!UICONTROL @partition]** は、キュー内のメッセージのコンテナです。オフセットは、パーティションを基準とした相対値です。<br>キューには約 15 のパーティションがあります。

例：

```
<trigger offset="1500435" partition="4" triggerId="LogoUpload_1_Visits_from_specific_Channel_or_ppp">
 <enrichments>{"analyticsHitSummary":{"dimensions":{" eVar01":{"type":"string","data":["PI4INE1ETDF6UK35GO13X7HO2ITLJHVH"],"name":" eVar01","source":"session summary"}, "timeGMT":{"type":"int","data":[1469164186,1469164195],"name":"timeGMT","source":"session summary"}},"products":{}}}</enrichments>
 <aliases/>
 </trigger>
```

### エンリッチメントデータフォーマット {#enrichment-format}

>[!NOTE]
>
>これは、考えられる様々な実装から得られる具体的な例です。

コンテンツは、トリガーごとに Analytics で定義されます。JSON 形式です。
例えば、LogoUpload_uploading_Visits トリガーの場合：

* **[!UICONTROL eVar01]** には、キャンペーン受信者との紐付けに使用される買い物客 ID を含めることができます。文字列形式です。<br>プライマリキーである買い物客 ID を見つけるために紐付ける必要があります。

* **[!UICONTROL timeGMT]** には:Analytics 側でのトリガーの時刻を含めることができます。UTC エポック形式です（01/01/1970 UTC からの秒数）。

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

イベントは、オフセット順に 1 つずつ処理されます。[!DNL pipelined] の各スレッドは異なるパーティションを処理します。

最後に取得したイベントの「オフセット」がデータベースに格納されます。したがって、プロセスが停止すると、最後のメッセージから再開されます。このデータは組み込みスキーマ xtk:pipelineOffset に格納されます。

このポインターは、各インスタンスと各コンシューマーに固有です。したがって、多くのインスタンスが異なるコンシューマーを使用して同じパイプラインにアクセスする場合、すべてのメッセージが同じ順序で取得されます。

パイプラインオプションの「consumer」パラメータは、呼び出し元のインスタンスを識別します。

現在、「staging」や「dev」などの環境ごとに異なるキューを使用する方法はありません。

### ログとエラー処理 {#logging-error-handling}

logInfo() などのログは [!DNL pipelined] ログに送られます。logError() などのエラーは [!DNL pipelined] ログに書き込まれ、エラーの結果、イベントが再試行キューに入れられます。パイプラインログを確認します。
エラーのメッセージは、[!DNL pipelined] オプションで設定された時間内に複数回再試行されます。

デバッグおよび監視のために、完全なトリガーデータがトリガーテーブルに書き込まれます。「data」フィールドに XML 形式で書き込まれます。または、トリガーデータを含んだ logInfo() も同じ目的を果たします。

### データの解析 {#data-parsing}

このサンプル JS コードは、エンリッチメント内の eVar01 を解析します。

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

エラーを避けるために、解析をおこなう場合は注意が必要です。
このコードはすべてのトリガーに使用されるので、ほとんどのデータは不要です。したがって、存在しない場合は空のままにすることができます。

### トリガーの保存 {#storing-triggers-js}

>[!NOTE]
>
>これは、考えられる様々な実装から得られる具体的な例です。

このサンプル JS コードは、トリガーをデータベースに保存します。

```
function processPipelineMessage(xmlTrigger)
 {
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

このコードは頻繁に実行されるので、最適なパフォーマンスにする必要があります。他のマーケティングアクティビティに悪影響が出る可能性があります。特に、マーケティングサーバーで 1 時間に 100 万個を超えるトリガーイベントを処理する場合はその可能性があります。また、適切に調整されていない場合もそうです。

この JavaScript のコンテキストは制限されています。API のすべての機能を使用できるわけではありません。例えば、getOption() や getCurrentdate() は機能しません。

処理を高速化するために、このスクリプトの複数のスレッドが同時に実行されます。コードはスレッドセーフにする必要があります。

## イベントの保存 {#store-events}

>[!NOTE]
>
>これは、考えられる様々な実装から得られる具体的な例です。

### パイプラインイベントスキーマ {#pipeline-event-schema}

イベントは、データベーステーブルに保存されます。マーケティングキャンペーンで顧客のターゲティング、トリガーを使用した E メールのエンリッチメントに使用されます。
トリガーごとに異なるデータ構造にすることができますが、すべてのトリガーを 1 つのテーブルに保持できます。
triggerType フィールドは、データの発生元となるトリガーを識別します。

このテーブルのサンプルスキーマコードを以下に示します。

| 属性 | タイプ | ラベル | 説明 |
|:-:|:-:|:-:|:-:|
| pipelineEventId | 長いテキスト | プライマリキー | トリガーの内部プライマリキー。 |
| data | メモ | トリガーデータ | XML 形式で記述したトリガーデータの完全な内容。デバッグおよび監査のために使用します。 |
| triggerType | 50 バイト長文字列 | TriggerType | トリガーの名前。Web サイトでの顧客の行動を識別します。 |
| shopper_id | 32 バイト長文字列 | shopper_id | 買い物客の内部識別子。紐付けワークフローで設定されます。0 の場合、Campaign で顧客が不明であることを意味します。 |
| shopper_key | 長いテキスト | shopper_key | Analytics でキャプチャされた、買い物客の外部識別子。 |
| created | 日時 | 作成日時 | イベントが Campaign で作成された日時。 |
| lastModified | 日時 | 最終変更日時 | イベントがアドビで最後に変更された日時。 |
| timeGMT | 日時 | タイムスタンプ | イベントが Analytics で生成された時刻。 |

### イベントの表示 {#display-events}

イベントは、イベントスキーマに基づいてシンプルなフォームで表示できます。

>[!NOTE]
>
>パイプラインイベントノードは組み込まれておらず、追加する必要があります。また、関連フォームも Campaign で作成する必要があります。これらの操作は、エキスパートユーザーのみに制限されます。この点について詳しくは、[ナビゲーション階層](../../configuration/using/about-navigation-hierarchy.md)および[フォームの編集](../../configuration/using/editing-forms.md)の節を参照してください。

![](assets/triggers_7.png)

## イベントの処理 {#processing-the-events}

### 紐付けワークフロー {#reconciliation-workflow}

紐付けとは、顧客を Analytics から Campaign データベースに照合するプロセスです。例えば、shopper_id を照合の条件にすることができます。

パフォーマンス上の理由から、照合はワークフローでバッチモードでおこなう必要があります。
ワークロードを最適化するには、頻度を 15 分に設定する必要があります。その結果、Adobe Campaign でのイベントの受信とマーケティングワークフローによる処理との間の遅延は、最大 15 分になります。

### JavaScript での単位紐付けのオプション {#options-unit-reconciliation}

理論的には、JavaScript でトリガーごとに紐付けクエリを実行できます。パフォーマンスが高くなる効果があり、結果が出るのが速くなります。高い反応度が必要な場合、これが特定のユースケースに必要になることがあります。

shopper_id にインデックスが設定されていない場合は、実行が難しい可能性があります。条件がマーケティングサーバーとは別のデータベースサーバー上にある場合は、データベースリンクが使用されますが、パフォーマンスが低下します。

### ワークフローのパージ {#purge-workflow}

トリガーは 1 時間以内に処理されるので、長時間トリガーを保持する理由はありません。トリガーの量は 1 時間あたり約 100 万個になることがあります。だからこそ、パージワークフローを用意する必要があるのです。パージは 1 日 1 回実行され、3 日前より古いトリガーがすべて削除されます。

### キャンペーンワークフロー {#campaign-workflow}

トリガーキャンペーンワークフローは、多くの場合、使用されたことがある他の繰り返しキャンペーンと似ています。
例えば、トリガーに関するクエリで開始し、最終日の特定のイベントを探すことができます。そのターゲットは E メールの送信に使用されます。エンリッチメントやデータはトリガーから得られます。設定が不要なので、マーケティングで安全に使用できます。
