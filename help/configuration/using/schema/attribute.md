---
product: campaign
title: 要素と属性 – 属性要素
description: 要素と属性
feature: Schema Extension
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: e4d34f56-b065-4dce-8974-11dc2767873a
source-git-commit: 254c89490fefa5d405bcecd2f1781df46450a873
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 1%

---

# 属性要素 {#attribute--element}


## コンテンツモデル {#content-model}

属性：==help

## 属性 {#attributes}

_operation （文字列）、advanced （ブール値）、applicableIf （文字列）、autoIncrement （ブール値）、belongsTo （文字列）、dataPolicy （文字列）、dbEnum （文字列）、defOnDuplicate （ブール値）、default （文字列）、desc （文字列）、edit （文字列）、enum （文字列）、expr （文字列）、featureDate （ブール値）、img （文字列）、inout （文字列）、label （文字列）、length （文字列）、localizable （ブール値）、name （NEN） notNull （ブール値）、pkgStatus （文字列）、ref （文字列）、必須（ブール値）、sql （ブール値）、sqlDefault （文字列）、sqlname （文字列）、sqltable （文字列）、target （MNTOKEN）、template （文字列）、translatedDefault （文字列）、translatedExpr （文字列）、type （MNTOKEN）、user （ブール値）、userEnum （文字列）、visibleIf （文字列）、xml （ブール値）

## 親 {#parents}

`<element>`

## 子 {#children}

`<help>`

## 説明 {#description}

`<attribute>`要素を使用すると、データベース内のフィールドを定義できます。

## 用途と使用状況 {#use-and-context-of-use}

`<attribute>`要素は`<element>`要素で宣言する必要があります。

`<attribute>`要素が`<srcschema>`で定義されているシーケンスは、データベース内のフィールド作成シーケンスには影響しません。 作成シーケンスはアルファベット順になります。

## 属性の説明 {#attribute-description}

* **_operation （文字列）**: データベースへの書き込みの種類を定義します。

  この属性は、主にすぐに使用できるスキーマを拡張する場合に使用されます。

  アクセス可能な値は次のとおりです。

   * &quot;none&quot;：和解のみ。 つまり、Adobe Campaignはアップデートせずに復元したり、存在しない場合はエラーを発生させたりします。
   * &quot;insertOrUpdate&quot;：挿入で更新します。 つまり、Adobe Campaignがエレメントを更新するか、エレメントが存在しない場合はエレメントを作成します。
   * &quot;insert&quot;：挿入。 つまり、Adobe Campaignはエレメントが存在するかどうかを確認せずに挿入します。
   * &quot;update&quot;：更新します。 つまり、Adobe Campaignはエレメントを更新するか、エレメントが存在しない場合はエラーを生成します。
   * &quot;delete&quot;：削除。 つまり、Adobe Campaignは復元と削除を行います。

* **詳細（ブール値）**：このオプションがアクティブ化されている場合（@advanced=&quot;true&quot;）、フォームでリストを設定するためにアクセス可能な使用可能なフィールドのリストで属性を非表示にできます。
* **applicableIf （文字列）**：この属性を使用すると、フィールドをオプションにできます。 制約が準拠している場合、データベースを更新する際に、`<attribute>`要素が考慮されます。 &quot;applicableIf&quot;はXTK式を受け取ります。
* **autoIncrement （ブール値）**：このオプションがアクティブ化されると、フィールドはカウンターになります。 これにより、値（主にID）を増分できます。 （外部使用）
* **belongsTo （文字列）**: フィールドを共有するテーブルの名前と名前空間を取得し、属性が宣言されているスキーマに入力します。 （`<schema>`でのみ使用）。
* **dataPolicy （文字列）**: SQLまたはXML フィールドで許可される値に対する承認制約を指定できます。 この属性の値は次のとおりです。

   * &quot;none&quot;：値なし
   * &quot;smartCase&quot;：先頭の文字は大文字
   * &quot;lowerCase&quot;：すべて小文字
   * &quot;upperCase&quot;：すべて大文字
   * &quot;email&quot;: メールアドレス
   * &quot;phone&quot;：電話番号
   * &quot;identifier&quot;：識別子名
   * &quot;resIdentifier&quot;: ファイル名

* **dbEnum （文字列）**: 「クローズ済み」列挙の内部名を受け取ります。 列挙値は`<srcschema>`で定義する必要があります。
* **defOnDuplicate （boolean）**：この属性がアクティブ化されると、レコードが複製されると、デフォルト値（@defaultで定義）が自動的にレコードに再適用されます。
* **default （文字列）**: デフォルトフィールドの値（関数の呼び出し、デフォルト値）を定義できます。 この属性はXTK式を受け取ります。
* **desc （string）**：属性の説明を挿入できます。 この説明は、要素とその用途を理解するために使用されます。 フォームに表示できます。
* **編集（文字列）**：この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum （string）**: フィールドにリンクされた列挙の名前を受け取ります。 列挙は、同じスキーマまたはリモートスキーマに挿入できます。
* **expr （文字列）**: フィールドの事前計算式を定義します。 この属性は、XpathまたはXTK式を受け取ります。
* **機能（文字列）**：特性フィールドを定義します。これらのフィールドは、既存のテーブル内のデータを拡張するために使用されますが、追加テーブル内のストレージに使用されます。 使用できる値は次のとおりです。

   * 「共有」：コンテンツは、データタイプごとに共有テーブルに保存されます
   * 「専用」：コンテンツは専用テーブルに保存されます

  SQL特性テーブルは、特性タイプに基づいて自動的に作成されます。

   * 専用：`Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * 共有：`Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

  特性フィールドには2つのタイプがあります。単純なoà<sup>1</sup> フィールドでは、1つの値が特性に対して許可されます。また、oà<sup>1</sup>複数選択フィールドでは、特性が複数の値を含むコレクション要素にリンクされます。

  スキーマで特性が定義されている場合、このスキーマには1つのフィールドに基づくメインキーが必要です（複合キーは許可されていません）。

* **featureDate （boolean）**: 「@feature」特性フィールドにリンクされた属性。 値が「true」の場合、値が最後に更新された日時を確認できます。
* **img （文字列）**: フィールドにリンクされた画像（名前空間+画像名）のパスを定義できます（例：img=&quot;cus:mypicture.jpg&quot;）。 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **label （文字列）**: フィールドにリンクされたラベル。主にインターフェイス内のユーザーに送信されます。 これにより、命名制限を回避できます。
* **長さ（文字列）**：最大 「文字列」タイプのSQL フィールドの値の文字数。 「@length」属性が指定されていない場合、Adobe Campaignは自動的に255文字のフィールドを作成します。
* **ローカライズ可能（ブール値）**：この属性がアクティブ化されている場合、翻訳（内部使用）用に「@label」属性の値を回復するようにコレクションツールに指示します。
* **name （MNTOKEN）**: テーブル内のフィールドの名前と一致する属性の名前。 「@name」属性の値は短く、好ましくは英語で、XMLの命名規則に準拠している必要があります。

  スキーマがデータベースに書き込まれると、Adobe Campaignによってフィールド名に接頭辞が自動的に追加されます。

   * &quot;i&quot;: &#39;integer&#39;型のプレフィックス。
   * &quot;d&quot;: &#39;double&#39;型のプレフィックス。
   * &quot;s&quot;：文字列型の接頭辞。
   * &quot;ts&quot;: &#39;date&#39; タイプのプレフィックス。

  テーブル内のフィールド名を完全に定義するには、属性を定義するときに「@sqlname」オプションを使用します。

* **notNull （ブール値）**: データベース内のNULL レコードの管理に関するAdobe Campaignの動作を再定義できます。 デフォルトでは、数値フィールドはnullではなく、文字列フィールドと日付タイプフィールドはnullにすることができます。
* **pkgStatus （文字列）**: パッケージの書き出し中に、「@pkgStatus」の値に応じて値が考慮されます。

   * &quot;always&quot;：常に存在する
   * &quot;never&quot;: never present
   * 「デフォルト（または何も）」：値がデフォルト値であるか、または他のインスタンスと互換性のない内部フィールドでない場合を除いて、値が書き出されます。

* **ref （文字列）**：この属性は、複数のスキーマで共有されている`<attribute>`要素への参照（定義ファクタリング）を定義します。 定義は現在のスキーマにコピーされません。
* **必須（ブール値）**：この属性がアクティブ化されている場合（@required=&quot;true&quot;）、このフィールドはインターフェイスで強調表示されます。 フィールドのラベルはフォームで赤になります。
* **sql （ブール値）**：この属性がアクティブ化されている場合（@sql=&quot;true&quot;）、属性を含む要素にxml=&quot;true&quot; プロパティがある場合でも、SQL属性を強制的に保存します。
* **sqlDefault （文字列）**：この属性を使用すると、@notNull属性がアクティブ化されている場合にデータベースを更新するために考慮されるデフォルト値を定義できます。 属性の作成後にこの属性が追加された場合、新しいレコードでもスキーマの動作は変更されません。 スキーマを変更し、新しいレコードの値を更新するには、属性を削除して再度作成する必要があります。
* テーブル作成中のフィールドの&#x200B;**sqlname （文字列）**:。 @sqlnameを指定しない場合、「@name」属性の値がデフォルトで使用されます。 スキーマがデータベースに書き込まれると、フィールドのタイプに応じて接頭辞が自動的に追加されます。
* **テンプレート（文字列）**：この属性は、複数のスキーマで共有されている`<attribute>`要素への参照を定義します。 定義は現在のスキーマに自動的にコピーされます。
* **translatedDefault （string）**: 「@default」属性が見つかった場合、「@translatedDefault」を使用すると、翻訳ツールで収集される@defaultで定義された式と一致するように式を再定義できます（内部使用）。
* **translatedExpr （string）**: 「@expr」属性が存在する場合、「@translatedExpr」属性を使用すると、翻訳ツールで収集される@exprで定義された式と一致するように式を再定義できます（内部使用）。
* **type （MNTOKEN）**: フィールドタイプ。

  フィールドタイプは汎用です。 インストールされたデータベースのタイプに応じて、Adobe Campaignは、構造更新時にインストールされたデータベースに固有の値に定義されたタイプを変更します。

  使用可能なタイプのリスト：

   * いずれか
   * bin
   * blob
   * ブール値
   * バイト
   * CDATA
   * 日時
   * datetime
   * datetimenotz
   * 日付
   * 倍精度浮動小数点数
   * 列挙
   * 浮動小数点数
   * html
   * int64
   * リンク
   * 長整数
   * メモ
   * MN トークン
   * パーセント
   * primarykey
   * 短い
   * 文字列
   * 時間
   * 期間
   * uuid

  「@type」属性が空のままの場合、Adobe Campaignはデフォルトで100の長さの文字列（STRING）をフィールドにリンクします。

  フィールドがSTRING タイプで、フィールド名が「@sqlname」属性の存在によって指定されていない場合、データベース内のフィールド名の前には自動的に「s」が付けられます。 この動作モードは、INTEGER （i）、DOUBLE （d）、DATE （ts）タイプのフィールドと同様です。

* **userEnum （文字列）**:「open」列挙の内部名を受け取ります。 列挙の値は、インターフェイスでユーザーが定義できます。
* **visibleIf （文字列）**：属性を表示または非表示にするXTK式の形式で条件を定義します。

  >[!IMPORTANT]
  >
  >属性は非表示ですが、そのデータには引き続きアクセスできます。

* **xml （ブール値）**：このオプションが有効になっている場合、フィールドの値にはリンクされたSQL フィールドがありません。 Adobe Campaignは、レコードの保存用にテキストタイプ「mData」フィールドを作成します。 つまり、これらのフィールドにはフィルタリングや並べ替えがありません。

### 例 {#examples}

値がデータベースに保存されている列挙値の例：

```
    <enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>

    <element label="Sample" name="Sample">
       <attribute dbEnum="myEnum" length="100" name="Number" required="true" type="string"/>
    </element>     
```

「@datapolicy」を含むXML フィールドの宣言：

```
<attribute dataPolicy="phone" desc="Mobile number" label="Mobile"
     length="32" name="mobilePhone" sqlname="sMobilePhone" type="string"/>
```

「@applicableIf」の例：「contains」属性は、国数が20を超える場合にのみ作成されます。

```
<attribute length="100" name="Continent" type="string" applicableIf="@country > 20"/>
```

「共有」タイプの「@feature」を含む例：

```
<attribute name="field1" label="Field 1" type="long" feature="shared"/>
<attribute name="field1" label="Field 1" type="long" feature="shared" sqlname="126" sqltable="Ft_Content_Long"/>
```

「dedicated」型の「@feature」を含む例：

```
<attribute name="field1" label="Field 1" type="long" feature="dedicated"/>
<attribute name="field1" label="Field 1" type="long" feature="dedicated" sqlname="sField1" sqltable="Ft_recipient_field1"/>
```
