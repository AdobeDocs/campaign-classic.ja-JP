---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: e4d34f56-b065-4dce-8974-11dc2767873a
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# 属性要素 {#attribute--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model}

属性：==help

## 属性 {#attributes}

_operation （文字列）、advanced (boolean)、 applicableIf （文字列）、 autoIncrement （ブール値）、 belonsTo （文字列）、 dataPolicy （文字列）、 dbEnum （文字列）、 defOnDuplicate （ブール値）、 default （文字列）、 enum （文字列）、 expr （文字列）、 feature （文字列）、 featureDate （ブール値）img （文字列）、inout （文字列）、 label （文字列）、 length （文字列）、ローカライズ可能（ブール値）、 name (MNTOKEN)、 notNull （ブール値）、 pkgStatus （文字列）、 ref （文字列）、 required （ブール値）、 sql （ブール値）、 sqlDefault （文字列）、 sqltable （文字列）、 templateDefault (string), translatedExpr (string), type (MNTOKEN), user (boolean), userEnum (string), visibleIf (string), xml (boolean)

## 親 {#parents}

`<element>`

## 子 {#children}

`<help>`

## 説明 {#description}

`<attribute>` 要素を使用して、データベース内にフィールドを定義できます。

## 使用と使用のコンテキスト {#use-and-context-of-use}

`<attribute>` 要素は、要素内で宣言する必要があ `<element>` ります。

`<srcschema>` 内で `<attribute>` 要素が定義される順序は、データベース内のフィールド作成順序に影響しません。 作成順はアルファベット順になります。

## 属性の説明 {#attribute-description}

* **_operation （文字列）**:データベースに書き込むタイプを定義します。

   この属性は、主に標準のスキーマを拡張する際に使用されます。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:紐付けのみ。 つまり、Adobe Campaignは、更新せずに要素を回復します。要素が存在しない場合は、エラーを生成します。
   * &quot;insertOrUpdate&quot;:を挿入して更新します。 つまり、Adobe Campaignは要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 つまり、Adobe Campaignは要素を更新するか、存在しない場合はエラーを生成します。
   * &quot;delete&quot;:削除します。 つまり、Adobe Campaignは要素を復元および削除します。

* **advanced (boolean)**:このオプションを有効にすると (@advanced=&quot;true&quot;)、フォームでリストを設定するためにアクセス可能なフィールドのリストの属性を非表示にできます。
* **applicableIf (string)**:この属性を使用すると、フィールドをオプションにできます。制約に従う場合、データベースを更新する際に `<attribute>` 要素が考慮されます。 「applicableIf」は XTK 式を受け取ります。
* **autoIncrement（ブール値）**:このオプションを有効にすると、フィールドがカウンターになります。これにより、値を増分できます（ほとんどの場合は ID）。 （外部使用）
* **belongsTo（文字列）**:は、フィールドを共有するテーブルの名前と名前空間を取得し、属性の宣言先のスキーマを設定します。（`<schema>` でのみ使用）。
* **dataPolicy （文字列）**:「SQL または XML」フィールドで許可する値に対する承認制約を指定できます。この属性の値は次のとおりです。

   * &quot;none&quot;:値なし
   * &quot;smartCase&quot;:先頭文字の大文字
   * &quot;lowerCase&quot;:すべて小文字
   * &quot;upperCase&quot;:すべて大文字
   * &quot;email&quot;:電子メールアドレス
   * &quot;phone&quot;:電話番号
   * &quot;identifier&quot;:識別子名
   * &quot;resIdentifier&quot;:ファイル名

* **dbEnum (string)**:は、「閉じられた」列挙の内部名を受け取ります。列挙の値は、`<srcschema>` で定義する必要があります。
* **defOnDuplicate（ブール値）**:この属性が有効な場合、レコードが重複すると、デフォルト値 (@defaultで定義 ) が自動的にレコードに再適用されます。
* **デフォルト（文字列）**:を使用すると、デフォルトのフィールドの値（関数の呼び出し、デフォルト値）を定義できます。この属性は XTK 式を受け取ります。
* **desc （文字列）**:属性の説明を挿入できます。この説明は、インターフェイスのステータスバーに表示されます。
* **編集（文字列）**:この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum (string)**:は、フィールドにリンクされている列挙の名前を受け取ります。列挙は、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**:フィールドの事前計算式を定義します。この属性は、Xpath または XTK 式を受け取ります。
* **機能（文字列）**:特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルに格納されます。指定できる値は次のとおりです。

   * &quot;shared&quot;:コンテンツは、データタイプごとに共有テーブルに格納されます
   * &quot;dedicated&quot;:コンテンツは専用のテーブルに格納されます。

   SQL 特性テーブルは、特性タイプに基づいて自動的に作成されます。

   * 専用：`Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

   次の 2 種類の特性フィールドがあります。単一の値が特性に対して承認される単純な oà¹フィールドと、複数選択フィールド（特性が複数の値を含むコレクション要素にリンクされるフィールド）。

   スキーマ内で特性が定義される場合、このスキーマは、単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されません）。

* **featureDate（ブール値）**:属性は「@feature」特性フィールドにリンクされています。値が「true」の場合は、値が最後に更新された日時を確認できます。
* **img （文字列）**:フィールドにリンクされた画像のパス（名前空間+画像名）を定義できます ( 例：img=&quot;cus:mypicture.jpg&quot;)。物理的には、イメージをアプリケーションサーバーにインポートする必要があります。
* **label （文字列）**:フィールドにリンクされたラベル。主に、インターフェイスのユーザー向けのラベルです。これにより、命名の制約を回避できます。
* **length （文字列）**:最大「文字列」タイプの SQL フィールドの値の文字数。 「@length」属性が指定されていない場合、Adobe Campaignは自動的に 255 文字のフィールドを作成します。
* **localizable（ブール値）**:この属性が有効な場合、この属性は、翻訳（内部使用）の「@label」属性の値を復元するように収集ツールに指示します。
* **名前 (MNTOKEN)**:テーブルのフィールド名と一致する属性の名前。「@name」属性の値は短く、できれば英語で記述し、XML の命名規則に従う必要があります。

   スキーマがデータベースに書き込まれると、Adobe Campaignによってプレフィックスがフィールド名に自動的に追加されます。

   * &quot;i&quot;:プレフィックスを「integer」型に設定します。
   * &quot;d&quot;:「double」型のプレフィックス。
   * &quot;s&quot;:プレフィックスを使用します。
   * &quot;ts&quot;:プレフィックスを使用して、「日付」タイプを指定します。

   テーブル内のフィールドの名前を完全に定義するには、属性を定義する際に「@sqlname」オプションを使用します。

* **notNull（ブール値）**:では、データベース内の NULL レコードの管理に関するAdobe Campaignの動作を再定義できます。デフォルトでは、数値フィールドは null ではなく、文字列および日付タイプのフィールドは null にできます。
* **pkgStatus （文字列）**:パッケージの書き出し時には、「@pkgStatus」の値に応じて値が考慮されます。

   * &quot;always&quot;:常に存在する
   * &quot;never&quot;:存在しない
   * &quot;default （または nothing）&quot;:この値は、デフォルト値である場合や、他のインスタンスと互換性のない内部フィールドでない場合を除き、エクスポートされます。

* **ref（文字列）**:この属性は、複数のスキーマ ( 定義 `<attribute>` ファクタリング ) で共有される要素への参照を定義します。定義は現在のスキーマにコピーされません。
* **必須（ブール値）**:この属性が有効な場合 (@required=&quot;true&quot;)、インターフェイスでフィールドがハイライト表示されます。フィールドのラベルは、フォームでは赤で表示されます。
* **sql（ブール値）**:この属性が有効になっている場合 (@sql=&quot;true&quot;)、属性を含む要素に xml=&quot;true&quot;プロパティが含まれている場合でも、SQL 属性の保存が強制されます。
* **sqlDefault（文字列）**:この属性を使用すると、@notNull属性が有効になっている場合に、データベースの更新に使用するデフォルト値を定義できます。属性の作成後にこの属性を追加した場合、新しいレコードでもスキーマの動作は変更されません。 スキーマを変更し、新しいレコードの値を更新するには、属性を削除して、再び作成する必要があります。
* **sqlname （文字列）**:」フィールドの値を指定します。@sqlnameを指定しない場合、デフォルトでは「@name」属性の値が使用されます。 スキーマがデータベースに書き込まれると、フィールドのタイプに応じてプレフィックスが自動的に追加されます。
* **template （文字列）**:この属性は、複数のスキーマで共有さ `<attribute>` れる要素への参照を定義します。定義は、現在のスキーマに自動的にコピーされます。
* **translatedDefault（文字列）**:「@default」属性が見つかった場合、「@translatedDefault」を使用して、翻訳ツールで収集される式を@defaultで定義した式に一致するように再定義できます（内部使用）。
* **translatedExpr (string)**:「@expr」属性が存在する場合、「@translatedExpr」属性を使用して、翻訳ツールで収集される式を再定義し、@exprで定義された式に一致するようにできます（内部使用）。
* **型 (MNTOKEN)**:フィールドタイプ。

   フィールドタイプは汎用です。 Adobe Campaignでは、インストールされているデータベースのタイプに応じて、定義されたタイプが、構造の更新時にインストールされたデータベースに固有の値に変更されます。

   使用可能なタイプのリスト：

   * いずれか
   * bin
   * blob
   * boolean
   * バイト
   * CDATA
   * 日時
   * datetimetz
   * datetimenotz
   * date
   * 重複
   * enum
   * float
   * html
   * int64
   * リンク
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

   「@type」属性が空の場合、Adobe Campaignはデフォルトで、長さ 100 の文字列 (STRING) をフィールドにリンクします。

   フィールドの型が STRING で、フィールドの名前が「@sqlname」属性の存在で指定されない場合、データベース内のフィールドの名前の前には自動的に「s」が付きます。 この動作モードは、「整数 (i)」、「ダブル (d)」、「日付 (ts)」タイプのフィールドと同様です。

* **userEnum (string)**:は、「開いている」列挙の内部名を受け取ります。列挙の値は、インターフェイスでユーザーが定義できます。
* **visibleIf (string)**:属性の表示/非表示を切り替える条件を XTK 式の形式で定義します。

   >[!IMPORTANT]
   >
   >属性は非表示ですが、そのデータには引き続きアクセスできます。

* **xml（ブール値）**:このオプションを有効にした場合、フィールドの値にはリンクされた SQL フィールドは含まれません。Adobe Campaignは、レコードストレージ用にテキストタイプ「mData」フィールドを作成します。 つまり、これらのフィールドにフィルターや並べ替えは適用されません。

### 例 {#examples}

データベースに値が格納される列挙値の例：

```
    <enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>

    <element label="Sample" name="Sample">
       <attribute dbEnum="myEnum" length="100" name="Number" required="true" type="string"/>
    </element>     
```

「@datapolicy」を含む XML フィールドの宣言：

```
<attribute dataPolicy="phone" desc="Mobile number" label="Mobile"
     length="32" name="mobilePhone" sqlname="sMobilePhone" type="string"/>
```

「@applicableIf」の例：「次を含む」属性は、国数が 20 を超える場合にのみ作成されます。

```
<attribute length="100" name="Continent" type="string" applicableIf="@country > 20"/>
```

「@feature」が「shared」タイプの場合の例：

```
<attribute name="field1" label="Field 1" type="long" feature="shared"/>
<attribute name="field1" label="Field 1" type="long" feature="shared" sqlname="126" sqltable="Ft_Content_Long"/>
```

「@feature」が「dedicated」タイプの場合の例：

```
<attribute name="field1" label="Field 1" type="long" feature="dedicated"/>
<attribute name="field1" label="Field 1" type="long" feature="dedicated" sqlname="sField1" sqltable="Ft_recipient_field1"/>
```
