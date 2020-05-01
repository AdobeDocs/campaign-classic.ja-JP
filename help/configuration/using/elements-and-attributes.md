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
source-git-commit: a2cb740fe9b71435f602b738bd270fd3a0954901

---


# 要素と属性 {#elements-and-attributes}

スキーマの編集時には、ソーススキーマ(xtk:srcSchema)に基づく承認システムを使用できます。 「Database structure update...」を使用してデータベースを更新する際に、エラーが発生する場合もあります。 ウィザード。

デフォルトでは、Adobe Campaignスキーマでは、すべてのBoolean型属性は「false」です。 これらをアクティブにするには、スキーマで属性を指定し、その値を「true」に設定する必要があります。

## `<attribute>` element {#attribute--element}

### コンテンツモデル {#content-model}

attribute:==help

### 属性 {#attributes}

_operation (string)、advanced (boolean)、applicableIf (string)、autoIncrement (boolean)、belonsTo (string)、dataPolicy (string)、dbEnum (string)、defOnDuplicate (boolean)、default (string)、eature (string)、featureDate (boolean)img （文字列）、inout （文字列）、label （文字列）、length （文字列）、localizable (boolean)、name (MNTOKEN)、notNull (boolean)、pkgStatus （文字列）、ref （文字列）、required (boolean)、sqlDefault （文字列）、sqlname （文字列）、ターゲット（文字列）、template （文字列）translatedDefault(string)、translatedExpr(string)、type(MNTOKEN)、user(boolean)、userEnum(string)、visibleIf(string)、xml(boolean)

### 親 {#parents}

`<element>`

### 子 {#children}

`<help>`

### 説明 {#description}

`<attribute>` 要素を使用すると、データベース内でフィールドを定義できます。

### 使用と使用の状況 {#use-and-context-of-use}

`<attribute>` 要素は、 `<element>` 要素内で宣言する必要があります。

内で `<attribute>` 要素が定義される順序は、データベース内のフィールド作成の順序には影響しま `<srcschema>` せん。 作成シーケンスはアルファベット順になります。

### 属性の説明 {#attribute-description}

* **_operation (string)**: データベースに書き込むタイプを定義します。

   この属性は主に、標準搭載されたスキーマを拡張する場合に使用します。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;: 和解のみ。 つまり、Adobe Campaignは、要素を更新せずに回復します。要素が存在しない場合はエラーが発生します。
   * &quot;insertOrUpdate&quot;: 挿入時に更新します。 つまり、Adobe Campaignは、要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;: 挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;: 更新。 これは、Adobe Campaignが要素を更新するか、存在しない場合はエラーを生成することを意味します。
   * &quot;delete&quot;: 削除。 つまり、Adobe Campaignは要素を回復および削除します。

* **advanced(boolean)**: このオプションをアクティブ化すると(@advanced=&quot;true&quot;)、フォーム内のリストの設定にアクセスできるフィールドのリスト上で属性を非表示にできます。
* **applicableIf (string)**: この属性を使用すると、フィールドをオプションにできます。 制約が適合している場合は、データベースを更新する際に `<attribute>` 要素が考慮されます。 &quot;applicableIf&quot;がXTK式を受け取ります。
* **autoIncrement (boolean)**: このオプションを有効にすると、フィールドはカウンターになります。 これにより、値を増やすことができます（ほとんどの場合ID）。 （外部使用）
* **belongsTo (string)**: フィールドを共有するテーブルの名前と名前空間を取得し、属性が宣言されているスキーマに値を設定します。 (aでのみ使用 `<schema>`)。
* **dataPolicy (string)**: 「SQL or XML」フィールドで許可される値に対して、承認制約を指定できます。 この属性の値は次のとおりです。

   * &quot;none&quot;: 値なし
   * &quot;smartCase&quot;: 大文字の先頭文字
   * &quot;lowerCase&quot;: 小文字全体
   * &quot;upperCase&quot;: 大文字のみ
   * &quot;email&quot;: 電子メールアドレス
   * &quot;phone&quot;: 電話番号
   * &quot;識別子&quot;: 識別子名
   * &quot;resIdentifier&quot;: ファイル名

* **dbEnum (string)**: は、「閉じた」定義済みリストの内部名を受け取ります。 定義済みリスト値は、で定義する必要があり `<srcschema>`ます。
* **defOnDuplicate (boolean)**: この属性がアクティブな場合、レコードが重複するときに、（@defaultで定義された）デフォルト値が自動的にレコードに再適用されます。
* **default（文字列）**: デフォルトのフィールドの値（関数の呼び出し、デフォルト値）を定義できます。 この属性はXTK式を受け取ります。
* **desc（文字列）**: 属性の説明を挿入できます。 この説明は、インターフェイスのステータスバーに表示されます。
* **編集（文字列）**: この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum（文字列）**: は、フィールドにリンクされている定義済みリストの名前を受け取ります。 定義済みリストは、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**: フィールドの事前計算式を定義します。 この属性は、XpathまたはXTK式を受け取ります。
* **機能（文字列）**: 特性フィールドを定義します。 これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルのストレージと共に使用されます。 指定できる値は次のとおりです。

   * &quot;共有&quot;: コンテンツは、データ型ごとに共有テーブルに保存されます
   * &quot;dedicated”: コンテンツは専用のテーブルに格納される
   SQL特性テーブルは、次の特性タイプに基づいて自動的に作成されます。

   * dedicated: `Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`
   次の2種類の特性フィールドがあります。 単一の値が特性に対して承認される単純なoa headフィールドと、oa hecoseフィールドです。このフィールドでは、特性が複数の値を含む収集要素にリンクされます。

   特性がスキーマで定義される場合、このスキーマは、単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されません）。

* **featureDate (boolean)**: 属性が「@feature」特性フィールドにリンクされている。 値が「true」の場合は、値が最後に更新された日時を確認できます。
* **img （文字列）**: フィールドにリンクされた画像のパス(名前空間+画像名)を定義できます(例： img=&quot;cus:mypicture.jpg&quot;)。 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **label (string)**: フィールドにリンクされているラベル。ほとんどの場合、インターフェイス内のユーザーにリンクされているラベルです。 命名の制約を回避できます。
* **length (string)**: 最大 「string」型SQLフィールドの値の文字数。 「@length」属性が指定されていない場合、Adobe Campaignは255文字のフィールドを自動的に作成します。
* **localizable (boolean)**: この属性がアクティブ化されている場合、収集ツールに対して翻訳用の「@label」属性の値の復元（内部使用）を指示します。
* **name (MNTOKEN)**: テーブルのフィールドの名前と一致する属性の名前。 「@name」属性の値は、短く、できれば英語で指定し、XMLの命名規則に従う必要があります。

   スキーマがデータベースに書き込まれると、フィールド名にプリフィックスがAdobe Campaign別に自動的に追加されます。

   * &quot;i&quot;: プレフィックスの値を指定します。
   * &quot;d&quot;: プレフィックスが表示されます。
   * &quot;s&quot;: のプレフィックスを指定します。
   * &quot;ts&quot;: プレフィックスに値を入力します。
   テーブル内のフィールドの名前を完全に定義するには、属性を定義する際に「@sqlname」オプションを使用します。

* **notNull (boolean)**: データベース内のNULLレコードの管理に関するAdobe Campaignの動作を再定義できます。 デフォルトでは、数値フィールドはnullではなく、文字列フィールドおよび日付型フィールドはnullにできます。
* **pkgStatus (string)**: パッケージのエクスポート中、「@pkgStatus」の値に応じて値が考慮されます。

   * &quot;always&quot;: 常に存在する
   * &quot;never&quot;: 存在しない
   * &quot;default (or nothing)&quot;: デフォルト値である場合や、他のインスタンスと互換性がない内部フィールドでない場合を除き、値がエクスポートされます。

* **ref （文字列）**: この属性は、複数のスキーマ（定義ファクタリング）が共有する `<attribute>` 要素への参照を定義します。 定義は現在のスキーマにコピーされません。
* **required (boolean)**: この属性がアクティブ化された場合(@required=&quot;true&quot;)、インターフェイスでフィールドがハイライト表示されます。 フィールドのラベルは、フォームでは赤で表示されます。
* **sql (boolean)**: この属性がアクティブ化される(@sql=&quot;true&quot;)と、属性を含む要素にxml=&quot;true&quot;プロパティが含まれている場合でも、SQL属性のストレージが強制されます。
* **sqlDefault (string)**: この属性を使用すると、@notNull属性がアクティブ化されている場合に、データベースの更新に使用されるデフォルト値を定義できます。 属性の作成後にこの属性を追加した場合、新しいレコードでもスキーマの動作は変更されません。 スキーマを変更し、新しいレコードの値を更新するには、属性を削除して、もう一度作成する必要があります。
* **sqlname （文字列）**: の値を含む)を設定する必要があります。 @sqlnameを指定しない場合、「@name」属性の値がデフォルトで使用されます。 スキーマがデータベースに書き込まれると、フィールドの種類に応じてプリフィックスが自動的に追加されます。
* **template (string)**: この属性は、複数のスキーマが共有する `<attribute>` 要素への参照を定義します。 定義は自動的に現在のスキーマにコピーされます。
* **translatedDefault(string)**: 「@default」属性が見つかった場合、「@translatedDefault」を使用すると、式を再定義して、翻訳ツールによって収集される@defaultで定義されているのと一致させることができます（内部使用）。
* **translatedExpr (string)**: 「@expr」属性が存在する場合、「@translatedExpr」属性を使用すると、式を再定義して@exprで定義されているものと一致させ、翻訳ツールによって収集されるようにすることができます（内部使用）。
* **type (MNTOKEN)**: フィールドタイプ。

   フィールドタイプは汎用です。 Adobe Campaignは、インストールされているデータベースの種類に応じて、定義された型を、構造の更新時にインストールされたデータベースに固有の値に変更します。

   使用可能なタイプのリスト:

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
   * 重複
   * 列挙
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
   「@type」属性を空のままにした場合、Adobe Campaignは、デフォルトで長さ100の文字列(STRING)をフィールドにリンクします。

   フィールドのタイプがSTRINGで、フィールドの名前が「@sqlname」属性の存在で指定されていない場合、データベース内のフィールドの名前の前に自動的に「s」が付きます。 この動作モードは、INTEGER (i)、重複(d)、およびDATES (ts)タイプのフィールドと同様です。

* **userEnum (string)**: は、「open」定義済みリストの内部名を受け取ります。 定義済みリストの値は、インターフェイス内のユーザーが定義できます。
* **visibleIf (string)**: 属性の表示/非表示を切り替える条件をXTK式の形式で定義します。

   >[!IMPORTANT]
   >
   >属性は非表示になりますが、そのデータにはアクセスできます。

* **xml（ブール値）**: このオプションが有効になっている場合、フィールドの値にリンクされたSQLフィールドはありません。 Adobe Campaignは、レコードストレージ用にテキストタイプ「mData」フィールドを作成します。 これは、これらのフィールドに対してフィルタや並べ替えが行われていないことを意味します。

### 例 {#examples}

データベースに値が格納される定義済みリスト値の例：

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

「@applicableIf」の例： 「次を含む」属性は、国数が20を超える場合にのみ作成されます。

```
<attribute length="100" name="Continent" type="string" applicableIf="@country > 20"/>
```

「共有」タイプの「@feature」の例：

```
<attribute name="field1" label="Field 1" type="long" feature="shared"/>
<attribute name="field1" label="Field 1" type="long" feature="shared" sqlname="126" sqltable="Ft_Content_Long"/>
```

「@feature」が「dedicated」タイプの例：

```
<attribute name="field1" label="Field 1" type="long" feature="dedicated"/>
<attribute name="field1" label="Field 1" type="long" feature="dedicated" sqlname="sField1" sqltable="Ft_recipient_field1"/>
```

## `<compute-string>` element {#compute-string--element}

### コンテンツモデル {#content-model-1}

compute-string:==EMPTY

### 属性 {#attributes-1}

@expr

### 親 {#parents-1}

`<element>`

### 子 {#children-1}

なし

### 説明 {#description-1}

この `<compute-string>` 要素を使用すると、XTK式に基づく文字列を生成し、いくつかの値に基づいて「組み込み」ラベルをインターフェイスに表示できます。

### 使用と使用の状況 {#use-and-context-of-use-1}

を定義し `<compute-string>` ない場合、デフォルトでは、スキーマ内の主キーの値を使用して `<compute-string>` 要素が入力されます。

### 属性の説明 {#attribute-description-1}

* **expr（文字列）**: XTKやXpathの式

### 例 {#examples-1}

```
<compute-string expr="@label + Iif(@code='','', ' (' + [folder/@label] + ')')"/>  
<compute-string expr="ToString([@centralCatalog-id]) + ',' + ToString([@localOrgUnit-id])" />
```

受信者で計算された文字列の結果： &quot;John Doe (john.doe@aol.com)&quot;:

```
<element name="recipient">
<compute-string expr="@lastName + ' ' + @firstName +' (' + @email + ')'
"/>
...
</element>
```

## `<condition>` element {#condition--element}

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

1つの `<sysfiler>` 要素に複数のフィルター条件を含めることができます。

### 属性の説明 {#attribute-description-2}

* **boolOperator (string)**: 複数 `<conditions>` が同じ `<sysfilter>` 要素内で定義されている場合、この属性を使用してそれらを組み合わせることができます。 デフォルトでは、論理リンクは `<condition>` 要素間の「AND」です。 「@boolOperator」属性を使用すると、「OR」と「AND」タイプのリンクを組み合わせることができます。
* **enabledIf (string)**: 条件アクティベーションテスト。
* **expr（文字列）**: XTK式。

### 例 {#examples-2}

```
<sysfilter>
  <condition enabledIf="hasNamedRight('admin')=false" expr="@city=[currentOperator/location/@city]" />
</sysfilter>
```

## `<dbindex>` element {#dbindex--element}

### コンテンツモデル {#content-model-3}

dbindex:==keyfield

### 属性 {#attributes-3}

* @_operation（文字列）
* @applicableIf (string)
* @label（文字列）
* @name (MNTOKEN)
* @unique（ブール値）

### 親 {#parents-3}

`<element>`

### 子 {#children-3}

`<keyfield>`

### 説明 {#description-3}

この要素を使用すると、テーブルにリンクされたインデックスを定義できます。

### 使用と使用の状況 {#use-and-context-of-use-3}

複数のインデックスを定義できます。 1つのインデックスで、テーブルの1つ以上のフィールドを参照できます。 インデックス宣言は、通常、メインスキーマ要素の定義に従います。

で定義される `<keyfield>` 要素の順序は非常に重要 `<dbindex>` です。 1つ目は、クエリが主に基づくインデクション基準で `<keyfield>` ある必要があります。

データベース内のインデックスの名前は、テーブルの名前とインデックスの名前を連結して計算されます。 次に例を示します。 インデックス作成クエリ中の、テーブル名「Sample」、名前空間「Cus」、インデックス名「MyIndex」 —>インデックスフィールドの名前： &quot;CusSample_myIndex&quot;.

### 属性の説明 {#attribute-description-3}

* **_operation (string)**: データベースに書き込むタイプを定義します。

   この属性は主に、標準搭載されたスキーマを拡張する場合に使用します。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;: 和解のみ。 つまり、Adobe Campaignは、要素を更新せずに回復します。要素が存在しない場合はエラーが発生します。
   * &quot;insertOrUpdate&quot;: 挿入時に更新します。 つまり、Adobe Campaignは、要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;: 挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;: 更新。 これは、Adobe Campaignが要素を更新するか、存在しない場合はエラーを生成することを意味します。
   * &quot;delete&quot;: 削除。 つまり、Adobe Campaignは要素を回復および削除します。

* **applicableIf (string)**: インデックスを考慮する条件 — XTK式を受け取ります。
* **label (string)**: indexラベル。
* **name (MNTOKEN)**: 一意のインデックス名。
* **unique (boolean)**: このオプションが有効な場合(@unique=&quot;true&quot;)、属性はフィールド全体でのインデックスの一意性を保証します。

### 例 {#examples-3}

「id」フィールドでのインデックスの作成。 ( `<dbindex>` 要素の「@unique」属性は、データベース(クエリ)にインデックスが作成されたときに、「UNIQUE」SQLキーワードの追加をトリガーします)。

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

「@mail」フィールドと「@phoneNumber」フィールドに複合インデックスを作成します。

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

## `<element>` element {#element--element}

### コンテンツモデル {#content-model-4}

element:=(attribute) | compute-string | dbindex |デフォルト |要素 |ヘルプ |結合 | key | sysFilter | translatedDefault)

### 属性 {#attributes-4}

_operation (string)、advanced (boolean)、集計(string)、applicableIf (string)、autopk (boolean)、belonsTo (string)、convDate (string)、dataSource (string)、defOnDuplicate (boolean)、desc (string)、displayAsField(boolean)、doesNotSupportDiff (boolean)、edit (string)、emptyKeyValue (string)、enum (string)、enumImage (string)、expandSchemaTarget (string)、expr (string)、externalJoin (boolean)、featureDate (boolean)、filerPath (string)、folderLink (string)folderModel（文字列）、folderProcess（文字列）、fullLoad（ブール値）、hierarchical（ブール値）、hierarchicalPath（文字列）、img（文字列）、inout（文字列）、integrity（文字列）、label（文字列）、length（文字列）、localizable（ブール値）、name(MNTOKEN)、noDbIndex（ブール値）（ブール値）、順序付き（ブール値）、オーバーフローテーブル（ブール値）、pkSequence（文字列）、pkgStatus（文字列）、ref（文字列）、revAdvanced（ブール値）、revCardinality（文字列）、revDesc（ブール値）、revExternalJoin（ブール値）、revIntegrity（文字列）、revLinLink文字列)、revTarget （文字列）、revVisibleIf （文字列）、sql （ブール値）、sqlname （文字列）、sqltable （文字列）、tableSpace （文字列）、tableSpaceIndex （文字列）、ターゲット(MNTOKEN)、template （文字列）、templateDefault （ブール値）、translatedExpr （文字列）、type （文字列）トークン)、連結されていない（ブール値）、ユーザー（ブール値）、userEnum（文字列）、visibleIf（文字列）、xml（ブール値）、xmlChildren（ブール値）

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

Adobe Campaignには4種類の `<element>` 要素があります。

* ルート `<element>` : スキーマに一致するSQLテーブルの名前を定義します。
* 構造 `<element>` : または要素のグループ `<element>` を定義し `<attribute>` ます。
* リンク `<element>` : リンクを定義します。 この要素には「@type=link」属性を含める必要があります。
* XML `<element>` : テキストタイプ「mData」フィールドを定義します。 この要素には「@type=xml」属性を含める必要があります。

### 属性の説明 {#attribute-description-4}

* **_operation (string)**: データベースに書き込むタイプを定義します。

   この属性は主に、標準搭載されたスキーマを拡張する場合に使用します。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;: 和解のみ。 つまり、Adobe Campaignは、要素を更新せずに回復します。要素が存在しない場合はエラーが発生します。
   * &quot;insertOrUpdate&quot;: 挿入時に更新します。 つまり、Adobe Campaignは、要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;: 挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;: 更新。 これは、Adobe Campaignが要素を更新するか、存在しない場合はエラーを生成することを意味します。
   * &quot;delete&quot;: 削除。 つまり、Adobe Campaignは要素を回復および削除します。

* **advanced(boolean)**: このオプションをアクティブ化すると(@advanced=&quot;true&quot;)、フォーム内のリストの設定にアクセスできるフィールドのリスト上で属性を非表示にできます。
* **集計（文字列）**: 別のスキーマーを `<element>` 介しての定義をコピーできます。 この属性は、「名前空間：名前」の形式のスキーマ宣言を受け取ります。
* **applicableIf (string)**: インデックスを適用する条件。 この属性はXTK式を受け取ります。
* **autopk (boolean)**: このオプションが有効な場合(autopk=&quot;true&quot;)、一意のキーが自動的に定義されます。 このオプションは、スキーマのメイン要素でのみ使用できます。 警告：Adobe Campaignは、生成されたキーが一意であることを保証するだけです。 キー値が連続していて増分的であることは保証されません。
* **dataPolicy (string)**: 「SQL」フィールドで許可される値に対して、承認制約を指定できます。 この属性の値は次のとおりです。

   * &quot;none&quot;: 値なし
   * &quot;smartCase&quot;: 大文字の先頭文字
   * &quot;lowerCase&quot;: 小文字全体
   * &quot;upperCase&quot;: 大文字のみ
   * &quot;email&quot;: 電子メールアドレス
   * &quot;phone&quot;: 電話番号
   * &quot;識別子&quot;: 識別子名
   * &quot;resIdentifier&quot;: ファイル名

* **dbEnum (string)**: は、「閉じた」定義済みリストの内部名を受け取ります。 定義済みリスト値は、で定義する必要があり `<srcschema>`ます。
* **defOnDuplicate (boolean)**: この属性がアクティブな場合、レコードが重複するときに、（@defaultで定義された）デフォルト値が自動的にレコードに再適用されます。
* **default（文字列）**: 要素の動作（関数の呼び出し、デフォルト値）を定義できます。 この属性はXTK式を受け取ります。
* **desc（文字列）**: 要素の説明を挿入できます。 この説明は、インターフェイスのステータスバーに表示されます。
* **displayAsField (boolean)**: この属性がアクティブ化されると、「リンク」タイプ `<element>` がスキーマのツリー表示にフィールドとして表示されます（「構造」タブ）。 これにより、リンクをローカルフィールドとして表示し、クエリ中に動作を変更することができます。 クエリのSELECTに要素が見つかると、リンクターゲットの値が使用されます。 クエリのWHEREに要素が見つかると、リンクの基になるキーが使用されます。
* **編集（文字列）**: この属性は、スキーマにリンクされたフォームで使用される入力の種類を指定します。
* **enum（文字列）**: は、フィールドにリンクされている定義済みリストの名前を受け取ります。 定義済みリストは、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**: この属性は、テーブルに定義が格納されていない計算済みフィールドを定義します。 XpathまたはXTK （文字列）式を受け取ります。
* **externalJoin (boolean)**: 「リンク」型要素の外部結合。
* **機能（文字列）**: 特性フィールドを定義します。 これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルのストレージと共に使用されます。 指定できる値は次のとおりです。

   * &quot;共有&quot;: コンテンツは、データ型ごとに共有テーブルに保存されます
   * &quot;dedicated”: コンテンツは専用のテーブルに格納される
   SQL特性テーブルは、次の特性タイプに基づいて自動的に作成されます。

   * dedicated: `Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`
   次の2種類の特性フィールドがあります。 単一の値が特性に対して承認される単純なフィールドと、複数の選択フィールド。複数の値を含むコレクション要素に特性がリンクされるフィールドです。

   特性がスキーマで定義される場合、このスキーマは、単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されません）。

* **featureDate (boolean)**: 属性が「@feature」特性フィールドにリンクされている。 値が「true」の場合は、値が最後に更新された日時を確認できます。
* **filterPath (string)**: この属性はXpathを受け取り、フィールドに対してフィルターを定義できます。
* **folderLink (string)**: この属性は、エンティティを含むファイルを回復するためのリンクの名前を受け取ります。
* **folderModel (string)**: エンティティストレージを有効にするフォルダーのタイプを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **folderProcess (string)**: エンティティモデルインスタンスが保存されるリンクを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **fullLoad (boolean)**: この属性は、フォーム内のフィールド選択時に、テーブル内のすべてのレコードを強制的に表示します。
* **img （文字列）**: は、要素にリンクされた画像のパスを受け取ります。 この属性の値は、「名前空間：画像名」タイプです。 次に例を示します。 img=&quot;cus:myImage.jpg&quot;. 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **整合性（文字列）**: ターゲットテーブルに対するソーステーブルのオカレンスの参照整合性。

   アクセス可能な値は次のとおりです。

   * &quot;define&quot;: Adobe Campaignがリンクを介して参照されている場合、エンティティは削除されません。
   * &quot;normal&quot;: ソースオカレンスを削除すると、ターゲットオカレンス上のリンクのキーが初期化されます（デフォルトモード）。このタイプの整合性は、すべての外部キーを初期化します
   * &quot;own&quot;: ソースオカレンスの削除によって、ターゲットオカレンスの削除がトリガされます
   * &quot;owncopy&quot;: 「own」（削除の場合）または重複（複製の場合）に似ている
   * &quot;neutral&quot;: 何もしない

* **label (string)**: 要素のラベル。
* **labelSingular (string)**: インターフェイスの一部で使用される要素のラベル（単数形）。
* **length (string)**: 最大 「string」型のSQLフィールドの値に対して承認された文字数。
* **localizable (boolean)**: この属性がアクティブ化されている場合、収集ツールに対して翻訳用の「@label」属性の値の復元（内部使用）を指示します。
* **name (MNTOKEN)**: テーブルの名前と一致する要素の内部名。 「@name」属性の値は、短く、できれば英語で指定する必要があり、XMLにリンクされた命名の制約に従ってください。

   スキーマがデータベースに書き込まれると、フィールド名にプリフィックスがAdobe Campaignによって自動的に追加されます。

   * &quot;i&quot;: プレフィックスの値を指定します。
   * &quot;d&quot;: プレフィックスが表示されます。
   * &quot;s&quot;: のプレフィックスを指定します。
   * &quot;ts&quot;: プレフィックスに値を入力します。
   自律的な方法でテーブルの名前を定義するには、メインのスキーマ要素の定義で「@sqltable」属性を使用する必要があります。

* **noDbIndex (boolean)**: 要素のインデックスを作成しないように指定できます。
* **ordered (boolean)**: 属性がアクティブ化された場合(ordered=&quot;true&quot;)、Adobe Campaignは要素宣言のシーケンスをXMLコレクション要素内に保持します。
* **pkSequence （文字列）**: は、自動増分キーの計算に使用されるシーケンスの名前を受け取ります。 この属性は、スキーマのルート要素で自動増分キーが定義されている場合にのみ使用できます。
* **pkgStatus (string)**: パッケージのエクスポート時に、値はこの属性の値の関数として考慮されます。

   * &quot;always&quot;: 要素は常に存在します
   * &quot;never&quot;: 要素が存在しない
   * &quot;default (or nothing)&quot;: 要素は、デフォルトの要素でない場合、または内部フィールドでなく、他のインスタンスと互換性がない場合を除き、エクスポートされます

* **ref （文字列）**: この属性は、複数のスキーマ（定義のファクタリング）が共有する>element>要素への参照を定義します。 定義は現在のスキーマにコピーされません。
* **required (boolean)**: この属性がアクティブ化された場合(@required=&quot;true&quot;)、インターフェイスでフィールドがハイライト表示されます。 フィールドのラベルは、フォームでは赤で表示されます。
* **revAdvanced （ブール値）**: この属性を有効にすると、反対側のリンクが「アドバンス」リンクであることを指定します。
* **revCardinality（文字列）**: この属性は、2つのテーブル間のリンクのカーディナリティを定義します。 「リンク」タイプで使用され `<element>`ます。

   次のような値を選択できます。

   * &quot;single&quot; : 単純な1-1タイプのリンク
   * &quot;unbound&quot;: 1-N型収集リンク
   デフォルトでは、リンクの作成時に属性が指定されていない場合、基数は1 ～ Nになります。

* **revDesc （文字列）**: この属性は、反対のリンクにリンクされた説明を受け取ります。
* **revExternalJoin （ブール値）**: この属性を有効にすると、反対のリンクに外部結合を強制できます。
* **revIntegrity （文字列）**: この属性は、ターゲットスキーマの整合性を定義します。 「@integrity」属性と同じ値が許可されます。 デフォルトでは、Adobe Campaignはこの属性に「normal」値を与えます。
* **revLabel（文字列）**: 反対のリンクのラベル。
* **revLink （文字列）**: 反対側のリンクの名前。 値が「_NONE_」の場合、宛先スキーマに対向するリンクは作成されません。
* **revTarget （文字列）**: 反対のリンクのターゲット。
* **sql (boolean)**: この属性がアクティブ化される(@sql=&quot;true&quot;)と、xml=&quot;true&quot;プロパティが含まれている場合でも、SQL要素のストレージが強制されます。
* **sqlname （文字列）**: テーブル作成時のフィールドの名前。 「@sqlname」を指定しない場合、「@name」属性の値がデフォルトで使用されます。 テーブルにスキーマを書き込むとき、フィールドの種類に応じてプリフィックスが自動的に追加されます。
* **sqltable （文字列）**: スキーマのメイン要素の場合、この属性は、デフォルトで生成されるSQLテーブルの名前をオーバーロードします。 「@sqltable」を指定しない場合、デフォルトの名前は次のように構造化されます。 名前空間（大文字の最初の文字）の後にSrcSchema &quot;@name&quot;の値が続く。
* **tableSpace (string)**: この属性を使用すると、テーブルの新しいデータ格納テーブルスペースを指定できます(ルートで有効 `<element>`)。
* **tableSpaceIndex (string)**: この属性を使用すると、テーブルの新しいインデックス・ストレージ表領域を指定できます(ルートで有効 `<element>`)。
* **ターゲット(MNTOKEN)**: は、テーブル間のリンクを作成する際に、ターゲットスキーマの名前を受け取ります。 この属性は、「リンク」タイプの要素に対してのみ有効です。
* **template (string)**: この属性は、複数のスキーマが共有する `<element>` 要素への参照を定義します。 定義は自動的に現在のスキーマにコピーされます。
* **translatedDefault(string)**: 「@default」属性が見つかった場合、「@translatedDefault」を使用すると、式を再定義して、翻訳ツールによって収集される@defaultで定義されているのと一致させることができます（内部使用）。
* **translatedExpr (string)**: 「@expr」属性が見つかった場合、「@translatedExpr」属性を使用すると、「@expr」で定義された式と一致する翻訳を再定義でき、翻訳ツールによって収集されます（内部使用）。
* **type (MNTOKEN)**: 要素に格納するデータのタイプを定義します。

   使用可能なタイプのリスト:

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
   * 重複
   * 列挙
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

* **unbound (boolean)**: 属性がアクティブ化された場合(unbound=&quot;true&quot;)、そのリンクは1-N個のカーディナリティのコレクション要素として宣言されます。
* **userEnum (string)**: は、「open」定義済みリストの内部名を受け取ります。 定義済みリスト値は、インターフェイスでユーザーが定義できます。
* **xml（ブール値）**: このオプションを有効にすると、要素で定義されたすべての値がXMLのTEXTタイプ「mData」フィールドに格納されます。 これは、これらのフィールドにフィルタや並べ替えが設定されないことを意味します。
* **xmlChildren (boolean)**: 各子のストレージを強制( `<element>  or  <attribute>   ) of the   <element>    element in an XML document.   </element>  </attribute> </element>`

## `<enumeration>` element {#enumeration--element}

### コンテンツモデル {#content-model-5}

定義済みリスト:==(help| value)

### 属性 {#attributes-5}

* @basetype（文字列）
* @default（文字列）
* @desc （文字列）
* @label（文字列）
* @name（文字列）
* @template (string)

### 親 {#parents-5}

`<srcschema>`

### 子 {#children-5}

* `<help>`
* `<value>`

### 説明 {#description-5}

この要素を使用して、値の定義済みリストを定義できます。 定義済みリストは、で定義されているスキーマに属していますが、別のスキーマを介してアクセスできます。

### 使用と使用の状況 {#use-and-context-of-use-4}

定義済みリストは、スキーマの開始時（メイン要素が定義される前）に定義されます。

### 属性の説明 {#attribute-description-5}

* **basetype (string)**: 定義済みリストに格納される値のタイプ。

   使用可能なタイプのリスト:

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
   * 重複
   * 列挙
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

* **default（文字列）**: デフォルト値。 デフォルト値は、定義済みリストで定義されている値の1つでもかまいません。
* **desc（文字列）**: 定義済みリストの説明。
* **label (string)**: 定義済みリストラベル
* **name（文字列）**: 定義済みリストの内部名。
* **template (string)**: この属性は、複数のスキーマが共有する `<enumeration>` 要素への参照を定義します。 定義は自動的に現在のスキーマにコピーされます。

### 例 {#examples-4}

データベースに値が格納される定義済みリスト値の例：

```
    <enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>

    <element label="Sample" name="Sample">
       <attribute dbEnum="myEnum" length="100" name="Number" required="true" type="string"/>
    </element>
```

デフォルト値を持つ定義済みリストの定義：

```
 <enumeration basetype="byte" default="email" name="canal">
    <value label="Email" name="email" value="0"/> 
    <value label="Téléphone" name="phone" value="1"/>
    <value label="Call Center" name="callcenter" value="2"/>
 </enumeration>
```

## `<help>` element {#help--element}

### コンテンツモデル {#content-model-6}

help:=EMPTY

### 属性 {#attributes-6}

なし

### 親 {#parents-6}

`<srcschema>`  ,  `<element>`   ,   `<attribute>`    ,    `<enumeration>`     ,     `<value>`      ,     `<param />`,      `<method />`

### 子 {#children-6}

なし

### 説明 {#description-6}

この要素では、 `<element>` または `<attribute>` 要素について説明します。 テキストのみを含めることができ、データベースのXMLに保存されます。

### 属性の説明 {#attribute-description-6}

この要素には属性がありません。

### 例 {#examples-5}

```
<method name="CheckOperation" static="true"
      <helpchecks the validity of a campaign</help
...
</method> 
```

## `<join>` element {#join--element}

### コンテンツモデル {#content-model-7}

join:==EMPTY

### 属性 {#attributes-7}

* @dstFilterExpr（文字列）
* @xpath-dst（文字列）
* @xpath-src（文字列）

### 親 {#parents-7}

`<element>`

### 子 {#children-7}

なし

### 説明 {#description-7}

SQLテーブル間の結合を作成するフィールドを定義できます。

### 使用と使用の状況 {#use-and-context-of-use-5}

要素は、親 `<join>` 要素が「リンク」タイプの場合にのみ使用でき `<element>` ます。 これは、親要素で「@type=link」属性が宣言されている必要があることを意味します。

要素でリモート・テーブルの名前と名前空間を指定する必要はありません `<join>` 。 親で指定する必要があり `<element>`ます。

規則に従って、リンクはスキーマの最後に定義されます。

リンクタイプ要素を定義するときに `<join>` 要素が指定されていない場合、リンクは両方のテーブルの主キーに自動的に配置されます。

### 属性の説明 {#attribute-description-7}

* **dstFilterExpr (string)**: この属性を使用すると、リモート・テーブルの有効な値の数を制限できます。
* **xpath-dst (string)**: この属性は、Xpath（リモートテーブルの@name属性）を受け取ります。
* **xpath-src（文字列）**: この属性は、Xpath(現在のスキーマの@name属性)を受け取ります。

### 例 {#examples-6}

現在のテーブルの「email」フィールドとリモートテーブルの「@compagny-id」フィールド間のリンク：

```
<join xpath-dst="@compagny-id" xpath-src="@email"/>
```

「@country」フィールドの内容（「EN」値を含む必要がある）に基づいて、「cus:Country」テーブルに向けてフィルターされたリンク。

```
<element name="StockEN" type="link" label="MyLink" target="cus:Stock">
   <join xpath-dst="@country" xpath-src="@code" dstFilterExpr="@country = 'EN'"/>
 </element>
```

## `<key>` element {#key--element}

### コンテンツモデル {#content-model-8}

key:==keyfield

### 属性 {#attributes-8}

* @allowEmptyPart (boolean)
* @applicableIf (string)
* @internal (boolean)
* @label（文字列）
* @name (MNTOKEN)
* @noDbIndex (boolean)

### 親 {#parents-8}

`<element>`

### 子 {#children-8}

`<keyfield>`

### 説明 {#description-8}

この要素では、テーブル内のレコードを識別するためのキーを定義できます。

テーブルには少なくとも1つのキーが必要です。

### 使用と使用の状況 {#use-and-context-of-use-6}

原則として、キーはスキーマのメイン要素とインデックスの後に宣言されます。

キーに複数のフィールド（複数の子など）が含まれる場合、キーは複合と呼ばれ `<keyfield>` ます。 主キーの定義に複合キーを使用しないでください。

スキーマのメイン要素に「@autopk=true」属性が含まれている場合、プライマリキーは一意です。 スキーマ1人につき主キーを1つだけ持つことができます。

最初の1000個の識別子は予約されているので、キーに対して値の範囲を定義する必要がある場合、開始は1000になります。

### 属性の説明 {#attribute-description-8}

* **allowEmptyPart (boolean)**: 複合キーの場合、この属性が有効な場合、そのキーの少なくとも1つが空でないと、そのキーは有効と見なされます。 この場合、空の概念の値は「0」です（ブール値またはすべてのタイプの数値データ）。 デフォルトでは、複合キーを構成するすべてのキーを入力する必要があります。
* **applicableIf (string)**: この属性を使用すると、キーをオプションにできます。 キー定義を適用する条件を定義します。 この属性はXTK式を受け取ります。
* **internal (boolean)**: この属性は、アクティブ化された場合に、キーがプライマリであることをAdobe Campaignに知らせます。
* **label (string)**: キーのラベル。
* **name (MNTOKEN)**: キーの内部名。
* **noDbIndex (boolean)**: アクティブ化された場合(noDbIndex=&quot;true&quot;)、キーに一致するフィールドのインデックスは作成されません。

### 例 {#examples-------}

「@expr」または「alias」フィールドを空にすることを許可する複合キーの宣言：

```
<key name="node" allowEmptyPart="true">
  <keyfield xpath="@expr"/>
   <keyfield xpath="@alias"/>
 </key>
```

STRING型の「Name」フィールドでの主キーの宣言と、一致するSQLクエリ `<srcschema>` の宣言：

```
 
<key name="PrimaryKey" internal="true">  
  <keyfield xpath="@name"/>
</key>

CREATE UNIQUE INDEX Schema_PrimaryKey ON Schema(sName);
```

## `<keyfield>` element {#keyfield--element}

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

* **xlink (MNTOKEN)**: リレーションテーブル（N-Nリンク）のジョインで定義された外部キーを自動的に参照できます。
* **xpath (MNTOKEN)**: 要素のインデックスまたはキーの定義 `<attribute>` 。 この属性は、キーまたはインデックスを定義するスキーマ属性へのパスを定義するXpathを受け取ります。

### 例 {#examples-}

「@name」上のXpathを持つインデックス内の「sName」フィールドの選択：

```
<keyfield xpath="@name"/>
```

## `<method>` element {#method--element}

### コンテンツモデル {#content-model-10}

method:==( help) |パラメーター)

### 属性 {#attributes-10}

* @_operation（文字列）
* @access (string)
* @const (boolean)
* @hidden（ブール値）
* @label（文字列）
* @library (string)
* @name (MNTOKEN)
* @pkonly (boolean)
* @static（ブール値）

### 親 {#parents-10}

`<methods>`  ,  `<interface />`

### 子 {#children-10}

* `<help>`
* `<parameters>`

### 説明 {#description-10}

この要素を使用して、SOAPメソッドを定義できます。

### 使用と使用の状況 {#use-and-context-of-use-7}

SOAPメソッドを使用すると、アプリケーションプロセスが有効になります。

「@library」は、新しいメソッド（非ネイティブ）を宣言するために必要です。 ライブラリに使用される名前空間と名前は、宣言が含まれるスキーマの名前空間と名前とは独立しています。

### 属性の説明 {#attribute-description-10}

* **access (string)**: この属性は、メソッドを使用するアクセス制御を定義します。 この属性がない場合は、識別は必須です。 次の値を指定できます。 &#39;anonymous&#39;、&#39;admin&#39;、および&#39;sql&#39;。
* **const(boolean)**: この属性がアクティブ化された場合、宣言されたメソッドがエンティティを変更することを意味します
* **label (string)**: メソッドのラベル。
* **library (string)**: このメソッドは、アプリケーションに固有のメソッドではありません。 この属性は、メソッド定義が見つかったメソッドライブラリの値を取ります(nms:mylibrary.js)。
* **name (MNTOKEN)**: 一意のメソッド名。
* **static (boolean)**: この属性が有効になっている場合、メソッドは自律型であると見なされ、呼び出し時にメソッドにすべてのパラメーターを指定する必要があります。

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

## `<methods>` element {#methods--element}

### コンテンツモデル {#content-model-11}

methods:==method

### 属性 {#attributes-11}

なし

### 親 {#parents-11}

`<srcschema>`

### 子 {#children-11}

method

### 説明 {#description-11}

この要素を使用して、 `<method>` 要素を定義できます。 メソッドを宣言する場合は必須です。

### 属性の説明 {#attribute-description-11}

この要素には属性がありません。

### 例 {#examples-8}

```
<methods async="true"
...// definition of one or more <method
</methods>
```

## `<param>` element {#param--element}

### コンテンツモデル {#content-model-12}

param:==help

### 属性 {#attributes-12}

* @_operation（文字列）
* @desc （文字列）
* @enum （文字列）
* @inout （文字列）
* @label（文字列）
* @localizable (string)
* @name (MNTOKEN)
* @名前空間(MNTOKEN)
* @type (string)

### 親 {#parents-12}

`<parameters>`

### 子 {#children-12}

`<help>`

### 説明 {#description-12}

この要素では、SOAPメソッドを呼び出すためのパラメーターを定義できます。

### 属性の説明 {#attribute-description-12}

* **desc（文字列）**: 要素に関する説明 `<param>` 。
* **inout (string)**: この属性は、SOAP呼び出しの入力(in)または出力(out)にパラメーターが存在するかどうかを定義します。 この属性を指定しない場合、デフォルトのパラメーターは入力(「@inout=in」)になります。
* **label (string)**: `<param>` label
* **localizable (string)**: この属性がアクティブ化されている場合、収集ツールに対して翻訳用の「@label」属性の値の復元（内部使用）を指示します。
* **name (MNTOKEN)**: 内部名 `<param>`
* **type (string)**: この属性は、 `<param>` 要素のタイプを定義します

   使用可能なタイプのリスト:

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
   * 重複
   * 列挙
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

文字列タイプの&quot;serviceName&quot;受信設定の定義：

```
<param desc="Name of the information service(s) (separated with commas)"
               name="serviceName" type="string" inout="in"/>
```

## `<parameters>` element {#parameters--element}

### コンテンツモデル {#content-model-13}

パラメーター：==param

### 属性 {#attributes-13}

なし

### 親 {#parents-13}

`<method>`

### 子 {#children-13}

`<param>`

### 説明 {#description-13}

この要素は、要素のグループを定義し `<parameter>` ます。

### 使用と使用の状況 {#use-and-context-of-use-8}

この要素は必須です。要素の `<param>` 子要素が1つだけの場合でも同様で `<method>` す。

### 属性の説明 {#attribute-description-13}

なし

### 例 {#examples-10}

```
<parameters
... //definition of one or more <param
</parameters>
```

## `<srcschema>` element {#srcschema--element}

### コンテンツモデル {#content-model-14}

srcSchema:=(attribute) | createdBy | data |要素 |定義済みリスト |ヘルプ |インターフェイス |メソッド | modifiedBy)

### 属性 {#attributes-14}

created(datetime)、createdBy-id(long)、desc(string)、entitySchema(string)、extendedSchema(string)、implements(string)、label(string)、labelSingular(string)、library(boolean)、mappingType(string)、modifiedBy-id(long)、name(name(string)、名前空間(string)、useRecycleBin (boolean)、表示(boolean)、xtkschema (string)

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

は、スキーマ `<srcschema>` のルート要素です。 スキーマの定義の入力ポイントです。

### 使用と使用の状況 {#use-and-context-of-use-9}

スキーマのプレゼンテーションは、スキーマの参照 [と](../../configuration/using/about-schema-reference.md) スキーマ構造についてで利用できます [](../../configuration/using/schema-structure.md)。

### 属性の説明 {#attribute-description-14}

* **作成日（日時）**: この属性は、スキーマの作成日時に関する情報を提供します。 「日付時間」のフォームがあります。 表示される値は、サーバーから取得されます。 時刻はUTC形式で表示されます。
* **createdBy-id (long)**: は、スキーマを作成した演算子の識別子です。
* **desc（文字列）**: スキーマの説明
* **entitySchema (string)**: 基本的な構文とAdobe Campaignが基になるスキーマ（デフォルトでは次の構文が使用されます）。 xtk:srcSchema)。 現在のスキーマを保存すると、Adobe Campaignは、@xtkschema属性で宣言されたスキーマを使用して、文法を承認します。
* **extendedSchema (string)**: は、現在のスキーマ拡張が基にしている、標準搭載されたスキーマの名前を受け取ります。 フォームは「名前空間：名前」です。
* **img （文字列）**: アイコンがスキーマにリンクされている場合(スキーマ作成ウィザードで定義できます)。
* **label (string)**: スキーマラベル
* **labelSingular (string)**: label（単数形）は、インターフェイスで表示します。
* **lastModified (datetime)**: この属性は、最後の変更の日時に関する情報を提供します。 「日付時間」のフォームがあります。 表示される値は、サーバーから取得されます。 時刻はUTC形式で表示されます。
* **library (boolean)**: スキーマをライブラリとして使用し、エンティティとしては使用しない。 したがって、このスキーマは「@ref」および「@template」属性により、他のスキーマから参照される場合があります。
* **mappingType (string)**:

   * &quot;sql&quot;: データベースマッピング
   * &quot;textFile&quot;: テキストファイルマッピング
   * &quot;xmlFile&quot;: XML形式のテキストファイルマッピング
   * &quot;binaryFile&quot;: バイナリファイルマッピング

* **modifiedBy-id (long)**: は、スキーマを変更した演算子の識別子に一致します。
* **name（文字列）**: 一意のスキーマ名。
* **名前空間（文字列）**: スキーマの名前空間(デフォルト： nms、xtk、nl)。 プロジェクト用に新しいスキーマを作成する場合は、専用の名前空間を使用することをお勧めします。
* **useRecycleBin (boolean)**: アプリケーションのごみ箱機能をアクティブにします。 削除したレコードは、最終的に削除される前にごみ箱に入れられます。 この関数は、「配信」モードでのみ使用できます。
* **表示（ブール値）**: アクティブ化された場合(@表示=&quot;true&quot;)、スキーマは表示として使用されます。 データベース構造の更新ウィザードでは、スキーマは考慮されません。 このオプションは、主に外部テーブルを参照するために使用します。
* **xtkschema （文字列）**: スキーマ文法を定義するスキーマの名前（デフォルトではxtk:srcSchema）。

### 例 {#examples-11}

`<srcschema>` 要素内の「nms:配信」を追加スキーマ

```
<srcSchema desc="Defines all the settings of a delivery (or delivery template)."  
           entitySchema="xtk:srcSchema" img="nms:campaign.png" implements="xtk:persist" 
           label="Diffusions" labelSingular="Diffusion" md5="DCD2164CD0276B1DCA6E1C9E2A75EC04"
           name="delivery" namespace="nms" useRecycleBin="true" xtkschema="xtk:srcSchema">
```

## `<sysfilter>` element {#sysfilter--element}

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

@name属性の条件を含むフィルターの定義：

```
<sysFilter>
      <condition expr="@name ='Doe'"/>
  <sysFilter>
```

## `<value>` element {#value--element}

### コンテンツモデル {#content-model-16}

value:==help

### 属性 {#attributes-16}

* @applicableIf (string)
* @desc （文字列）
* @enabledIf (string)
* @img (string)
* @label（文字列）
* @name（文字列）
* @value（文字列）

### 親 {#parents-16}

`<enumeration>`

### 子 {#children-16}

`<help>`

### 説明 {#description-16}

この要素を使用すると、定義済みリストに保存される値を定義できます。

### 属性の説明 {#attribute-description-16}

* **applicableIf (string)**: この属性を使用すると、定義済みリスト値をオプションにできます。 XTK式を受け取ります。
* **desc（文字列）**: 定義済みリスト値の説明。
* **enabledIf (string)**: 定義済みリスト値をアクティブ化する条件を指定します。
* **img （文字列）**: 画像が「名前空間:image_name」フォームの定義済みリストにリンクされている。 画像をアプリケーションサーバーに読み込む必要があります。
* **label (string)**: 定義済みリスト値のラベル。
* **name（文字列）**: 定義済みリスト値の内部名。
* **value（文字列）**: 定義済みリスト値の値。 値のタイプは、定義済みリストのタイプに基づいて定義されます。 定義済みリストが文字列型の場合、文字列型の値のみを含めることができます。

### 例 {#examples-13}

```
<enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>
```
