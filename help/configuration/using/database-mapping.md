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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: dbff132e3bf88c408838f91e50e4b047947ee32a

---


# データベースマッピング{#database-mapping}

サンプルスキーマのSQLマッピングは次のXMLドキュメントを提供します。

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

スキーマのルート要素は、現在は存在しま **`<srcschema>`**&#x200B;せんが、 **`<schema>`**。

これにより、別のタイプのドキュメントが生成され、ソーススキーマから自動的に生成され、単にスキーマと呼ばれます。 このスキーマは、Adobe Campaignアプリケーションで使用されます。

SQL名は、要素名とタイプに基づいて自動的に決定されます。

SQLの命名規則は次のとおりです。

* 表：スキーマの名前空間と名前の連結

   この例では、テーブルの名前は、 **sqltable属性のスキーマのメイン要素を介して入力さ** れます。

   ```
   <element name="recipient" sqltable="CusRecipient">
   ```

* フィールド：先頭に接頭辞が付く要素の名前（整数の場合は&#39;i&#39;、倍精度の場合は&#39;d&#39;、文字列の場合は&#39;s&#39;、日付の場合は&#39;ts&#39;など）。

   フィールド名は、入力された各フ **ィールドのsqlname** 属性を使用して入力 **`<attribute>`** します **`<element>`**。

   ```
   <attribute desc="E-mail address of recipient" label="Email" length="80" name="email" sqlname="sEmail" type="string"/> 
   ```

>[!NOTE]
>
>SQL名は、ソース・スキーマからオーバーロードできます。 これを行うには、関連する要素に「sqltable」または「sqlname」属性を設定します。

拡張スキーマから生成されたテーブルを作成するSQLスクリプトは次のとおりです。

```
CREATE TABLE CusRecipient(
  iGender NUMERIC(3) NOT NULL Default 0,   
  sCity VARCHAR(50),   
  sEmail VARCHAR(80),
  tsCreated TIMESTAMP Default NULL);
```

SQLフィールドの制約は次のとおりです。

* 数値フィールドと日付フィールドにnull値がない場合、
* 数値フィールドは0に初期化されます。

## XMLフィールド {#xml-fields}

デフォルトでは、型指定された **`<attribute>`** 要素は **`<element>`** すべて、データスキーマテーブルのSQLフィールドにマップされます。 ただし、SQLではなくXMLでこのフィールドを参照できます。つまり、データは、すべてのXMLフィールドの値を含むテーブルのメモ型フィールド(「mData」)に格納されます。 これらのデータの保存は、スキーマ構造を監視するXMLドキュメントです。

XMLでフィールドにデータを入力するには、 **xml** 属性に値「true」を指定して、関連する要素に追加する必要があります。

**例**:xmlフィールドの使用例を2つ示します。

* 複数行コメントフィールド：

   ```
   <element name="comment" xml="true" type="memo" label="Comment"/>
   ```

* HTML形式のデータの説明：

   ```
   <element name="description" xml="true" type="html" label="Description"/>
   ```

   「html」タイプを使用すると、HTMLコンテンツをCDATAタグに格納し、Adobe Campaignクライアントインターフェイスに特別なHTML編集チェックを表示できます。

XMLフィールドを使用すると、データベースの物理構造を変更する必要なく、フィールドを追加できます。 もう1つの利点は、使用するリソースが少ないことです（SQLフィールドに割り当てるサイズ、テーブルあたりのフィールド数の制限など）。

主な欠点は、XMLフィールドのインデックス作成やフィルタリングが不可能であることです。

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
* unique属性に値「true」が含まれている場合、インデックスはすべてのフィールドで一意にす **る** （重複を避ける）ことができます。
* インデックスのSQL名は、テーブルのSQL名とインデックスの名前から決定されます。

>[!NOTE]
>
>標準として、インデックスはスキーマのメイン要素から宣言された最初の要素です。

>[!NOTE]
>
>インデックスは、テーブルマッピング（標準またはFDA）中に自動的に作成されます。

**例**：

* 電子メールアドレスと市区町村にインデックスを追加します。

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

* 「id」名前フィールドに一意のインデックスを追加します。

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

キーは、データスキーマのメイン要素から宣言されます。

```
<key name="name_of_key">
  <keyfield xpath="xpath_of_field1"/>
  <keyfield xpath="xpath_of_field2"/>
  ...
</key>
```

キーは次の規則に従います。

* キーは、テーブル内の1つ以上のフィールドを参照できます。
* キーがスキーマ内で最初に入力される場合、または値が「 **true** 」の内部属性が含まれる場合、キーは「primary」（または「priority」）と呼ばれます。
* 一意のインデックスは、各キー定義に対して暗黙的に宣言されます。 値が「true」のnoDbIndex属性を追加すると、キーに対するインデッ **クスの作成を防ぐことができます** 。

>[!NOTE]
>
>標準として、キーは、インデックスの定義後にスキーマのメイン要素から宣言された要素です。

>[!NOTE]
>
>テーブルのマッピング（標準またはFDA）中にキーが作成され、Adobe Campaignは一意のインデックスを検索します。

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

   生成されたスキーマ：

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

* 「id」名前フィールドに主キーまたは内部キーを追加します。

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

   生成されたスキーマ：

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

ほとんどのAdobe Campaignテーブルの主キーは、データベースエンジンによって自動生成される32ビット長整数です。 キー値の計算は、データベース全体で一意の番号を生成するシーケンス(デフォルトでは **XtkNewId** SQL関数)に依存します。 レコードの挿入時に、キーの内容が自動的に入力されます。

インクリメンタルキーの利点は、テーブル間の結合に変更不可能なテクニカルキーを提供することです。 また、このキーは全角整数を使用するので、メモリをあまり使用しません。

ソーススキーマで、pkSequence属性で使用するシーケンスの名前を指定で **きます** 。 この属性がソーススキーマで指定されていない場合は、 **XtkNewId** デフォルトのシーケンスが使用されます。 アプリケーションは、 **nms:broadLog** およびnms:trackingSchemas( **NmsBroadLogIdとMsBroadLogId LogLogLog** )に対してシーケンスを使用します。これは、最も多くのレコードを含む専用のテーブル&#x200B;******** であるからです。

ACC 18.10からは、 **XtkNewIdは** 、あらかじめ用意されているスキーマのシーケンスのデフォルト値ではなくなりました。 これで、スキーマを作成したり、専用のシーケンスを使用して既存のスキーマを拡張したりできるようになりました。

>[!IMPORTANT]
>
>新しいスキーマを作成するときや、スキーマ拡張の際には、スキーマ全体で同じプライマリキーシーケンス値（@pkSequence）を維持する必要があります。

>[!NOTE]
>
>Adobe Campaignスキーマ(**NmsTrackingLogIdなど** )で参照されるシーケンスは、SQL関数に関連付ける必要があります。この関数は、パラメーター内のIDの数をコンマで区切って返します。 この関数はGetNewXXXIdsと呼ばれ ******る必要があります**。 **XXXはシーケンスの名前です(** 例：**GetNewNmsTrackingLogIds** )。 各データベースエンジンの **** NmsLogIdシーケンス作成例をリカバリするには、 **datakit/ms/eng/sql/posttrackingディレクトリ内の、アプリケーションと共に提供されるgres-nms.sql** 、 ******** oracle-nms.sql、またはoracle-nms.sqlを表示します。

一意のキーを宣言するには、 **autopk** 属性（値「true」）をデータスキーマのメイン要素に設定します。

**例**：

ソーススキーマでインクリメンタルキーを宣言する：

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient" autopk="true">
  ...
  </element>
</srcSchema>
```

生成されたスキーマ：

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

キーとそのインデックスの定義に加えて、自動生成された主キーを含めるために、拡張スキーマに「id」と呼ばれる数値フィールドが追加されました。

>[!IMPORTANT]
>
>主キーが0に設定されたレコードは、テーブルの作成時に自動的に挿入されます。 このレコードは、ボリュームテーブルで有効でない外部結合を避けるために使用されます。 デフォルトでは、すべての外部キーは値0で初期化され、データ項目が入力されていない場合に結果を常に結合時に返すことができます。

## リンク：表間の関係 {#links--relation-between-tables}

リンクは、テーブル間の関連付けを示します。

様々な種類の関連付け（「カーディナリティ」と呼ばれる）は、次のとおりです。

* 基数1 ～ 1:ソース・テーブルの1つのオカレンスは、ターゲット・テーブルの対応するオカレンスを最大1つ持つことができます。
* 基数1 ～ N:1つのソース・テーブルのオカレンスは、ターゲット・テーブルの対応するオカレンスを複数持つことができますが、1つのオカレンスは、ソース・テーブルの対応するオカレンスを最大1つ持つことができます。
* 基数N-N:1つのソーステーブルに対応する複数のオカレンスを含めることも、逆の場合もあります。

インターフェイスでは、異なるタイプのリレーションをアイコンで簡単に区別できます。

キャンペーンテーブル/データベースとの結合リレーションの場合：

* ![](assets/join_with_campaign11.png) :基数1 ～ 1。 例えば、受信者と現在の注文の間などです。 受信者は、現在の注文テーブルの1つのオカレンスに一度に1つだけ関連付けることができます。
* ![](assets/externaljoin11.png) :基数1-1、外部結合。 例えば、受信者と国の間で発生します。 受信者は、テーブルの国の1つのオカレンスにのみ関連付けることができます。 国テーブルの内容は保存されません。
* ![](assets/join_with_campaign1n.png) :基数1 ～ N。例えば、受信者と購読テーブルの間などです。 受信者は、購読テーブルでの複数のオカレンスに関連付けることができます。

フェデレーテッドデータベースアクセスを使用した加入関係の場合：

* ![](assets/join_fda_11.png) :基数1-1
* ![](assets/join_fda_1m.png) :基数1-N

For more information on FDA tables, refer to [Accessing an external database](../../platform/using/about-fda.md).

リンクは、メイン要素を介してリンクされたテーブルの外部キーを含むスキーマで宣言する必要があります。

```
<element name="name_of_link" type="link" target="key_of_destination_schema">
  <join xpath-dst="xpath_of_field1_destination_table" xpath-src="xpath_of_field1_source_table"/>
  <join xpath-dst="xpath_of_field2_destination_table" xpath-src="xpath_of_field2_source_table"/>
  ...
</element>
```

リンクは次の規則に従います。

* リンクの定義は、次の属性を持つリ **ンク**・タイプ **`<element>`** に入力されます。

   * **name**:ソーステーブルからのリンクの名前、
   * **target**:ターゲットスキーマ名、
   * **label**:リンクのラベル、
   * **revLink** （オプション）:ターゲット・スキーマからの逆リンクの名前（デフォルトで自動的に推測される）
   * **整合性** （オプション）:ターゲット・テーブルのオカレンスに対するソース・テーブルのオカレンスの参照整合性。 使用可能な値は次のとおりです。

      * **define**:ソースオカレンスがターゲットオカレンスで参照されなくなった場合は、そのソースオカレンスを削除できます。
      * **normal**:ソースオカレンスを削除すると、ターゲットオカレンスへのリンクのキーが初期化され（デフォルトモード）、この種類の整合性はすべての外部キーを初期化します。
      * **own**:ソースオカレンスを削除すると、ターゲットオカレンスが削除されます。
      * **owncopy**:(削除の場合 **は** )自身と同じか、重複の場合は重複する。
      * **中立**:は何もしません。
   * **revIntegrity** （オプション）:ターゲット・スキーマの整合性（オプション、デフォルトでは「通常」）、
   * **revCardinality** （オプション）:値が「single」の場合、カーディナリティはタイプ1-1（デフォルトで1-N）で入力されます。
   * **externalJoin** （オプション）:外部結合を強制する
   * **revExternalJoin** （オプション）:外部結合をリバースリンクに強制的に設定する


* リンクは、ソーステーブルから宛先テーブルに1つ以上のフィールドを参照します。 結合（要素）を構成するフィールドは、デ `<join>` フォルトでターゲットスキーマの内部キーを使用して自動的に推測されるので、入力する必要はありません。
* 拡張スキーマ内のリンクの外部キーにインデックスが自動的に追加されます。
* リンクは2つのハーフリンクで構成され、最初のリンクはソーススキーマから宣言され、2番目のリンクはターゲットスキーマの拡張スキーマに自動的に作成されます。
* externalJoin属性が追加され、値が&quot;true **** &quot;の場合（PostgreSQLでサポートされる）、結合は外部結合になります。

>[!NOTE]
>
>標準として、リンクはスキーマの末尾で宣言された要素です。

### Example 1 {#example-1}

1-N 「cus:company」スキーマテーブルとの関係：

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient">
    ...
    <element label="Company" name="company" revIntegrity="define" revLabel="Contact" target="cus:company" type="link"/>
  </element>
</srcSchema>
```

生成されたスキーマ：

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

リンクの定義は、結合を構成するフィールド(つまり、宛先スキーマのXPath(「@id」)でプライマリキーを構成し、スキーマのXPath(「@company-id」)で外部キーを構成する)で補足されます。

外部キーは、次の命名規則に従って、宛先テーブルの関連フィールドと同じ特性を使用する要素に自動的に追加されます。ターゲットスキーマの名前の後に、関連するフィールドの名前（この例では「company-id」）が続きます。

ターゲットの拡張スキーマ(「cus:company」):

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

「cus:recipient」テーブルへの逆リンクが次のパラメーターと共に追加されました。

* **name**:ソース・スキーマの名前から自動的に推定される（ソース・スキーマのリンク定義の「revLink」属性で強制可能）
* **revLink**:逆リンク名
* **target**:リンクされたスキーマのキー（「cus:recipient」スキーマ）
* **連結なし**:リンクは1-N基数のコレクション要素として宣言されます（デフォルト）。
* **整合性**:デフォルトで「define」（ソース・スキーマ上のリンク定義の「revIntegrity」属性を使用して強制可能）

### Example 2 {#example-2}

この例では、「nms:address」スキーマテーブルへのリンクを宣言します。 結合は外部結合で、受信者の電子メールアドレスと、リンクテーブル(「nms:address」)の「@address」フィールドに明示的に入力されます。

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

フォルダへのリンク（「xtk:folder」スキーマ）:

```
<element default="DefaultFolder('nmsFolder')" label="Folder" name="folder" revDesc="Recipients in the folder" revIntegrity="own" revLabel="Recipients" target="xtk:folder" type="link"/>
```

デフォルト値は、「DefaultFolder(&#39;nmsFolder&#39;)」関数に入力された最初の有効なパラメータータイプファイルの識別子を返します。

### Example 5 {#example-5}

この例では、 **** xlink属性と(「email」)テーブルのフィールドを使用して、リンク（「company」から「cus:company」スキーマ）にキーを作成します。

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

生成されたスキーマ：

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

「companyEmail」ネームキーの定義が、「company」リンクの外部キーで拡張されました。 このキーは、両方のフィールドで一意のインデックスを生成します。
