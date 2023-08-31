---
product: campaign
title: データ指向の API
description: データ指向の API
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: API
role: Data Engineer, Developer
exl-id: a392c55e-541a-40b1-a910-4a6dc79abd2d
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '1868'
ht-degree: 1%

---

# データ指向の API{#data-oriented-apis}

データ指向 API を使用すると、データモデル全体に対処できます。

## データモデルの概要 {#overview-of-the-datamodel}

Adobe Campaignでは、エンティティごとに専用の読み取り API を提供していません（getRecipient 関数や getDelivery 関数などは提供していません）。 QUERY &amp; WRITER データの読み取りおよび変更メソッドを使用して、モデルのデータにアクセスします。

Adobe Campaignでは、コレクションを管理できます。クエリを使用すると、ベース全体で収集された情報のセットを復元できます。 SQL モードでのアクセスとは異なり、Adobe Campaign API はデータ列ではなく XML ツリーを返します。 Adobe Campaignは、収集したすべてのデータを含む複合ドキュメントを作成します。

この操作モードでは、XML ドキュメントの属性と要素、およびデータベース内のテーブルの列の間の 1 対 1 のマッピングは提供されません。

XML ドキュメントは、データベースの MEMO タイプのフィールドに格納されます。

## モデルの説明 {#description-of-the-model}

スクリプト内のデータベースのフィールドに対処できるように、Adobe Campaignデータモデルに関する知識が必要です。

データモデルの表示については、 [Adobe Campaign Data Model の説明](../../configuration/using/data-model-description.md).

## クエリとライター {#query-and-writer}

以下の概要スキーマでは、データベースと顧客 (Web ページまたはAdobe Campaignクライアントコンソール ) の間の読み取り (ExecuteQuery) および書き込み (Writer) の低レベルの交換について詳しく説明します。

![](assets/s_ncs_integration_webservices_schema_writer.png)

### ExecuteQuery {#executequery}

列と条件の場合は、クエリを使用できます。

これにより、基になる SQL を分離できます。 クエリ言語は、基になるエンジンに依存しません。一部の関数は再マッピングされ、複数の SELECT SQL 注文が生成される場合があります。

詳しくは、 [スキーマ「xtk:queryDef」の「ExecuteQuery」メソッドの例](../../configuration/using/web-service-calls.md#example-on-the--executequery--method-of-schema--xtk-querydef-).

The **ExecuteQuery** メソッドは、 [ExecuteQuery (xtk:queryDef)](#executequery--xtk-querydef-).

### Write {#write}

書き込みコマンドを使用すると、単純なドキュメントや複雑なドキュメントを書き込み、基本の 1 つ以上のテーブルにエントリを記述できます。

トランザクション API を使用すると、 **updateOrInsert** コマンド：1 つのコマンドを使用して、データを作成または更新できます。 また、変更の結合 (**結合**)：この操作モードを使用すると、部分的な更新を許可できます。

XML 構造は、データの論理ビューを提供し、SQL テーブルの物理構造を回避できます。

Write メソッドについて詳しくは、 [書き込み/書き込みコレクション (xtk:session)](#write---writecollection--xtk-session-).

## ExecuteQuery (xtk:queryDef) {#executequery--xtk-querydef-}

このメソッドを使用すると、スキーマに関連付けられたデータからクエリを実行できます。 認証文字列（ログインする必要があります）と、パラメーターとして送信するクエリを記述する XML ドキュメントを取ります。 戻りパラメーターは、クエリが参照するスキーマの形式でクエリの結果を含む XML ドキュメントです。

「xtk:queryDef」スキーマの「ExecuteQuery」メソッドの定義：

```
<method name="ExecuteQuery" const="true">
  <parameters>
    <param desc="Output XML document" name="output" type="DOMDocument" inout="out"/>
  </parameters>
</method>
```

>[!NOTE]
>
>これは「const」メソッドです。 入力パラメーターは、「xtk:queryDef」スキーマの形式で XML ドキュメントに含まれます。

### 入力クエリの XML ドキュメントの形式 {#format-of-the-xml-document-of-the-input-query}

クエリの XML ドキュメントの構造は、「xtk:queryDef」スキーマに記述します。 このドキュメントでは、SQL クエリの句 (「select」、「where」、「order by」、「group by」、「having」) について説明します。

```
<queryDef schema="schema_key" operation="operation_type">
  <select>
    <node expr="expression1">
    <node expr="expression2">
    ...
  </select>
  <where> 
    <condition expr="expression1"/> 
    <condition expr="expression2"/>
    ... 
  </where>
  <orderBy>
    <node expr="expression1">
    <node expr="expression2">
    ...
  </orderBy>
  <groupBy>
    <node expr="expression1">
    <node expr="expression2">
    ...
  </groupBy>
  <having>
    <condition expr="expression1"/> 
    <condition expr="expression2"/>
    ...
  </having>
</queryDef>
```

サブクエリ ( `<subquery>`  ) は、  `<condition> `  要素を選択します。 の構文   `<subquery> `   要素は    `<querydef>`.

の例 `<subquery>  : </subquery>`

```
<condition setOperator="NOT IN" expr="@id" enabledIf="$(/ignored/@ownerType)=1">
  <subQuery schema="xtk:operatorGroup">
     <select>
       <node expr="[@operator-id]" />
     </select>
     <where>
       <condition expr="[@group-id]=$long(../@owner-id)"/>
     </where>
   </subQuery>
</condition>  
  
```

クエリは、 **スキーマ** 属性。

必要な操作のタイプは、 **操作** 属性で、次のいずれかの値が含まれます。

* **get**：テーブルからレコードを取得し、データが存在しない場合はエラーを返します。
* **getIfExists**：テーブルからレコードを取得し、データが存在しない場合は空のドキュメントを返します。
* **選択**：複数のレコードを返すカーソルを作成し、データがない場合は空のドキュメントを返します。
* **count**：データ数を戻します。

The **XPath** 構文は、入力スキーマに基づいてデータを検索するために使用します。 XPath の詳細については、 [データスキーマ](../../configuration/using/data-schemas.md).

#### 「get」操作の例 {#example-with-the--get--operation}

E メールのフィルターを使用して、受信者の姓と名（「nms:recipient」スキーマ）を取得します。

```
<queryDef schema="nms:recipient" operation="get">
  <!-- fields to retrieve -->
  <select>
    <node expr="@firstName"/>
    <node expr="@lastName"/>
  </select> 

  <!-- condition on email -->
  <where>  
    <condition expr="@email= 'john.doe@aol.com'"/>
  </where>
</queryDef>
```

#### 「select」操作の例 {#example-with-the--select--operation}

あるフォルダーでフィルターされた受信者のリストと、生年月日の降順で並べ替えられた E メールドメインを返します。

```
<queryDef schema="nms:recipient" operation="select">
  <select>
    <node expr="@email"/>
    <!-- builds a string with the concatenation of the last name and first name separated by a dash -->      
    <node expr="@lastName+'-'+@firstName"/>
    <!-- get year of birth date -->
    <node expr="Year(@birthDate)"/>
  </select> 

  <where>  
     <condition expr="[@folder-id] = 1234 and @domain like 'Adobe%'"/>
  </where>

  <!-- order by birth date -->
  <orderBy>
    <node expr="@birthDate" sortDesc="true"/> <!-- by default sortDesc="false" -->
  </orderBy>
</queryDef>
```

式には、単純なフィールドや、演算や文字列の連結などの複雑な式を使用できます。

返されるレコード数を制限するには、 **lineCount** 属性 `<querydef>` 要素を選択します。

クエリが返すレコードの数を 100 に制限するには：

```
<queryDef schema="nms:recipient" operation="select" lineCount="100">
...
```

次の 100 件のレコードを取得するには、同じクエリを再度実行し、 **startLine** 属性。

```
<queryDef schema="nms:recipient" operation="select" lineCount="100" startLine="100">
...
```

#### 「count」操作の例 {#example-with-the--count--operation}

クエリのレコード数をカウントするには、次の手順に従います。

```
<queryDef schema="nms:recipient" operation="count"">
  <!-- condition on the folder and domain of the email -->
  <where>  
    <condition expr="[@folder-id] = 1234" and @domain like 'Adobe%'"/>
  </where>
</queryDef>
```

>[!NOTE]
>
>ここでも、前の例の条件を使用します。 The `<select>` および句は使用されません。 `</select>`

#### データのグループ化 {#data-grouping}

複数回参照されている E メールアドレスを取得するには：

```
<queryDef schema="nms:recipient" operation="select">
  <select>
    <node expr="@email"/>
    <node expr="count(@email)"/>
  </select>

  <!-- email grouping clause -->
  <groupby>
    <node expr="@email"/>
  </groupby>

  <!-- grouping condition -->
  <having>
    <condition expr="count(@email) > 1"/>
  </having>

</queryDef>
```

クエリを簡略化するには、 **groupBy** 属性は、グループ化するフィールドに直接属性を持ちます。

```
<select>
  <node expr="@email" groupBy="true"/>
</select>
```

>[!NOTE]
>
>現在は、 `<groupby>` 要素を選択します。

#### 条件でのブラケティング {#bracketing-in-conditions}

以下に、同じ条件でのブラケットの例を 2 つ示します。

* 単一の式の単純なバージョン：

  ```
  <where>
    <condition expr="(@age > 15 or @age <= 45) and  (@city = 'Newton' or @city = 'Culver City') "/>
  </where>
  ```

* を使用した構造化バージョン `<condition>` 要素：

  ```
  <where>
    <condition bool-operator="AND">
      <condition expr="@age > 15" bool-operator="OR"/>
      <condition expr="@age <= 45"/>
    </condition>
    <condition>
      <condition expr="@city = 'Newton'" bool-operator="OR"/>
      <condition expr="@city = 'Culver City'"/>
    </condition>
  </where>
  ```

同じフィールドに複数の条件が適用される場合は、「OR」演算子を「IN」演算子に置き換えることができます。

```
<where>
  <condition>
    <condition expr="@age IN (15, 45)"/>
    <condition expr="@city IN ('Newton', 'Culver City')"/>
  </condition>
</where>
```

この構文は、条件で 2 つ以上のデータが使用される場合にクエリを簡素化します。

#### リンクの例 {#examples-on-links}

* リンク 1-1 または N1：テーブルに外部キー（テーブルからリンクが開始する）がある場合、リンクされたテーブルのフィールドを直接フィルターまたは取得できます。

  フォルダーラベルのフィルターの例：

  ```
  <where>
    <condition expr="[folder/@label] like 'Segment%'"/>
  </where>
  ```

  「nms:recipient」スキーマからフォルダーのフィールドを取得するには、次のようにします。

  ```
  <select>
    <!-- label of recipient folder -->
    <node expr="[folder/@label]"/>
    <!-- displays the string count of the folder -->
    <node expr="partition"/>
  </select>
  ```

* コレクションリンク (1N)：コレクションテーブルのフィールドに対するフィルタリングは、 **EXISTS** または **存在しない** 演算子を使用します。

  「ニュースレター」情報サービスを購読した受信者をフィルターするには、次の手順を実行します。

  ```
  <where>
    <condition expr="subscription" setOperator="EXISTS">
      <condition expr="@name = 'Newsletter'"/>
    </condition>
  </where>
  ```

  コレクションリンクのフィールドを `<select>` クエリが基数積を返すので、句はお勧めしません。 リンクされたテーブルに 1 つのレコードのみが含まれる場合にのみ使用します ( 例： `<node expr="">`) をクリックします。

  「subscription」コレクションリンクの例：

  ```
  <select>
    <node expr="subscription/@label"/>
  </select>
  ```

  サブリストを取得して、 `<select>` 句を使用します。 参照されるフィールドの XPath は、コレクション要素のコンテキストに基づいています。

  フィルター ( `<orderby>`  ) および制限 (  `<where>`  ) 要素をコレクション要素に追加できます。

  この例では、クエリは受信者ごとに、受信者が購読する E メールと情報サービスのリストを返します。

  ```
  <queryDef schema="nms:recipient" operation="select">
    <select>
      <node expr="@email"/>
  
      <!-- collection table (unbound type) -->
      <node expr="subscription">  
        <node expr="[service/@label]"/>    
        <!-- sub-condition on the collection table -->
        <where>  
          <condition expr="@expirationDate >= GetDate()"/>
        </where>
        <orderBy>
          <node expr="@expirationDate"/> 
        </orderBy>
      </node>
    </select> 
  </queryDef>
  ```

#### 「where」句と「select」句のパラメーターのバインド {#binding-the-parameters-of-the--where--and--select--clause}

パラメーターの連結により、エンジンはクエリで使用されるパラメーターの値を設定できます。 エンジンは値のエスケープを担当し、取得するパラメータのキャッシュの利点もあるので、これは非常に便利です。

クエリが構築されると、「連結」の値が文字 (? ODBC で、 `#[index]#` postgres...内 ) を SQL クエリの本文に追加します。

```
<select>
  <!--the value will be bound by the engine -->
  <node expr="@startDate = #2002/02/01#"/>                   
  <!-- the value will not be bound by the engine but visible directly in the query -->
  <node expr="@startDate = #2002/02/01#" noSqlBind="true"/> 
</select>
```

パラメーターのバインドを避けるには、「noSqlBind」属性に値「true」を設定する必要があります。

>[!IMPORTANT]
>
>クエリに「order-by」または「group-by」の命令が含まれる場合、データベースエンジンは値を「バインド」できません。 @noSqlBind=&quot;true&quot;属性は、クエリの「select」または「where」の指示に配置する必要があります。

#### クエリの構築に関するヒント： {#query-building-tip-}

クエリの構文を理解できるように、Adobe Campaignクライアントコンソール ( **[!UICONTROL ツール/汎用クエリエディター…]** メニュー ) を参照してください。 手順は次のとおりです。

1. 取得するデータを選択します。

   ![](assets/s_ncs_integration_webservices_queyr1.png)

1. フィルター条件を定義します。

   ![](assets/s_ncs_integration_webservices_queyr2.png)

1. クエリを実行し、Ctrl キーを押しながら F4 キーを押してクエリのソースコードを表示します。

   ![](assets/s_ncs_integration_webservices_queyr3.png)

### 出力ドキュメントの形式 {#output-document-format}

戻りパラメーターは、クエリに関連付けられたスキーマの形式の XML ドキュメントです。

「get」操作での「nms:recipient」スキーマからの戻り値の例：

```
<recipient email="john.doe@adobe.com" lastName"Doe" firstName="John"/>
```

「選択」操作で返されるドキュメントは、次の要素の列挙です。

```
<!-- the name of the first element does not matter -->
<recipient-collection>   
  <recipient email="john.doe@adobe.com" lastName"Doe" firstName="John"/>
  <recipient email="peter.martinez@adobe.com" lastName"Martinez" firstName="Peter"/>
  <recipient...
</recipient-collection>  
```

「count」タイプの操作に対して返されるドキュメントの例：

```
<recipient count="3"/>
```

#### エイリアス {#alias}

エイリアスを使用すると、出力ドキュメント内のデータの場所を変更できます。 The **alias** 属性は、対応するフィールドで XPath を指定する必要があります。

```
<queryDef schema="nms:recipient" operation="get">
  <select>
    <node expr="@firstName" alias="@firstName"/>
    <node expr="@lastName"/>
    <node expr="[folder/@label]" alias="@My_folder"/>
  </select> 
</queryDef>
```

戻り値:

```
<recipient My_folder="Recipients" First name ="John" lastName="Doe"/>
```

次の代わりに使用します。

```
<recipient firstName="John" lastName="Doe">
  <folder label="Recipients"/>
</recipient>
```

### SOAP メッセージの例 {#example-of-soap-messages}

* クエリ:

  ```
  <?xml version='1.0' encoding='ISO-8859-1'?>
  <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <ExecuteQuery xmlns='urn:xtk:queryDef' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
        <__sessiontoken xsi:type='xsd:string'/>
        <entity xsi:type='ns:Element' SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
          <queryDef operation="get" schema="nms:recipient" xtkschema="xtk:queryDef">
            <select>
              <node expr="@email"/>
              <node expr="@lastName"/>
              <node expr="@firstName"/>
            </select>
            <where>
              <condition expr="@id = 3599"/>
            </where>
          </queryDef>
        </entity>
      </ExecuteQuery>
    </SOAP-ENV:Body>
  </SOAP-ENV:Envelope>
  ```

* 応答:

  ```
  <?xml version='1.0' encoding='ISO-8859-1'?>
  <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <ExecuteQueryResponse xmlns='urn:xtk:queryDef' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
        <pdomOutput xsi:type='ns:Element' SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
          <recipient email="john.doe@adobe.com" lastName"Doe" firstName="John"/>
        </pdomOutput>
      </ExecuteQueryResponse>
    </SOAP-ENV:Body>
  </SOAP-ENV:Envelope>
  ```

## 書き込み/書き込みコレクション (xtk:session) {#write---writecollection--xtk-session-}

これらのサービスは、エンティティ（「Write」メソッド）またはエンティティのコレクション（「WriteCollection」メソッド）の挿入、更新、削除に使用されます。

更新するエンティティは、データスキーマに関連付けられています。 入力パラメーターは、認証文字列（ログインする必要があります）と、更新するデータを含む XML ドキュメントです。

このドキュメントでは、書き込み手順を設定する手順を説明します。

この呼び出しは、エラーを除き、データを返しません。

「xtk:session」スキーマの「Write」および「WriteCollection」メソッドの定義：

```
<method name="Write" static="true">
  <parameters>
    <param name="doc" type="DOMDocument" desc="Difference document"/>
  </parameters>
</method>
<method name="WriteCollection" static="true">
  <parameters>
    <param name="doc" type="DOMDocument" desc="Difference collection document"/>
  </parameters>
</method>
```

>[!NOTE]
>
>これは「静的」メソッドです。 入力パラメーターは、更新するスキーマの形式で XML ドキュメントに含まれます。

### 概要 {#overview}

データの紐付けは、関連付けられたスキーマに入力されたキーの定義に基づいて動作します。 書き込みプロシージャは、入力ドキュメントに入力されたデータに基づいて、最初の適格なキーを検索します。 データベース内のエンティティの存在に基づいて、エンティティが挿入または更新されます。

更新するエンティティのスキーマのキーは、 **xtkschema** 属性。

したがって、紐付けキーは、 **_key** キーを構成する XPath のリストを含む属性（コンマ区切り）。

操作のタイプを強制するには、 **_operation** 属性の値は次のとおりです。

* **挿入**：レコードを強制的に挿入します（紐付けキーは使用されません）。
* **insertOrUpdate**：紐付けキー（デフォルトのモード）に応じて、レコードを更新または挿入します。
* **更新**：レコードを更新します。データが存在しない場合は何もしません。
* **削除**：レコードを削除します。
* **なし**：リンクの紐付けにのみ使用され、更新や挿入は使用されません。

### 「Write」メソッドの使用例 {#example-with-the--write--method}

E メールアドレス、生年月日、市区町村を使用して受信者（暗黙の「insertOrUpdate」操作）を更新または挿入する場合：

```
<recipient xtkschema="nms:recipient" email="john.doe@adobe.com" birthDate="1956/05/04" folder-id=1203 _key="@email, [@folder-id]">
  <location city="Newton"/>
</recipient>
```

受信者の削除：

```
<recipient xtkschema="nms:recipient" _operation="delete" email="rene.dupont@adobe.com" folder-id=1203 _key="@email, [@folder-id]"/>
```

>[!NOTE]
>
>削除操作の場合、入力ドキュメントには、紐付けキーを構成するフィールドのみを含める必要があります。

### 「WriteCollection」メソッドの使用例 {#example-with-the--writecollection--method}

複数の受信者の更新または挿入：

```
<recipient-collection xtkschema="nms:recipient">    
  <recipient email="john.doe@adobe.com" firstName="John" lastName="Doe" _key="@email"/>
  <recipient email="peter.martinez@adobe.com" firstName="Peter" lastName="Martinez" _key="@email"/>
  <recipient ...
</recipient-collection>
```

### リンクの例 {#example-on-links}

#### 例 1 {#example-1}

内部名 (@name) に基づいたフォルダーと受信者の関連付け。

```
<recipient _key="[folder/@name], @email" email="john.doe@adobe.net" lastName="Doe" firstName="John" xtkschema="nms:recipient">
  <folder name="Folder2" _operation="none"/>
</recipient>
```

「_key」属性と「_operation」属性は、リンクされた要素に対して入力できます。 この要素の動作は、入力スキーマのメイン要素の動作と同じです。

メインエンティティのキーの定義 (「nms:recipient」) は、リンクされたテーブル（要素）のフィールドで構成されます `<folder>`  スキーマ「xtk:folder」) および電子メール。

>[!NOTE]
>
>folder 要素に対して入力した操作「none」は、更新や挿入を行わないで、フォルダーに対する紐付けを定義します。

#### 例 2 {#example-2}

受信者から会社（「cus:company」スキーマ内のリンクされたテーブル）を更新する場合：

```
<recipient _key="[folder/@name], @email" email="john.doe@adobe.net" lastName="Doe" firstName="John" xtkschema="nms:recipient">
  <company name="adobe" code="ERT12T" _key="@name" _operation="update"/>
</recipient>
```

#### 例 3 {#example-3}

グループ関係テーブル (「nms:rcpGrpRel」) を持つグループに受信者を追加する：

```
<recipient _key="@email" email="martin.ledger@adobe.net" xtkschema="nms:recipient">
  <rcpGrpRel _key="[rcpGroup/@name]">
    <rcpGroup name="GRP1"/>
  </rcpGrpRel>
</recipient>
```

>[!NOTE]
>
>キーの定義が `<rcpgroup>` 要素を使用する必要はありません。グループ名に基づく暗黙のキーが「nms:group」スキーマで定義されているからです。

### XML コレクション要素 {#xml-collection-elements}

デフォルトでは、XML コレクション要素を更新するには、すべてのコレクション要素を設定する必要があります。 データベースのデータは、入力ドキュメントのデータに置き換えられます。 更新する要素のみがドキュメントに含まれている場合、データベースの XML データとの結合を強制するには、更新するすべてのコレクション要素に対して「_operation」属性を設定する必要があります。

### SOAP メッセージの例 {#example-of-soap-messages-1}

* クエリ:

  ```
  <?xml version='1.0' encoding='ISO-8859-1'?>
  <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <Write xmlns='urn:xtk:persist' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
        <__sessiontoken xsi:type='xsd:string'/>
        <domDoc xsi:type='ns:Element' SOAP-ENV:encodingStyle='http://xml.apache.org/xml-soap/literalxml'>
          <recipient xtkschema="nms:recipient" email="rene.dupont@adobe.com" firstName="René" lastName="Dupont" _key="@email">
        </domDoc>
      </Write>
    </SOAP-ENV:Body>
  </SOAP-ENV:Envelope>
  ```

* 応答:

  ```
  <?xml version='1.0' encoding='ISO-8859-1'?>
  <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <WriteResponse xmlns='urn:' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
      </WriteResponse>
    </SOAP-ENV:Body>
  </SOAP-ENV:Envelope>
  ```

  次のエラーで返されます：

  ```
  <?xml version='1.0'?>
  <SOAP-ENV:Envelope xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <SOAP-ENV:Fault>
        <faultcode>SOAP-ENV:Server</faultcode>
        <faultstring xsi:type="xsd:string">Error while executing the method 'Write' of service 'xtk:persist'.</faultstring>
        <detail xsi:type="xsd:string">PostgreSQL error: ERROR:  duplicate key violates unique constraint &quot;nmsrecipient_id&quot;Impossible to save document of type 'Recipients (nms:recipient)'</detail>
      </SOAP-ENV:Fault>
    </SOAP-ENV:Body>
  </SOAP-ENV:Envelope>
  ```
