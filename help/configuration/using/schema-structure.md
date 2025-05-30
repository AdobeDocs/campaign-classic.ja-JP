---
product: campaign
title: Adobe Campaignのスキーマ構造について
description: スキーマの構造
feature: Custom Resources
role: Data Engineer, Developer
audience: configuration
content-type: reference
level: Intermediate, Experienced
topic-tags: schema-reference
exl-id: 3405efb8-a37c-4622-a271-63d7a4148751
source-git-commit: 2bfcec5eaa1145cfb88adfa9c8b2f72ee3cd9469
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 67%

---

# スキーマ構造について {#schema-structure}

スキーマの基本構造は次のとおりです。

## データスキーマ  {#data-schema}

`<srcschema>` の場合、構造は次のようになります。

```sql
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

データスキーマの XML ドキュメントには、スキーマの名前と名前空間を生成する **name** 属性と **namespace** 属性が設定された **`<srcschema>`** ルート要素を含める必要があります。

```sql
<srcSchema name="schema_name" namespace="namespace">
...
</srcSchema>
```

次の XML コンテンツを使用して、データスキーマの構造を説明します。

```sql
<recipient email="John.doe@aol.com" created="2009/03/12" gender="1"> 
  <location city="London"/>
</recipient>
```

対応するデータスキーマを使用して、次の操作をおこないます。

```sql
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

スキーマのエントリポイントは、スキーマの主な要素です。 メイン要素はスキーマと同じ名前なので、識別は容易です。また、メイン要素はルート要素の子でなければなりません。コンテンツの記述は、この要素から始まります。

この例では、メイン要素を次の行で表しています。

```
<element name="recipient">
```

メイン要素の後に続く **`<attribute>`** 要素と **`<element>`** 要素は、XML 構造内のデータ項目の場所と名前を定義するために使用されます。

サンプルスキーマでは、次のようになります。

```sql
<attribute name="email"/>
<attribute name="created"/>
<attribute name="gender"/>
<element name="location">
  <attribute name="city"/>
</element>
```

次のルールが適用されます。

* 各 **`<element>`** と **`<attribute>`** は、**name** 属性を介して名前で識別する必要があります。

  >[!IMPORTANT]
  >
  >要素名は簡潔なもの（できれば英語）にし、XML 命名規則で許可されている文字のみを含める必要があります。

* XML 構造に **`<attribute>`** 要素と **`<element>`** 要素を含めることができるのは、**`<element>`** 要素のみです。
* **`<attribute>`** 要素には、**`<element>`** 内で一意の名前が必要です。
* 複数行のデータ文字列では、**`<elements>`** を使用することをお勧めします。

## データタイプ {#data-types}

データタイプは、**`<attribute>`** 要素と **`<element>`** 要素の **type** 属性を介して入力されます。

詳細なリストは、[`<attribute>` 要素の説明 ](../../configuration/using/schema/attribute.md) および [`<element>` 要素 ](../../configuration/using/schema/element.md) で利用できます。

この属性が空の場合、要素に子要素が含まれていない限り、**string** がデフォルトのデータタイプになります。 子要素が含まれる場合は、要素を階層的に構成するためにのみ使用します（この例では&#x200B;**`<location>`**&#x200B;要素）。

スキーマでは、次のデータタイプをサポートしています。

* **string**：文字列。例：名、町名など

  サイズは、**length** 属性を使用して指定できます。オプションであり、デフォルト値は「255」です。

* **boolean**：ブール値フィールド可能な値の例：true または false、0 または 1、yes または no など
* **byte**、**short**、**long**：整数（1 バイト、2 バイト、4 バイト）。例：年齢、アカウント番号、ポイント数など
* **double**：倍精度浮動小数点数。例：価格、料金など
* **date**、**datetime**：日付、および日付 + 時刻。例：生年月日、購入日など
* **datetimenotz**：タイムゾーンデータを含まない日付＋時刻。
* **timespan**：継続時間。例：年齢順。
* **memo**：長いテキストフィールド（複数行）。例：説明、注釈など
* **uuid**:GUID をサポートする「uniqueidentifier」フィールド（Microsoft SQL Server でのみサポート）。

  >[!NOTE]
  >
  >Microsoft SQL Server 以外の RDBMS に **uuid** フィールドを含めるには、関数 `the newuuid()` 追加し、デフォルト値を設定する必要があります。

次に、入力したタイプのスキーマ例を示します。

```sql
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

### Adobe Campaign/DBMS データのタイプのマッピング {#mapping-the-types-of-adobe-campaign-dbms-data}

次の表に、様々なデータベース管理システム向けにAdobe Campaignで生成されるデータのタイプのマッピングを示します。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>Adobe Campaign</strong><br /> </td> 
   <td> <strong>PosgreSQL</strong><br /> </td> 
   <td> <strong>Oracle</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> 文字列<br /> </td> 
   <td> VARCHAR （255） <br /> </td> 
   <td> VARCHAR2 （Unicode の場合は NVARCHAR2） <br /> </td> 
  </tr> 
  <tr> 
   <td> ブール値 <br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> NUMBER （3） <br /> </td> 
  </tr> 
  <tr> 
   <td> バイト <br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> NUMBER （3） <br /> </td> 
  </tr> 
  <tr> 
   <td> 短い <br /> </td> 
   <td> SMALLINT<br /> </td> 
   <td> NUMBER （5） <br /> </td> 
  </tr> 
  <tr> 
   <td> ダブル <br /> </td> 
   <td> 倍精度 <br /> </td> 
   <td> 浮動小数 <br /> </td> 
  </tr> 
  <tr> 
   <td> 長い <br /> </td> 
   <td> 整数 <br /> </td> 
   <td> NUMBER （10） <br /> </td> 
  </tr> 
  <tr> 
   <td> Int64<br /> </td> 
   <td> BIGINT<br /> </td> 
   <td> NUMBER （20） <br /> </td> 
  </tr> 
  <tr> 
   <td> 日付<br /> </td> 
   <td> 日付 <br /> </td> 
   <td> 日付 <br /> </td> 
  </tr> 
  <tr> 
   <td> 時間 <br /> </td> 
   <td> 時間 <br /> </td> 
   <td> 浮動小数 <br /> </td> 
  </tr> 
  <tr> 
   <td> 日時 <br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> 日付 <br /> </td> 
  </tr> 
  <tr> 
   <td> Datetimenoz<br /> </td> 
   <td> TIMESTAMP<br /> </td> 
   <td> 日付 <br /> </td> 
  </tr> 
  <tr> 
   <td> 期間 <br /> </td> 
   <td> 倍精度 <br /> </td> 
   <td> 浮動小数 <br /> </td> 
  </tr> 
  <tr> 
   <td> メモ<br /> </td> 
   <td> テキスト <br /> </td> 
   <td> CLOB （Unicode の場合は NCLOB） <br /> </td> 
  </tr> 
  <tr> 
   <td> Blob<br /> </td> 
   <td> BLOB<br /> </td> 
   <td> BLOB<br /> </td> 
  </tr> 
 </tbody> 
</table>

## プロパティ {#properties}

データスキーマの **`<elements>`** 要素と **`<attributes>`** 要素は、様々なプロパティを使用して強化できます。 現在の要素を説明するためにラベルを入力できます。

### ラベルと説明 {#labels-and-descriptions}

* **label** プロパティを使用すると、簡単な説明を入力できます。

  >[!NOTE]
  >
  >ラベルは、インスタンスの現在の言語に関連付けられます。

  **例**：

  ```sql
  <attribute name="email" type="string" length="80" label="Email"/>
  ```

  ラベルは、Adobe Campaign クライアントコンソールの入力フォームに表示されます。

  ![](assets/d_ncs_integration_schema_label.png)

* **desc** プロパティを使用すると、詳細な説明を入力できます。

  説明は、Adobe Campaign クライアントコンソールのメインウィンドウのステータスバーにある入力フォームに表示されます。

  >[!NOTE]
  >
  >説明は、インスタンスの現在の言語に関連付けられます。

  **例**：

  ```sql
  <attribute name="email" type="string" length="80" label="Email" desc="Email of recipient"/>
  ```

### デフォルト値 {#default-values}

コンテンツ作成時にデフォルト値を返す式を定義するには、**default** プロパティを使用します。

値は、XPath 言語に準拠した式である必要があります。 詳しくは、[XPath を使用した参照 ](../../configuration/using/schema-structure.md#referencing-with-xpath) を参照してください。

**例**：

* 現在の日付：**default=&quot;GetDate()&quot;**
* カウンター：**default=&quot;&#39;FRM&#39;+CounterValue(&#39;myCounter&#39;)&quot;**

  この例では、デフォルト値は文字列を連結して構築され、**CounterValue** 関数を任意のカウンター名で呼び出しています。 返される数字は、挿入のたびに 1 ずつ増分されます。

  >[!NOTE]
  >
  >Adobe Campaign クライアントコンソールで、エクスプローラーの **[!UICONTROL 管理/カウンター]** フォルダーを参照して、カウンターを管理します。

フィールドにデフォルト値をリンクするには、`<default>` または `<sqldefault>` を使用できます   フィールド。

`<default>`：エンティティを作成時にデフォルト値をフィールドに事前入力できます。値はデフォルトの SQL 値ではありません。

`<sqldefault>`：フィールドの作成時に値を追加できます。この値は SQL 結果として表示されます。 スキーマを更新時に、この値の影響を受けるのは新しいレコードだけです。

### 列挙 {#enumerations}

#### 列挙を開く {#free-enumeration}

**userEnum** プロパティを使用すると、開いている定義済みリストを定義して、このフィールドに入力した値を保存して表示することができます。

構文は以下のようになります。

`userEnum="name of enumeration"`

これらの値が、入力フォームのドロップダウンリストに表示されます。

![](assets/d_ncs_integration_schema_user_enum.png)

>[!NOTE]
>
>Adobe Campaign クライアントコンソールで、定義済みリストを管理するエクスプローラーの **[!UICONTROL 管理/定義済みリスト]** フォルダーを参照します。

#### 定義済みリストを設定 {#set-enumeration}

**enum** プロパティを使用すると、考えられる値のリストが事前にわかっている場合に使用できる、固定の定義済みリストを定義できます。

**enum** 属性は、メイン要素の外側のスキーマに入力される定義済みリストクラスの定義を参照します。

定義済みリストを使用すると、通常の入力フィールドに値を入力する代わりに、ドロップダウンリストから値を選択できるようになります。

![](assets/d_ncs_integration_schema_enum.png)

データスキーマの定義済みリスト宣言の例：

```sql
<enumeration name="gender" basetype="byte" default="0">    
  <value name="unknown" label="Not specified" value="0"/>    
  <value name="male" label="male" value="1"/>   
  <value name="female" label="female" value="2"/>   
</enumeration>
```

定義済みリストは、メイン要素の外側で **`<enumeration>`** 要素を介して宣言されます。

定義済みリストのプロパティは次のとおりです。

* **baseType**：値に関連付けられているデータのタイプ
* **label**：定義済みリストの説明
* **name**：列挙の名前
* **default**：列挙のデフォルト値

定義済みリストの値は、次の属性を持つ **`<value>`** 要素で宣言します。

* **name**：内部的に保存された値の名前
* **label**: グラフィカルインターフェイスに表示されるラベル

#### dbenum 定義済みリスト {#dbenum-enumeration}

***dbenum** プロパティを使用すると、**enum** プロパティと類似したプロパティを持つ定義済みリストを定義できます。

ただし、**name** 属性は値を内部に格納するのではなく、スキーマを変更せずに関連するテーブルを拡張できるコードを格納します。

この定義済みリストは、キャンペーンの特性を指定する場合などに使用します。

![](assets/d_ncs_configuration_schema_dbenum.png)

### 例 {#example}

プロパティが設定されたスキーマの例を示します。

```sql
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

**unbound** 属性の値が「true」の場合、コレクション要素にデータを埋め込むことができます。

**例**：スキーマ内の **`<group>`** コレクション要素の定義。

```sql
<element name="group" unbound="true" label="List of groups">
  <attribute name="label" type="string" label="Label"/>
</element>
```

XML コンテンツの投影を使用する場合：

```sql
<group label="Group1"/>
<group label="Group2"/>
```

## XPath を使用した参照 {#referencing-with-xpath}

Adobe Campaign では、XPath 言語を使用して、データスキーマに属する要素または属性を参照します。

XPath は、XML ドキュメントのツリー内にノードを配置するための構文です。

要素は名前で指定し、属性は名前の前に「@」文字を付けて指定します。

**例**：

* **@email**：メールを選択します。
* **location/@city**：**`<location>`** 要素の「市区町村」属性を選択します。
* **../@email**：現在の要素の親要素からメールアドレスを選択します。
* **group`[1]/@label`**：最初の **`<group>`** コレクション要素の子要素である「label」属性を選択します。
* **group`[@label='test1']`**：**`<group>`** 要素の子で、値「test1」を含む「label」属性を選択します。

>[!NOTE]
>
>パスがサブ要素を越えると、制約が追加されます。 この場合、次の式を角括弧で囲む必要があります。
>
>* **location/@city** が無効です。**`[location/@city]`** を使用してください。
>* **`[@email]`** と **@email** は同等です。
>

次の算術演算のように、複雑な式を定義することもできます。

* **@gender+1**：**gender** 属性の内容に 1 を追加します。
* **@email + &#39;（&#39;+@created+&#39;）&#39;**：丸括弧内の作成日に追加されたメールアドレスの値を受け取って、文字列を作成します（文字列型の場合は、定数を引用符で囲みます）。

この言語の可能性を広げるため、式に高レベルの関数が追加されました。

使用可能な関数のリストについては、Adobe Campaign クライアントコンソールの任意の式エディターを参照してください。

![](assets/d_ncs_integration_schema_function.png)

**例**：

* **GetDate()**：現在の日付を返します。
* **Year （@created）**:「created」属性に含まれる日付の年を返します。
* **GetEmailDomain （@email）**：メールアドレスのドメインを返します

## 文字列計算を使用した文字列の作成 {#building-a-string-via-the-compute-string}

**文字列計算**&#x200B;は、スキーマに関連付けられたテーブルのレコードを表す文字列の構築に使用する XPath 式です。 **文字列計算** は、主にグラフィカルインターフェイスで、選択したレコードのラベルを表示するために使用します。

**文字列計算**&#x200B;は、データスキーマのメイン要素の下の **`<compute-string>`** 要素を介して定義します。**expr** 属性には、表示を計算する XPath 式が含まれます。

**例**：受信者テーブルの文字列を計算します。

```sql
<srcSchema name="recipient" namespace="nms">  
  <element name="recipient">
    <compute-string expr="@lastName + ' ' + @firstName +' (' + @email + ')' "/>
    ...
  </element>
</srcSchema>
```

受信者の文字列計算の結果：**Doe John (john.doe@aol.com)**

>[!NOTE]
>
>スキーマに文字列計算が含まれていない場合、デフォルトでは、スキーマのプライマリキーの値が文字列計算に入力されます。


## 詳細情報

詳しくは、次のリンクを参照してください。

* [スキーマの基本を学ぶ](about-schema-reference.md)
* [データベースマッピング](database-mapping.md)
* [リンク管理](database-links.md)
* [キーの管理](database-keys.md)
* [Campaign データモデル](about-data-model.md)