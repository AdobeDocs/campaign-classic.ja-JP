---
title: データベースマッピング
seo-title: データベースマッピング
description: データベースマッピング
seo-description: null
page-status-flag: never-activated
uuid: a51df3eb-cae6-4e8d-8386-d62defc1b610
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: schema-reference
discoiquuid: bc06c00d-f421-452e-bde0-b4ecc12c72c8
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1976'
ht-degree: 1%

---


# データベースマッピング{#database-mapping}

この例のスキーマのSQLマッピングでは、次のXMLドキュメントが提供されます。

```
<schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">
  <enumeration basetype="byte" name="gender">    
    <value label="Not specified" name="unknown" value="0"/>    
    <value label="Male" name="male" value="1"/>    
    <value label="Female" name="female" value="2"/> 
  </enumeration>  

  <element name="recipient" sqltable="CusRecipient">    
    <attribute desc="Recipient e-mail address" label="Email" length="80" name="email" sqlname="sEmail" type="string"/>    
    <attribute default="GetDate()" label="Date of creation" name="created" sqlname="tsCreated" type="datetime"/>    
    <attribute enum="gender" label="Gender" name="gender" sqlname="iGender" type="byte"/>    
    <element label="Location" name="location">      
      <attribute label="City" length="50" name="city" sqlname="sCity" type="string" userEnum="city"/>    
    </element>  
  </element>
</schema>
```

## 説明 {#description}

スキーマのルート要素は、現在は存在しません **`<srcschema>`**&#x200B;が、 **`<schema>`**.

これにより、別のタイプのドキュメントが発生します。これは、ソーススキーマから自動的に生成され、単にスキーマと呼ばれます。 このスキーマは、Adobe Campaignアプリケーションで使用されます。

SQL名は、要素名と型に基づいて自動的に決定されます。

SQLの命名規則は次のとおりです。

* 表：スキーマの名前空間と名前の連結

   この例では、 **sqltable** 属性のスキーマのメイン要素を介してテーブルの名前が入力されます。

   ```
   <element name="recipient" sqltable="CusRecipient">
   ```

* フィールド：型に従って定義されたプレフィックスが先頭に付く要素の名前(整数の場合は「i」、重複の場合は「d」、文字列の場合は「s」、日付の場合は「ts」など)。

   フィールド名は、入力された各およ **び****`<attribute>`****`<element>`**:

   ```
   <attribute desc="E-mail address of recipient" label="Email" length="80" name="email" sqlname="sEmail" type="string"/> 
   ```

>[!NOTE]
>
>SQL名は、ソース・スキーマからオーバーロードできます。 これを行うには、関連する要素に「sqltable」または「sqlname」属性を設定します。

拡張スキーマから生成されるテーブルを作成するSQLスクリプトは、次のとおりです。

```
CREATE TABLE CusRecipient(
  iGender NUMERIC(3) NOT NULL Default 0,   
  sCity VARCHAR(50),   
  sEmail VARCHAR(80),
  tsCreated TIMESTAMP Default NULL);
```

SQLフィールドの制約は次のとおりです。

* 数値フィールドと日付フィールドにnull値がない。
* 数値フィールドは0に初期化されます。

## XMLフィールド {#xml-fields}

デフォルトでは、型指定された要素 **`<attribute>`** および **`<element>`** 要素は、データスキーマテーブルのSQLフィールドにマップされます。 ただし、このフィールドをSQLではなくXMLで参照することができます。つまり、データは、すべてのXMLフィールドの値を含むテーブルのメモ型フィールド(&quot;mData&quot;)に格納されます。 これらのデータのストレージは、スキーマ構造を監視するXMLドキュメントです。

XMLでフィールドにデータを埋め込むには、値が「true」の **xml** 属性を関連する要素に追加する必要があります。

**例**:次に、XMLフィールドの使用例を2つ示します。

* 複数行コメントフィールド：

   ```
   <element name="comment" xml="true" type="memo" label="Comment"/>
   ```

* HTML形式のデータの説明：

   ```
   <element name="description" xml="true" type="html" label="Description"/>
   ```

   「html」タイプを使用すると、HTMLコンテンツをCDATAタグに格納し、Adobe Campaignクライアントインターフェイスに特別なHTML編集チェックを表示できます。

XMLフィールドを使用すると、データベースの物理構造を変更することなく、フィールドを追加できます。 もう1つの利点は、使用するリソースが少ないことです（SQLフィールドに割り当てるサイズ、テーブルあたりのフィールド数の制限など）。

主な短所は、XMLフィールドのインデックス付けやフィルタリングが不可能であることです。

## インデックス付きフィールド {#indexed-fields}

インデックスを使用すると、アプリケーションで使用するSQLクエリのパフォーマンスを最適化できます。

データスキーマのメイン要素からインデックスが宣言されます。

```
<dbindex name="name_of_index" unique="true/false">
  <keyfield xpath="xpath_of_field1"/>
  <keyfield xpath="xpath_of_field2"/>
  ...
</key>
```

インデックスは次の規則に従います。

* インデックスは、テーブル内の1つ以上のフィールドを参照できます。
* unique属性に値「true」が含まれている場合は、すべてのフィールドでインデックスを一意にする( **重複を避ける** )ことができます。
* インデックスのSQL名は、テーブルのSQL名とインデックスの名前から決定されます。

>[!NOTE]
>
>標準として、インデックスはスキーマのメイン要素から宣言された最初の要素です。

>[!NOTE]
>
>インデックスは、テーブルマッピング(標準またはFDA)中に自動的に作成されます。

**例**：

* 電子メールアドレスと市区町村にインデックスを追加する：

   ```
   <srcSchema name="recipient" namespace="cus">
     <element name="recipient">
       <dbindex name="email">
         <keyfield xpath="@email"/> 
         <keyfield xpath="location/@city"/> 
       </dbindex>
   
       <attribute name="email" type="string" length="80" label="Email" desc="E-mail address of recipient"/>
       <element name="location" label="Location">
         <attribute name="city" type="string" length="50" label="City" userEnum="city"/>
       </element>
     </element>
   </srcSchema>
   ```

* 「id」名フィールドに一意のインデックスを追加します。

   ```
   <srcSchema name="recipient" namespace="cus">
     <element name="recipient">
       <dbindex name="id" unique="true">
         <keyfield xpath="@id"/> 
       </dbindex>
   
       <dbindex name="email">
         <keyfield xpath="@email"/> 
       </dbindex>
   
       <attribute name="id" type="long" label="Identifier"/>
       <attribute name="email" type="string" length="80" label="Email" desc="E-mail address of recipient"/>
     </element>
   </srcSchema>
   ```

## キーの管理 {#management-of-keys}

テーブルには、テーブル内のレコードを識別するためのキーが少なくとも1つ必要です。

キーがデータスキーマのメイン要素から宣言されます。

```
<key name="name_of_key">
  <keyfield xpath="xpath_of_field1"/>
  <keyfield xpath="xpath_of_field2"/>
  ...
</key>
```

キーは次の規則に従います。

* キーは、テーブル内の1つ以上のフィールドを参照できます。
* キーは、値が入力されるスキーマ内で最初に存在する場合や、値が「true」の **internal** 属性が含まれている場合は、「primary」（または「priority」）と呼ばれます。
* 一意のインデックスは、各キー定義に対して暗黙的に宣言されます。 値が「true」のnoDbIndex **** 属性を追加すると、キーにインデックスが作成されるのを防ぐことができます。

>[!NOTE]
>
>標準として、キーは、インデックスが定義された後にスキーマのメイン要素から宣言された要素です。

>[!NOTE]
>
>テーブルのマッピング(標準またはFDA)中にキーが作成され、Adobe Campaignは一意のインデックスを検索します。

**例**：

* 電子メールアドレスと市区町村にキーを追加する：

   ```
   <srcSchema name="recipient" namespace="cus">
     <element name="recipient">
       <key name="email">
         <keyfield xpath="@email"/> 
         <keyfield xpath="location/@city"/> 
       </key>
   
       <attribute name="email" type="string" length="80" label="Email" desc="E-mail address of recipient"/>
       <element name="location" label="Location">
         <attribute name="city" type="string" length="50" label="City" userEnum="city"/>
       </element>
     </element>
   </srcSchema>
   ```

   生成されたスキーマ:

   ```
   <schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">  
     <element name="recipient" sqltable="CusRecipient">    
      <dbindex name="email" unique="true">      
        <keyfield xpath="@email"/>      
        <keyfield xpath="location/@city"/>    
      </dbindex>    
   
      <key name="email">      
       <keyfield xpath="@email"/>      
       <keyfield xpath="location/@city"/>    
      </key>    
   
      <attribute desc="E-mail address of recipient" label="Email" length="80" name="email" sqlname="sEmail" type="string"/>    
      <element label="Location" name="location">      
        <attribute label="City" length="50" name="city" sqlname="sCity" type="string" userEnum="city"/>    
      </element>  
     </element>
   </schema>
   ```

* 「id」名フィールドに主キーまたは内部キーを追加します。

   ```
   <srcSchema name="recipient" namespace="cus">
     <element name="recipient">
       <key name="id" internal="true">
         <keyfield xpath="@id"/> 
       </key>
   
       <key name="email" noDbIndex="true">
         <keyfield xpath="@email"/> 
       </key>
   
       <attribute name="id" type="long" label="Identifier"/>
       <attribute name="email" type="string" length="80" label="Email" desc="E-mail address of recipient"/>
     </element>
   </srcSchema>
   ```

   生成されたスキーマ:

   ```
   <schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">  
     <element name="recipient" sqltable="CusRecipient">    
       <key name="email">      
         <keyfield xpath="@email"/>    
       </key>    
   
       <dbindex name="id" unique="true">      
         <keyfield xpath="@id"/>    
       </dbindex>    
   
       <key internal="true" name="id">      
        <keyfield xpath="@id"/>    
       </key>    
   
       <attribute label="Identifier" name="id" sqlname="iRecipientId" type="long"/>    
       <attribute desc="E-mail address of recipient" label="Email" length="80" name="email" sqlname="sEmail" type="string"/>  
     </element>
   </schema>
   ```

### 自動増分キー {#auto-incremental-key}

ほとんどのAdobe Campaignテーブルの主キーは、データベースエンジンによって自動生成される32ビットの長い整数です。 キー値の計算は、データベース全体で一意の数値を生成するシーケンス( **XtkNewId** SQL関数)によって決まります。 レコードを挿入すると、キーの内容が自動的に入力されます。

増分キーの利点は、テーブル間の結合に変更不可能な技術キーを提供することです。 また、このキーは重複バイトの整数を使用するので、メモリをあまり占有しません。

ソーススキーマで、pkSequence **** 属性で使用するシーケンスの名前を指定できます。 この属性がソーススキーマに指定されていない場合、 **XtkNewId** デフォルトのシーケンスが使用されます。 nms:broadLog **とnms:trackingLog** スキーマ(NmsLogIdとMsTrackingLogIdは部分的なテーブルで最も多くのレコードが含まれるため **、各** は専用のシーケンスを使用します&#x200B;**(NmsBroadLogIdと****** NmsTrackingLogId)。

ACC 18.10では、 **XtkNewId** は追加設定なしのスキーマ内のシーケンスのデフォルト値ではなくなりました。 これで、スキーマを構築したり、専用のシーケンスを使用して既存のスキーマを拡張したりできます。

>[!IMPORTANT]
>
>新しいスキーマを作成するときや、スキーマ拡張の際には、スキーマ全体で同じプライマリキーシーケンス値（@pkSequence）を維持する必要があります。

>[!NOTE]
>
>Adobe Campaignスキーマ(**NmsTrackingLogId** など)で参照されるシーケンスは、SQL関数に関連付ける必要があります。この関数は、パラメーター内のIDの数をコンマで区切って返します。 この関数はGetNewXXXIds ******と呼ぶ必要があります。** XXXはシーケンスの名前です( **例えば、GetNewNmsTrackingLogIds****** )。 アプリケーションと共に提供される **gres-nms.sql**、 **-nms.sql** 、または **oracle-nms.sql****** ファイルをdatakit/nms/eng/sql/directoryに表示し、各データベースエンジンの「NmsMsMssqlLogIdシーケンスの作成」の例を回復します。

一意のキーを宣言するには、データスキーマのメイン要素に **autopk** 属性（値「true」）を設定します。

**例**：

ソーススキーマで増分キーを宣言しています：

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient" autopk="true">
  ...
  </element>
</srcSchema>
```

生成されたスキーマ:

```
<schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">  
  <element name="recipient" autopk="true" pkSequence="XtkNewId" sqltable="CusRecipient"> 
    <dbindex name="id" unique="true">
      <keyfield xpath="@id"/>
    </dbindex>

    <key internal="true" name="id">
      <keyfield xpath="@id"/>
    </key>

    <attribute desc="Internal primary key" label="Primary key" name="id" sqlname="iRecipientId" type="long"/>
  </element>
</schema>
```

キーとそのインデックスの定義に加えて、自動生成された主キーを含めるために、拡張スキーマに「id」という数値フィールドが追加されました。

>[!IMPORTANT]
>
>プライマリ・キーが0に設定されたレコードは、テーブルの作成時に自動的に挿入されます。 このレコードは、外部結合を避けるために使用されます。外部結合はボリュームテーブルでは有効ではありません。 デフォルトでは、すべての外部キーは値0で初期化されるので、データ項目が入力されていない場合でも結合時に結果が常に返されます。

## リンク：テーブル間の関係 {#links--relation-between-tables}

リンクは、テーブル間の関連付けを示します。

各種の連想（カーディナリティ）は、次のとおりです。

* 基数1 ～ 1:ソーステーブルの1つのオカレンスには、ターゲットテーブルの対応するオカレンスを1つ以上含めることができます。
* 基数1 ～ N:1つのソーステーブルのオカレンスには、対応する複数のターゲットテーブルのオカレンスを含めることができますが、1つのターゲットテーブルのオカレンスには、対応するソーステーブルのオカレンスを1つだけ含めることができます。
* 基数N-N:ソーステーブルの1つのオカレンスには、対応する複数のターゲットテーブルのオカレンスを含めることができます。逆の場合も同様です。

インターフェースでは、異なるタイプのリレーションをアイコンで簡単に区別できます。

キャンペーンテーブル/データベースとの結合リレーションの場合：

* ![](assets/join_with_campaign11.png) :基数1-1 例えば、受信者と現在の注文の間。 受信者は、現在の注文テーブルの1つのオカレンスに対してのみ関連付けることができます。
* ![](assets/externaljoin11.png) :基数1-1、外部結合。 例えば、受信者とその国の間に。 受信者は、テーブルの国の1つのオカレンスにのみ関連付けることができます。 国テーブルの内容は保存されません。
* ![](assets/join_with_campaign1n.png) :基数1-N例えば、受信者と購読テーブルの間などです。 受信者は、購読テーブルでの複数のオカレンスに関連付けることができます。

フェデレーテッド・データベース・アクセスを使用した加入関係の場合：

* ![](assets/join_fda_11.png) :基数1-1
* ![](assets/join_fda_1m.png) :基数1-N

For more information on FDA tables, refer to [Accessing an external database](../../platform/using/about-fda.md).

メイン要素を介してリンクされたテーブルの外部キーを含むスキーマでリンクを宣言する必要があります。

```
<element name="name_of_link" type="link" target="key_of_destination_schema">
  <join xpath-dst="xpath_of_field1_destination_table" xpath-src="xpath_of_field1_source_table"/>
  <join xpath-dst="xpath_of_field2_destination_table" xpath-src="xpath_of_field2_source_table"/>
  ...
</element>
```

リンクは次の規則に従います。

* リンクの定義は、次の属性を持つ **リンクタイプ****`<element>`** に入力されます。

   * **name**:ソーステーブルからのリンク名、
   * **ターゲット**:ターゲットスキーマの名前、
   * **label**:リンクのラベル、
   * **revLink** （オプション）:ターゲットスキーマからの逆リンクの名前（デフォルトで自動的に推定）
   * **integrity** （オプション）:ターゲットテーブルのオカレンスに対するソーステーブルの参照整合性。 有効な値は次のとおりです。

      * **define**:ソースオカレンスがターゲットオカレンスから参照されなくなった場合は、ソースオカレンスを削除できます。
      * **normal**:ソースオカレンスを削除すると、リンクのキーがターゲットオカレンス（デフォルトモード）に初期化され、この種の整合性はすべての外部キーを初期化します。
      * **own**:ソースオカレンスを削除すると、ターゲットオカレンスが削除されます。
      * **owncopy**:(削除の場合は **** )自分のものと同じか、（複製の場合は）その出現を重複するのと同じ。
      * **neutral**:は何もしません。
   * **revIntegrity** （オプション）:ターゲットスキーマの整合性（オプション、デフォルトでは「通常」）、
   * **revCardinality** （オプション）:に値「single」を指定すると、カーディナリティがタイプ1-1（デフォルトでは1-N）で入力されます。
   * **externalJoin** （オプション）:外部結合を強制する
   * **revExternalJoin** （オプション）:外側の結合を逆方向のリンクに強制的に設定する


* リンクは、ソーステーブルの1つ以上のフィールドを宛先テーブルに対して参照します。 結合( `<join>` 要素)を構成するフィールドは、デフォルトでターゲットスキーマの内部キーを使用して自動的に推定されるので、入力する必要はありません。
* 拡張スキーマ内のリンクの外部キーにインデックスが自動的に追加されます。
* リンクは2つのハーフリンクで構成されます。1つ目はソーススキーマから宣言され、2つ目はターゲットスキーマの拡張スキーマに自動的に作成されます。
* 結合は、 **externalJoin** 属性が追加され、値が「true」の場合（PostgreSQLでサポートされる）、外部結合になります。

>[!NOTE]
>
>標準として、リンクはスキーマの最後に宣言された要素です。

### Example 1 {#example-1}

1-N 「cus:会社」スキーマテーブルとの関係：

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient">
    ...
    <element label="Company" name="company" revIntegrity="define" revLabel="Contact" target="cus:company" type="link"/>
  </element>
</srcSchema>
```

生成されたスキーマ:

```
<schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">  
  <element name="recipient" sqltable="CusRecipient"> 
    <dbindex name="companyId">      
      <keyfield xpath="@company-id"/>    
    </dbindex>
    ...
    <element label="Company" name="company" revLink="recipient" target="cus:company" type="link">      
      <join xpath-dst="@id" xpath-src="@company-id"/>    
    </element>    
    <attribute advanced="true" label="Foreign key of 'Company' link (field 'id')" name="company-id" sqlname="iCompanyId" type="long"/>
  </element>
</schema>
```

リンクの定義は、結合を構成するフィールド(宛先スキーマのXPath(「@id」)でプライマリキー、スキーマのXPath(「@会社ID」)で外部キーによって補足されます。

外部キーは、次の命名規則に従って、宛先テーブルの関連するフィールドと同じ特性を使用する要素に自動的に追加されます。ターゲットスキーマの名前に続けて、関連するフィールドの名前を付けます(この例では「会社ID」)。

ターゲットの拡張スキーマ(「cus:会社」):

```
<schema mappingType="sql" name="company" namespace="cus" xtkschema="xtk:schema">  
  <element name="company" sqltable="CusCompany" autopk="true"> 
    <dbindex name="id" unique="true">     
      <keyfield xpath="@id"/>    
    </dbindex>   
    <key internal="true" name="id">      
      <keyfield xpath="@id"/>    
    </key>
    ...
    <attribute desc="Internal primary key" label="Primary key" name="id" sqlname="iCompanyId" type="long"/>
    ...
    <element belongsTo="cus:recipient" integrity="define" label="Contact" name="recipient" revLink="company" target="nms:recipient" type="link" unbound="true">      
      <join xpath-dst="@company-id" xpath-src="@id"/>    
    </element>
  </element>
</schema>
```

「cus:受信者」テーブルへの逆リンクが次のパラメータと共に追加されました。

* **name**:ソーススキーマの名前から自動的に推定される(ソーススキーマのリンク定義の「revLink」属性を使用して強制できる)
* **revLink**:逆リンク名
* **ターゲット**:リンクスキーマのキー(「cus:受信者」スキーマ)
* **unbound**:リンクは、1-N個のカーディナリティのコレクション要素として宣言されています（デフォルト）。
* **整合性**:デフォルトで「定義」(ソース・スキーマのリンク定義の「revIntegrity」属性を使用して強制できます)。

### Example 2 {#example-2}

この例では、「nms:address」スキーマテーブルへのリンクを宣言します。 結合は外部結合で、受信者の電子メールアドレスと、リンクテーブルの「@address」フィールド(「nms:address」)を明示的に入力します。

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient"> 
    ...
    <element integrity="neutral" label="Info about email" name="emailInfo" revIntegrity="neutral" revLink="recipient" target="nms:address" type="link" externalJoin="true">      
      <join xpath-dst="@address" xpath-src="@email"/>
    </element>
  </element>
</srcSchema>
```

### Example 3 {#example-3}

1-1 「cus:extension」スキーマテーブルとの関係：

```
<element integrity="own" label="Extension" name="extension" revCardinality="single" revLink="recipient" target="cus:extension" type="link"/>
```

### Example 4 {#example-4}

フォルダーへのリンク(「xtk:folder」スキーマ):

```
<element default="DefaultFolder('nmsFolder')" label="Folder" name="folder" revDesc="Recipients in the folder" revIntegrity="own" revLabel="Recipients" target="xtk:folder" type="link"/>
```

デフォルト値は、&quot;DefaultFolder(&#39;nmsFolder&#39;)&quot;関数で入力された最初の有効なパラメータタイプファイルの識別子を返します。

### Example 5 {#example-5}

この例では、 **xlink属性と(「email」)テーブルのフィールドを持つリンク(「会社」から「cus:会社」スキーマ)にキーを作成します。** xlink属性は次のように指定します。

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient">
    <key name="companyEmail"> 
      <keyfield xpath="@email"/>
      <keyfield xlink="company"/>
    </key>
    
    <attribute name="email" type="string" length="80" label="Email" desc="Recipient email"/>
    <element label="Company" name="company" revIntegrity="define" revLabel="Contact" target="cus:company" type="link"/>
  </element>
</srcSchema>
```

生成されたスキーマ:

```
<schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">  
  <element name="recipient" sqltable="CusRecipient"> 
    <dbindex name="companyId">      
      <keyfield xpath="@company-id"/>    
    </dbindex>

    <dbindex name="companyEmail" unique="true">
      <keyfield xpath="@email"/>      
      <keyfield xpath="@company-id"/>    
    </dbindex>    

    <key name="companyEmail">      
      <keyfield xpath="@email"/>      
      <keyfield xpath="@company-id"/>    
    </key>

    <attribute desc="E-mail address of recipient" label="Email" length="80" name="email" sqlname="sEmail" type="string"/>
    <element label="Company" name="company" revLink="recipient" target="sfa:company" type="link">      
      <join xpath-dst="@id" xpath-src="@company-id"/>    
    </element>    
    <attribute advanced="true" label="Foreign key of link 'Company' (field 'id')" name="company-id" sqlname="iCompanyId" type="long"/>
  </element>
</schema>
```

「companyEmail」名前キーの定義が、「会社」リンクの外部キーで拡張されました。 このキーは、両方のフィールドで一意のインデックスを生成します。
