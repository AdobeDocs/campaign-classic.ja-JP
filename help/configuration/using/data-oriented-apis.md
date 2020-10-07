---
title: データ指向 API
seo-title: データ指向 API
description: データ指向 API
seo-description: null
page-status-flag: never-activated
uuid: f81356b3-8eef-4b65-9510-47c9d4b4e871
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: api
discoiquuid: fba46d42-0253-425b-bbc2-6702d4140e05
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 1%

---


# データ指向 API{#data-oriented-apis}

データ指向APIを使用すると、データモデル全体に対応できます。

## データモデルの概要 {#overview-of-the-datamodel}

Adobe Campaignは、エンティティごとの専用の読み取りAPIをオファーしません（getRecipient関数やgetDelivery関数は使用しません）。 モデルのデータにアクセスするには、クエリおよびライターのデータ読み取りおよび修正方法を使用します。

Adobe Campaignを使用すると、コレクションを管理できます。クエリを使用すると、基本的に収集された一連の情報を復元できます。 SQLモードでのアクセスとは異なり、Adobe CampaignAPIはデータ列ではなくXMLツリーを返します。 Adobe Campaignは、収集されたすべてのデータを含む複合ドキュメントを作成します。

このオペレーティングモードでは、XMLドキュメントの属性と要素、およびデータベース内のテーブルの列の間の1対1のマッピングはオファーされません。

XMLドキュメントは、データベースのMEMO型のフィールドに格納されます。

## モデルの説明 {#description-of-the-model}

スクリプト内のAdobe Campaignのフィールドに対処するには、データベースデータモデルに精通している必要があります。

データモデルの表示については、 [Adobe Campaignデータモデルの説明を参照してください](../../configuration/using/data-model-description.md)。

構造を生成するには、次の記事を参照してください。 [データモデルまたはデータディクショナリの生成方法](https://helpx.adobe.com/campaign/kb/generate-data-model.html)。

## クエリ・ライター {#query-and-writer}

以下の紹介スキーマは、データベースとお客様(WebページまたはAdobe Campaignクライアントコンソール)の間で読み取り(ExecuteQuery)と書き込み(Writer)の低レベルのやり取りについて詳しく説明しています。

![](assets/s_ncs_integration_webservices_schema_writer.png)

### ExecuteQuery {#executequery}

列と条件の場合は、クエリを使用できます。

これにより、基になるSQLを分離できます。 クエリ言語は、基になるエンジンに依存しません。一部の関数は再マッピングされ、SELECT SQLの注文がいくつか生成される場合があります。

この詳細については、スキーマ&#39;xtk:queryDef&#39;の&#39;ExecuteQuery&#39;メソッドの [例を参照してください](../../configuration/using/web-service-calls.md#example-on-the--executequery--method-of-schema--xtk-querydef-)。

ExecuteQuery **メソッドは、ExecuteQuery (xtk:queryDef)**[](#executequery--xtk-querydef-).

### 書き込む {#write}

書き込みコマンドを使用すると、基本の1つ以上のテーブル内のエントリを含む単純なドキュメントや複雑なエントリを作成できます。

トランザクションAPIを使用すると、 **updateOrInsert** コマンドを使用して調整を管理できます。1つのコマンドで、データの作成や更新を行うことができます。 変更結合(**結合**)を設定することもできます。このオペレーティングモードを使用すると、部分的な更新を承認できます。

XML構造は、データの論理表示をオファーし、SQLテーブルの物理構造を回避できます。

Writeメソッドは、 [Write / WriteCollection (xtk:session)で示され](#write---writecollection--xtk-session-)ます。

## ExecuteQuery (xtk:queryDef) {#executequery--xtk-querydef-}

このメソッドを使用すると、スキーマに関連付けられたデータからクエリを実行できます。 認証文字列（ログインする必要がある）と、クエリーをパラメーターとして送信することを説明するXMLドキュメントを取ります。 returnパラメーターは、クエリが参照するスキーマーの形式でクエリの結果を含むXMLドキュメントです。

「xtk:queryDef」スキーマ内の「ExecuteQuery」メソッドの定義：

```
<method name="ExecuteQuery" const="true">
  <parameters>
    <param desc="Output XML document" name="output" type="DOMDocument" inout="out"/>
  </parameters>
</method>
```

>[!NOTE]
>
>これは「const」メソッドです。 入力パラメーターは、&quot;xtk:queryDef&quot;スキーマの形式のXMLドキュメントに含まれます。

### 入力クエリーのXMLドキュメントの形式 {#format-of-the-xml-document-of-the-input-query}

クエリのXMLドキュメントの構造は、&quot;xtk:queryDef &quot;スキーマに記述されています。 このドキュメントでは、SQLクエリの句を説明します。&quot;select&quot;、&quot;where&quot;、&quot;order by&quot;、&quot;group by&quot;、&quot;having&quot;

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

副クエリ( `<subquery>` )は、 `<condition> ` 要素内で定義できます。 要素の構文は、 `<subquery> ` の構文に基づき `<querydef>`ます。

Example of a `<subquery>  : </subquery>`

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

クエリは、 **スキーマ属性から開始スキーマを参照する必要があります** 。

目的の操作のタイプは、 **操作** 属性に入力され、次の値のいずれかが含まれます。

* **get**:テーブルからレコードを取得し、データが存在しない場合はエラーを返します。
* **getIfExists**:テーブルからレコードを取得し、データが存在しない場合は空のドキュメントを返します。
* **選択**:複数のレコードを返すカーソルを作成し、データがない場合は空のドキュメントを返します。
* **count**:データカウントを返します。

XPath **** 構文は、入力スキーマに基づいてデータを検索するために使用されます。 XPathの詳細については、「 [データスキーマ](../../configuration/using/data-schemas.md)」を参照してください。

#### 「get」操作の例 {#example-with-the--get--operation}

電子メールのフィルタを含む受信者(「nms:受信者」スキーマ)の姓と名を取得します。

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

フォルダおよび電子メールドメインでフィルタされた受信者のリストを、生年月日の降順で返します。

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

返すレコード数を制限するには、 **lineCount** 属性を `<querydef>` 要素に追加します。

クエリが返すレコード数を100件に制限するには：

```
<queryDef schema="nms:recipient" operation="select" lineCount="100">
...
```

次の100件のレコードを取得するには、 **startLine** 属性を追加して、同じクエリを再び実行します。

```
<queryDef schema="nms:recipient" operation="select" lineCount="100" startLine="100">
...
```

#### 「count」操作の例 {#example-with-the--count--operation}

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
>前述の例の条件を使用します。 AND句 `<select>` は使用されません。 </select>`

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

クエリは、 **groupBy** 属性を直接フィールドに追加してグループ化すると簡単にできます。

```
<select>
  <node expr="@email" groupBy="true"/>
</select>
```

>[!NOTE]
>
>要素を設定する必要はなくなり `<groupby>` ました。

#### 条件でのかっこ付け {#bracketing-in-conditions}

同じ条件でのかっこ付けの例を2つ示します。

* 単一の式での単純なバージョン：

   ```
   <where>
     <condition expr="(@age > 15 or @age <= 45) and  (@city = 'Newton' or @city = 'Culver City') "/>
   </where>
   ```

* 要素を含む構造化バージョン `<condition>` :

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

同じフィールドに複数の条件が適用される場合、「OR」演算子を「IN」演算に置き換えることができます。

```
<where>
  <condition>
    <condition expr="@age IN (15, 45)"/>
    <condition expr="@city IN ('Newton', 'Culver City')"/>
  </condition>
</where>
```

この構文を使用すると、条件に2つ以上のデータを使用する場合のクエリが簡単になります。

#### リンクの例 {#examples-on-links}

* リンク1 ～ 1またはN1:テーブルに外部キー(テーブルからのリンク開始)がある場合、リンクテーブルのフィールドを直接フィルタまたは取得できます。

   フォルダーラベルのフィルターの例：

   ```
   <where>
     <condition expr="[folder/@label] like 'Segment%'"/>
   </where>
   ```

   「nms:folder」スキーマから受信者ーのフィールドを取得するには：

   ```
   <select>
     <!-- label of recipient folder -->
     <node expr="[folder/@label]"/>
     <!-- displays the string count of the folder -->
     <node expr="partition"/>
   </select>
   ```

* コレクションリンク(1N):コレクションテーブルのフィールドに対するフィルタリングは、 **EXISTS** 演算子または **NOT EXISTS** 演算子を使用して実行する必要があります。

   「ニュースレター」情報サービスを購読している受信者をフィルターするには：

   ```
   <where>
     <condition expr="subscription" setOperator="EXISTS">
       <condition expr="@name = 'Newsletter'"/>
     </condition>
   </where>
   ```

   クエリが基本積を返すので、 `<select>` 句からコレクションリンクのフィールドを直接取得することはお勧めしません。 この変数は、リンクテーブルにレコードが1つだけ含まれている場合(例 `<node expr="">`)にのみ使用されます。

   「購読」コレクションリンクの例：

   ```
   <select>
     <node expr="subscription/@label"/>
   </select>
   ```

   句内のコレクションリンクのリストを含むサブ要素を取得でき `<select>` ます。 参照先のフィールドのXPathは、コレクション要素からコンテキストを持ちます。

   フィルタリング( `<orderby>` )要素と制限( `<where>` )要素をコレクション要素に追加できます。

   この例では、クエリは受信者ごとに、受信者がサブスクライブする情報サービスの電子メールとリストを返します。

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

#### &#39;where&#39;句と&#39;select&#39;句のパラメーターのバインド {#binding-the-parameters-of-the--where--and--select--clause}

パラメーターのバインディングを使用すると、クエリで使用されるパラメーターの値を設定できます。 エンジンは値のエスケープ処理を行い、パラメータを取得するためのキャッシュの利点が増えるので、これは非常に役立ちます。

クエリを構築すると、「連結された」値は文字(? ODBCでは、SQLクエリ `#[index]#` の本文のpostgres...)。

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
>クエリに「order-by」または「group-by」命令が含まれる場合、データベースエンジンは値を「バインド」できません。 @noSqlBind=&quot;true&quot;属性は、クエリの「select」命令や「where」命令に配置する必要があります。

#### クエリ構築のヒント： {#query-building-tip-}

クエリの構文を理解するために、クエリクライアントコンソール([ **[!UICONTROL ツール/汎用クエリエディター...]** ]メニュー)の汎用クエリエディターを使用してAdobe Campaignを書くことができます。 手順は次のとおりです。

1. 取得するデータを選択します。

   ![](assets/s_ncs_integration_webservices_queyr1.png)

1. フィルター条件を定義します。

   ![](assets/s_ncs_integration_webservices_queyr2.png)

1. クエリを実行し、Ctrl + F4キーを押して、クエリソースコードを表示します。

   ![](assets/s_ncs_integration_webservices_queyr3.png)

### 出力ドキュメントの形式 {#output-document-format}

returnパラメーターは、クエリに関連付けられたスキーマの形式のXMLドキュメントです。

「get」操作での「nms:受信者」スキーマからの戻り値の例：

```
<recipient email="john.doe@adobe.com" lastName"Doe" firstName="John"/>
```

「select」操作では、返されるドキュメントは要素の定義済みリストです。

```
<!-- the name of the first element does not matter -->
<recipient-collection>   
  <recipient email="john.doe@adobe.com" lastName"Doe" firstName="John"/>
  <recipient email="peter.martinez@adobe.com" lastName"Martinez" firstName="Peter"/>
  <recipient...
</recipient-collection>  
```

「count」型の演算に対して返されるドキュメントの例：

```
<recipient count="3"/>
```

#### エイリアス {#alias}

エイリアスを使用すると、出力ドキュメントー内のデータの場所を変更できます。 **** alias属性では、対応するフィールドにXPathを指定する必要があります。

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

代わりに：

```
<recipient firstName="John" lastName="Doe">
  <folder label="Recipients"/>
</recipient>
```

### SOAPメッセージの例 {#example-of-soap-messages}

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

これらのサービスは、エンティティ（「Write」メソッド）またはエンティティのコレクション（「WriteCollection」メソッド）の挿入、更新、または削除に使用されます。

更新されるエンティティは、データスキーマに関連付けられます。 入力パラメーターは、認証文字列（ログインする必要がある）と、更新するデータを含むXMLドキュメントです。

このドキュメントは、書き込み手順を構成する手順によって補われます。

この呼び出しは、エラー以外のデータを返しません。

「xtk:session」スキーマ内の「Write」メソッドと「WriteCollection」メソッドの定義：

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
>これは「静的」なメソッドです。 入力パラメーターは、更新するスキーマの形式でXMLドキュメントに含まれます。

### 概要 {#overview}

データの調整は、関連付けられたスキーマに入力されたキーの定義に基づいて動作します。 書き込みプロシージャは、入力ドキュメントに入力されたデータに基づいて、最初の有効なキーを探します。 エンティティは、データベース内の存在に基づいて挿入または更新されます。

更新するエンティティのスキーマのキーは、 **xtkschema** 属性に基づいて完了します。

したがって、キーを構成するXPathsのリストを含む **_key** 属性（コンマ区切り）を使用して、紐付けキーを強制できます。

次の値を **_operation** 属性に入力することで、操作のタイプを強制的に指定できます。

* **insert**:レコードを強制的に挿入します(紐付けキーは使用されません)。
* **insertOrUpdate**:紐付けキー（デフォルトモード）、
* **update**:レコードを更新します。は、データが存在しない場合は何もしません。
* **delete**:レコードを削除します。
* **none**:リンクの調整にのみ使用され、更新や挿入は使用されません。

### &#39;Write&#39;メソッドの使用例 {#example-with-the--write--method}

受信者（暗黙的な「insertOrUpdate」操作）を電子メールアドレス、生年月日、生まれた日付、および町村で更新または挿入するには：

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
>削除を行う場合は、入力ドキュメントにその紐付けキーを構成するフィールドのみを含める必要があります。

### &#39;WriteCollection&#39;メソッドの使用例 {#example-with-the--writecollection--method}

複数の受信者の更新または挿入：

```
<recipient-collection xtkschema="nms:recipient">    
  <recipient email="john.doe@adobe.com" firstName="John" lastName="Doe" _key="@email"/>
  <recipient email="peter.martinez@adobe.com" firstName="Peter" lastName="Martinez" _key="@email"/>
  <recipient ...
</recipient-collection>
```

### リンクの例 {#example-on-links}

#### Example 1 {#example-1}

内部名(@name)に基づいて受信者ーとフォルダーを関連付けます。

```
<recipient _key="[folder/@name], @email" email="john.doe@adobe.net" lastName="Doe" firstName="John" xtkschema="nms:recipient">
  <folder name="Folder2" _operation="none"/>
</recipient>
```

「_key」属性と「_operation」属性は、リンクされた要素に入力できます。 このスキーマの動作は、入力要素のメイン要素の動作と同じです。

メインエンティティのキーの定義(「nms:folder」)は、リンクテーブルのフィールド(要素 `<folder>` スキーマ「xtk:folder」)と電子メールで構成されます。

>[!NOTE]
>
>フォルダー要素に入力された操作「なし」は、更新や挿入を行わずに、フォルダーに関する調整を定義します。

#### Example 2 {#example-2}

受信者から会社(「cus:会社」スキーマ内のリンクテーブル)を更新：

```
<recipient _key="[folder/@name], @email" email="john.doe@adobe.net" lastName="Doe" firstName="John" xtkschema="nms:recipient">
  <company name="adobe" code="ERT12T" _key="@name" _operation="update"/>
</recipient>
```

#### Example 3 {#example-3}

グループリレーションテーブル(&quot;nms:rcpGrpRel&quot;)を持つグループに受信者を追加する：

```
<recipient _key="@email" email="martin.ledger@adobe.net" xtkschema="nms:recipient">
  <rcpGrpRel _key="[rcpGroup/@name]">
    <rcpGroup name="GRP1"/>
  </rcpGrpRel>
</recipient>
```

>[!NOTE]
>
>グループ名に基づく暗黙的なキーが「nms:group」スキーマで定義されているので、キーの定義は `<rcpgroup>` 要素に入力されません。

### XMLコレクション要素 {#xml-collection-elements}

デフォルトでは、XMLコレクション要素を更新するには、すべてのコレクション要素を設定する必要があります。 データベースのデータは、入力ドキュメントーのデータに置き換えられます。 ドキュメントに更新する要素のみが含まれている場合は、データベースのXMLデータとの結合を強制するために、更新するすべてのコレクション要素に「_operation」属性を設定する必要があります。

### SOAPメッセージの例 {#example-of-soap-messages-1}

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

   エラーを返す：

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

