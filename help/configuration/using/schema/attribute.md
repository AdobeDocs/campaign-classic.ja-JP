---
product: campaign
title: 要素と属性 – 属性要素
description: 要素と属性
feature: Schema Extension
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: e4d34f56-b065-4dce-8974-11dc2767873a
source-git-commit: 728848eab059fc669c241346a2ff1feebd79222c
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 1%

---

# 属性要素 {#attribute--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model}

属性：==help

## 属性 {#attributes}

_operation （string）、advanced （boolean）、applicableIf （string）、autoIncrement （boolean）、belongsTo （string）、dataPolicy （string）、dbEnum （string）、defOnDuplicate （boolean）、default （string）、desc （string）、edit （string）、enum （string）、expr （string）、feature （string）、featureDate （boolean）、img （string）、inout （string）、length （string）、localizable （boolean）、name （MNTOKEN）、notNull （boolean）、pkgStatus （string）、ref （string）、required （boolean）、sql （boolean）、sqlDefault （string）、sqlDefault （string）、sqlname （string）、sqltable （string）、target （MNTOKEN）、template （string）、translatedDefault （string）、translatedExpr （string）、type （MNTOKEN）、user （boolean）、userEnum （string）、visibleIf （string）、xml （boolean）

## 親 {#parents}

`<element>`

## 子 {#children}

`<help>`

## 説明 {#description}

`<attribute>` 要素を使用して、データベース内のフィールドを定義できます。

## 用途および使用コンテキスト {#use-and-context-of-use}

`<attribute>` 要素は、`<element>` 要素で宣言する必要があります。

`<srcschema>` で定義され `<attribute>` 要素の順序は、データベースのフィールド作成順序には影響しません。 作成シーケンスはアルファベット順になります。

## 属性の説明 {#attribute-description}

* **_operation （文字列）**：データベースへの書き込みのタイプを定義します。

  この属性は、主に標準スキーマを拡張する際に使用されます。

  アクセス可能な値は次のとおりです。

   * 「なし」：紐付けのみ。 つまり、Adobe Campaignは要素を更新せずに復元し、要素が存在しない場合はエラーを生成します。
   * &quot;insertOrUpdate&quot;：挿入で更新します。 つまり、Adobe Campaignは要素を更新し、存在しない場合は作成します。
   * 「挿入」：挿入。 つまり、Adobe Campaignは、存在するかどうかを確認せずに要素を挿入します。
   * 「更新」：更新。 つまり、Adobe Campaignは要素を更新するか、要素が存在しない場合はエラーを生成します。
   * 「削除」：削除。 つまり、Adobe Campaignは要素を復元して削除します。

* **詳細（ブール値）**：このオプションを有効にすると（@advanced=&quot;true&quot;）、フォームでのリストの設定にアクセスできる使用可能なフィールドのリストで属性を非表示にできます。
* **applicableIf （string）**：この属性を使用すると、フィールドをオプションにすることができます。 制約が準拠している場合、データベースの更新時に `<attribute>` 要素が考慮されます。 「applicableIf」は XTK 式を受け取ります。
* **autoIncrement （ブール値）**：このオプションを有効にすると、フィールドはカウンターになります。 これにより、値（主に ID）を増分できます。 （外部使用）
* **belongsTo （string）**：フィールドを共有するテーブルの名前と名前空間を受け取り、属性が宣言されているスキーマを設定します。 （`<schema>` でのみ使用）。
* **dataPolicy （文字列）**:SQL または XML フィールドで許可される値に対して承認制約を指定できます。 この属性の値は次のとおりです。

   * 「なし」：値なし
   * 「smartCase」：最初の文字は大文字
   * 「lowerCase」：すべて小文字
   * 「upperCase」：すべて大文字
   * 「email」：メールアドレス
   * 「phone」：電話番号
   * &quot;identifier&quot;：識別子名
   * &quot;resIdentifier&quot;: ファイル名

* **dbEnum （string）**:「クローズド」列挙の内部名を受け取ります。 定義済みリストの値は、`<srcschema>` で定義する必要があります。
* **defOnDuplicate （boolean）**：この属性を有効にすると、レコードが複製されたときに、デフォルト値（@default で定義）が自動的にレコードに再適用されます。
* **default （文字列）**：デフォルトフィールドの値を定義できます（関数の呼び出し、デフォルト値）。 この属性は XTK 式を受け取ります。
* **desc （string）**：属性の説明を挿入できます。 この説明は、要素の概要と用途を理解するために使用されます。 フォームに表示できます。
* **edit （string）**：この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum （string）**：フィールドにリンクされた定義済みリストの名前を受け取ります。 定義済みリストは、同じスキーマまたはリモートスキーマに挿入できます。
* **expr （文字列）**：フィールドの事前計算式を定義します。 この属性は、Xpath または XTK 式を受け取ります。
* **feature （string）**：特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルへの格納は保持されます。 指定できる値は次のとおりです。

   * 「共有」：コンテンツは、データタイプごとに共有テーブルに保存されます
   * 「dedicated」：コンテンツは専用テーブルに保存されます

  SQL 特性テーブルは、特性タイプに基づいて自動的に作成されます。

   * 専用：`Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * 共有：`Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

  特性フィールドには、特性に対して単一の値が付与される単純な oà<sup>1</sup> フィールドと、複数の値を含むことができる収集要素に特性がリンクされる oà<sup>1</sup> 複数選択フィールドの 2 種類があります。

  スキーマ内で特性が定義される場合、このスキーマには、単一のフィールドに基づくメインキーが必要です（複合キーは許可されていません）。

* **featureDate （ブール値）**:「@feature」特性フィールドにリンクされた属性。 値が「true」の場合は、値が最後に更新された日時を調べることができます。
* **img （文字列）**：フィールドにリンクされた画像のパスを定義します（名前空間+画像名）（例：img=&quot;cus:mypicture.jpg&quot;）。 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **label （string）**：フィールドにリンクされたラベルで、主にインターフェイス内のユーザーが宛先となります。 これにより、名前付け制約を回避できます。
* **length （string）**：最大 「文字列」タイプの SQL フィールドの値の文字数。 「@length」属性を指定しない場合、Adobe Campaignは自動的に 255 文字のフィールドを作成します。
* **localizable （boolean）**：有効な場合、この属性は、翻訳の「@label」属性の値を復元するようにコレクションツールに指示します（内部使用）。
* **name （MNTOKEN）**：テーブルのフィールド名と一致する属性の名前。 「@name」属性の値は短く（できれば英語）、XML 命名規則に従う必要があります。

  スキーマがデータベースに書き込まれると、Adobe Campaignによって、フィールド名にプレフィックスが自動的に追加されます。

   * 「i」:「integer」タイプのプレフィックス。
   * &quot;d&quot;: 「double」タイプのプレフィックス。
   * 「s」：文字列タイプのプレフィックス。
   * 「ts」:「日付」タイプのプレフィックス。

  テーブルのフィールド名を完全に定義するには、属性の定義時に「@sqlname」オプションを使用します。

* **notNull （ブール値）**：データベース内の NULL レコードの管理に関するAdobe Campaignの動作を再定義できます。 デフォルトでは、数値フィールドは null ではなく、文字列および日付タイプのフィールドは null にできます。
* **pkgStatus （文字列）**：パッケージのエクスポート中に、「@pkgStatus」の値に応じて値が考慮されます。

   * 「常時」：常時ある
   * 「なし」：なし
   * 「default （or nothing）」：デフォルト値の場合と、他のインスタンスと互換性のない内部フィールドでない場合を除き、値が書き出されます。

* **ref （string）**：この属性は、複数のスキーマで共有される `<attribute>` 要素への参照を定義します（定義ファクタリング）。 定義は現在のスキーマにコピーされません。
* **必須（ブール値）**：この属性をアクティブにする（@required=&quot;true&quot;）と、インターフェイスでフィールドがハイライト表示されます。 フォームではフィールドのラベルは赤になります。
* **sql （ブール）**：この属性がアクティブ化されている場合（@sql=&quot;true&quot;）、属性を含む要素に xml=&quot;true&quot; プロパティが設定されている場合でも、SQL 属性が強制的に格納されます。
* **sqlDefault （string）**：この属性を使用すると、@notNull 属性が有効化された場合にデータベースの更新に考慮されるデフォルト値を定義できます。 この属性が属性の作成後に追加された場合、新しいレコードに対してもスキーマの動作は変更されません。 スキーマを変更し、新しいレコードの値を更新するには、属性を削除して再度作成する必要があります。
* **sqlname （文字列）**：テーブルの作成中のフィールドの。 @sqlname を指定しない場合、「@name」属性の値がデフォルトで使用されます。 データベースにスキーマを書き込むと、フィールドのタイプに応じて、プレフィックスが自動的に追加されます。
* **template （文字列）**：この属性は、複数のスキーマで共有される `<attribute>` 要素への参照を定義します。 定義は、現在のスキーマに自動的にコピーされます。
* **translatedDefault （string）**:「@default」属性が見つかった場合、「@translatedDefault」を使用すると、@default で定義された式と一致し、翻訳ツールによって収集される式を再定義できます（内部使用）。
* **translatedExpr （文字列）**:「@expr」属性が存在する場合、「@translatedExpr」属性を使用すると、@expr で定義された式と一致し、翻訳ツールによって収集される式を再定義できます（内部使用）。
* **type （MNTOKEN）**：フィールドタイプ。

  フィールドタイプは汎用です。 Adobe Campaignは、インストールされているデータベースの種類に応じて、定義された種類を、構造の更新中にインストールされたデータベースに固有の値に変更します。

  使用可能なタイプのリスト：

   * いずれか
   * bin
   * blob
   * ブール値
   * バイト
   * CDATA
   * 日時
   * datetimetz
   * datetimenoz
   * 日付
   * 倍精度浮動小数点数
   * 列挙
   * 浮動小数点数
   * html
   * int64
   * リンク
   * 長い
   * メモ
   * MNTOKEN
   * 割合
   * primarykey
   * 短い
   * 文字列
   * 時間
   * 期間
   * uuid

  「@type」属性を空のままにすると、Adobe Campaignはデフォルトで長さが 100 の文字列（STRING）をフィールドにリンクします。

  フィールドが文字列型で、フィールド名が「@sqlname」属性によって指定されていない場合、データベース内のフィールド名の先頭には自動的に「s」が付きます。 この操作モードは、INTEGER （i）、DOUBLE （d）、DATES （ts）タイプのフィールドと似ています。

* **userEnum （文字列）**:「開いている」列挙の内部名を受け取ります。 定義済みリストの値は、インターフェイスでユーザーが定義できます。
* **visibleIf （文字列）**：属性を表示または非表示にする条件を XTK 式の形式で定義します。

  >[!IMPORTANT]
  >
  >属性は非表示ですが、そのデータには引き続きアクセスできます。

* **xml （ブール値）**：このオプションを有効にすると、フィールドの値にリンクされた SQL フィールドがなくなります。 Adobe Campaignは、レコードのストレージ用にテキストタイプ「mData」フィールドを作成します。 つまり、これらのフィールドに対してフィルタリングや並べ替えは行われません。

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

「@datapolicy」を含む XML フィールドの宣言：

```
<attribute dataPolicy="phone" desc="Mobile number" label="Mobile"
     length="32" name="mobilePhone" sqlname="sMobilePhone" type="string"/>
```

「@applicableIf」の例：「contains」属性は、国の数が 20 を超える場合にのみ作成されます。

```
<attribute length="100" name="Continent" type="string" applicableIf="@country > 20"/>
```

「共有」タイプの「@feature」を使用した例：

```
<attribute name="field1" label="Field 1" type="long" feature="shared"/>
<attribute name="field1" label="Field 1" type="long" feature="shared" sqlname="126" sqltable="Ft_Content_Long"/>
```

「dedicated」タイプの「@feature」を使用した例：

```
<attribute name="field1" label="Field 1" type="long" feature="dedicated"/>
<attribute name="field1" label="Field 1" type="long" feature="dedicated" sqlname="sField1" sqltable="Ft_recipient_field1"/>
```
