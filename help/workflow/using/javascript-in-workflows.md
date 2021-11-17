---
product: campaign
title: ワークフローでの JavaScript コードの例
description: 以下の例は、ワークフローでの JavaScript コードの使用方法を示しています
audience: workflow
content-type: reference
topic-tags: advanced-management
source-git-commit: fa3a3e1801738928876734aa42342f0a5b49e320
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 3%

---

# ワークフローでの JavaScript コードの例{#javascript-in-workflows}

![](../../assets/common.svg)

以下の例は、ワークフローでの JavaScript コードの使用方法を示しています。

* [データベースに書き込み](#write-example)
* [データベースのクエリ](#read-example)
* [静的 SOAP メソッドを使用したワークフローのトリガー](#trigger-example)
* [非静的 SOAP メソッドを使用してデータベースを操作する](#interact-example)

[詳細情報](https://experienceleague.adobe.com/developer/campaign-api/api/p-14.html?lang=ja) 静的および非静的 SOAP メソッドについて

この例では、ECMAScript for XML(E4X) 拡張機能が使用されています。 この拡張機能を使用すると、JavaScript 呼び出しと XML プリミティブを同じスクリプトに組み合わせることができます。

これらの例を試すには、次の手順に従います。

1. ワークフローを作成し、以下のアクティビティをワークフローに追加します。
   1. アクティビティを開始
   1. JavaScript コードアクティビティ
   1. 終了アクティビティ

   [詳細情報](building-a-workflow.md) ワークフローの構築について

1. アクティビティに JavaScript コードを追加します。 [詳細情報](advanced-parameters.md)。
1. ワークフローを保存します。
1. 例をテストします。
   1. ワークフローを開始します。[詳細情報](starting-a-workflow.md)。
   1. ジャーナルを開きます。 [詳細情報](monitoring-workflow-execution.md#displaying-logs)。

## 例 1:データベースに書き込む{#write-example}

データベースに書き込むには、静的 `Write` メソッド `xtk:session` schema:

1. XML で書き込みリクエストを作成します。

1. レコードを書き込みます。

   1. を `Write` メソッド `xtk:session` スキーマ。

      >[!IMPORTANT]
      > Adobe Campaign v8 を使用する場合は、 **取り込み** および **データの更新/削除** の API `Write` メソッドをSnowflake表に追加します。 [詳細を表示](https://experienceleague.adobe.com/docs/campaign/campaign-v8/architecture/api/new-apis.html){target=&quot;_blank&quot;}。

   1. XML コードを書き込みリクエストの引数として渡します。

### 手順 1:書き込み要求を作成する

レコードの追加、更新、削除を行うことができます。

#### レコードを挿入

これは、 `insert` operation はデフォルトの操作です。指定する必要はありません。

この情報を XML 属性として指定します。

* 変更するテーブルのスキーマ
* 入力するテーブルフィールド

例：

```javascript
var myXML = <recipient xtkschema="nms:recipient"
    firstName="Isabel"
    lastName="Garcia"
    email="isabel.garcia@mycompany.com"/>
```

#### レコードの更新

以下を使用： `_update` 操作。 [詳細情報](../../configuration/using/data-oriented-apis.md)。

この情報を XML 属性として指定します。

* 変更するテーブルのスキーマ
* 更新するテーブルフィールド
* 更新するレコードを識別するために必要なキー引数

例：

```javascript
var myXML = <recipient xtkschema="nms:recipient"
    status="Client"
    email="isabel.garcia@mycompany.com"
    operation="_update"
    _key="@email"/>
```

#### レコードの削除

以下を使用： `DeleteCollection` メソッド。 [詳細情報](https://experienceleague.adobe.com/developer/campaign-api/api/sm-session-DeleteCollection.html)。

次の情報を指定します。

* 変更するテーブルのスキーマ
* この `where` 更新するレコードを識別するために必要な句を XML 要素の形式で指定する

例：

```javascript
xtk.session.DeleteCollection(
    "nms:recipient",
    <where>
        <condition expr="[@email] = 'isabel.garcia@mycompany.com'"/>
    </where>,
    false
    )
```

### 手順 2:記録を書く

非静的 `Write` メソッド `xtk:session` schema:

```javascript
xtk.session.Write(myXML)
```

このメソッドでは値は返されません。

完全なコードをワークフローの「 JavaScript コード」アクティビティに追加します。

```javascript
var myXML = <recipient xtkschema="nms:recipient"
    firstName="Isabel"
    lastName="Garcia"
    email="isabel.garcia@mycompany.com"/>

xtk.session.Write(myXML)
```

このビデオでは、データベースに書き込む方法を示します。
>[!VIDEO](https://video.tv.adobe.com/v/18472/?learn=on)

## 例 2:データベースのクエリ{#read-example}

データベースに対してクエリを実行する場合は、非静的 `xtk:queryDef` インスタンスメソッド：

1. XML でクエリを作成します。
1. クエリオブジェクトを作成します。
1. クエリを実行します。

### 手順 1:クエリの作成

の XML コードを指定します。 `queryDef` エンティティ。

構文：

```xml
<queryDef schema="nms:recipient" operation="">
    <!-- select, where, and orderBy clauses as XML elements -->
</queryDef>
```

次の情報を指定します。

* 読み取るテーブルのスキーマ
* 操作
* 返される列 ( `select` 句
* 条件、 `where` 句
* フィルター条件 ( `orderBy` 句

次の操作を使用できます。

| 運用 | 結果 |
| --- | --- |
| `select` | 0 個以上の要素がコレクションとして返される。 |
| `getIfExists` | 1 つの要素が返されます。 一致する要素が存在しない場合は、空の要素が返されます。 |
| `get` | 1 つの要素が返されます。 一致する要素が存在しない場合は、エラーが返されます。 |
| `count` | 一致するレコードの数は、 `count` 属性。 |

を書く `select`, `where`、および `orderBy` 句を XML 要素として：

* `select` 句

   返す列を指定します。 例えば、人物の名と姓を選択するには、次のコードを記述します。

   ```xml
   <select>
       <node expr="@firstName"/>
       <node expr="@lastName"/>
   </select>
   ```

   を使用 `nms:recipient` スキーマの場合、要素は次の形式で返されます。

   ```xml
   <recipient firstName="Bo" lastName="Didley"/>
   ```

* `where` 句

   条件を指定するには、 `where` 句を使用します。 例えば、 **トレーニング** フォルダーには、次のコードを記述できます。

   ```xml
   <where>
       <condition expr="[folder/@label]='Training'"/>
   </where>
   ```

   複数の式を組み合わせる場合は、最初の式にブール演算子を使用します。 例えば、イザベル・ガルシアという名前の人をすべて選択するには、次のコードを記述します。

   ```xml
   <condition boolOperator="AND" expr="@firstName='Isabel'"/>
   <condition expr="@lastName='Garcia'"/>
   ```

* `orderBy` 句

   結果セットを並べ替えるには、 `orderBy` 句を XML 要素として指定し、 `sortDesc` 属性。 例えば、姓を昇順に並べ替えるには、次のコードを記述します。

   ```xml
   <orderBy>
       <node expr="@lastName> sortDesc="false"/>
   </orderBy>
   ```

### 手順 2:クエリオブジェクトの作成

XML コードからエンティティを作成するには、 `create(`*`content`*`)` メソッド：

```javascript
var query = xtk.queryDef.create(
    <queryDef schema="nms:recipient" operation="select">
    …
    </queryDef>)
```

プレフィックス `create(`*`content`*`)` メソッドを使用して、作成するエンティティのスキーマを指定します。

この *`content`* 引数は文字列引数で、オプションです。 この引数には、エンティティを記述する XML コードが含まれます。

### 手順 3:クエリを実行

次の手順に従います。

1. を `ExecuteQuery` メソッド `queryDef` エンティティ：

   ```javascript
   var res = query.ExecuteQuery()
   ```

1. 結果を処理します。
   1. 結果を繰り返し処理 `select` 操作、ループ構成体を使用する。
   1. 結果をテストするには、 `getIfExists` 操作。
   1. 結果をカウントするには、 `count` 操作。

#### の結果 `select` 操作

すべての一致がコレクションとして返されます。

```xml
<recipient-collection>
    <recipient email="jane.smith@mycompany.com">
    <recipient email="john.harris@mycompany.com">
</recipient-collection>
```

結果を繰り返し処理するには、 `for each` ループ：

```javascript
for each (var rcp in res:recipient)
    logInfo(rcp.@email)
```

ループにはローカルの受信者変数が含まれます。 受信者のコレクションに返された受信者ごとに、受信者の E メールが印刷されます。 [詳細情報](https://experienceleague.adobe.com/developer/campaign-api/api/f-logInfo.html) について `logInfo` 関数に置き換えます。

#### の結果 `getIfExists` 操作

それぞれの一致が要素として返されます。

```xml
<recipient id="52,378,079">
```

一致する要素がない場合は、空の要素が返されます。

```xml
<recipient/>
```

プライマリキーノード ( `@id` 属性：

```javascript
if (res.@id !=undefined)
    { // match was found
    …
    }
```

#### の結果 `get` 操作

一致の 1 つが要素として返されます。

```xml
<recipient id="52,378,079">
```

一致するものがない場合は、エラーが返されます。

>[!TIP]
>
>一致があることがわかっている場合は、 `get` 操作。 それ以外の場合は、 `getIfExists` 操作。 このベストプラクティスを使用すると、エラーによって予期しない問題が発生します。 次の `get` 操作、使用しない `try…catch` 文。 問題は、ワークフローのエラー処理プロセスによって処理されます。

#### の結果 `count` 操作

要素 `count` 属性が返される：

```xml
<recipient count="200">
```

結果を使用するには、 `@count` 属性：

```javascript
if (res.@count > 0)
    { // matches were found
    …
    }
```

の `select` 操作の実行時に、次のコードをワークフローの「JavaScript コード」アクティビティに追加します。

```javascript
var myXML =
<queryDef schema="nms:recipient" operation="select">
    <select>
        <node expr="@firstName"/>
        <node expr="@lastName"/>
    </select>
</queryDef>

var query = xtk.queryDef.create(myXML)

var res = query.ExecuteQuery()

for each (var rcp in res.recipient)
    logInfo(rcp.@firstName + " " + rcp.@lastName)
```

これは、 `select` operation はデフォルトの操作です。指定する必要はありません。

このビデオでは、データベースからの読み取り方法を示します。
>[!VIDEO](https://video.tv.adobe.com/v/18475/?learn=on)

## トリガー {#trigger-example}

ワークフローのトリガーは、例えば、テクニカルワークフロー内でプログラム的に、または Web アプリケーションページにユーザーが入力した情報を処理するために実行できます。

ワークフロートリガーは、イベントを使用して機能します。 イベントには、次の機能を使用できます。

* イベントを投稿するには、静的な `PostEvent` メソッド。 [詳細情報](https://experienceleague.adobe.com/developer/campaign-api/api/sm-workflow-PostEvent.html)。
* イベントを受け取るには、 **[!UICONTROL 外部シグナル]** アクティビティ。 [詳細情報](external-signal.md)。

ワークフローは、様々な方法でトリガー設定できます。

* ワークフローをインライントリガー、つまり、 **[!UICONTROL JavaScript コード]** アクティビティ。
* ワークフローは、別のトリガーの完了時に完了することができます。
   * 初期化スクリプトを **[!UICONTROL 終了]** 最初のワークフローの「 」アクティビティ。
   * を **[!UICONTROL 外部シグナル]** 「 」アクティビティを追加します。

      最初のワークフローが完了すると、イベントが投稿されます。 送信トランジションが有効化され、イベント変数が設定されます。 次に、ターゲットワークフローがイベントを受け取ります。

      >[!TIP]
      >
      >ベストプラクティスとして、アクティビティにスクリプトを追加する場合は、アクティビティ名を 2 つのハイフンで囲みます（例： ）。 `-- end --`. [詳細情報](workflow-best-practices.md) ワークフローのベストプラクティスについて

の構文 `PostEvent` メソッド：

```javascript
PostEvent(
    String     //ID of the target workflow
    String     //Name of the target activity
    String     //Name of the transition to be activated in case of multiple transitions
    XML        //Event parameters, in the <variables/> element
    Boolean    //To trigger the target workflow only once, set this parameter to true.
)
```

この例では、ワークフローの完了時に、短いテキストが **シグナル** の活動 **wkfExampleReceiver** ワークフロー：

```javascript
var strLabel = "Adobe Campaign, Marketing that delivers"
xtk.workflow.PostEvent(
    "wkfExampleReceiver",
    "signal",
    "",
    <variables strLine={strLabel}/>,
    false)
```

最後のパラメーターは `false`、 **wkfExampleReceiver** ワークフローは、最初のワークフローが完了するたびにトリガーされます。

ワークフローをトリガーする際は、次の原則に留意してください。

* この `PostEvent` コマンドは非同期で実行されます。 コマンドがサーバーキューに配置されます。 イベントが投稿されると、メソッドが返されます。
* ターゲットワークフローを開始する必要があります。 そうしないと、エラーがログファイルに書き込まれます。
* ターゲットワークフローが休止されている場合、 `PostEvent` コマンドは、ワークフローが再開されるまで待機中です。
* トリガーされるアクティビティでは、タスクが進行中である必要はありません。

このビデオでは、静的 API メソッドの使用方法を示します。
>[!VIDEO](https://video.tv.adobe.com/v/18481/?learn=on)

このビデオでは、ワークフローのトリガー方法を示します。
>[!VIDEO](https://video.tv.adobe.com/v/18485/?learn=on)

## データベースとのやり取り {#interact-example}

以下の例では、これらの操作の実行方法を示します。

* 以下を使用： `get` および `create` 非静的 SOAP メソッドを使用するスキーマのメソッド
* SQL クエリを実行するメソッドの作成
* 以下を使用： `write` レコードの挿入、更新、削除を行うメソッド

次の手順に従います。

1. クエリを定義します。

   * を使用してエンティティを取得する `create` 対応するスキーマのメソッド ( 例： `xtk:workflow` スキーマ。 [詳細情報](https://experienceleague.adobe.com/developer/campaign-api/api/f-create.html)。
   * 以下を使用： `queryDef` メソッドを使用して SQL クエリを発行します。

1. を使用してクエリを実行します。 `ExecuteQuery` メソッド。 [詳細情報](https://experienceleague.adobe.com/developer/campaign-api/api/sm-queryDef-ExecuteQuery.html)。

   以下を使用： `for each` ループを使用して結果を取得します。

### の構文 `queryDef` メソッド `select` 句

```xml
<queryDef schema="schema_key" operation="operation_type">
    <select>
        <node expr="expression1">
        <node sql="expression2">
    </select>
    <where> 
        <condition expr="expression1"/> 
        <condition sql="expression2"/>
    </where>
    <orderBy>
        <node expr="expression1">
        <node sql="expression2">
    </orderBy>
    <groupBy>
        <node expr="expression1">
        <node sql="expression2">
    </groupBy>
    <having>
        <condition expr="expression1"/> 
        <condition sql="expression2"/>
    </having>
</queryDef>
```

### `Create` メソッド

#### 例 1:レコードを選択してジャーナルに書き込み

内部名： **wfExamples** フォルダーが選択されます。 結果は内部名で昇順に並べ替えられ、ジャーナルに書き込まれます。

```javascript
var query = xtk.queryDef.create(
    <queryDef schema="xtk:workflow" operation="select">
        <select>
            <node expr="@internalName"/>
        </select>
        <where>
            <condition expr="[folder/@name]='wfExamples'"/>
        </where>
        <orderBy>
            <node expr="@internalName" sortDesc="false"/>
        </orderBy>
    </queryDef>
    )

var res = query.ExecuteQuery()
for each (var w in res.workflow)
    logInfo(w.@internalName)
```

#### 例 2:レコードを削除

Chris Smith という名前の受信者すべての名、姓、E メールおよび ID が選択されます。 結果は E メールで昇順に並べ替えられ、ジャーナルに書き込まれます。 A `delete` 操作を使用して、選択したレコードが削除されます。

```javascript
// Build the query, create a query object and hold the object in a variable
var query = xtk.queryDef.create(
        <queryDef schema="nms:recipient" operation="select">
            <select>
                <node expr="@firstName"/>
                <node expr="@lastName"/>
                <node expr="@email"/>
                <node expr="@id"/>
            </select>
            <where>
                <condition expr="[folder/@label]='Recipients'"/>
                <condition expr="[@lastName]='Smith'"/>
                <condition expr="[@firstName]='Chris'"/>
            </where>
            <orderBy>
                <node expr="@email" sortDesc="false"/>
            </orderBy>
        </queryDef>
)

//Run the query using the ExecuteQuery method against the created object
var res = query.ExecuteQuery()

//Loop through the results, print out the person's name and email, then delete the records
for each (var rec in res.recipient)
    {
     logInfo("Delete record = Email: " + rec.@email + ', ' + rec.@firstName + ' ' + rec.@lastName)
     xtk.session.Write(<recipient xtkschema="nms:recipient" _operation="delete" id={rec.@id}/>)
    }
```

#### 例 3:レコードを選択してジャーナルに書き込み

この例では、静的でないメソッドが使用されます。 情報がに保存されているすべての受信者の E メールと生年月日 **1234** フォルダーと、その電子メールドメイン名が「adobe」で始まるフォルダーが選択されます。 結果は生年月日を降順で並べ替えられます。 受信者の E メールがジャーナルに書き込まれます。

```javascript
var query = xtk.queryDef.create(
<queryDef schema="nms:recipient" operation="select">
    <select>
        <node expr="@email"/>
        <node sql="sEmail"/>
        <node expr="Year(@birthDate)"/>
    </select>
    <where>
        <condition expr="[@folder-id] = 1234 and @domain like 'adobe%'"/>
        <condition sql="iFolderId = 1234 and sDomain like 'adobe%'"/>
    </where>
    <orderBy>
        <node expr="@birthDate" sortDesc="true"/>
    </orderBy>
</queryDef>
)

var res = query.ExecuteQuery()
for each (var w in res.recipient)
    logInfo(w.@email)
```

### `Write` メソッド

レコードの挿入、更新、削除を行うことができます。 以下を使用して、 `Write` メソッドを使用できます。Adobe Campaign内の任意のスキーマで使用できます。 このメソッドは静的なので、オブジェクトを作成する必要はありません。 次の操作を使用できます。

* この `update` 操作
* この `insertOrUpdate` 操作、 `_key` 更新するレコードを識別する引数

   指定しない場合、 **受信者** フォルダに一致するレコードが存在する場合、そのレコードは任意のサブフォルダに更新されます。 それ以外の場合は、レコードはルートに作成されます **受信者** フォルダー。

* この `delete` 操作

>[!IMPORTANT]
> Adobe Campaign v8 を使用する場合は、 **取り込み** および **データの更新/削除** の API `Write` メソッドをSnowflake表に追加します。 [詳細を表示](https://experienceleague.adobe.com/docs/campaign/campaign-v8/architecture/api/new-apis.html){target=&quot;_blank&quot;}。

#### 例 1:レコードを挿入または更新する

```javascript
xtk.session.Write(
<recipient
    xtkschema="nms:recipient"
    _operation="insertOrUpdate" _key="@email"
    lastName="Lennon"
    firstName="John"
    email="johnlennon@thebeatles.com"
/>
)
```

#### 例 2:レコードを削除

次の使用例は、静的メソッドと非静的メソッドを組み合わせます。

```javascript
var query=xtk.queryDef.create(
<queryDef schema="nms:recipient" operation="select">
    <select>
        <node expr="@Id"/>
    </select>
    <where>
        <condition expr="[@email]='johnlennon@thebeatles.com'"/>
    </where>
</queryDef>
);

var res = query.ExecuteQuery()
for each (var w in res.recipient) {
xtk.session.Write(
    <recipient xtkschema="nms:recipient" _operation="delete" id={w.@id}/>
);
}
```

このビデオでは、静的でない API メソッドの使用方法を示します。
>[!VIDEO](https://video.tv.adobe.com/v/18477/?learn=on)

このビデオでは、ワークフローでの静的でない API メソッドの使用例を示します。
>[!VIDEO](https://video.tv.adobe.com/v/18476/?learn=on)

## 関連トピック

* [データ指向 API](../../configuration/using/data-oriented-apis.md)
* [JavaScript のスクリプトとテンプレート](javascript-scripts-and-templates.md)
* [JavaScript での SOAP メソッド](../../configuration/using/soap-methods-in-javascript.md)

### API ドキュメント

* [SOAP 呼び出しのサンプル](https://experienceleague.adobe.com/developer/campaign-api/api/p-14.html)
* メソッド:
   * [作成](https://experienceleague.adobe.com/developer/campaign-api/api/f-create.html)
   * [DeleteCollection](https://experienceleague.adobe.com/developer/campaign-api/api/sm-session-DeleteCollection.html)
   * [ExecuteQuery](https://experienceleague.adobe.com/developer/campaign-api/api/sm-queryDef-ExecuteQuery.html)
   * [PostEvent](https://experienceleague.adobe.com/developer/campaign-api/api/sm-workflow-PostEvent.html)
   * [書き込む](https://experienceleague.adobe.com/developer/campaign-api/api/sm-session-Write.html)
* [logInfo 関数](https://experienceleague.adobe.com/developer/campaign-api/api/f-logInfo.html)