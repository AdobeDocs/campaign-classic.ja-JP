---
title: 要素と属性
seo-title: 要素と属性
description: 要素と属性
seo-description: null
page-status-flag: never-activated
uuid: 72b0128a-a453-4646-93e5-b399914abb76
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: schema-reference
discoiquuid: 5e24d94a-f9c1-4642-a881-dfc4b5492f14
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: dbff132e3bf88c408838f91e50e4b047947ee32a

---


# 要素と属性 {#elements-and-attributes}

スキーマを編集する場合は、ソーススキーマ(xtk:srcSchema)に基づく承認システムを使用できます。 「データベース構造の更新…」を使用してデータベースを更新する際に、エラーが発生する場合もあります。 ウィザード。

デフォルトでは、Adobe Campaignスキーマでは、すべてのBoolean型属性は「false」です。 これらをアクティブにするには、スキーマで属性を指定し、その値を「true」に設定する必要があります。

## `<attribute>` 要素 {#attribute--element}

### コンテンツモデル {#content-model}

attribute:==help

### 属性 {#attributes}

_operation (string)、advanced (boolean)、applicableIf (string)、autoIncrement (boolean)、belonsTo (string)、dataPolicy (string)、dbEnum (string)、defOnDuplicate (boolean)、default (string)、desc (string)、expr (string)、feature (string)、feature (boolean)img （文字列）、inout （文字列）、label （文字列）、length （文字列）、localizable （文字列）、name (MNTOKEN)、notNull （ブール値）、pkgStatus （文字列）、ref （文字列）、required （ブール値）、sql （ブール値）、sqlname （文字列）、sqltable （文字列）、target (MNTOKEN)、template （文字列）デフォルト（文字列）、translatedExpr （文字列）、type (MNTOKEN)、user （ブール値）、userEnum （文字列）、visibleIf （文字列）、xml （ブール値）

### 親 {#parents}

`<element>`

### 子 {#children}

`<help>`

### 説明 {#description}

`<attribute>` 要素を使用すると、データベース内のフィールドを定義できます。

### 使用と使用の状況 {#use-and-context-of-use}

`<attribute>` 要素は要素内で宣言する必要があ `<element>` ります。

内で要素が定義さ `<attribute>` れるシーケンスは、デ `<srcschema>` ータベース内のフィールド作成シーケンスに影響しません。 作成シーケンスはアルファベット順になります。

### 属性の説明 {#attribute-description}

* **_operation (string)**:データベースに書き込む書き込みの種類を定義します。

   この属性は、主に標準のスキーマを拡張する際に使用されます。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:調整のみ。 つまり、Adobe Campaignは、要素を更新せずに回復し、要素が存在しない場合はエラーを生成します。
   * &quot;insertOrUpdate&quot;:挿入時に更新します。 つまり、Adobe Campaignは要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 つまり、要素が存在しない場合は、Adobe Campaignが要素を更新するか、エラーを生成します。
   * &quot;delete&quot;:削除。 つまり、Adobe Campaignは要素を回復および削除します。

* **advanced(boolean)**:このオプションを有効にすると(@advanced=&quot;true&quot;)、フォーム内のリストを設定するためにアクセス可能なフィールドのリストの属性を非表示にできます。
* **applicableIf (string)**:この属性を使用すると、フィールドをオプションにできます。 制約 `<attribute>` が準拠している場合、要素はデータベースを更新する際に考慮されます。 &quot;applicableIf&quot;はXTK式を受け取ります。
* **autoIncrement (boolean)**:このオプションを有効にすると、フィールドはカウンターになります。 これにより、値を増分できます（ほとんどのID）。 （外部使用）
* **belongsTo (string)**:フィールドを共有するテーブルの名前と名前空間を取得し、属性が宣言されているスキーマを入力します。 (aでのみ使用され `<schema>`ます)。
* **dataPolicy (string)**:sqlまたはXMLフィールドで許可される値に対する承認制約を指定できます。 この属性の値は次のとおりです。

   * &quot;none&quot;:値なし
   * &quot;smartCase&quot;:先頭文字大文字
   * &quot;lowerCase&quot;:小文字
   * &quot;upperCase&quot;:大文字
   * &quot;email&quot;:電子メールアドレス
   * &quot;phone”:電話番号
   * &quot;識別子&quot;:識別子名
   * &quot;resIdentifier&quot;:ファイル名

* **dbEnum (string)**:「閉じた」列挙の内部名を受け取ります。 列挙値は、で定義する必要があります `<srcschema>`。
* **defOnDuplicate (boolean)**:この属性がアクティブな場合、レコードが重複すると、デフォルト値（@defaultで定義）がレコードに自動的に再適用されます。
* **default（文字列）**:デフォルトフィールドの値（関数の呼び出し、デフォルト値）を定義できます。 この属性はXTK式を受け取ります。
* **desc（文字列）**:属性の説明を挿入できます。 この説明は、インターフェイスのステータスバーに表示されます。
* **編集（文字列）**:この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum (string)**:フィールドにリンクされた列挙の名前を受け取ります。 列挙は、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**:フィールドの事前計算式を定義します。 この属性は、XpathまたはXTK式を受け取ります。
* **feature (string)**:特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張する目的で使用されますが、別のテーブルに保存する目的で使用されます。 指定できる値は次のとおりです。

   * &quot;shared&quot;:コンテンツは、データ型ごとに共有テーブルに保存されます
   * &quot;dedicated&quot;:コンテンツは専用のテーブルに保存される
   SQL特性テーブルは、次の特性タイプに基づいて自動的に作成されます。

   * dedicated: `Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`
   特性フィールドには2種類あります。1つの値が特性に対して承認される単純なオアフィールドと、複数の値を含む収集要素にリンクされるオアフィールドです。

   スキーマで特性を定義する場合、このスキーマは単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されません）。

* **featureDate (boolean)**:属性が「@feature」特性フィールドにリンクされている。 値が「true」の場合は、値が最後に更新された日時を確認できます。
* **img (string)**:フィールドにリンクされた画像のパス（名前空間+画像名）を定義できます(例：img=&quot;cus:mypicture.jpg&quot;)。 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **label (string)**:フィールドにリンクされたラベル。ほとんどの場合、インターフェイス内のユーザーにリンクされます。 これにより、命名の制約を回避できます。
* **length (string)**:最大 string型のSQLフィールドの値の文字数。 「@length」属性が指定されていない場合、Adobe Campaignは255文字のフィールドを自動的に作成します。
* **localizable (boolean)**:この属性がアクティブ化されている場合、この属性は、翻訳（内部使用）のために「@label」属性の値を回復するようコレクションツールに指示します。
* **name (MNTOKEN)**:テーブル内のフィールドの名前と一致する属性の名前。 「@name」属性の値は、短く、できれば英語で指定し、XMLの命名の制約に準拠する必要があります。

   スキーマがデータベースに書き込まれると、Adobe Campaignによってフィールド名に接頭辞が自動的に追加されます。

   * &quot;i&quot;:&#39;integer&#39;型のプレフィックス。
   * &quot;d&quot;:&#39;double&#39;型のプレフィックス。
   * &quot;s&quot;:文字列タイプのプレフィックス。
   * &quot;ts&quot;:「日付」タイプのプレフィックス。
   テーブル内のフィールドの名前を完全に定義するには、属性を定義する際に「@sqlname」オプションを使用します。

* **notNull (boolean)**:データベース内のNULLレコードの管理に関するAdobe Campaignの動作を再定義できます。 デフォルトでは、数値フィールドはnullではなく、文字列フィールドと日付型フィールドはnullに設定できます。
* **pkgStatus (string)**:パッケージのエクスポート時に、「@pkgStatus」の値に応じて次の値が考慮されます。

   * &quot;always&quot;:常に存在する
   * &quot;never&quot;:存在しない
   * &quot;default (or nothing)&quot;:値がデフォルト値の場合、または他のインスタンスと互換性がない内部フィールドでない場合を除き、値がエクスポートされます。

* **ref (string)**:この属性は、複数のスキーマ(定義ファ `<attribute>` クタリング)で共有される要素への参照を定義します。 定義は現在のスキーマにコピーされません。
* **必須（ブール値）**:この属性がアクティブ化されている(@required=&quot;true&quot;)場合、インターフェイス内でフィールドがハイライト表示されます。 フィールドのラベルは、フォームでは赤で表示されます。
* **sql (boolean)**:この属性がアクティブ化されると(@sql=&quot;true&quot;)、属性を含む要素にxml=&quot;true&quot;プロパティが含まれている場合でも、SQL属性の保存が強制されます。
* **sqlDefault（文字列）**:この属性を使用すると、@notNull属性がアクティブ化されている場合にデータベースの更新に使用されるデフォルト値を定義できます。 属性の作成後にこの属性を追加した場合、新しいレコードに対してもスキーマの動作は変更されません。 スキーマを変更し、新しいレコードの値を更新するには、属性を削除して再び作成する必要があります。
* **sqlname（文字列）**:の値を含む値を取得します。 @sqlnameを指定しない場合、「@name」属性の値がデフォルトで使用されます。 データベースにスキーマが書き込まれると、フィールドの種類に応じて自動的に接頭辞が追加されます。
* **template (string)**:この属性は、複数のスキーマで共有される `<attribute>` 要素への参照を定義します。 定義は自動的に現在のスキーマにコピーされます。
* **translatedDefault(string)**:「@default」属性が見つかった場合、「@translatedDefault」を使用すると、翻訳ツールによって収集される式を、@defaultで定義された式と一致するように再定義できます（内部使用）。
* **translatedExpr (string)**:「@expr」属性が存在する場合、「@translatedExpr」属性を使用すると、翻訳ツールで収集する式を、@exprで定義された式と一致するように再定義できます（内部使用）。
* **type (MNTOKEN)**:フィールドタイプ。

   フィールドタイプは汎用です。 Adobe Campaignでは、インストールされているデータベースのタイプに応じて、定義されたタイプを、構造の更新時にインストールされるデータベースに固有の値に変更します。

   使用可能なタイプのリスト：

   * ANY
   * bin
   * blob
   * boolean
   * バイト
   * CDATA
   * datetime
   * datetimetz
   * datetimenotz
   * 日付
   * double
   * enum
   * float
   * html
   * int64
   * link
   * 長い
   * メモ
   * MNTOKEN
   * percent
   * primarykey
   * short
   * 文字列
   * 時間
   * 間隔
   * uuid
   「@type」属性を空のままにした場合、Adobe Campaignは、長さ100の文字列(STRING)をデフォルトでフィールドにリンクします。

   フィールドのタイプがSTRINGで、フィールドの名前が「@sqlname」属性の存在によって指定されていない場合、データベース内のフィールドの名前の前に自動的に「s」が付きます。 この動作モードは、INTEGER (i)、DOUBLE (d)、およびDATES (ts)タイプのフィールドと同様です。

* **userEnum (string)**:は、「open」列挙の内部名を受け取ります。 列挙の値は、インターフェイス内のユーザーによって定義できます。
* **visibleIf (string)**:属性の表示/非表示を切り替える条件をXTK式の形式で定義します。

   >[!IMPORTANT]
   >
   >属性は非表示ですが、そのデータにはアクセスできます。

* **xml（ブール値）**:このオプションが有効な場合、フィールドの値にリンクされたSQLフィールドは含まれません。 Adobe Campaignでは、レコードの保存用にテキストタイプ「mData」フィールドを作成します。 つまり、これらのフィールドにはフィルターや並べ替えが存在しません。

### 例 {#examples}

値がデータベースに格納される列挙値の例：

```
    <enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>

    <element label="Sample" name="Sample">
       <attribute dbEnum="myEnum" length="100" name="Number" required="true" type="string"/>
    </element>     
```

「@datapolicy」を使用したXMLフィールドの宣言：

```
<attribute dataPolicy="phone" desc="Mobile number" label="Mobile"
     length="32" name="mobilePhone" sqlname="sMobilePhone" type="string"/>
```

「@applicableIf」の例：「次を含む」属性は、国数が20を超える場合にのみ作成されます。

```
<attribute length="100" name="Continent" type="string" applicableIf="@country > 20"/>
```

「共有」タイプの「@feature」の例：

```
<attribute name="field1" label="Field 1" type="long" feature="shared"/>
<attribute name="field1" label="Field 1" type="long" feature="shared" sqlname="126" sqltable="Ft_Content_Long"/>
```

「dedicated」タイプの「@feature」の例：

```
<attribute name="field1" label="Field 1" type="long" feature="dedicated"/>
<attribute name="field1" label="Field 1" type="long" feature="dedicated" sqlname="sField1" sqltable="Ft_recipient_field1"/>
```

## `<compute-string>` 要素 {#compute-string--element}

### コンテンツモデル {#content-model-1}

compute-string:==EMPTY

### 属性 {#attributes-1}

@expr

### 親 {#parents-1}

`<element>`

### 子 {#children-1}

なし

### 説明 {#description-1}

この要 `<compute-string>` 素を使用すると、XTK式に基づく文字列を生成し、複数の値に基づいて「組み込み」ラベルをインターフェイスに表示できます。

### 使用と使用の状況 {#use-and-context-of-use-1}

を定義しな `<compute-string>` い場合、デフォ `<compute-string>` ルトでは、スキーマの主キーの値を使用して要素が入力されます。

### 属性の説明 {#attribute-description-1}

* **expr（文字列）**:XTKおよび/またはXpath式

### 例 {#examples-1}

```
<compute-string expr="@label + Iif(@code='','', ' (' + [folder/@label] + ')')"/>  
<compute-string expr="ToString([@centralCatalog-id]) + ',' + ToString([@localOrgUnit-id])" />
```

受信者に対して計算された文字列の結果：&quot;John Doe (john.doe@aol.com)&quot;:

```
<element name="recipient">
<compute-string expr="@lastName + ' ' + @firstName +' (' + @email + ')'
"/>
...
</element>
```

## `<condition>` 要素 {#condition--element}

### コンテンツモデル {#content-model-2}

条件：==EMPTY

### 属性 {#attributes-2}

* @boolOperator (string)
* @enabledIf (string)
* @expr（文字列）

### 親 {#parents-2}

`<sysfilter>`

### 子 {#children-2}

なし

### 説明 {#description-2}

この要素を使用して、フィルター条件を定義できます。

### 使用と使用の状況 {#use-and-context-of-use-2}

1つの要素 `<sysfiler>` に複数のフィルター条件を含めることができます。

### 属性の説明 {#attribute-description-2}

* **boolOperator (string)**:同じ要素内 `<conditions>` で複数が定義されている場 `<sysfilter>` 合、この属性を使用してそれらを結合できます。 デフォルトでは、論理リンクは「AND」 `<condition>` になっています。 「@boolOperator」属性を使用すると、「OR」と「AND」タイプのリンクを組み合わせることができます。
* **enabledIf (string)**:条件アクティベーションテスト。
* **expr（文字列）**:xtk式。

### 例 {#examples-2}

```
<sysfilter>
  <condition enabledIf="hasNamedRight('admin')=false" expr="@city=[currentOperator/location/@city]" />
</sysfilter>
```

## `<dbindex>` 要素 {#dbindex--element}

### コンテンツモデル {#content-model-3}

dbindex:==keyfield

### 属性 {#attributes-3}

* @_operation （文字列）
* @applicableIf (string)
* @label （文字列）
* @name (MNTOKEN)
* @unique (boolean)

### 親 {#parents-3}

`<element>`

### 子 {#children-3}

`<keyfield>`

### 説明 {#description-3}

この要素を使用すると、テーブルにリンクされたインデックスを定義できます。

### 使用と使用の状況 {#use-and-context-of-use-3}

複数のインデックスを定義できます。 1つのインデックスで、テーブルの1つ以上のフィールドを参照できます。 インデックス宣言は、通常、メインスキーマ要素の定義に従います。

内で定義される要 `<keyfield>` 素の順序は非常に `<dbindex>` 重要です。 1つ目は、ク `<keyfield>` エリーが主に基づくインデクション基準である必要があります。

データベース内のインデックスの名前は、テーブルの名前とインデックスの名前を連結して計算されます。 例：テーブル名「Sample」、名前空間「Cus」、インデックス名「MyIndex」 —>インデックス作成クエリ中のインデックスフィールドの名前：&quot;CusSample_myIndex&quot;

### 属性の説明 {#attribute-description-3}

* **_operation (string)**:データベースに書き込む書き込みの種類を定義します。

   この属性は、主に標準のスキーマを拡張する際に使用されます。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:調整のみ。 つまり、Adobe Campaignは、要素を更新せずに回復し、要素が存在しない場合はエラーを生成します。
   * &quot;insertOrUpdate&quot;:挿入時に更新します。 つまり、Adobe Campaignは要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 つまり、要素が存在しない場合は、Adobe Campaignが要素を更新するか、エラーを生成します。
   * &quot;delete&quot;:削除。 つまり、Adobe Campaignは要素を回復および削除します。

* **applicableIf (string)**:インデックスを考慮する条件 — XTK式を受け取ります。
* **label (string)**:インデックスのラベル。
* **name (MNTOKEN)**:一意のインデックス名。
* **unique (boolean)**:このオプションが有効な場合(@unique=&quot;true&quot;)、属性はフィールド全体でインデックスの一意性を保証します。

### 例 {#examples-3}

「id」フィールドでのインデックスの作成。 (要素の「@unique」属性は、データベース(クエ `<dbindex>` リ)にインデックスが作成されると、SQLキーワード「UNIQUE」の追加をトリガーします)。

```
<element label="Sample" name="Sample">
  <dbindex name="myIndex" label="My index on the ID field" unique="true" applicableIf="HasPackage('nms:social')">
      <keyfield xpath="@id"/>
  </dbindex>
    <attribute name="id" type="long"/>
</element>          
```

```
ALTER TABLE CusSample ADD iSampleId INTEGER;
UPDATE CusSample SET iSampleId = 0;
ALTER TABLE CusSample ALTER COLUMN iSampleId SET Default 0;
ALTER TABLE CusSample ALTER COLUMN iSampleId SET NOT NULL; 
CREATE UNIQUE INDEX CusSample_myIndex ON CusSample(iSampleId);
```

「@mail」フィールドと「@phoneNumber」フィールドに複合インデックスを作成する：

```
<element label="NewSchemaUser" name="NewSchemaUser">
  <dbindex name="myIndex" label="My composite index">
         <keyfield xpath="@email"/>
         <keyfield xpath="@phone"/>
  </dbindex>
  
  <attribute name="email" type="string"/>
  <attribute name="phone" type="string"/>
</element>      
```

```
CREATE INDEX DocNewSchemaUser_myIndex ON DocNewSchemaUser(sEmail, sPhone);
```

## `<element>` 要素 {#element--element}

### コンテンツモデル {#content-model-4}

element:=(attribute)| compute-string| dbindex|デフォルト|要素|ヘルプ|結合| key| sysFilter| translatedDefault)

### 属性 {#attributes-4}

_operation (string)、advanced (boolean)、aggregate (string)、applicableIf (string)、autopk (boolean)、belonsTo (string)、convDate (string)、dataPolicy (string)、dataSource (string)、defEnum (boolean)、defOnDuplicate (boolean)、des (string)、des (string)、des(string)boolean)、doesNotSupportDiff (boolean)、edit (string)、emptyKeyValue (string)、enum (string)、enumImage (string)、expandSchemaTarget (string)、expr (string)、externalJoin (boolean)、featureDate (boolean)、filterPath (string)、folderLink (folder)モデル（文字列）、folderProcess （文字列）、fullLoad (boolean)、hierarchical (boolean)、img （文字列）、inout （文字列）、integrity （文字列）、label （文字列）、length （文字列）、localizable (boolean)、name (MNTOKEN)、noDbIndex (boolean)boolean)、順序付けられた(boolean)、オーバーフローテーブル(boolean)、pkSequence(string)、pkgStatus(string)、ref(string)、revAdvanced(boolean)、revCardinality(string)、revDesc(boolean)、revExternalJoin(boolean)、revIntegrity(string)、revLabel(string)、revLink(string))、revTarget （文字列）、revVisibleIf （文字列）、sql （ブール値）、sqlname （文字列）、sqltable （文字列）、tableSpace （文字列）、tableSpaceIndex （文字列）、target (MNTOKEN)、templaryTable （文字列）、translatedDefault （文字列）、translatedExpr （文字列）、type (MNTOKEN))、非連結(boolean)、ユーザー(boolean)、userEnum(string)、visibleIf(string)、xml(boolean)、xmlChildren(boolean)

### 親 {#parents-4}

`<srcschema>`

`<element>`

### 子 {#children-4}

* `<attribute>`
* `<compute-string>`
* `<dbindex>`
* `<default>`
* `<element>`
* `<help>`
* `<join>`
* `<key>`
* `<sysfilter>`
* `<translateddefault>`

### 説明 {#description-4}

Adobe Campaignには4種類のエレメ `<element>` ントがあります。

* ルート `<element>` :スキーマに一致するSQLテーブルの名前を定義します。
* 構造 `<element>` :または要素のグループを `<element>` 定義し `<attribute>` ます。
* リンク `<element>` :リンクを定義します。 この要素には「@type=link」属性を含める必要があります。
* XML `<element>` :テキストタイプ「mData」フィールドを定義します。 この要素には「@type=xml」属性を含める必要があります。

### 属性の説明 {#attribute-description-4}

* **_operation (string)**:データベースに書き込む書き込みの種類を定義します。

   この属性は、主に標準のスキーマを拡張する際に使用されます。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:調整のみ。 つまり、Adobe Campaignは、要素を更新せずに回復し、要素が存在しない場合はエラーを生成します。
   * &quot;insertOrUpdate&quot;:挿入時に更新します。 つまり、Adobe Campaignは要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 つまり、要素が存在しない場合は、Adobe Campaignが要素を更新するか、エラーを生成します。
   * &quot;delete&quot;:削除。 つまり、Adobe Campaignは要素を回復および削除します。

* **advanced(boolean)**:このオプションを有効にすると(@advanced=&quot;true&quot;)、フォーム内のリストを設定するためにアクセス可能なフィールドのリストの属性を非表示にできます。
* **集計（文字列）**:別のスキーマを介しての定義をコ `<element>` ピーできます。 この属性は、「namespace:name」の形式でスキーマ宣言を受け取ります。
* **applicableIf (string)**:インデックスを適用する条件。 この属性はXTK式を受け取ります。
* **autopk (boolean)**:このオプションが有効な場合(autopk=&quot;true&quot;)、一意のキーが自動的に定義されます。 このオプションは、スキーマのメイン要素でのみ使用できます。 警告：Adobe Campaignは、生成されたキーが一意であることのみを保証します。 キー値が連続して増分されていることは保証されません。
* **dataPolicy (string)**:sqlフィールドで許可される値に対する承認制約を指定できます。 この属性の値は次のとおりです。

   * &quot;none&quot;:値なし
   * &quot;smartCase&quot;:先頭文字大文字
   * &quot;lowerCase&quot;:小文字
   * &quot;upperCase&quot;:大文字
   * &quot;email&quot;:電子メールアドレス
   * &quot;phone”:電話番号
   * &quot;識別子&quot;:識別子名
   * &quot;resIdentifier&quot;:ファイル名

* **dbEnum (string)**:「閉じた」列挙の内部名を受け取ります。 列挙値は、で定義する必要があります `<srcschema>`。
* **defOnDuplicate (boolean)**:この属性がアクティブな場合、レコードが重複すると、デフォルト値（@defaultで定義）がレコードに自動的に再適用されます。
* **default（文字列）**:要素の動作（関数の呼び出し、デフォルト値）を定義できます。 この属性はXTK式を受け取ります。
* **desc（文字列）**:要素の説明を挿入できます。 この説明は、インターフェイスのステータスバーに表示されます。
* **displayAsField (boolean)**:この属性がアクティブ化されると、「リンク」タイプが `<element>` スキーマのツリービューにフィールドとして表示されます（「構造」タブ）。 これにより、リンクをローカルフィールドとして表示し、クエリ中の動作を変更することができます。 クエリーのSELECTで要素が見つかると、リンクターゲットの値が使用されます。 クエリのWHEREに要素が見つかると、リンクの基になるキーが使用されます。
* **編集（文字列）**:この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum (string)**:フィールドにリンクされた列挙の名前を受け取ります。 列挙は、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**:この属性は、テーブルに定義が保存されていない計算済みフィールドを定義します。 XpathまたはXTK （文字列）式を受け取ります。
* **externalJoin (boolean)**:「リンク」タイプ要素の外部結合。
* **feature (string)**:特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張する目的で使用されますが、別のテーブルに保存する目的で使用されます。 指定できる値は次のとおりです。

   * &quot;shared&quot;:コンテンツは、データ型ごとに共有テーブルに保存されます
   * &quot;dedicated&quot;:コンテンツは専用のテーブルに保存される
   SQL特性テーブルは、次の特性タイプに基づいて自動的に作成されます。

   * dedicated: `Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`
   特性フィールドには2種類あります。単一の値が特性に対して承認される単純なフィールドと、複数の値を含む収集要素にリンクされる複数選択フィールド。

   スキーマで特性を定義する場合、このスキーマは単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されません）。

* **featureDate (boolean)**:属性が「@feature」特性フィールドにリンクされている。 値が「true」の場合は、値が最後に更新された日時を確認できます。
* **filterPath (string)**:この属性はXpathを受け取り、フィールドに対してフィルターを定義できます。
* **folderLink (string)**:この属性は、エンティティを含むファイルを回復するためのリンクの名前を受け取ります。
* **folderModel (string)**:エンティティの保存を有効にするフォルダーのタイプを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **folderProcess (string)**:エンティティモデルインスタンスが保存されるリンクを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **fullLoad (boolean)**:この属性は、フォーム内のフィールド選択中に、テーブル内のすべてのレコードを強制的に表示します。
* **img (string)**:は、要素にリンクされた画像のパスを受け取ります。 この属性の値は、「namespace:image name」タイプです。 例：img=&quot;cus:myImage.jpg&quot;. 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **整合性（文字列）**:ターゲット・テーブルに対するソース・テーブルのオカレンスの参照整合性。

   アクセス可能な値は次のとおりです。

   * &quot;define&quot;:Adobe Campaignは、リンクを介して参照されているエンティティを削除しません。
   * &quot;normal&quot;:ソースオカレンスを削除すると、ターゲットオカレンス上のリンクのキーが初期化されます（デフォルトモード）。このタイプの整合性は、すべての外部キーを初期化します
   * &quot;own&quot;:ソースオカレンスを削除すると、ターゲットオカレンスの削除がトリガーされます
   * &quot;owncopy&quot;:「own」（削除の場合）または重複回数（複製の場合）に似ている
   * &quot;neutral&quot;:何もしない

* **label (string)**:要素のラベル。
* **labelSingular (string)**:インターフェイスの一部で使用される要素のラベル（単数形）。
* **length (string)**:最大 「文字列」型のSQLフィールドの値に対して許可された文字の数。
* **localizable (boolean)**:この属性がアクティブ化されている場合、この属性は、翻訳（内部使用）のために「@label」属性の値を回復するようコレクションツールに指示します。
* **name (MNTOKEN)**:テーブルの名前と一致する要素の内部名。 「@name」属性の値は短く、できれば英語で指定する必要があり、XMLにリンクされた命名の制約に従う必要があります。

   データベースにスキーマが書き込まれると、Adobe Campaignによってフィールド名に接頭辞が自動的に追加されます。

   * &quot;i&quot;:&#39;integer&#39;型のプレフィックス。
   * &quot;d&quot;:&#39;double&#39;型のプレフィックス。
   * &quot;s&quot;:文字列タイプのプレフィックス。
   * &quot;ts&quot;:「日付」タイプのプレフィックス。
   自律的な方法でテーブルの名前を定義するには、メインスキーマ要素の定義で「@sqltable」属性を使用する必要があります。

* **noDbIndex (boolean)**:要素のインデックスを作成しないように指定できます。
* **ordered (boolean)**:属性がアクティブ化される(ordered=&quot;true&quot;)と、Adobe Campaignは要素宣言のシーケンスをXMLコレクション要素内に維持します。
* **pkSequence (string)**:は、自動増分キーの計算に使用されるシーケンスの名前を受け取ります。 この属性は、自動増分キーがスキーマのルート要素で定義されている場合にのみ使用できます。
* **pkgStatus (string)**:パッケージのエクスポート時に、値はこの属性の値の関数として考慮されます。

   * &quot;always&quot;:要素は常に存在します
   * &quot;never&quot;:要素が存在しない
   * &quot;default (or nothing)&quot;:要素がデフォルトの要素でない場合、または内部フィールドでなく、他のインスタンスと互換性がない場合を除き、要素はエクスポートされます

* **ref (string)**:この属性は、複数のスキーマ（定義ファクタリング）で共有される>element>要素への参照を定義します。 定義は現在のスキーマにコピーされません。
* **必須（ブール値）**:この属性がアクティブ化されている(@required=&quot;true&quot;)場合、インターフェイス内でフィールドがハイライト表示されます。 フィールドのラベルは、フォームでは赤で表示されます。
* **revAdvanced (boolean)**:この属性を有効にすると、反対側のリンクが「詳細」リンクであることを指定します。
* **revCardinality (string)**:この属性は、2つのテーブル間のリンクのカーディナリティを定義します。 「リンク」タイプで使用されます `<element>`。

   次のような値を選択できます。

   * &quot;single&quot; :単純な1-1タイプのリンク
   * &quot;unbound&quot;:1-N型の収集リンク
   デフォルトでは、リンクの作成中に属性が指定されていない場合、基数は1 ～ nになります。

* **revDesc（文字列）**:この属性は、反対のリンクにリンクされた説明を受け取ります。
* **revExternalJoin (boolean)**:この属性を有効にすると、反対側のリンクに外部結合を強制できます。
* **revIntegrity (string)**:この属性は、ターゲット・スキーマの整合性を定義します。 「@integrity」属性と同じ値が許可されます。 デフォルトでは、Adobe Campaignはこの属性に「normal」値を与えます。
* **revLabel（文字列）**:反対のリンクのラベル。
* **revLink （文字列）**:反対のリンクの名前。 値が「_NONE_」の場合、宛先スキーマに対するリンクは作成されません。
* **revTarget （文字列）**:対象リンク。
* **sql (boolean)**:この属性がアクティブ化されると(@sql=&quot;true&quot;)、要素にxml=&quot;true&quot;プロパティが含まれている場合でも、SQL要素の保存が強制されます。
* **sqlname（文字列）**:テーブル作成中のフィールドの名前。 「@sqlname」を指定しない場合、「@name」属性の値がデフォルトで使用されます。 テーブルにスキーマを書き込むとき、フィールドの種類に応じて自動的に接頭辞が追加されます。
* **sqltable（文字列）**:スキーマのメイン要素の場合、この属性は、デフォルトで生成されたSQLテーブルの名前をオーバーロードします。 「@sqltable」を指定しない場合、デフォルトの名前は次のように構造化されます。namespace（先頭文字の大文字）の後にSrcSchema &quot;@name&quot;の値が続く。
* **tableSpace (string)**:この属性を使用すると、表の表領域を格納する新しいデータを指定できます(ルートで有効 `<element>`)。
* **tableSpaceIndex (string)**:この属性を使用すると、テーブルの新しいインデックス・ストレージ・テーブルスペースを指定できます(ルートで有効 `<element>`)。
* **target (MNTOKEN)**:テーブル間のリンクを作成する際に、ターゲット・スキーマの名前を受け取ります。 この属性は、「リンク」タイプの要素に対してのみ有効です。
* **template (string)**:この属性は、複数のスキーマで共有される `<element>` 要素への参照を定義します。 定義は自動的に現在のスキーマにコピーされます。
* **translatedDefault(string)**:「@default」属性が見つかった場合、「@translatedDefault」を使用すると、翻訳ツールによって収集される式を、@defaultで定義された式と一致するように再定義できます（内部使用）。
* **translatedExpr (string)**:「@expr」属性が見つかった場合、「@translatedExpr」属性を使用すると、「@expr」で定義された式に一致する式を再定義できます。この式は、翻訳ツールによって収集されます（内部使用）。
* **type (MNTOKEN)**:要素に格納されるデータのタイプを定義します。

   使用可能なタイプのリスト：

   * ANY
   * bin
   * blob
   * boolean
   * バイト
   * CDATA
   * datetime
   * datetimetz
   * datetimenotz
   * 日付
   * double
   * enum
   * float
   * html
   * int64
   * link
   * 長い
   * メモ
   * MNTOKEN
   * percent
   * primarykey
   * short
   * 文字列
   * 時間
   * 間隔
   * uuid

* **unbound (boolean)**:属性がアクティブ化されている(unbound=&quot;true&quot;)場合、リンクは1-N基数のコレクション要素として宣言されます。
* **userEnum (string)**:は、「open」列挙の内部名を受け取ります。 列挙値は、インターフェイス内のユーザーが定義できます。
* **xml（ブール値）**:このオプションを有効にすると、要素で定義されたすべての値がXMLのTEXTタイプ「mData」フィールドに格納されます。 つまり、これらのフィールドにはフィルターや並べ替えが設定されません。
* **xmlChildren (boolean)**:各子( `<element>  or  <attribute>   ) of the   <element>    element in an XML document.   </element>  </attribute> </element>`

## `<enumeration>` 要素 {#enumeration--element}

### コンテンツモデル {#content-model-5}

列挙：==(help| value)

### 属性 {#attributes-5}

* @basetype (string)
* @default（文字列）
* @desc（文字列）
* @label （文字列）
* @name（文字列）
* @template （文字列）

### 親 {#parents-5}

`<srcschema>`

### 子 {#children-5}

* `<help>`
* `<value>`

### 説明 {#description-5}

この要素を使用して、値の列挙を定義できます。 列挙は、定義されたスキーマに属していますが、別のスキーマを介してアクセスできます。

### 使用と使用の状況 {#use-and-context-of-use-4}

列挙は、スキーマの開始時（メイン要素が定義される前）に定義されます。

### 属性の説明 {#attribute-description-5}

* **basetype (string)**:列挙に格納される値のタイプ。

   使用可能なタイプのリスト：

   * ANY
   * bin
   * blob
   * boolean
   * バイト
   * CDATA
   * datetime
   * datetimetz
   * datetimenotz
   * 日付
   * DOMDocument
   * DOMElement
   * double
   * enum
   * float
   * html
   * int64
   * link
   * 長い
   * メモ
   * MNTOKEN
   * percent
   * primarykey
   * short
   * 文字列
   * 時間
   * 間隔
   * uuid

* **default（文字列）**:デフォルト値。 デフォルト値は、列挙で定義された値の1つでもかまいません。
* **desc（文字列）**:列挙の説明。
* **label (string)**:列挙ラベル。
* **name（文字列）**:列挙の内部名。
* **template (string)**:この属性は、複数のスキーマで共有される `<enumeration>` 要素への参照を定義します。 定義は自動的に現在のスキーマにコピーされます。

### 例 {#examples-4}

値がデータベースに格納される列挙値の例：

```
    <enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>

    <element label="Sample" name="Sample">
       <attribute dbEnum="myEnum" length="100" name="Number" required="true" type="string"/>
    </element>
```

デフォルト値を持つ列挙の定義：

```
 <enumeration basetype="byte" default="email" name="canal">
    <value label="Email" name="email" value="0"/> 
    <value label="Téléphone" name="phone" value="1"/>
    <value label="Call Center" name="callcenter" value="2"/>
 </enumeration>
```

## `<help>` 要素 {#help--element}

### コンテンツモデル {#content-model-6}

help:==EMPTY

### 属性 {#attributes-6}

なし

### 親 {#parents-6}

`<srcschema>`  ,  `<element>`   ,   `<attribute>`    ,    `<enumeration>`     ,     `<value>`      ,     `<param />`,      `<method />`

### 子 {#children-6}

なし

### 説明 {#description-6}

この要素では、要素または要素を説 `<element>` 明でき `<attribute>` ます。 テキストのみを含めることができ、データベースのXMLに保存されます。

### 属性の説明 {#attribute-description-6}

この要素には属性がありません。

### 例 {#examples-5}

```
<method name="CheckOperation" static="true"
      <helpchecks the validity of a campaign</help
...
</method> 
```

## `<join>` 要素 {#join--element}

### コンテンツモデル {#content-model-7}

join:==EMPTY

### 属性 {#attributes-7}

* @dstFilterExpr （文字列）
* @xpath-dst （文字列）
* @xpath-src（文字列）

### 親 {#parents-7}

`<element>`

### 子 {#children-7}

なし

### 説明 {#description-7}

SQLテーブル間の結合を作成するフィールドを定義できます。

### 使用と使用の状況 {#use-and-context-of-use-5}

要素 `<join>` は、親要素が「リンク」タイプの `<element>` 場合にのみ使用できます。 つまり、親要素で「@type=link」属性が宣言されている必要があります。

要素でリモート・テーブルの名前と名前空間を指定する必要はありま `<join>` せん。 親で指定する必要があります `<element>`。

慣例により、リンクはスキーマの末尾で定義されます。

リンクタ `<join>` イプ要素を定義する際に要素が指定されていない場合、リンクは自動的に両方のテーブルの主キーに配置されます。

### 属性の説明 {#attribute-description-7}

* **dstFilterExpr (string)**:この属性を使用すると、リモート・テーブルの有効な値の数を制限できます。
* **xpath-dst（文字列）**:この属性は、Xpath（リモートテーブルの@name属性）を受け取ります。
* **xpath-src（文字列）**:この属性はXpath（現在のスキーマの@name属性）を受け取ります。

### 例 {#examples-6}

現在のテーブルの「email」フィールドとリモートテーブルの「@compagny-id」フィールド間のリンク：

```
<join xpath-dst="@compagny-id" xpath-src="@email"/>
```

「EN」値を含む「@country」フィールドのコンテンツに基づいて、「cus:Country」テーブルに対するフィルターされたリンク：

```
<element name="StockEN" type="link" label="MyLink" target="cus:Stock">
   <join xpath-dst="@country" xpath-src="@code" dstFilterExpr="@country = 'EN'"/>
 </element>
```

## `<key>` 要素 {#key--element}

### コンテンツモデル {#content-model-8}

key:==keyfield

### 属性 {#attributes-8}

* @allowEmptyPart (boolean)
* @applicableIf (string)
* @internal (boolean)
* @label （文字列）
* @name (MNTOKEN)
* @noDbIndex (boolean)

### 親 {#parents-8}

`<element>`

### 子 {#children-8}

`<keyfield>`

### 説明 {#description-8}

この要素を使用すると、テーブル内のレコードを識別するためのキーを定義できます。

テーブルには少なくとも1つのキーが必要です。

### 使用と使用の状況 {#use-and-context-of-use-6}

原則として、キーはスキーマのメイン要素とインデックスの後に宣言されます。

キーに複数のフィールド（例：複数の子）が含まれる場合、キーは複合と呼ば `<keyfield>` れます。 複合キーを使用して主キーを定義しないでください。

スキーマのメイン要素に「@autopk=true」属性が含まれている場合、プライマリ・キーは一意です。 1つのスキーマにつき1つの主キーしか持つことができません。

最初の1000個の識別子は予約されているので、キーに対して値の範囲を定義する必要がある場合は、1000から始めます。

### 属性の説明 {#attribute-description-8}

* **allowEmptyPart (boolean)**:複合キーの場合、この属性が有効な場合、そのキーの少なくとも1つが空でないと、そのキーは有効と見なされます。 この場合、空の概念の値は「0」（ブール値またはすべてのタイプの数値データ）になります。 デフォルトでは、複合キーを構成するすべてのキーを入力する必要があります。
* **applicableIf (string)**:この属性を使用すると、キーをオプションにできます。 キー定義を適用する条件を定義します。 この属性はXTK式を受け取ります。
* **internal (boolean)**:この属性を有効にすると、Adobe Campaignにそのキーがプライマリキーであることを通知します。
* **label (string)**:キーのラベル。
* **name (MNTOKEN)**:キーの内部名。
* **noDbIndex (boolean)**:アクティブ化された場合(noDbIndex=&quot;true&quot;)、キーに一致するフィールドのインデックスは作成されません。

### 例 {#examples-------}

「@expr」または「alias」フィールドを空にすることを許可する複合キーの宣言：

```
<key name="node" allowEmptyPart="true">
  <keyfield xpath="@expr"/>
   <keyfield xpath="@alias"/>
 </key>
```

STRING型の「Name」フィールドでの主キーの宣言と、一致するSQLク `<srcschema>` エリ：

```
 
<key name="PrimaryKey" internal="true">  
  <keyfield xpath="@name"/>
</key>

CREATE UNIQUE INDEX Schema_PrimaryKey ON Schema(sName);
```

## `<keyfield>` 要素 {#keyfield--element}

### コンテンツモデル {#content-model-9}

keyfield:==EMPTY

### 属性 {#attributes-9}

* @xlink (MNTOKEN)
* @xpath (MNTOKEN)

### 親 {#parents-9}

`<key>`  ,  `<dbindex />`

### 子 {#children-9}

なし

### 説明 {#description-9}

この要素は、インデックスまたはキーに統合するフィールドを定義します。

### 属性の説明 {#attribute-description-9}

* **xlink (MNTOKEN)**:リレーションテーブル（N-Nリンク）のジョインで定義された外部キーを自動的に参照できます。
* **xpath (MNTOKEN)**:要素のインデックスまたはキーの定 `<attribute>` 義。 この属性は、キーまたはインデックスを定義するスキーマ属性へのパスを定義するXpathを受け取ります。

### 例 {#examples-}

「@name」上のXpathを持つインデックス内の「sName」フィールドを選択します。

```
<keyfield xpath="@name"/>
```

## `<method>` 要素 {#method--element}

### コンテンツモデル {#content-model-10}

method:==（ヘルプ）|パラメーター)

### 属性 {#attributes-10}

* @_operation （文字列）
* @access （文字列）
* @const (boolean)
* @hidden (boolean)
* @label （文字列）
* @library (string)
* @name (MNTOKEN)
* @pkonly （ブール値）
* @static（ブール値）

### 親 {#parents-10}

`<methods>`  ,  `<interface />`

### 子 {#children-10}

* `<help>`
* `<parameters>`

### 説明 {#description-10}

この要素を使用して、SOAPメソッドを定義できます。

### 使用と使用の状況 {#use-and-context-of-use-7}

SOAPメソッドは、アプリケーションプロセスを有効にします。

「@library」は、新しいメソッド（非ネイティブ）を宣言するために必要です。ライブラリに使用される名前空間と名前は、宣言が存在するスキーマの名前空間と名前とは独立しています。

### 属性の説明 {#attribute-description-10}

* **access (string)**:この属性は、メソッドを使用するためのアクセス制御を定義します。 この属性がない場合、識別は必須です。 次の値を使用できます。「anonymous」、「admin」および「sql」。
* **const (boolean)**:この属性が有効な場合、宣言されたメソッドがエンティティを変更することを意味します
* **label (string)**:メソッドのラベル。
* **library (string)**:このメソッドは、アプリケーションにネイティブではありません。 この属性は、メソッド定義が存在するメソッドライブラリの値(nms:mylibrary.js)を取ります。
* **name (MNTOKEN)**:一意のメソッド名。
* **static(boolean)**:この属性が有効な場合、メソッドは自律型であると見なされ、呼び出し時にメソッドにすべてのパラメータを指定する必要があります。

### 例 {#examples-7}

初期設定の「購読」メソッドの定義：

```
 
<method name="Subscribe" static="true">
      <help>Creation of update of a recipient's subscription to an information service</help>
      <parameters>
        <param desc="Name of the information service(s) (separated with commas)"
               name="serviceName" type="string"/>
        <param desc="Recipient to subscribe and possibly create" name="recipient"
               type="DOMElement"/>
        <param desc="Create the recipient if they don't exist" name="create" type="boolean"/>
      </parameters>     
    </method>
```

## `<methods>` 要素 {#methods--element}

### コンテンツモデル {#content-model-11}

メソッド：==method

### 属性 {#attributes-11}

なし

### 親 {#parents-11}

`<srcschema>`

### 子 {#children-11}

method

### 説明 {#description-11}

この要素を使用して、要素を定義で `<method>` きます。 メソッドを宣言する場合は必須です。

### 属性の説明 {#attribute-description-11}

この要素には属性がありません。

### 例 {#examples-8}

```
<methods async="true"
...// definition of one or more <method
</methods>
```

## `<param>` 要素 {#param--element}

### コンテンツモデル {#content-model-12}

param:==help

### 属性 {#attributes-12}

* @_operation （文字列）
* @desc（文字列）
* @enum （文字列）
* @inout （文字列）
* @label （文字列）
* @localizable (string)
* @name (MNTOKEN)
* @namespace (MNTOKEN)
* @type （文字列）

### 親 {#parents-12}

`<parameters>`

### 子 {#children-12}

`<help>`

### 説明 {#description-12}

この要素を使用すると、SOAPメソッドを呼び出すためのパラメーターを定義できます。

### 属性の説明 {#attribute-description-12}

* **desc（文字列）**:要素に関する説明 `<param>` です。
* **inout (string)**:この属性は、パラメーターがSOAP呼び出しの入力(in)または出力(out)にあるかどうかを定義します。 この属性を指定しない場合、デフォルトのパラメーターはinput (&quot;@inout=in&quot;)です。
* **label (string)**: `<param>` ラベル
* **localizable (string)**:この属性がアクティブ化されている場合、この属性は、翻訳（内部使用）のために「@label」属性の値を回復するようコレクションツールに指示します。
* **name (MNTOKEN)**:内部名 `<param>`
* **type (string)**:この属性は要素のタイプを定義しま `<param>` す

   使用可能なタイプのリスト：

   * ANY
   * bin
   * blob
   * boolean
   * バイト
   * CDATA
   * datetime
   * datetimetz
   * datetimenotz
   * 日付
   * DOMDocument
   * DOMElement
   * double
   * enum
   * float
   * html
   * int64
   * link
   * 長い
   * メモ
   * MNTOKEN
   * percent
   * primarykey
   * short
   * 文字列
   * 時間
   * 間隔
   * uuid

### 例 {#examples-9}

文字列タイプの「serviceName」受信設定の定義：

```
<param desc="Name of the information service(s) (separated with commas)"
               name="serviceName" type="string" inout="in"/>
```

## `<parameters>` 要素 {#parameters--element}

### コンテンツモデル {#content-model-13}

パラメーター：==param

### 属性 {#attributes-13}

なし

### 親 {#parents-13}

`<method>`

### 子 {#children-13}

`<param>`

### 説明 {#description-13}

この要素は要素のグループを定義 `<parameter>` します。

### 使用と使用の状況 {#use-and-context-of-use-8}

この要素は、要素の子要素が1つでも必 `<param>` 須の要素で `<method>` す。

### 属性の説明 {#attribute-description-13}

なし

### 例 {#examples-10}

```
<parameters
... //definition of one or more <param
</parameters>
```

## `<srcschema>` 要素 {#srcschema--element}

### コンテンツモデル {#content-model-14}

srcSchema:=(attribute)| createdBy| data|要素|列挙|ヘルプ|インターフェイス|メソッド| modifiedBy)

### 属性 {#attributes-14}

created (datetime)、createdBy-id (long)、desc (string)、entitySchema (string)、extendedSchema (string)、implements (string)、label (string)、lastModified (string)、library (boolean)、mappingType (string)、modifiedBy-id (long)、name (string)、name (string)、namespace)useRecycleBin (boolean)、view (boolean)、xtkschema (string)

### 親 {#parents-14}

なし

### 子 {#children-14}

* `<attribute>`
* `<createdby>`
* `<data>`
* `<element>`
* `<enumeration>`
* `<help>`
* `<interface>`
* `<methods>`
* `<modifiedby>`

### 説明 {#description-14}

はス `<srcschema>` キーマのルート要素です。 スキーマの定義の入力ポイントです。

### 使用と使用の状況 {#use-and-context-of-use-9}

スキーマ表示は、「スキーマ参照につ [いて](../../configuration/using/about-schema-reference.md) 」と「スキー [マ構造」で使用できます](../../configuration/using/schema-structure.md)。

### 属性の説明 {#attribute-description-14}

* **作成日時**:この属性は、スキーマの作成日時に関する情報を提供します。 「日付時刻」のフォームがあります。 表示される値はサーバーから取得されます。 時刻はUTC形式で表示されます。
* **createdBy-id (long)**:は、スキーマを作成した演算子の識別子です。
* **desc（文字列）**:スキーマ記述
* **entitySchema (string)**:構文と承認が基になる基本スキーマ(Adobe Campaignのデフォルト：xtk:srcSchema)。 現在のスキーマを保存すると、Adobe Campaignは、@xtkschema属性で宣言されたスキーマを使用して文法を承認します。
* **extendedSchema (string)**:は、現在のスキーマ拡張の基になる、あらかじめ用意されているスキーマの名前を受け取ります。 フォームは「namespace:name」です。
* **img (string)**:アイコンがスキーマにリンクされている（スキーマ作成ウィザードで定義できる）。
* **label (string)**:スキーマラベル。
* **labelSingular (string)**:label（単数形）は、インターフェイスに表示されます。
* **lastModified (datetime)**:この属性は、最後の変更の日時に関する情報を提供します。 「日付時刻」のフォームがあります。 表示される値はサーバーから取得されます。 時刻はUTC形式で表示されます。
* **library (boolean)**:スキーマをエンティティではなくライブラリとして使用する。 したがって、このスキーマは「@ref」および「@template」属性によって他のスキーマから参照される場合があります。
* **mappingType (string)**:

   * &quot;sql&quot;:データベースマッピング
   * &quot;textFile&quot;:テキストファイルマッピング
   * &quot;xmlFile&quot;:XML形式のテキストファイルマッピング
   * &quot;binaryFile&quot;:バイナリファイルマッピング

* **modifiedBy-id (long)**:スキーマを変更した演算子の識別子に一致します。
* **name（文字列）**:一意のスキーマ名。
* **namespace (string)**:スキーマの名前空間(デフォルト：nms、xtk、nl)。 プロジェクト用に新しいスキーマを作成する場合は、専用の名前空間を使用することをお勧めします。
* **useRecycleBin (boolean)**:アプリケーションのごみ箱機能をアクティブにします。 削除したレコードは、最終的に削除する前にごみ箱に入れられます。 この関数は、「配信」モードでのみ使用できます。
* **view (boolean)**:アクティブ化(@view=&quot;true&quot;)されると、スキーマがビューとして使用されます。 データベース構造の更新ウィザードでは、スキーマは考慮されません。 このオプションは、主に外部テーブルを参照するために使用します。
* **xtkschema （文字列）**:スキーマ文法を定義するスキーマの名前（デフォルトではxtk:srcSchema）。

### 例 {#examples-11}

`<srcschema>` 要素（初期設定のスキーマから「nms:delivery」）

```
<srcSchema desc="Defines all the settings of a delivery (or delivery template)."  
           entitySchema="xtk:srcSchema" img="nms:campaign.png" implements="xtk:persist" 
           label="Diffusions" labelSingular="Diffusion" md5="DCD2164CD0276B1DCA6E1C9E2A75EC04"
           name="delivery" namespace="nms" useRecycleBin="true" xtkschema="xtk:srcSchema">
```

## `<sysfilter>` 要素 {#sysfilter--element}

### コンテンツモデル {#content-model-15}

sysFilter:==condition

### 属性 {#attributes-15}

なし

### 親 {#parents-15}

`<element>`

### 子 {#children-15}

`<condition>`

### 説明 {#description-15}

この要素を使用して、フィルターを定義できます。

### 属性の説明 {#attribute-description-15}

この要素には属性がありません。

### 例 {#examples-12}

@name属性に条件を持つフィルターの定義：

```
<sysFilter>
      <condition expr="@name ='Doe'"/>
  <sysFilter>
```

## `<value>` 要素 {#value--element}

### コンテンツモデル {#content-model-16}

value:==help

### 属性 {#attributes-16}

* @applicableIf (string)
* @desc（文字列）
* @enabledIf (string)
* @img (string)
* @label （文字列）
* @name（文字列）
* @value （文字列）

### 親 {#parents-16}

`<enumeration>`

### 子 {#children-16}

`<help>`

### 説明 {#description-16}

この要素を使用すると、列挙に格納される値を定義できます。

### 属性の説明 {#attribute-description-16}

* **applicableIf (string)**:この属性を使用すると、列挙値をオプションにできます。 XTK式を受け取ります。
* **desc（文字列）**:列挙値の説明。
* **enabledIf (string)**:列挙値をアクティブ化する条件。
* **img (string)**:「namespace:image_name」フォーム内の列挙にリンクされた画像。 画像は、アプリケーションサーバーに読み込む必要があります。
* **label (string)**:列挙値のラベル。
* **name（文字列）**:列挙値の内部名。
* **value（文字列）**:列挙値の値。 値のタイプは、列挙のタイプに基づいて定義されます。 列挙が文字列タイプの場合は、文字列タイプの値のみを含めることができます。

### 例 {#examples-13}

```
<enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>
```
