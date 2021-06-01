---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: e4d34f56-b065-4dce-8974-11dc2767873a
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# 属性要素{#attribute--element}

## コンテンツモデル{#content-model}

属性：==help

## 属性 {#attributes}

_operation （文字列）、advanced (boolean)、 applicableIf （文字列）、 autoIncrement （ブール値）、 belonsTo （文字列）、 dataPolicy （文字列）、 dbEnum （文字列）、 defOnDuplicate （ブール値）、 default （文字列）、 desc （文字列）、 enum （文字列）、 expr （文字列）、 feature （文字列）、 feature （文字列）、 feature （文字列）、 featureDutureDatureDature Date （ブール値）img （文字列）、inout （文字列）、label （文字列）、length （文字列）、ローカライズ可能（ブール値）、name (MNTOKEN)、 notNull （ブール値）、 pkgStatus （文字列）、 ref （文字列）、必須（ブール値）、 sql （ブール値）、 sqlDefault （文字列）、 sqlname （文字列）、 target （文字列）、Default (string), translatedExpr (string), type (MNTOKEN), user (boolean), userEnum (string), visibleIf (string), xml (boolean)

## 親 {#parents}

`<element>`

## 子 {#children}

`<help>`

## 説明 {#description}

`<attribute>` 要素を使用すると、データベース内にフィールドを定義できます。

## {#use-and-context-of-use}の使用と使用のコンテキスト

`<attribute>` 要素は、要素内で宣言する必要があ `<element>` ります。

`<srcschema>`内で`<attribute>`要素が定義されている順序は、データベース内のフィールド作成順序には影響しません。 作成順はアルファベット順になります。

## 属性の説明{#attribute-description}

* **_operation （文字列）**:データベースに書き込むタイプを定義します。

   この属性は、主に標準のスキーマを拡張する際に使用されます。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:紐付けのみ。 つまり、Adobe Campaignは更新せずに要素を回復し、要素が存在しない場合はエラーを生成します。
   * &quot;insertOrUpdate&quot;:を挿入して更新します。 つまり、Adobe Campaignは要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 つまり、Adobe Campaignは要素を更新するか、存在しない場合はエラーを生成します。
   * &quot;delete&quot;:削除します。 つまり、Adobe Campaignは要素を復元および削除します。

* **詳細（ブール値）**:このオプションを有効にすると(@advanced=&quot;true&quot;)、フォームでリストを設定するためにアクセス可能なフィールドのリストの属性を非表示にできます。
* **applicableIf (string)**:この属性を使用すると、フィールドをオプションにできます。制約に従う場合、データベースを更新する際に`<attribute>`要素が考慮されます。 「applicableIf」はXTK式を受け取ります。
* **autoIncrement（ブール値）**:このオプションを有効にすると、フィールドがカウンターになります。これにより、値を増分できます（ほとんどの場合はID）。 （外部使用）
* **belongsTo（文字列）**:は、フィールドを共有するテーブルの名前と名前空間を取得し、属性が宣言されているスキーマを入力します。（`<schema>`でのみ使用）。
* **dataPolicy （文字列）**:では、「SQLまたはXML」フィールドで許可する値に対して承認制約を指定できます。この属性の値は次のとおりです。

   * &quot;none&quot;:値なし
   * &quot;smartCase&quot;:先頭文字の大文字
   * &quot;lowerCase&quot;:すべて小文字
   * &quot;upperCase&quot;:すべて大文字
   * &quot;email&quot;:Eメールアドレス
   * &quot;phone&quot;:電話番号
   * &quot;identifier&quot;:identifier name
   * &quot;resIdentifier&quot;:ファイル名

* **dbEnum（文字列）**:は、「閉じられた」列挙の内部名を受け取ります。列挙の値は、`<srcschema>`で定義する必要があります。
* **defOnDuplicate（ブール値）**:この属性が有効になっている場合、レコードの複製時に、デフォルト値(@defaultで定義)が自動的にレコードに再適用されます。
* **デフォルト（文字列）**:を使用すると、デフォルトのフィールドの値を定義できます（関数の呼び出し、デフォルト値）。この属性は、XTK式を受け取ります。
* **desc（文字列）**:属性の説明を挿入できます。この説明は、インターフェイスのステータスバーに表示されます。
* **編集（文字列）**:この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum （文字列）**:は、フィールドにリンクされている列挙の名前を受け取ります。列挙は、同じスキーマまたはリモートスキーマに挿入できます。
* **式（文字列）**:フィールドの事前計算式を定義します。この属性は、XpathまたはXTK式を受け取ります。
* **機能（文字列）**:特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルの格納に使用されます。指定できる値は次のとおりです。

   * &quot;shared&quot;:コンテンツは、データタイプごとに共有テーブルに格納されます
   * &quot;dedicated&quot;:コンテンツは専用のテーブルに格納されます

   SQL特性テーブルは、特性タイプに基づいて自動的に作成されます。

   * 専用：`Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

   次の2種類の特性フィールドがあります。単一の値が特性に対して承認される単純なoà¹フィールドと、複数の選択フィールド（複数の値を含むコレクション要素に特性がリンクされる）。

   スキーマ内で特性が定義される場合、このスキーマは、単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されません）。

* **featureDate（ブール値）**:属性が「@feature」特性フィールドにリンクされている。値が「true」の場合は、値が最後に更新された日時を確認できます。
* **img （文字列）**:フィールドにリンクされた画像のパス（名前空間+画像名）を定義できます(例：img=&quot;cus:mypicture.jpg&quot;)として渡されます。物理的には、イメージをアプリケーションサーバーに読み込む必要があります。
* **label（文字列）**:フィールドにリンクされたラベル。主に、インターフェイスのユーザー向けのラベルです。これにより、命名の制約を回避できます。
* **長さ（文字列）**:最大「string」タイプのSQLフィールドの値の文字数。 「@length」属性が指定されていない場合、Adobe Campaignは自動的に255文字のフィールドを作成します。
* **localizable（ブール値）**:有効になっている場合、この属性は、翻訳用の「@label」属性の値を復元するように収集ツールに指示します（内部使用）。
* **名前(MNTOKEN)**:テーブルのフィールド名と一致する属性の名前。「@name」属性の値は、短く、できれば英語で記述し、XMLの命名規則に従う必要があります。

   スキーマがデータベースに書き込まれると、Adobe Campaignによって、フィールド名にプレフィックスが自動的に追加されます。

   * &quot;i&quot;:プレフィックスを使用します。
   * &quot;d&quot;:「double」型のプレフィックス。
   * &quot;s&quot;:プレフィックスを使用します。
   * &quot;ts&quot;:プレフィックスを使用します。

   テーブル内のフィールドの名前を完全に定義するには、属性を定義する際に「@sqlname」オプションを使用します。

* **notNull（ブール値）**:では、データベース内のNULLレコードの管理に関するAdobe Campaignの動作を再定義できます。デフォルトでは、数値フィールドはnullではなく、文字列および日付タイプのフィールドはnullにできます。
* **pkgStatus （文字列）**:パッケージのエクスポート時に、「@pkgStatus」の値に応じて値が考慮されます。

   * &quot;always&quot;:常に存在する
   * &quot;never&quot;:存在しない
   * &quot;default （または何も）&quot;:値は、デフォルト値の場合や、他のインスタンスと互換性のない内部フィールドでない場合を除き、エクスポートされます。

* **ref（文字列）**:この属性は、複数のスキーマ(定 `<attribute>` 義ファクタリング)で共有される要素への参照を定義します。定義は現在のスキーマにコピーされません。
* **必須（ブール値）**:この属性が有効になっている場合(@required=&quot;true&quot;)、インターフェイスでフィールドがハイライト表示されます。フィールドのラベルは、フォームでは赤色で表示されます。
* **sql（ブール値）**:この属性が有効になっている場合(@sql=&quot;true&quot;)、属性を含む要素にxml=&quot;true&quot;プロパティが含まれている場合でも、SQL属性を強制的に保存します。
* **sqlDefault（文字列）**:この属性を使用すると、@notNull属性が有効になっている場合に、データベースの更新に使用するデフォルト値を定義できます。属性の作成後にこの属性を追加した場合、新しいレコードでもスキーマの動作は変更されません。 スキーマを変更し、新しいレコードの値を更新するには、属性を削除して、再度作成する必要があります。
* **sqlname （文字列）**:」フィールドの値を指定します。@sqlnameを指定しない場合、「@name」属性の値がデフォルトで使用されます。 スキーマがデータベースに書き込まれると、フィールドのタイプに応じてプレフィックスが自動的に追加されます。
* **テンプレート（文字列）**:この属性は、複数のスキーマで共有さ `<attribute>` れる要素への参照を定義します。定義は、現在のスキーマに自動的にコピーされます。
* **translatedDefault（文字列）**:「@default」属性が見つかった場合、「@translatedDefault」を使用して、翻訳ツール（内部使用）で収集される式を再定義し、@defaultで定義された式に一致するようにします。
* **translatedExpr（文字列）**:「@expr」属性が存在する場合、「@translatedExpr」属性を使用して、翻訳ツール（内部使用）で収集される式を再定義し、@exprで定義された式に一致させることができます。
* **型(MNTOKEN)**:フィールドタイプ。

   フィールドタイプは汎用です。 Adobe Campaignでは、インストールされているデータベースのタイプに応じて、定義されたタイプを、構造の更新時にインストールされたデータベースに固有の値に変更します。

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

   「@type」属性が空の場合、Adobe Campaignはデフォルトで、長さ100の文字列(STRING)をフィールドにリンクします。

   フィールドの型がSTRINGで、フィールドの名前が「@sqlname」属性の存在で指定されていない場合、データベース内のフィールドの名前の前に自動的に「s」が付きます。 この動作モードは、INTEGER (i)、DOUBLE (d)、DATES (ts)タイプのフィールドと同様です。

* **userEnum（文字列）**:は、「open」列挙の内部名を受け取ります。列挙の値は、インターフェイスでユーザーが定義できます。
* **visibleIf（文字列）**:属性の表示/非表示を切り替える条件をXTK式の形式で定義します。

   >[!IMPORTANT]
   >
   >属性は非表示ですが、そのデータには引き続きアクセスできます。

* **xml（ブール値）**:このオプションを有効にした場合、フィールドの値にはリンクされたSQLフィールドは含まれません。Adobe Campaignは、レコードストレージ用にテキストタイプ「mData」フィールドを作成します。 つまり、これらのフィールドにフィルターや並べ替えが適用されません。

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

「@datapolicy」を使用したXMLフィールドの宣言：

```
<attribute dataPolicy="phone" desc="Mobile number" label="Mobile"
     length="32" name="mobilePhone" sqlname="sMobilePhone" type="string"/>
```

「@applicableIf」の例：「次を含む」属性は、国数が20を超える場合にのみ作成されます。

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
