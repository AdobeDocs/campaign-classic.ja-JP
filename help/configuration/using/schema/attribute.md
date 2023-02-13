---
product: campaign
title: 要素と属性 — 属性要素
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: e4d34f56-b065-4dce-8974-11dc2767873a
source-git-commit: 40da5774c8a6a228992c4aa400e2d9924215611e
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 1%

---

# 属性要素 {#attribute--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model}

attribute:==help

## 属性 {#attributes}

_operation （文字列）、advanced (boolean)、 applicableIf （文字列）、 autoIncrement （ブール値）、 belonsTo （文字列）、 dataPolicy （文字列）、 dbEnum （文字列）、 defOnDuplicate （ブール値）、 default （文字列）、 edit （文字列）、 enum （文字列）、 expr （文字列）、 feature （文字列）、 featureBooleanimg（文字列）、inout（文字列）、label（文字列）、length（文字列）、localizable（ブール値）、name（ブール値）、notNull（ブール値）、pkgStatus（文字列）、ref（文字列）、required（ブール値）、sqlDefault（文字列）、sqlname（文字列）、target（文字列）、template（文字列）、Default (string), translatedExpr (string), type (MNTOKEN), user (boolean), userEnum (string), visibleIf (string), xml (boolean)

## 親 {#parents}

`<element>`

## 子 {#children}

`<help>`

## 説明 {#description}

`<attribute>` 要素を使用すると、データベースにフィールドを定義できます。

## 使用と使用のコンテキスト {#use-and-context-of-use}

`<attribute>` 要素は `<element>` 要素。

シーケンス `<attribute>` 要素が `<srcschema>` は、データベース内のフィールド作成順序に影響を与えません。 作成順はアルファベット順になります。

## 属性の説明 {#attribute-description}

* **_operation （文字列）**:は、データベースに書き込むタイプを定義します。

   この属性は、主に標準のスキーマを拡張する際に使用されます。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:紐付けのみ。 つまり、Adobe Campaignは、更新せずに要素を復元します。要素が存在しない場合は、エラーを生成します。
   * &quot;insertOrUpdate&quot;:挿入で更新。 つまり、Adobe Campaignは要素を更新します。要素が存在しない場合は作成します。
   * &quot;insert&quot;:挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 つまり、Adobe Campaignは要素を更新します。要素が存在しない場合は、エラーを生成します。
   * &quot;delete&quot;:削除します。 つまり、Adobe Campaignは要素を復元および削除します。

* **advanced (boolean)**:このオプションを有効にすると (@advanced=&quot;true&quot;)、フォーム内のリストを設定するためにアクセス可能なフィールドのリストの属性を非表示にできます。
* **applicableIf（文字列）**:この属性を使用すると、フィールドをオプションにできます。 この `<attribute>` 制約に準拠する場合、要素は、データベースを更新する際に考慮されます。 「applicableIf」は XTK 式を受け取ります。
* **autoIncrement（ブール値）**:このオプションを有効にすると、フィールドがカウンターになります。 これにより、値を増分できます（ほとんどの場合、ID）。 （外部使用）
* **belongsTo（文字列）**:は、フィールドを共有するテーブルの名前と名前空間を取得し、属性が宣言されているスキーマを入力します。 ( `<schema>`) をクリックします。
* **dataPolicy （文字列）**:「SQL」フィールドまたは「XML」フィールドで許可される値に対して承認制約を指定できます。 この属性の値は次のとおりです。

   * &quot;none&quot;:値なし
   * &quot;smartCase&quot;:先頭文字の大文字
   * &quot;lowerCase&quot;:すべて小文字
   * &quot;upperCase&quot;:すべて大文字
   * &quot;email&quot;:電子メールアドレス
   * &quot;phone&quot;:電話番号
   * &quot;identifier&quot;:識別子名
   * &quot;resIdentifier&quot;:ファイル名

* **dbEnum （文字列）**:は、「閉じられた」列挙の内部名を受け取ります。 列挙の値は、 `<srcschema>`.
* **defOnDuplicate（ブール値）**:この属性が有効になっている場合、レコードが重複すると、(@defaultで定義されている ) デフォルト値が自動的にレコードに再適用されます。
* **default (string)**:デフォルトのフィールドの値を定義できます（関数の呼び出し、デフォルト値）。 この属性は XTK 式を受け取ります。
* **desc （文字列）**:属性の説明を挿入できます。 この説明は、インターフェイスのステータスバーに表示されます。
* **編集（文字列）**:この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum (string)**:は、フィールドにリンクされている列挙の名前を受け取ります。 列挙は、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**:フィールドの事前計算式を定義します。 この属性は、Xpath または XTK 式を受け取ります。
* **feature （文字列）**:特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルに格納されます。 指定できる値は次のとおりです。

   * &quot;shared&quot;:コンテンツは、データタイプごとに共有テーブルに保存されます
   * &quot;dedicated&quot;:コンテンツは専用テーブルに格納されます

   SQL 特性テーブルは、次の特性タイプに基づいて自動的に作成されます。

   * 専用： `Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

   次の 2 種類の特性フィールドがあります。1 つの値が特性に対して許可される単純な oà¹フィールドと、複数選択フィールド（特性が複数の値を含むコレクション要素にリンクされる）。

   スキーマ内で特性が定義される場合、このスキーマは、単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されていません）。

* **featureDate（ブール値）**:「@feature」特性フィールドにリンクされた属性。 値が「true」の場合は、値が最後に更新された日時を確認できます。
* **img （文字列）**:フィールドにリンクされた画像のパスを定義できます（名前空間+画像名）( 例：img=&quot;cus:mypicture.jpg&quot;) と同じです。 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **label （文字列）**:フィールドにリンクされたラベル。主に、インターフェイスのユーザーに対するラベルです。 これにより、命名の制約を回避できます。
* **length （文字列）**:最大 「文字列」タイプの SQL フィールドの値の文字数。 「@length」属性が指定されていない場合、Adobe Campaignは自動的に 255 文字のフィールドを作成します。
* **localizable(boolean)**:有効化されている場合、この属性は、翻訳の「@label」属性の値を復元するようコレクションツールに指示します（内部使用）。
* **名前 (MNTOKEN)**:テーブルのフィールド名に一致する属性の名前。 「@name」属性の値は、短く、できれば英語で記述し、XML の命名規則に従う必要があります。

   スキーマがデータベースに書き込まれると、Adobe Campaignによって、フィールド名にプレフィックスが自動的に追加されます。

   * &quot;i&quot;:「integer」タイプのプレフィックス。
   * &quot;d&quot;:「double」タイプのプレフィックス。
   * &quot;s&quot;:文字列タイプのプレフィックス。
   * &quot;ts&quot;:「日付」タイプのプレフィックス。

   テーブル内のフィールドの名前を完全に定義するには、属性を定義する際に「@sqlname」オプションを使用します。

* **notNull（ブール値）**:では、データベース内の NULL レコードの管理に関するAdobe Campaignの動作を再定義できます。 デフォルトでは、数値フィールドは null ではなく、文字列および日付タイプのフィールドは null です。
* **pkgStatus （文字列）**:パッケージの書き出し時には、「@pkgStatus」の値に応じて値が考慮されます。

   * &quot;always&quot;:常に存在する
   * &quot;never&quot;:存在しない
   * &quot;default （または何も指定しない）&quot;:値は、デフォルト値の場合や、他のインスタンスと互換性がない内部フィールドでない場合を除き、エクスポートされます。

* **ref（文字列）**:この属性は、 `<attribute>` 複数のスキーマで共有される要素（定義のファクタリング）。 定義は現在のスキーマにコピーされません。
* **必須（ブール値）**:この属性が有効化されている場合 (@required=&quot;true&quot;)、インターフェイスでフィールドがハイライト表示されます。 フィールドのラベルは、フォームでは赤で表示されます。
* **sql（ブール値）**:この属性が有効になっている場合 (@sql=&quot;true&quot;)、属性を含む要素に xml=&quot;true&quot;プロパティが含まれている場合でも、SQL 属性の保存が強制されます。
* **sqlDefault（文字列）**:この属性を使用すると、@notNull属性が有効化されている場合に、データベースの更新に使用するデフォルト値を定義できます。 属性の作成後にこの属性を追加した場合、新しいレコードでもスキーマの動作は変更されません。 スキーマを変更し、新しいレコードの値を更新するには、属性を削除して、もう一度作成する必要があります。
* **sqlname （文字列）**:」フィールドの値を指定します。 @sqlnameを指定しない場合、デフォルトでは「@name」属性の値が使用されます。 スキーマがデータベースに書き込まれると、フィールドのタイプに応じて、プレフィックスが自動的に追加されます。
* **template （文字列）**:この属性は、 `<attribute>` 複数のスキーマで共有される要素。 定義は、現在のスキーマに自動的にコピーされます。
* **translatedDefault (string)**:「@default」属性が見つかった場合、「@translatedDefault」を使用して、翻訳ツール（内部使用）で収集される式を再定義し、@defaultで定義された式に一致させることができます。
* **translatedExpr (string)**:「@expr」属性が存在する場合、「@translatedExpr」属性を使用して、翻訳ツール（内部使用）で収集される式を再定義し、@exprで定義された式に一致させることができます。
* **型 (MNTOKEN)**:フィールドタイプ。

   フィールドタイプは汎用です。 Adobe Campaignでは、インストールされているデータベースの種類に応じて、定義されているタイプを、構造の更新時にインストールされたデータベースに固有の値に変更します。

   使用可能なタイプのリスト：

   * いずれか
   * bin
   * blob
   * ブール値
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

   「@type」属性が空のままの場合、Adobe Campaignはデフォルトで、長さが 100 の文字列 (STRING) をフィールドにリンクします。

   フィールドのタイプが STRING で、フィールドの名前が「@sqlname」属性の存在で指定されていない場合、データベース内のフィールド名の前に自動的に「s」が付きます。 この動作モードは、INTEGER (i)、DOUBLE (d)、DATES (ts) タイプのフィールドと同様です。

* **userEnum (string)**:は、「open」列挙の内部名を受け取ります。 列挙の値は、インターフェイスでユーザーが定義できます。
* **visibleIf (string)**:は、属性の表示/非表示を切り替える XTK 式の形式で条件を定義します。

   >[!IMPORTANT]
   >
   >属性は非表示ですが、そのデータには引き続きアクセスできます。

* **xml（ブール値）**:このオプションを有効にした場合、フィールドの値には、リンクされた SQL フィールドは含まれません。 Adobe Campaignは、レコードストレージ用にテキストタイプ「mData」フィールドを作成します。 つまり、これらのフィールドにはフィルターや並べ替えが含まれていません。

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

「@datapolicy」を使用した XML フィールドの宣言：

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

「専用」タイプの「@feature」の例：

```
<attribute name="field1" label="Field 1" type="long" feature="dedicated"/>
<attribute name="field1" label="Field 1" type="long" feature="dedicated" sqlname="sField1" sqltable="Ft_recipient_field1"/>
```
