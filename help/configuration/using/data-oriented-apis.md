---
product: campaign
title: データ指向の API
description: データ指向の API
audience: configuration
content-type: reference
topic-tags: api
exl-id: a392c55e-541a-40b1-a910-4a6dc79abd2d
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 1%

---

# データ指向の API{#data-oriented-apis}

データ指向APIを使用すると、データモデル全体に対処できます。

## データモデル{#overview-of-the-datamodel}の概要

Adobe Campaignでは、エンティティごとに専用の読み取りAPIを提供していません（getRecipient関数やgetDelivery関数などは提供していません）。 QUERY &amp; WRITERデータの読み取りおよび変更メソッドを使用して、モデルのデータにアクセスします。

Adobe Campaignでは、コレクションを管理できます。クエリを使用すると、ベース全体で収集された情報のセットを復元できます。 SQLモードでのアクセスとは異なり、Adobe Campaign APIはデータ列ではなくXMLツリーを返します。 Adobe Campaignは、収集したすべてのデータを含む複合ドキュメントを作成します。

この操作モードでは、XMLドキュメントの属性と要素と、データベース内のテーブルの列との間の1対1のマッピングは提供されません。

XMLドキュメントは、データベースのMEMO型のフィールドに格納されます。

## モデル{#description-of-the-model}の説明

スクリプト内のデータベースのフィールドに対処できるAdobe Campaignデータモデルに精通している必要があります。

データモデルの表示については、[Adobe Campaignデータモデルの説明](../../configuration/using/data-model-description.md)を参照してください。

構造を生成するには、次の記事を参照してください。[データモデルまたはデータディクショナリの生成方法](https://helpx.adobe.com/campaign/kb/generate-data-model.html)。

## クエリとライター{#query-and-writer}

以下の概要スキーマでは、データベースと顧客(WebページまたはAdobe Campaignクライアントコンソール)の間の読み取り(ExecuteQuery)および書き込み(Writer)の低レベルの交換について詳しく説明します。

![](assets/s_ncs_integration_webservices_schema_writer.png)

### ExecuteQuery {#executequery}

列と条件に対しては、クエリを使用できます。

これにより、基になるSQLを分離できます。 クエリ言語は、基になるエンジンに依存しません。一部の関数は再マッピングされ、複数のSELECT SQLオーダーが生成される場合があります。

詳しくは、スキーマ「xtk:queryDef」](../../configuration/using/web-service-calls.md#example-on-the--executequery--method-of-schema--xtk-querydef-)の「ExecuteQuery」メソッドの例を参照してください。[

**ExecuteQuery**&#x200B;メソッドは、[ExecuteQuery(xtk:queryDef)](#executequery--xtk-querydef-)で説明しています。

### 書き込む {#write}

書き込みコマンドを使用すると、基本の1つ以上のテーブルにエントリを含む、単純なドキュメントや複雑なドキュメントを書き込むことができます。

トランザクションAPIを使用すると、 **updateOrInsert**&#x200B;コマンドで紐付けを管理できます。1つのコマンドで、データを作成または更新できます。 変更の結合(**merge**)を設定することもできます。この操作モードを使用すると、部分的な更新を承認できます。

XML構造は、データの論理ビューを提供し、SQLテーブルの物理構造を回避します。

Writeメソッドについては、 [Write / WriteCollection (xtk:session)](#write---writecollection--xtk-session-)で説明しています。

## ExecuteQuery (xtk:queryDef) {#executequery--xtk-querydef-}

このメソッドを使用すると、スキーマに関連付けられたデータからクエリを実行できます。 認証文字列（ログインする必要がある）と、パラメーターとして送信するクエリを記述するXMLドキュメントを取ります。 戻りパラメーターは、クエリが参照するスキーマの形式でクエリの結果を含むXMLドキュメントです。

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
>これは「const」メソッドです。 入力パラメーターは、「xtk:queryDef」スキーマの形式のXMLドキュメントに含まれます。

### 入力クエリ{#format-of-the-xml-document-of-the-input-query}のXMLドキュメントの形式

クエリのXMLドキュメントの構造は、「xtk:queryDef」スキーマに記述します。 このドキュメントでは、SQLクエリの句について説明します。&quot;select&quot;、&quot;where&quot;、&quot;order by&quot;、&quot;group by&quot;、&quot;having&quot;

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

サブクエリ( `<subquery>` )は、 `<condition> `要素で定義できます。 の構文   `<subquery> `   要素は、    `<querydef>`.

`<subquery>  : </subquery>`の例

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

クエリは、**schema**&#x200B;属性から開始スキーマを参照する必要があります。

必要な操作のタイプは、**operation**&#x200B;属性に入力され、次の値のいずれかが含まれます。

* **get**:テーブルからレコードを取得し、データが存在しない場合はエラーを返します。
* **getIfExists**:テーブルからレコードを取得し、データが存在しない場合は空のドキュメントを返します。
* ****&#x200B;を選択します。は、複数のレコードを返すカーソルを作成し、データがない場合は空のドキュメントを返します。
* **count**:はデータ数を返します。

**XPath**&#x200B;構文は、入力スキーマに基づいてデータを検索するために使用されます。 XPathの詳細については、[データスキーマ](../../configuration/using/data-schemas.md)を参照してください。

#### 「get」操作の例{#example-with-the--get--operation}

電子メールのフィルターを使用して、受信者の姓と名（「nms:recipient」スキーマ）を取得します。

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

#### 「select」操作の例{#example-with-the--select--operation}

フォルダーおよび電子メールドメインでフィルターされた受信者のリストを返します。このリストは、生年月日の降順で並べ替えられます。

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

式には、単純なフィールドや、算術演算や文字列の連結などの複雑な式を使用できます。

返されるレコードの数を制限するには、**lineCount**&#x200B;属性を`<querydef>`要素に追加します。

クエリが返すレコードの数を100に制限するには：

```
<queryDef schema="nms:recipient" operation="select" lineCount="100">
...
```

次の100個のレコードを取得するには、**startLine**&#x200B;属性を追加して、同じクエリを再実行します。

```
<queryDef schema="nms:recipient" operation="select" lineCount="100" startLine="100">
...
```

#### 「count」操作の例{#example-with-the--count--operation}

クエリのレコード数をカウントするには：

```
<queryDef schema="nms:recipient" operation="count"">
  <!-- condition on the folder and domain of the e-mail -->
  <where>  
    <condition expr="[@folder-id] = 1234" and @domain like 'Adobe%'"/>
  </where>
</queryDef>
```

>[!NOTE]
>
>ここでも、前の例の条件を使用します。 `<select>`句と句は使用されません。`</select>`

#### データのグループ化 {#data-grouping}

複数回参照される電子メールアドレスを取得するには：

```
<queryDef schema="nms:recipient" operation="select">
  <select>
    <node expr="@email"/>
    <node expr="count(@email)"/>
  </select>

  <!-- e-mail grouping clause -->
  <groupby>
    <node expr="@email"/>
  </groupby>

  <!-- grouping condition -->
  <having>
    <condition expr="count(@email) > 1"/>
  </having>

</queryDef>
```

**groupBy**&#x200B;属性を直接グループ化するフィールドに追加すると、クエリを簡略化できます。

```
<select>
  <node expr="@email" groupBy="true"/>
</select>
```

>[!NOTE]
>
>`<groupby>`要素を設定する必要はなくなりました。

#### 条件{#bracketing-in-conditions}での括弧

同じ条件での括弧の例を2つ示します。

* 単一の式の単純なバージョン：

   ```
   <where>
     <condition expr="(@age > 15 or @age <= 45) and  (@city = 'Newton' or @city = 'Culver City') "/>
   </where>
   ```

* `<condition>`要素を含む構造化バージョン：

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

この構文は、条件で2つ以上のデータが使用される場合にクエリを簡素化します。

#### リンクの例{#examples-on-links}

* リンク1 ～ 1またはN1:テーブルに外部キー（リンクがテーブルから開始する）がある場合、リンクされたテーブルのフィールドを直接フィルターまたは取得できます。

   フォルダーラベルのフィルターの例：

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

* コレクションリンク(1N):コレクションテーブルのフィールドに対するフィルタリングは、**EXISTS**&#x200B;演算子または&#x200B;**NOT EXISTS**&#x200B;演算子を使用して実行する必要があります。

   「ニュースレター」情報サービスを購読した受信者をフィルターするには：

   ```
   <where>
     <condition expr="subscription" setOperator="EXISTS">
       <condition expr="@name = 'Newsletter'"/>
     </condition>
   </where>
   ```

   `<select>`句からコレクションリンクのフィールドを直接取得することは、クエリが基本積を返すので、お勧めしません。 リンクされたテーブルに1つのレコードのみが含まれる場合にのみ使用されます（例：`<node expr="">`）。

   「購読」コレクションリンクの例：

   ```
   <select>
     <node expr="subscription/@label"/>
   </select>
   ```

   `<select>`句内のコレクションリンクの要素を含むサブリストを取得できます。 参照されるフィールドのXPathは、コレクション要素のコンテキストを基に作成されます。

   フィルタリング( `<orderby>` )要素と制限( `<where>` )要素をコレクション要素に追加できます。

   この例では、各受信者に対して、クエリは、受信者が購読登録した電子メールと情報サービスのリストを返します。

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

#### &#39;where&#39;句と&#39;select&#39;句のパラメーターのバインド{#binding-the-parameters-of-the--where--and--select--clause}

パラメーターのバインディングによって、エンジンはクエリで使用されるパラメーターの値を設定できます。 エンジンは値のエスケープを担当し、取得するパラメーターのキャッシュにはさらに利点があるので、これは非常に便利です。

クエリが構築されると、「連結」された値が文字(? ODBCで、SQLクエリの本文に`#[index]#`（postgres...内）を入力します。

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
>クエリに「order-by」または「group-by」命令が含まれる場合、データベースエンジンは値を「バインド」できません。 @noSqlBind=&quot;true&quot;属性は、クエリの&quot;select&quot;や&quot;where&quot;命令に配置する必要があります。

#### クエリの作成に関するヒント：{#query-building-tip-}

クエリの構文を理解しやすくするために、Adobe Campaignクライアントコンソール(**[!UICONTROL ツール/汎用クエリエディター…]**&#x200B;メニュー)を参照してください。 手順は次のとおりです。

1. 取得するデータを選択します。

   ![](assets/s_ncs_integration_webservices_queyr1.png)

1. フィルター条件を定義します。

   ![](assets/s_ncs_integration_webservices_queyr2.png)

1. クエリを実行し、Ctrl + F4キーを押してクエリのソースコードを表示します。

   ![](assets/s_ncs_integration_webservices_queyr3.png)

### 出力ドキュメント形式{#output-document-format}

戻りパラメーターは、クエリに関連付けられたスキーマの形式のXMLドキュメントです。

「get」操作での「nms:recipient」スキーマからの戻り値の例：

```
<recipient email="john.doe@adobe.com" lastName"Doe" firstName="John"/>
```

「選択」操作では、返されるドキュメントは要素の列挙です。

```
<!-- the name of the first element does not matter -->
<recipient-collection>   
  <recipient email="john.doe@adobe.com" lastName"Doe" firstName="John"/>
  <recipient email="peter.martinez@adobe.com" lastName"Martinez" firstName="Peter"/>
  <recipient...
</recipient-collection>  
```

「count」型の操作に対して返されるドキュメントの例：

```
<recipient count="3"/>
```

#### エイリアス {#alias}

エイリアスを使用すると、出力ドキュメント内のデータの場所を変更できます。 **alias**&#x200B;属性は、対応するフィールドでXPathを指定する必要があります。

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

### SOAPメッセージの例{#example-of-soap-messages}

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

## 書き込み/書き込みコレクション(xtk:session) {#write---writecollection--xtk-session-}

これらのサービスは、エンティティ（「Write」メソッド）やエンティティのコレクション（「WriteCollection」メソッド）の挿入、更新、削除に使用されます。

更新されるエンティティは、データスキーマに関連付けられています。 入力パラメーターは、認証文字列（ログインする必要がある）と、更新するデータを含むXMLドキュメントです。

このドキュメントは、書き込み手順を設定する手順で補完されます。

この呼び出しは、エラーを除いてデータを返しません。

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
>これは「静的」メソッドです。 入力パラメーターは、更新するスキーマの形式でXMLドキュメントに含まれます。

### 概要 {#overview}

データの紐付けは、関連付けられたスキーマに入力されたキーの定義に基づいて動作します。 書き込みプロシージャは、入力ドキュメントに入力されたデータに基づいて、最初の適格なキーを検索します。 エンティティは、データベース内のエンティティの存在に基づいて挿入または更新されます。

更新するエンティティのスキーマのキーは、**xtkschema**&#x200B;属性に基づいて設定されます。

したがって、紐付けキーは、キーを構成するXPathのリストを含む&#x200B;**_key**&#x200B;属性（コンマ区切り）で強制的に使用できます。

**_operation**&#x200B;属性に次の値を入力することで、操作のタイプを強制できます。

* **挿入**:レコードを強制的に挿入します（紐付けキーは使用されません）。
* **insertOrUpdate**:紐付けキー（デフォルトモード）に応じて、レコードを更新または挿入します。
* **更新**:レコードを更新します。は、データが存在しない場合は何もしません。
* **削除**:レコードを削除します。
* **none**:リンクの紐付けにのみ使用され、更新や挿入は使用されません。

### &#39;Write&#39;メソッドの例{#example-with-the--write--method}

Eメールアドレス、生年月日、市区町村を使用して受信者（暗黙の「insertOrUpdate」操作）を更新または挿入する場合：

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
>削除操作の場合、入力ドキュメントには紐付けキーを構成するフィールドのみを含める必要があります。

### &#39;WriteCollection&#39;メソッドの例{#example-with-the--writecollection--method}

複数の受信者の更新または挿入：

```
<recipient-collection xtkschema="nms:recipient">    
  <recipient email="john.doe@adobe.com" firstName="John" lastName="Doe" _key="@email"/>
  <recipient email="peter.martinez@adobe.com" firstName="Peter" lastName="Martinez" _key="@email"/>
  <recipient ...
</recipient-collection>
```

### リンク{#example-on-links}の例

#### 例 1 {#example-1}

内部名(@name)に基づいたフォルダーと受信者の関連付け。

```
<recipient _key="[folder/@name], @email" email="john.doe@adobe.net" lastName="Doe" firstName="John" xtkschema="nms:recipient">
  <folder name="Folder2" _operation="none"/>
</recipient>
```

「_key」属性と「_operation」属性は、リンクされた要素に入力できます。 この要素の動作は、入力スキーマのメイン要素の動作と同じです。

メインエンティティのキーの定義(「nms:recipient」)は、リンクされたテーブル（要素`<folder>`スキーマ「xtk:folder」）のフィールドと電子メールで構成されます。

>[!NOTE]
>
>folder要素に対して入力された操作「なし」は、更新や挿入を行わずにフォルダーに対する紐付けを定義します。

#### 例 2 {#example-2}

受信者から会社（「cus:company」スキーマ内のリンクされたテーブル）を更新する場合：

```
<recipient _key="[folder/@name], @email" email="john.doe@adobe.net" lastName="Doe" firstName="John" xtkschema="nms:recipient">
  <company name="adobe" code="ERT12T" _key="@name" _operation="update"/>
</recipient>
```

#### 例 3 {#example-3}

グループ関係テーブル(「nms:rcpGrpRel」)を持つグループに受信者を追加する

```
<recipient _key="@email" email="martin.ledger@adobe.net" xtkschema="nms:recipient">
  <rcpGrpRel _key="[rcpGroup/@name]">
    <rcpGroup name="GRP1"/>
  </rcpGrpRel>
</recipient>
```

>[!NOTE]
>
>グループ名に基づく暗黙のキーは「nms:group」スキーマで定義されるので、キーの定義は`<rcpgroup>`要素に入力されません。

### XMLコレクション要素{#xml-collection-elements}

デフォルトでは、XMLコレクション要素を更新するには、すべてのコレクション要素に値を入力する必要があります。 データベースのデータは、入力ドキュメントのデータに置き換えられます。 更新する要素のみがドキュメントに含まれている場合、データベースのXMLデータとの結合を強制するには、更新するすべてのコレクション要素に「_operation」属性を設定する必要があります。

### SOAPメッセージの例{#example-of-soap-messages-1}

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

   次のエラーで返す：

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
