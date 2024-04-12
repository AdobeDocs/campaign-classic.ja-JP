---
product: campaign
title: データ指向の API
description: データ指向の API
feature: API
role: Data Engineer, Developer
exl-id: a392c55e-541a-40b1-a910-4a6dc79abd2d
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1868'
ht-degree: 1%

---

# データ指向の API{#data-oriented-apis}

データ指向の API を使用すると、データモデル全体に対処できます。

## データモデルの概要 {#overview-of-the-datamodel}

Adobe Campaignは、エンティティごとに専用の読み取り API を提供していません（getRecipient 関数や getDelivery 関数など）。 モデルのデータにアクセスするには、QUERY &amp; WRITER データの読み取り方法と変更方法を使用します。

Adobe Campaignでは、コレクションを管理できます。クエリを使用すると、ベース全体で収集された一連の情報を復元できます。 SQL モードでのアクセスとは異なり、Adobe Campaign API はデータ列ではなく XML ツリーを返します。 したがって、Adobe Campaignは、収集されたすべてのデータを含む複合ドキュメントを作成します。

この操作モードでは、XML ドキュメントの属性と要素、およびデータベース内のテーブルの列が 1 対 1 で対応していません。

XML ドキュメントは、データベースのメモ型フィールドに格納されます。

## モデルの説明 {#description-of-the-model}

スクリプトでデータベースのフィールドに対処できるようにするには、Adobe Campaign データモデルに精通している必要があります。

データモデルのプレゼンテーションについては、を参照してください。 [Adobe Campaign データモデルの説明](../../configuration/using/data-model-description.md).

## クエリとライター {#query-and-writer}

次の概要スキーマでは、データベースと顧客（web ページまたはAdobe Campaign クライアントコンソール）の間での読み取り（ExecuteQuery）と書き込み（Writer）のレベルの低い交換について詳しく説明します。

![](assets/s_ncs_integration_webservices_schema_writer.png)

### ExecuteQuery {#executequery}

列と条件には、クエリを使用できます。

これにより、基になる SQL を分離できます。 クエリ言語は、基になるエンジンに依存しません。一部の関数は再マップされ、それによって複数の SELECT SQL 命令が生成される場合があります。

詳しくは、次を参照してください [スキーマ「xtk:queryDef」の「ExecuteQuery」メソッドの例](../../configuration/using/web-service-calls.md#example-on-the--executequery--method-of-schema--xtk-querydef-).

この **ExecuteQuery** メソッドの詳細 [ExecuteQuery （xtk:queryDef）](#executequery--xtk-querydef-).

### 書き込む {#write}

書き込みコマンドを使用すると、ベースの 1 つ以上のテーブルにエントリを含む、単純なドキュメントや複雑なドキュメントを書き込むことができます。

トランザクション API では、 **updateOrInsert** コマンド：1 つのコマンドを使用して、データを作成または更新できます。 変更の結合を設定することもできます（**結合**）：この操作モードでは、部分更新を許可できます。

XML 構造はデータの論理ビューを提供し、SQL テーブルの物理構造を回避できます。

Write メソッドは、次の場所で提供されます。 [書き込み/書き込みコレクション（xtk:session）](#write---writecollection--xtk-session-).

## ExecuteQuery （xtk:queryDef） {#executequery--xtk-querydef-}

このメソッドを使用すると、スキーマに関連付けられたデータからクエリを実行できます。 これは、認証文字列（ログインする必要があります）と、パラメーターとして送信されるクエリを記述した XML ドキュメントを受け取ります。 戻りパラメーターは、クエリの結果を、クエリが参照するスキーマの形式で含む XML ドキュメントです。

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

クエリの XML ドキュメントの構造については、「xtk:queryDef」スキーマを参照してください。 このドキュメントでは、SQL クエリーの句として「select」、「where」、「order by」、「group by」、「having」について説明します。

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

サブクエリ （ `<subquery>`  ）は  `<condition> `  要素。 の構文   `<subquery> `   要素は、の構文に基づいています    `<querydef>`.

例 `<subquery>  : </subquery>`

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

クエリは、から開始スキーマを参照する必要があります **スキーマ** 属性。

必要な操作のタイプは、に入力します。 **操作** 属性で、次のいずれかの値が含まれます。

* **取得**：テーブルからレコードを取得し、データが存在しない場合はエラーを返します。
* **getIfExists**：テーブルからレコードを取得し、データが存在しない場合は空のドキュメントを返します。
* **選択**：複数のレコードを返すカーソルを作成し、データがない場合は空のドキュメントを返します。
* **count**：データ数を返します。

この **XPath** 構文は、入力スキーマに基づいてデータを検索するために使用されます。 XPath の詳細については、を参照してください。 [データスキーマ](../../configuration/using/data-schemas.md).

#### 「get」操作の例 {#example-with-the--get--operation}

メールのフィルターを使用して、受信者の姓と名（「nms：受信者」スキーマ）を取得します。

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

フォルダーおよび電子メールドメインでフィルタリングされた受信者のリストを、生年月日の降順に並べ替えて返します。

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

式には、単純なフィールドや、算術演算や文字列の連結などの複雑な式を指定できます。

返されるレコードの数を制限するには、 **lineCount** の属性 `<querydef>` 要素。

クエリによって返されるレコードの数を 100 に制限するには、次の手順に従います。

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
>ここでも、前の例の条件を使用します。 この `<select>` および句は使用されません。 `</select>`

#### データのグループ化 {#data-grouping}

複数回参照されるメールアドレスを取得するには：

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

クエリは、を追加することで簡略化できます **groupBy** グループ化するフィールドに直接属性を設定します。

```
<select>
  <node expr="@email" groupBy="true"/>
</select>
```

>[!NOTE]
>
>を入力する必要はなくなりました `<groupby>` 要素。

#### 状態の括弧 {#bracketing-in-conditions}

同じ条件で括弧を使用した例を 2 つ示します。

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

この構文により、条件で 3 つ以上のデータが使用される場合のクエリが簡略化されます。

#### リンクの例 {#examples-on-links}

* リンク 1-1 または N1：テーブルに外部キーがある（リンクはテーブルから開始する）場合、リンクされたテーブルのフィールドを直接フィルタリングまたは取得できます。

  フォルダーラベルに対するフィルターの例：

  ```
  <where>
    <condition expr="[folder/@label] like 'Segment%'"/>
  </where>
  ```

  「nms:recipient」スキーマからフォルダーのフィールドを取得するには：

  ```
  <select>
    <!-- label of recipient folder -->
    <node expr="[folder/@label]"/>
    <!-- displays the string count of the folder -->
    <node expr="partition"/>
  </select>
  ```

* コレクションリンク （1N）：コレクションテーブルのフィールドに対するフィルタリングは、次を使用して実行する必要があります **が存在する** または **存在しない** 演算子。

  「ニュースレター」情報サービスを購読している受信者をフィルタリングするには：

  ```
  <where>
    <condition expr="subscription" setOperator="EXISTS">
      <condition expr="@name = 'Newsletter'"/>
    </condition>
  </where>
  ```

  からのコレクションリンクのフィールドの直接取得 `<select>` クエリが基数を返すので、句はお勧めできません。 リンク テーブルにレコードが 1 つしか含まれていない場合にのみ使用されます（例 `<node expr="">`）に設定します。

  「購読」コレクションリンクの例：

  ```
  <select>
    <node expr="subscription/@label"/>
  </select>
  ```

  内のコレクションリンクの要素を含むサブリストを取得できます `<select>` 句。 参照されるフィールドの XPath は、コレクション要素のコンテキストに基づいています。

  フィルター（ `<orderby>`  ）と制限（  `<where>`  ）要素をコレクション要素に追加できます。

  この例では、受信者ごとに、受信者が登録しているメールと情報サービスのリストがクエリによって返されます。

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

パラメーターのバインディングにより、エンジンはクエリで使用されるパラメーターの値を設定できます。 エンジンが値のエスケープを担当し、取得するパラメーターにキャッシュを使用する利点もあるため、これは非常に便利です。

クエリを構築すると、「連結」値は文字（? ODBC では、次の操作が可能です。 `#[index]#` （postgres では…）を SQL クエリの本文に追加します。

```
<select>
  <!--the value will be bound by the engine -->
  <node expr="@startDate = #2002/02/01#"/>                   
  <!-- the value will not be bound by the engine but visible directly in the query -->
  <node expr="@startDate = #2002/02/01#" noSqlBind="true"/> 
</select>
```

パラメーターをバインドしないようにするには、「noSqlBind」属性に値「true」を設定する必要があります。

>[!IMPORTANT]
>
>クエリに「order-by」または「group-by」命令が含まれている場合、データベースエンジンは値を「バインド」できません。 @noSqlBind=&quot;true&quot;属性は、クエリの「select」命令や「where」命令に配置する必要があります。

#### クエリ作成のヒント： {#query-building-tip-}

クエリの構文に役立つように、Adobe Campaign クライアントコンソールの汎用クエリエディター（ **[!UICONTROL ツール/汎用クエリエディター…]** メニュー）。 手順は次のとおりです。

1. 取得するデータを選択します。

   ![](assets/s_ncs_integration_webservices_queyr1.png)

1. フィルター条件を定義します。

   ![](assets/s_ncs_integration_webservices_queyr2.png)

1. クエリを実行し、Ctrl + F4 キーを押して、クエリのソースコードを表示します。

   ![](assets/s_ncs_integration_webservices_queyr3.png)

### 出力ドキュメント形式 {#output-document-format}

戻りパラメーターは、クエリに関連付けられたスキーマの形式を持つ XML ドキュメントです。

「get」操作で「nms:recipient」スキーマから返される例：

```
<recipient email="john.doe@adobe.com" lastName"Doe" firstName="John"/>
```

「選択」操作で、返されるドキュメントは要素の列挙です。

```
<!-- the name of the first element does not matter -->
<recipient-collection>   
  <recipient email="john.doe@adobe.com" lastName"Doe" firstName="John"/>
  <recipient email="peter.martinez@adobe.com" lastName"Martinez" firstName="Peter"/>
  <recipient...
</recipient-collection>  
```

「count」タイプの操作で返されるドキュメントの例：

```
<recipient count="3"/>
```

#### エイリアス {#alias}

エイリアスを使用すると、出力ドキュメント内のデータの場所を変更できます。 この **エイリアス** 属性は、対応するフィールドに XPath を指定する必要があります。

```
<queryDef schema="nms:recipient" operation="get">
  <select>
    <node expr="@firstName" alias="@firstName"/>
    <node expr="@lastName"/>
    <node expr="[folder/@label]" alias="@My_folder"/>
  </select> 
</queryDef>
```

戻り値：

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

* クエリ :

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

* 応答：

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

## 書き込み/書き込みコレクション（xtk:session） {#write---writecollection--xtk-session-}

これらのサービスは、エンティティ（「Write」メソッド）またはエンティティのコレクション（「WriteCollection」メソッド）の挿入、更新、削除に使用されます。

更新するエンティティは、データスキーマに関連付けられています。 入力パラメーターは、認証文字列（ログインする必要があります）と、更新するデータを含む XML ドキュメントです。

このドキュメントでは、書き込み手順の設定手順について説明します。

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

データの紐付けは、関連するスキーマに入力されたキーの定義に基づいて動作します。 書き込みプロシージャは、入力ドキュメントに入力されたデータに基づいて、最初の適格なキーを探します。 エンティティは、データベース内の存在に基づいて挿入または更新されます。

更新するエンティティのスキーマのキーは、に基づいて入力されます **xtkschema** 属性。

したがって、紐付けキーは、を使用して強制できます。 **_key** キーを構成する XPath のリストを含む属性（コンマ区切り）。

にデータを入力することにより、操作タイプを強制することができます。 **操作（_o）** 次の値を持つ属性：

* **挿入**：レコードを強制的に挿入（紐付けキーは使用されません）、
* **insertOrUpdate**：紐付けキーに応じてレコードを更新または挿入します（デフォルトモード）。
* **更新**：レコードを更新します。データが存在しない場合は何も行いません。
* **削除**：レコードを削除します。
* **なし**：リンクの紐付けにのみ使用され、更新や挿入は行われません。

### 「Write」メソッドの例 {#example-with-the--write--method}

メールアドレス、生年月日、市区町村を使用して、受信者を更新または挿入（暗黙的な「insertOrUpdate」操作）します。

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

### 「WriteCollection」メソッドの例 {#example-with-the--writecollection--method}

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

内部名（@name）に基づいてフォルダーを受信者に関連付けます。

```
<recipient _key="[folder/@name], @email" email="john.doe@adobe.net" lastName="Doe" firstName="John" xtkschema="nms:recipient">
  <folder name="Folder2" _operation="none"/>
</recipient>
```

「_key」属性と「_operation」属性は、リンクされた要素に対して入力できます。 この要素の動作は、入力スキーマのメイン要素の動作と同じです。

メインエンティティ（「nms:recipient」）のキーの定義は、リンクされたテーブル（要素）のフィールドで構成されます `<folder>`  スキーマ「xtk:folder」）とメール。

>[!NOTE]
>
>フォルダー要素に対して入力された操作「なし」は、更新または挿入を行わずにフォルダーの紐付けを定義します。

#### 例 2 {#example-2}

受信者からの会社（「cus:company」スキーマ内のリンクされたテーブル）の更新：

```
<recipient _key="[folder/@name], @email" email="john.doe@adobe.net" lastName="Doe" firstName="John" xtkschema="nms:recipient">
  <company name="adobe" code="ERT12T" _key="@name" _operation="update"/>
</recipient>
```

#### 例 3 {#example-3}

グループ関係テーブル（&quot;nms:rcpGrpRel&quot;）を使用してグループに受信者を追加する：

```
<recipient _key="@email" email="martin.ledger@adobe.net" xtkschema="nms:recipient">
  <rcpGrpRel _key="[rcpGroup/@name]">
    <rcpGroup name="GRP1"/>
  </rcpGrpRel>
</recipient>
```

>[!NOTE]
>
>キーの定義は、 `<rcpgroup>` 要素：グループ名に基づく暗黙のキーが「nms:group」スキーマで定義されているからです。

### XML コレクション要素 {#xml-collection-elements}

デフォルトでは、XML コレクション要素を更新するために、すべてのコレクション要素を入力する必要があります。 データベースのデータは、入力ドキュメントのデータに置き換えられます。 更新する要素のみがドキュメントに含まれている場合、データベースの XML データとのマージを強制するには、更新するすべてのコレクション要素に「_operation」属性を設定する必要があります。

### SOAP メッセージの例 {#example-of-soap-messages-1}

* クエリ :

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

* 応答：

  ```
  <?xml version='1.0' encoding='ISO-8859-1'?>
  <SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='http://xml.apache.org/xml-soap' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
    <SOAP-ENV:Body>
      <WriteResponse xmlns='urn:' SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'>
      </WriteResponse>
    </SOAP-ENV:Body>
  </SOAP-ENV:Envelope>
  ```

  次のエラーで返されます。

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
