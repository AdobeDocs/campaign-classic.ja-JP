---
title: スキーマの構造
seo-title: スキーマの構造
description: スキーマの構造
seo-description: null
page-status-flag: never-activated
uuid: 9be70907-6154-4890-91e8-fd0fac30ab05
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: schema-reference
discoiquuid: b5c8faf7-d0ae-4d95-b7fe-6ef9674a33d2
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: dbff132e3bf88c408838f91e50e4b047947ee32a

---


# スキーマの構造{#schema-structure}

の基本構造は次の `<srcschema>` とおりです。

```
<srcSchema>
    <enumeration>
        ...          //definition of enumerations
    </enumeration>
   
    <element>         //definition of the root <element>    (mandatory)

        <compute-string/>  //definition of a compute-string
        <dbindex>
            ...        //definition of indexes
        </dbindex>
        <key>
            ...        //definition of keys
        </key>
        <sysFilter>
            ...           //definition of filters
        </sysFilter>
        <attribute>
            ...             //definition of fields
        </attribute>
    
            <element>           //definition of sub-<element> 
                  <attribute>           //(collection, links or XML)
                  ...                         //and additional fields
                  </attribute>
                ...
            </element>
      
    </element> 

        <methods>                 //definition of SOAP methods
            <method>
                ...
            </method>
            ...
    </methods>  
          
</srcSchema>
```

The XML document of a data schema must contain the **`<srcschema>`** root element with the **name** and **namespace** attributes to populate the schema name and its namespace.

```
<srcSchema name="schema_name" namespace="namespace">
...
</srcSchema>
```

次のXMLコンテンツを使用して、データスキーマの構造を説明します。

```
<recipient email="John.doe@aol.com" created="2009/03/12" gender="1"> 
  <location city="London"/>
</recipient>
```

対応するデータスキーマを使用する場合：

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient">
    <attribute name="email"/>
    <attribute name="created"/>
    <attribute name="gender"/>
    <element name="location">
      <attribute name="city"/>
   </element>
  </element>
</srcSchema>
```

## 説明 {#description}

スキーマのエントリポイントは、スキーマのメイン要素です。メイン要素はスキーマと同じ名前なので、識別は容易です。また、メイン要素はルート要素の子でなければなりません。コンテンツの記述は、この要素から始まります。

この例では、主要な要素は次の行で表されます。

```
<element name="recipient">
```

メイン要 **`<attribute>`** 素とそ **`<element>`** の後に続く要素を使用して、XML構造内のデータ項目の場所と名前を定義できます。

サンプルスキーマには、次のものがあります。

```
<attribute name="email"/>
<attribute name="created"/>
<attribute name="gender"/>
<element name="location">
  <attribute name="city"/>
</element>
```

次の規則に従う必要があります。

* および **`<element>`** は、 **`<attribute>`** name属性を使用して名前で識別する必要が **あります** 。

   >[!IMPORTANT]
   >
   >要素の名前は簡潔で、できれば英語で記述し、XML命名規則に従って許可された文字のみを含める必要があります。

* XML構造 **`<element>`** 内の要素と要素を **`<attribute>`** 含めるこ **`<element>`** とができるのは要素のみです。
* 要素 **`<attribute>`** は、内部に一意の名前を持つ必要がありま **`<element>`**&#x200B;す。
* 複数行のデータ文字列に**`<elements>`**を使用することをお勧めします。

## データタイプ {#data-types}

データ型は、要素と要素の **type属性** で入 **`<attribute>`** 力し **`<element>`** ます。

詳細なリストは、要素と要素の説明に記載さ [`<attribute>` れて](../../configuration/using/elements-and-attributes.md#attribute--element) いま [`<element>` す](../../configuration/using/elements-and-attributes.md#element--element)。

この属性に値が入力されない場合、要素に **子要素が含まれていない限り** 、stringがデフォルトのデータ型になります。 その場合は、要素を階層的に構成する(この例の要素&#x200B;**`<location>`** )ためにのみ使用されます。

スキーマでは、次のデータ型がサポートされています。

* **string**:文字列。 例：名、町名等

   サイズは、 **length** 属性（オプション、デフォルト値は「255」）で指定できます。

* **boolean**:Booleanフィールド。 使用可能な値の例：true/false、0/1、yes/noなど
* **byte**、 **short**、 **long**:整数（1バイト、2バイト、4バイト）。 例：年齢、口座番号、ポイント数等
* **double**:倍精度浮動小数点数。 例：価格、料金等
* **date**、 **datetime**:日付と日付+時間。 例：生年月日、購入年月日等
* **datetimenotz**:タイムゾーンデータを含まない日付+時間。
* **timespan**:継続時間。 例：年功。
* **メモ**:長いテキストフィールド（複数行）。 例：説明、コメントなど
* **uuid**:GUIDをサポートする「uniqueidentifier」フィールド（Microsoft SQL serverでのみサポートされます）。

   >[!NOTE]
   >
   >Microsoft SQL server以外のエ **ンジンに** uuidフィールドを含めるには、「newuuid()」関数を追加し、デフォルト値で完了する必要があります。

次に、タイプを入力したスキーマの例を示します。

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient">
    <attribute name="email" type="string" length="80"/>
    <attribute name="created" type="datetime"/>
    <attribute name="gender" type="byte"/>
    <element name="location">
      <attribute name="city" type="string" length="50"/>
   </element>
  </element>
</srcSchema>
```

### Adobe Campaign/DBMSデータのタイプのマッピング {#mapping-the-types-of-adobe-campaign-dbms-data}

次の表に、様々なデータベース管理システム用にAdobe Campaignで生成されたデータのタイプのマッピングを示します。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>Adobe Campaign</strong><br /> </td> 
   <td> <strong>PosgreSQL</strong><br /> </td> 
   <td> <strong>Oracle</strong><br /> </td> 
   <td> <strong>Teradata</strong><br /> </td> 
   <td> <strong>DB2</strong><br /> </td> 
   <td> <strong>MS SQL</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> 文字列<br /> </td> 
   <td> VARCHAR(255)<br /> </td> 
   <td> VARCHAR2 （unicodeの場合はNVARCHAR2）<br /> </td> 
   <td> VARCHAR(VARCHAR CHARACTER SET UNICODE（Unicodeの場合）<br /> </td> 
   <td> VARCHAR<br /> </td> 
   <td> VARCHAR （unicodeの場合はNVARCHAR）<br /> </td> 
  </tr> 
  <tr> 
   <td> ブール値<br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> NUMBER(3)<br /> </td> 
   <td> NUMERIC(3)<br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> TINYINT<br /> </td> 
  </tr> 
  <tr> 
   <td> Byte<br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> NUMBER(3)<br /> </td> 
   <td> NUMERIC(3)<br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> TINYINT<br /> </td> 
  </tr> 
  <tr> 
   <td> 短い<br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> NUMBER(5)<br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> SMALLINT<br /> </td> 
  </tr> 
  <tr> 
   <td> 重複<br /> </td> 
   <td> 倍精度<br /> </td> 
   <td> FLOAT<br /> </td> 
   <td> FLOAT<br /> </td> 
   <td> DOUBLE<br /> </td> 
   <td> FLOAT<br /> </td> 
  </tr> 
  <tr> 
   <td> 長い<br /> </td> 
   <td> INTEGER<br /> </td> 
   <td> NUMBER(10)<br /> </td> 
   <td> INTEGER<br /> </td> 
   <td> INTEGER<br /> </td> 
   <td> INT<br /> </td> 
  </tr> 
  <tr> 
   <td> Int64<br /> </td> 
   <td> BIGINT<br /> </td> 
   <td> NUMBER(20)<br /> </td> 
   <td> NUMERIC(20)<br /> </td> 
   <td> BIGINT<br /> </td> 
   <td> BIGINT<br /> </td> 
  </tr> 
  <tr> 
   <td> 日付<br /> </td> 
   <td> DATE<br /> </td> 
   <td> DATE<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> DATE<br /> </td> 
   <td> DATETIME<br /> </td> 
  </tr> 
  <tr> 
   <td> 時間<br /> </td> 
   <td> TIME<br /> </td> 
   <td> FLOAT<br /> </td> 
   <td> TIME<br /> </td> 
   <td> TIME<br /> </td> 
   <td> FLOAT<br /> </td> 
  </tr> 
  <tr> 
   <td> 日時<br /> </td> 
   <td> TIMESTAMPZ<br /> </td> 
   <td> DATE<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> MS SQL &lt; 2008:DATETIME<br /> MS SQL &gt;= 2012:DATETIMEOFFSET<br /> </td> 
  </tr> 
  <tr> 
   <td> Datetimenotz<br /> </td> 
   <td> TIMESTAMPZ<br /> </td> 
   <td> DATE<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> MS SQL &lt; 2008:DATETIME<br /> MS SQL &gt;= 2012:DATETIME2<br /> </td> 
  </tr> 
  <tr> 
   <td> Timespan<br /> </td> 
   <td> 倍精度<br /> </td> 
   <td> FLOAT<br /> </td> 
   <td> FLOAT<br /> </td> 
   <td> DOUBLE<br /> </td> 
   <td> FLOAT<br /> </td> 
  </tr> 
  <tr> 
   <td> メモ<br /> </td> 
   <td> TEXT<br /> </td> 
   <td> CLOB（Unicodeの場合はNCLOB）<br /> </td> 
   <td> CLOB（UNICODEの場合はCLOB文字セットUNICODE）<br /> </td> 
   <td> CLOB(6M)<br /> </td> 
   <td> TEXT（Unicodeの場合はNTEXT）<br /> </td> 
  </tr> 
  <tr> 
   <td> BLOB<br /> </td> 
   <td> BLOB<br /> </td> 
   <td> BLOB<br /> </td> 
   <td> BLOB<br /> </td> 
   <td> BLOB(4M)<br /> </td> 
   <td> IMAGE<br /> </td> 
  </tr> 
 </tbody> 
</table>

## プロパティ {#properties}

データ **`<elements>`** スキーマの **`<attributes>`** 要素と要素は、様々なプロパティを使用して強化できます。 現在の要素を説明するためにラベルを入力できます。

### ラベルと説明 {#labels-and-descriptions}

* labelプ **ロパティで** 、簡単な説明を入力できます。

   >[!NOTE]
   >
   >ラベルは、インスタンスの現在の言語に関連付けられます。

   **例**：

   ```
   <attribute name="email" type="string" length="80" label="Email"/>
   ```

   ラベルは、Adobe Campaignクライアントコンソール入力フォームから確認できます。

   ![](assets/d_ncs_integration_schema_label.png)

* **descプロパティを使用すると** 、詳細な説明を入力できます。

   この説明は、Adobe Campaignクライアントコンソールのメインウィンドウのステータスバーにある入力フォームから確認できます。

   >[!NOTE]
   >
   >説明は、インスタンスの現在の言語に関連付けられます。

   **例**：

   ```
   <attribute name="email" type="string" length="80" label="Email" desc="Email of recipient"/>
   ```

### デフォルト値 {#default-values}

defaultプロ **パティを使用すると** 、コンテンツ作成時にデフォルト値を返す式を定義できます。

値は、XPath言語に準拠した式である必要があります。 詳しくは、「XPathを使用した参照」を参 [照してください](../../configuration/using/schema-structure.md#referencing-with-xpath)。

**例**：

* 現在の日付： **default=&quot;GetDate()&quot;**
* カウンタ： **default=&quot;&#39;FRM&#39;+CounterValue(&#39;myCounter&#39;)&quot;**

   この例では、文字列を連結し、CounterValue関数を空のカウンタ名で呼び出して、デ **フォルト値を構築します** 。 返される数値は、挿入のたびに1増分されます。

   >[!NOTE]
   >
   >Adobe Campaignクライアントコンソールでは、このノードを使 **[!UICONTROL Administration>Counters]** 用してカウンターを管理します。

デフォルト値をフィールドにリンクするには、 `<default>  or  <sqldefault>   field.  </sqldefault> </default>`

`<default>` :エンティティを作成する際に、フィールドにデフォルト値を事前入力できます。 この値はデフォルトのSQL値ではありません。

`<sqldefault>` :フィールドの作成時に値を追加できます。 この値はSQL結果として表示されます。 スキーマの更新中、新しいレコードのみがこの値の影響を受けます。

### 列挙 {#enumerations}

#### 無料列挙 {#free-enumeration}

userEnumプロ **パティを使用すると** 、このフィールドに入力された値を記憶し、表示する無料の列挙を定義できます。 構文は以下のようになります。

**userEnum=&quot;列挙名&quot;**

列挙に与えられた名前は自由に選択し、他のフィールドと共有できます。

次の値は、入力フォームのコンボボックスに表示されます。

![](assets/d_ncs_integration_schema_user_enum.png)

>[!NOTE]
>
>Adobe Campaignクライアントコンソールでは、ノードを **[!UICONTROL Administration > Enumerations]** 使用して列挙を管理します。

#### 列挙の設定 {#set-enumeration}

enumプ **ロパティを使用すると** 、可能な値のリストが事前にわかっている場合に使用する固定列挙を定義できます。

enum属 **性は** 、メイン要素の外部にあるスキーマに入力された列挙クラスの定義を参照します。

列挙により、ユーザーは通常の入力フィールドに値を入力する代わりに、コンボボックスから値を選択できます。

![](assets/d_ncs_integration_schema_enum.png)

データスキーマの列挙宣言の例：

```
<enumeration name="gender" basetype="byte" default="0">    
  <value name="unknown" label="Not specified" value="0"/>    
  <value name="male" label="male" value="1"/>   
  <value name="female" label="female" value="2"/>   
</enumeration>
```

列挙は、要素を介してメイン要素の外で宣言され **`<enumeration>`** ます。

列挙プロパティは次のとおりです。

* **baseType**:値に関連付けられているデータのタイプ、
* **label**:列挙の説明、
* **name**:列挙の名前、
* **default**:列挙のデフォルト値。

列挙値は、次の属性を持つ要素 **`<value>`** で宣言されています。

* **name**:内部に保存される値の名前。
* **label**:グラフィカル・インタフェースを介して表示されるラベル。

#### ドベナム列挙 {#dbenum-enumeration}

* dbenumプ **ロパティを使用すると** 、enumプロパティと類似したプロパティを持つ列挙を定義 **できます** 。

   ただし、 **name属性には値が内部的に格納されるわけではありませんが** 、スキーマを変更せずに関連するテーブルを拡張できるコードが格納されています。

   値はノードを介して定義され **[!UICONTROL Administration>Enumerations]** ます。

   この列挙は、例えばキャンペーンの特性を指定するために使用されます。

   ![](assets/d_ncs_configuration_schema_dbenum.png)

### 例 ：{#example}

プロパティが設定されたスキーマの例を次に示します。

```
<srcSchema name="recipient" namespace="cus">
  <enumeration name="gender" basetype="byte">    
    <value name="unknown" label="Not specified" value="0"/>    
    <value name="male" label="male" value="1"/>   
    <value name="female" label="female" value="2"/>   
  </enumeration>

  <element name="recipient">
    <attribute name="email" type="string" length="80" label="Email" desc="Email of recipient"/>
    <attribute name="created" type="datetime" label="Date of creation" default="GetDate()"/>
    <attribute name="gender" type="byte" label="gender" enum="gender"/>
    <element name="location" label="Location">
      <attribute name="city" type="string" length="50" label="City" userEnum="city"/>
   </element>
  </element>
</srcSchema>
```

## コレクション {#collections}

コレクションは、同じ名前と同じ階層レベルを持つ要素のリストです。

値が **「true** 」の非連結属性を使用すると、コレクション要素を設定できます。

**例**:スキーマ内の **`<group>`** コレクション要素の定義。

```
<element name="group" unbound="true" label="List of groups">
  <attribute name="label" type="string" label="Label"/>
</element>
```

XMLコンテンツの投影を使用する場合：

```
<group label="Group1"/>
<group label="Group2"/>
```

## XPathを使用した参照 {#referencing-with-xpath}

Adobe Campaign では、XPath 言語を使用して、データスキーマに属する要素または属性を参照します。

XPath は、XML ドキュメントのツリー内にノードを配置するための構文です。

要素は名前で指定し、属性は名前の前に「@」文字を付けて指定します。

**例**：

* **@email**:電子メールを選択し、
* **location/@city**:要素の下の「市区町村」属性を選択しま **`<location>`** す
* **../@email**:現在の要素の親要素から電子メールアドレスを選択します
* **group`[1]/@label`**:最初のコレクション要素の子である「label」属性を選択&#x200B;**`<group>`**します
* **group`[@label='test1']`**:要素の子で、値「test1」を含む「label」**`<group>`**属性を選択します。

>[!NOTE]
>
>パスがサブ要素と交差すると、追加の制約が追加されます。 この場合、次の式を角括弧で囲む必要があります。
>
>* **location/@city** is not valid;お使いください **`[location/@city]`**
>* **`[@email]`** と **@emailは同等です** 。
>



また、次の算術演算など、複雑な式を定義することもできます。

* **@gender+1**:性別属性の内容に1 **を** 、
* **@email + &#39;(&#39;+@created+&#39;)&#39;**:作成日の丸括弧の間に追加された電子メールアドレスの値を取り、文字列を作成します（文字列型の場合は、定数を引用符で囲みます）。

この言語の潜在能力を高めるために、式に高レベルの関数が追加されました。

使用可能な関数のリストには、Adobe Campaignクライアントコンソールの式エディターからアクセスできます。

![](assets/d_ncs_integration_schema_function.png)

**例**：

* **GetDate()**:現在の日付を返す
* **Year(@created)**:「created」属性に含まれる日付の年を返します。
* **GetEmailDomain(@email)**:電子メールアドレスのドメインを返します。

## 計算文字列を使用した文字列の作成 {#building-a-string-via-the-compute-string}

計算文 **字列は** 、スキーマに関連付けられたテーブル内のレコードを表す文字列を構築するために使用されるXPath式です。 **計算文字列は** 、主にグラフィカルインターフェイスで使用され、選択したレコードのラベルを表示します。

計算文 **字列は** 、データスキーマ **`<compute-string>`** のメイン要素の下の要素を介して定義されます。 expr属 **性に** 、表示を計算するXPath式が含まれます。

**例**:受信者テーブルの文字列を計算します。

```
<srcSchema name="recipient" namespace="nms">  
  <element name="recipient">
    <compute-string expr="@lastName + ' ' + @firstName +' (' + @email + ')' "/>
    ...
  </element>
</srcSchema>
```

受信者の計算済み文字列の結果：Doe **John (john.doe@aol.com)**

>[!NOTE]
>
>スキーマに計算文字列が含まれていない場合、デフォルトでは、スキーマの主キーの値が計算文字列に入力されます。

