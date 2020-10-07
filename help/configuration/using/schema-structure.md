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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 12%

---


# スキーマの構造{#schema-structure}

の基本的な構造 `<srcschema>` は次のとおりです。

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

データスキーマの XML ドキュメントには、**name** 属性と **namespace** 属性が設定された **`<srcschema>`** ルート要素が必要です。これにより、スキーマの名前と名前空間が指定されます。

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

対応するデータスキーマを使用して、次の操作を行います。

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

メイン要素 **`<attribute>`** とその後 **`<element>`** に続く要素を使用して、XML構造内のデータ項目の場所と名前を定義できます。

サンプルスキーマでは、次のようになります。

```
<attribute name="email"/>
<attribute name="created"/>
<attribute name="gender"/>
<element name="location">
  <attribute name="city"/>
</element>
```

次の規則に従う必要があります。

* お **`<element>`** よびは、 **`<attribute>`** name **** 属性で名前で識別する必要があります。

   >[!IMPORTANT]
   >
   >要素名は簡潔で、できれば英語で記述し、XML命名規則に従って、許可された文字のみを含める必要があります。

* XML構造に含めることができるのは **`<element>`** 要素 **`<attribute>`** と **`<element>`** 要素だけです。
* 要素は、 **`<attribute>`** 要素内に一意の名前を持つ必要があり **`<element>`**&#x200B;ます。
* 複数行のデータ文字列 **`<elements>`** での使用をお勧めします。

## データタイプ {#data-types}

データタイプは、および **要素の** type **`<attribute>`** 属性を使用して入力 **`<element>`** します。

詳細なリストは、要素と要素の説明で確認でき [`<attribute>` ます](../../configuration/using/elements-and-attributes.md#attribute--element)[`<element>`](../../configuration/using/elements-and-attributes.md#element--element)。

この属性に値が入力されていない場合、要素に子要素が含まれていない限り、 **string** がデフォルトのデータ型になります。 要素が含まれる場合は、要素を階層的に構成する目的(この例では&#x200B;**`<location>`** 要素)でのみ使用します。

スキーマでは、次のデータ型がサポートされています。

* **string**:文字列。 例：名、町名等

   サイズは、 **length** 属性（オプション、デフォルト値は「255」）を使用して指定できます。

* **boolean**:ブール値フィールド 可能な値の例：true/false、0/1、yes/noなど
* **byte**, **short**, **long**:整数（1バイト、2バイト、4バイト）。 例：年齢、口座番号、ポイント数等
* **重複**:重複精度浮動小数点数。 例：価格、料金等
* **date**, **datetime**:日付と日付+時間。 例：生年月日、購入年月日等
* **datetimenotz**:タイムゾーンデータを含まない日付+時刻。
* **timespan**:継続時間。 例：年功序列。
* **メモ**:長いテキストフィールド（複数行） 例：説明、コメントなど
* **uuid**:GUIDをサポートする「uniqueidentifier」フィールド（Microsoft SQL Serverでのみサポート）。

   >[!NOTE]
   >
   >Microsoft SQL Server以外のエンジンに **uuid** フィールドを含めるには、「newuuid()」関数を追加し、デフォルト値で完了する必要があります。

次に、入力したタイプのスキーマ例を示します。

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
   <td> VARCHAR2 （Unicodeの場合はNVARCHAR2）<br /> </td> 
   <td> VARCHAR(VARCHAR文字セット（Unicodeの場合はUNICODE）<br /> </td> 
   <td> VARCHAR<br /> </td> 
   <td> VARCHAR （Unicodeの場合はNVARCHAR）<br /> </td> 
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
   <td> 重複精度<br /> </td> 
   <td> FLOAT<br /> </td> 
   <td> FLOAT<br /> </td> 
   <td> DOUBLE<br /> </td> 
   <td> FLOAT<br /> </td> 
  </tr> 
  <tr> 
   <td> 長いテキスト<br /> </td> 
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
   <td> 日付<br /> </td> 
   <td> 日付<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> 日付<br /> </td> 
   <td> DATETIME<br /> </td> 
  </tr> 
  <tr> 
   <td> 時間<br /> </td> 
   <td> 時間<br /> </td> 
   <td> FLOAT<br /> </td> 
   <td> 時間<br /> </td> 
   <td> 時間<br /> </td> 
   <td> FLOAT<br /> </td> 
  </tr> 
  <tr> 
   <td> 日時<br /> </td> 
   <td> TIMESTAMPZ<br /> </td> 
   <td> 日付<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> MS SQL &lt; 2008:DATETIME<br /> MS SQL &gt;= 2012:DATETIMEOFFSET<br /> </td> 
  </tr> 
  <tr> 
   <td> Datetimenotz<br /> </td> 
   <td> TIMESTAMPZ<br /> </td> 
   <td> 日付<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> MS SQL &lt; 2008:DATETIME<br /> MS SQL &gt;= 2012:DATETIME2<br /> </td> 
  </tr> 
  <tr> 
   <td> Timespan<br /> </td> 
   <td> 重複精度<br /> </td> 
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

データスキーマ **`<elements>`** の要素と **`<attributes>`** 要素は、様々なプロパティを使用して強化できます。 現在の要素を説明するためにラベルを入力できます。

### ラベルと説明 {#labels-and-descriptions}

* 「 **label** 」プロパティを使用すると、簡単な説明を入力できます。

   >[!NOTE]
   >
   >ラベルは、インスタンスの現在の言語に関連付けられます。

   **例**：

   ```
   <attribute name="email" type="string" length="80" label="Email"/>
   ```

   ラベルは、Adobe Campaignクライアントコンソールの入力フォームから確認できます。

   ![](assets/d_ncs_integration_schema_label.png)

* **desc** プロパティを使用すると、詳細な説明を入力できます。

   説明は、Adobe Campaignクライアントコンソールのメインウィンドウのステータスバーにある入力フォームから確認できます。

   >[!NOTE]
   >
   >説明は、インスタンスの現在の言語に関連付けられます。

   **例**：

   ```
   <attribute name="email" type="string" length="80" label="Email" desc="Email of recipient"/>
   ```

### デフォルト値 {#default-values}

**default** プロパティを使用すると、コンテンツ作成時にデフォルト値を返す式を定義できます。

値は、XPath言語に準拠した式である必要があります。 この方法について詳しくは、「XPathを使用した [参照](../../configuration/using/schema-structure.md#referencing-with-xpath)」を参照してください。

**例**：

* 現在の日付： **default=&quot;GetDate()&quot;**
* カウンタ： **default=&quot;&#39;FRM&#39;+CounterValue(&#39;myCounter&#39;)&quot;**

   この例では、文字列を連結して、 **CounterValue** 関数を空のカウンタ名で呼び出して、デフォルト値を構築します。 返される数字は、挿入のたびに1ずつ増分されます。

   >[!NOTE]
   >
   >Adobe Campaignクライアントコンソールでは、 **[!UICONTROL 管理/カウンタ]** ノードを使用してカウンタを管理します。

デフォルト値をフィールドにリンクするには、 `<default>  or  <sqldefault>   field.  </sqldefault> </default>`

`<default>` :エンティティを作成する際に、フィールドにデフォルト値を事前入力できます。 値はデフォルトのSQL値ではありません。

`<sqldefault>` :フィールドの作成時に値を追加できます。 この値はSQL結果として表示されます。 スキーマの更新中、新しいレコードのみがこの値の影響を受けます。

### 列挙 {#enumerations}

#### 無料定義済みリスト {#free-enumeration}

userEnum **** プロパティを使用すると、このフィールドに入力した値を記憶し、表示するための空き定義済みリストを定義できます。 構文は以下のようになります。

**userEnum=&quot;定義済みリスト名&quot;**

定義済みリストに与えられた名前は自由に選択し、他のフィールドと共有できます。

次の値は、入力フォームのドロップダウンリストに表示されます。

![](assets/d_ncs_integration_schema_user_enum.png)

>[!NOTE]
>
>Adobe Campaignクライアントコンソールでは、 **[!UICONTROL 定義済みリストの管理/定義済みリスト]** ノードを使用してを管理します。

#### 定義済みリストの設定 {#set-enumeration}

**enum** プロパティを使用すると、可能な値のリストがあらかじめわかっている場合に使用される固定定義済みリストを定義できます。

**enum** 属性は、メイン要素の外側のスキーマに入力された定義済みリストクラスの定義を参照します。

定義済みリストを使用すると、ユーザーは、通常の入力フィールドに値を入力する代わりに、ドロップダウンリストから値を選択できます。

![](assets/d_ncs_integration_schema_enum.png)

データスキーマの定義済みリスト宣言の例：

```
<enumeration name="gender" basetype="byte" default="0">    
  <value name="unknown" label="Not specified" value="0"/>    
  <value name="male" label="male" value="1"/>   
  <value name="female" label="female" value="2"/>   
</enumeration>
```

定義済みリストは、その要素を介してメイン要素の外側で宣言され **`<enumeration>`** ます。

定義済みリストのプロパティは次のとおりです。

* **baseType**:値に関連付けられているデータのタイプ、
* **label**:定義済みリストの説明
* **name**:定義済みリストの名前
* **default**:定義済みリストのデフォルト値。

定義済みリスト値は、次の属性を使用して **`<value>`** 要素内で宣言されます。

* **name**:内部的に保存された値の名前、
* **label**:グラフィカルインターフェースを介して表示されるラベル。

#### ドベナム定義済みリスト {#dbenum-enumeration}

* dbenum **プロパティを使用すると** 、 **** enumプロパティと類似のプロパティを持つ定義済みリストを定義できます。

   ただし、 **name** 属性は値を内部的に保存するのではなく、関連するテーブルのスキーマを変更せずに関連するテーブルを拡張できるコードを保存します。

   値は、 **[!UICONTROL 管理/定義済みリスト]** ・ノードで定義します。

   この定義済みリストは、キャンペーンの特性を指定する場合などに使用します。

   ![](assets/d_ncs_configuration_schema_dbenum.png)

### 例 {#example}

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

**unbound** 属性の値が「true」の場合、コレクション要素を設定できます。

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
* **location/@city**:要素の下の「市区町村」属性を選択し **`<location>`** ます
* **../@email**:現在の要素の親要素から電子メールアドレスを選択します
* **group`[1]/@label`**:最初のコレクション要素の子である「label」属性を選択し **`<group>`** ます
* **group`[@label='test1']`**:要素の子で、値「test1」を含む「label」属性を **`<group>`** 選択します

>[!NOTE]
>
>パスがサブ要素を越えると、追加の制約が追加されます。 この場合、次の式を角括弧で囲む必要があります。
>
>* **location/@city** is not valid;使用する **`[location/@city]`**
>* **`[@email]`** と **@email** は同等です。

>



次の算術演算など、複雑な式を定義することもできます。

* **@gender+1**:gender **属性の内容に1を追加します** 。
* **@email + &#39;(&#39;+@created+&#39;&#39;**:作成日の丸括弧内に追加された電子メールアドレスの値を受け取って文字列を作成します（文字列型の場合は、定数を引用符で囲みます）。

この言語の潜在能力を高めるため、式に高レベルの関数が追加されました。

使用可能な機能のリストは、Adobe Campaignクライアントコンソールの任意の式エディターからアクセスできます。

![](assets/d_ncs_integration_schema_function.png)

**例**：

* **GetDate()**:現在の日付を返します。
* **Year(@created)**:「created」属性に含まれる日付の年を返します。
* **GetEmailDomain(@email)**:電子メールアドレスのドメインを返します。

## 計算文字列を使用した文字列の作成 {#building-a-string-via-the-compute-string}

「 **Compute string** 」は、スキーマに関連付けられたテーブル内のレコードを表す文字列を構築するために使用されるXPath式です。 **計算文字列** ：主にグラフィカルインターフェイスで、選択したレコードのラベルを表示するために使用されます。

「 **計算文字列** 」は、データスキーマのメイン要素の下の **`<compute-string>`** 要素を介して定義されます。 「 **expr** 」属性には、表示を計算するXPath式が含まれます。

**例**:受信者テーブルの文字列を計算します。

```
<srcSchema name="recipient" namespace="nms">  
  <element name="recipient">
    <compute-string expr="@lastName + ' ' + @firstName +' (' + @email + ')' "/>
    ...
  </element>
</srcSchema>
```

受信者の計算済み文字列の結果： **Doe John(john.doe@aol.com)**

>[!NOTE]
>
>スキーマにCompute文字列が含まれていない場合、デフォルトでは、スキーマの主キーの値がCompute文字列に入力されます。

