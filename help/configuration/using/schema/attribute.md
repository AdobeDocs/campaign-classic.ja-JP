---
solution: Campaign Classic
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
translation-type: tm+mt
source-git-commit: 922257b157f8d76d6e703b0510ff689d1aa4d067
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---


# 属性要素{#attribute--element}

## コンテンツモデル{#content-model}

attribute:==help

## 属性 {#attributes}

_operation (string)、advanced (boolean)、applicableIf (string)、autoIncrement (boolean)、belonsTo (string)、dataPolicy (string)、dbEnum (string)、defOnDuplicate (boolean)、default (string)、edit (string)、enum (string)、 feature (string)、featureDate (boolean)img （文字列）、inout （文字列）、label （文字列）、length （文字列）、localizable (boolean)、name (MNTOKEN)、notNull (boolean)、pkgStatus （文字列）、ref （文字列）、required (boolean)、sqlDefault （文字列）、sqlname （文字列）、ターゲット（文字列）、template （文字列）translatedDefault(string)、translatedExpr(string)、type(MNTOKEN)、user(boolean)、userEnum(string)、visibleIf(string)、xml(boolean)

## 親{#parents}

`<element>`

## 子 {#children}

`<help>`

## 説明 {#description}

`<attribute>` 要素を使用すると、データベース内でフィールドを定義できます。

## 使用と使用のコンテキスト{#use-and-context-of-use}

`<attribute>` 要素は `<element>` 要素内で宣言する必要があります。

`<attribute>`要素が`<srcschema>`で定義されるシーケンスは、データベース内のフィールド作成シーケンスに影響を与えません。 作成シーケンスはアルファベット順になります。

## 属性の説明{#attribute-description}

* **_operation (string)**:データベースに書き込むタイプを定義します。

   この属性は主に、標準搭載されたスキーマを拡張する場合に使用します。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:和解のみ。 つまり、Adobe Campaignは、要素を更新せずに回復します。要素が存在しない場合はエラーが発生します。
   * &quot;insertOrUpdate&quot;:挿入時に更新します。 つまり、Adobe Campaignは、要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 これは、Adobe Campaignが要素を更新するか、存在しない場合はエラーを生成することを意味します。
   * &quot;delete&quot;:削除。 つまり、Adobe Campaignは要素を回復および削除します。

* **advanced(boolean)**:このオプションをアクティブ化すると(@advanced=&quot;true&quot;)、フォーム内のリストの設定にアクセスできるフィールドのリスト上で属性を非表示にできます。
* **applicableIf (string)**:この属性を使用すると、フィールドをオプションにできます。`<attribute>`要素は、制約が適合している場合にデータベースを更新する際に考慮されます。 &quot;applicableIf&quot;がXTK式を受け取ります。
* **autoIncrement (boolean)**:このオプションを有効にすると、フィールドはカウンターになります。これにより、値を増やすことができます（ほとんどの場合ID）。 （外部使用）
* **belongsTo (string)**:フィールドを共有するテーブルの名前と名前空間を取得し、属性が宣言されているスキーマに値を設定します。（`<schema>`でのみ使用）。
* **dataPolicy (string)**:「SQL or XML」フィールドで許可される値に対して、承認制約を指定できます。この属性の値は次のとおりです。

   * &quot;none&quot;:値なし
   * &quot;smartCase&quot;:大文字の先頭文字
   * &quot;lowerCase&quot;:小文字全体
   * &quot;upperCase&quot;:大文字のみ
   * &quot;email&quot;:電子メールアドレス
   * &quot;phone&quot;:電話番号
   * &quot;識別子&quot;:識別子名
   * &quot;resIdentifier&quot;:ファイル名

* **dbEnum (string)**:は、「閉じた」定義済みリストの内部名を受け取ります。定義済みリスト値は`<srcschema>`で定義する必要があります。
* **defOnDuplicate (boolean)**:この属性がアクティブな場合、レコードが重複するときに、（@defaultで定義された）デフォルト値が自動的にレコードに再適用されます。
* **default（文字列）**:デフォルトのフィールドの値（関数の呼び出し、デフォルト値）を定義できます。この属性はXTK式を受け取ります。
* **desc（文字列）**:属性の説明を挿入できます。この説明は、インターフェイスのステータスバーに表示されます。
* **編集（文字列）**:この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum（文字列）**:は、フィールドにリンクされている定義済みリストの名前を受け取ります。定義済みリストは、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**:フィールドの事前計算式を定義します。この属性は、XpathまたはXTK式を受け取ります。
* **機能（文字列）**:特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルのストレージと共に使用されます。指定できる値は次のとおりです。

   * &quot;共有&quot;:コンテンツは、データ型ごとに共有テーブルに保存されます
   * &quot;dedicated”:コンテンツは専用のテーブルに格納される

   SQL特性テーブルは、次の特性タイプに基づいて自動的に作成されます。

   * 専用：`Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

   次の2種類の特性フィールドがあります。単一の値が特性に対して承認される単純なoa headフィールドと、oa hecoseフィールドです。このフィールドでは、特性が複数の値を含む収集要素にリンクされます。

   特性がスキーマで定義される場合、このスキーマは、単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されません）。

* **featureDate (boolean)**:属性が「@feature」特性フィールドにリンクされている。値が「true」の場合は、値が最後に更新された日時を確認できます。
* **img （文字列）**:フィールドにリンクされた画像のパス(名前空間+画像名)を定義できます(例：img=&quot;cus:mypicture.jpg&quot;)。物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **label (string)**:フィールドにリンクされているラベル。ほとんどの場合、インターフェイス内のユーザーにリンクされているラベルです。命名の制約を回避できます。
* **length (string)**:最大「string」型SQLフィールドの値の文字数。 「@length」属性が指定されていない場合、Adobe Campaignは255文字のフィールドを自動的に作成します。
* **localizable (boolean)**:この属性がアクティブ化されている場合、収集ツールに対して翻訳用の「@label」属性の値を復元するよう指示します（内部使用）。
* **name (MNTOKEN)**:テーブルのフィールドの名前と一致する属性の名前。「@name」属性の値は、短く、できれば英語で指定し、XMLの命名規則に従う必要があります。

   スキーマがデータベースに書き込まれると、フィールド名にプリフィックスがAdobe Campaign別に自動的に追加されます。

   * &quot;i&quot;:プレフィックスの値を指定します。
   * &quot;d&quot;:プレフィックスが表示されます。
   * &quot;s&quot;:のプレフィックスを指定します。
   * &quot;ts&quot;:プレフィックスに値を入力します。

   テーブル内のフィールドの名前を完全に定義するには、属性を定義する際に「@sqlname」オプションを使用します。

* **notNull (boolean)**:データベース内のNULLレコードの管理に関するAdobe Campaignの動作を再定義できます。デフォルトでは、数値フィールドはnullではなく、文字列フィールドおよび日付型フィールドはnullにできます。
* **pkgStatus (string)**:パッケージのエクスポート中、「@pkgStatus」の値に応じて値が考慮されます。

   * &quot;always&quot;:常に存在する
   * &quot;never&quot;:存在しない
   * &quot;default (or nothing)&quot;:デフォルト値である場合や、他のインスタンスと互換性がない内部フィールドでない場合を除き、値がエクスポートされます。

* **ref （文字列）**:この属性は、複数のスキーマ（定義ファクタリング）が共有する `<attribute>` 要素への参照を定義します。定義は現在のスキーマにコピーされません。
* **required (boolean)**:この属性がアクティブ化された場合(@required=&quot;true&quot;)、インターフェイスでフィールドがハイライト表示されます。フィールドのラベルは、フォームでは赤で表示されます。
* **sql (boolean)**:この属性がアクティブ化される(@sql=&quot;true&quot;)と、属性を含む要素にxml=&quot;true&quot;プロパティが含まれている場合でも、SQL属性のストレージが強制されます。
* **sqlDefault (string)**:この属性を使用すると、@notNull属性がアクティブ化されている場合に、データベースの更新に使用されるデフォルト値を定義できます。属性の作成後にこの属性を追加した場合、新しいレコードでもスキーマの動作は変更されません。 スキーマを変更し、新しいレコードの値を更新するには、属性を削除して、もう一度作成する必要があります。
* **sqlname （文字列）**:の値を含む)を設定する必要があります。@sqlnameを指定しない場合、「@name」属性の値がデフォルトで使用されます。 スキーマがデータベースに書き込まれると、フィールドの種類に応じてプリフィックスが自動的に追加されます。
* **template (string)**:この属性は、複数のスキーマが共有する `<attribute>` 要素への参照を定義します。定義は自動的に現在のスキーマにコピーされます。
* **translatedDefault(string)**:「@default」属性が見つかった場合、「@translatedDefault」を使用すると、式を再定義して、翻訳ツールによって収集される@defaultで定義されているのと一致させることができます（内部使用）。
* **translatedExpr (string)**:「@expr」属性が存在する場合、「@translatedExpr」属性を使用すると、式を再定義して@exprで定義されているものと一致させ、翻訳ツールによって収集されるようにすることができます（内部使用）。
* **type (MNTOKEN)**:フィールドタイプ。

   フィールドタイプは汎用です。 Adobe Campaignは、インストールされているデータベースの種類に応じて、定義された型を、構造の更新時にインストールされたデータベースに固有の値に変更します。

   使用可能なタイプのリスト:

   * いずれか
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

* **userEnum (string)**:は、「open」定義済みリストの内部名を受け取ります。定義済みリストの値は、インターフェイス内のユーザーが定義できます。
* **visibleIf (string)**:属性の表示/非表示を切り替える条件をXTK式の形式で定義します。

   >[!IMPORTANT]
   >
   >属性は非表示になりますが、そのデータにはアクセスできます。

* **xml（ブール値）**:このオプションが有効になっている場合、フィールドの値にリンクされたSQLフィールドはありません。Adobe Campaignは、レコードストレージ用にテキストタイプ「mData」フィールドを作成します。 これは、これらのフィールドに対してフィルタや並べ替えが行われていないことを意味します。

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

「@applicableIf」の例：「次を含む」属性は、国数が20を超える場合にのみ作成されます。

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
