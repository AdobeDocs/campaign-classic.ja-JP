---
product: campaign
title: スキーマ要素と属性 – エレメント要素
description: 要素エレメント
feature: Schema Extension
exl-id: 60f15ae5-b2bd-48f9-aa45-8f795a3071aa
TQID: https://experienceleague.adobe.com/MbBmc-H9eZfmqWy-vZb6dd-m-l0G-UxtY-HAboNURjc
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 2035
ht-degree: 1%

---

# 要素エレメント {#element--element}


## コンテンツモデル {#content-model-4}

element:==（attribute | compute-string | dbindex | default | element | help | join | key | sysFilter | translatedDefault）

## 属性 {#attributes-4}

_operation （文字列）、advanced （ブール値）、aggregate （文字列）、applicableIf （文字列）、autopk （ブール値）、belongsTo （文字列）、convDate （文字列）、dataPolicy （文字列）、dataSource （文字列）、dbEnum （文字列）、defOnDuplicate （ブール値）、default （文字列）、desc （文字列）、displayAsField （ブール値）、doesNotSupportDiff （ブール値）、edit （文字列）、emptyKeyValue （文字列）、enum （文字列） expandSchemaTarget （文字列）、expr （文字列）、externalJoin （ブール値）、feature （文字列）、featureDate （ブール値）、filterPath （文字列）、folderLink （文字列）、folderModel （文字列）、folderProcess （文字列）、fullLoad （ブール値）、階層（ブール値）、hierarchicalPath （文字列）、img （文字列）、inout （文字列）、integrity （文字列）、label （文字列）、labelSingular （文字列）、length （文字列）、localizable （ブール値）、name （MNTOKEN）, noDbIndex （boolean）, noKey （boolean）, ordered （boolean）, overflowtable （boolean）, pkSequence （string）, pkgStatus （string）, ref （string）, required （boolean）, revAdvanced （boolean）, revCardinality （string）, revDesc （string）, revExternalJoin （boolean）, revIntegrity （string）, revLabel （string）, revLink （string）, revstring revVisibleIf （文字列）, sql （ブール値）, sqlname （文字列）, sqltable （文字列）, tableSpace （文字列）, tableSpaceIndex （文字列）, target （MNTOKEN）, template （文字列）, temporaryTable （ブール値）, translatedDefault （文字列）, translatedExpr （文字列）, type （MNTOKEN）, unbound （ブール値）, user （ブール値）, userEnum （文字列）, visibleIf （文字列）, xml （ブール値）, xmlChildren （ブール値）

## 親 {#parents-4}

`<srcschema>`

`<element>`

## 子 {#children-4}

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

## 説明 {#description-4}

Adobe Campaignの`<element>`要素には4つの種類があります。

* ルート `<element>`：スキーマに一致するSQL テーブルの名前を定義します。
* 構造`<element>` :`<element>`または`<attribute>`要素のグループを定義します。
* リンク `<element>`：リンクを定義します。 この要素には、「@type=link」属性を含める必要があります。
* XML `<element>`：テキストタイプ「mData」フィールドを定義します。 この要素には、「@type=xml」属性を含める必要があります。

## 属性の説明 {#attribute-description-4}

* **_operation （文字列）**: データベースへの書き込みの種類を定義します。

  この属性は、主にすぐに使用できるスキーマを拡張する場合に使用されます。

  アクセス可能な値は次のとおりです。

   * &quot;none&quot;：和解のみ。 つまり、Adobe Campaignはアップデートせずに復元したり、存在しない場合はエラーを発生させたりします。
   * &quot;insertOrUpdate&quot;：挿入で更新します。 つまり、Adobe Campaignがエレメントを更新するか、エレメントが存在しない場合はエレメントを作成します。
   * &quot;insert&quot;：挿入。 つまり、Adobe Campaignはエレメントが存在するかどうかを確認せずに挿入します。
   * &quot;update&quot;：更新します。 つまり、Adobe Campaignはエレメントを更新するか、エレメントが存在しない場合はエラーを生成します。
   * &quot;delete&quot;：削除。 つまり、Adobe Campaignは復元と削除を行います。

* **詳細（ブール値）**：このオプションがアクティブ化されている場合（@advanced=&quot;true&quot;）、フォームでリストを設定するためにアクセス可能な使用可能なフィールドのリストで属性を非表示にできます。
* **集計（文字列）**：別のスキーマを介して`<element>`の定義をコピーできます。 この属性は、「名前空間:name」の形式でスキーマ宣言を受け取ります。
* **applicableIf （文字列）**: インデックスを適用するための条件。 この属性はXTK式を受け取ります。
* **autopk （ブール値）**：このオプションがアクティブ化されている場合（autopk=&quot;true&quot;）、一意のキーが自動的に定義されます。 このオプションは、スキーマのメイン要素でのみ使用できます。 警告：Adobe Campaignでは、生成されるキーが一意であることが保証されます。 キー値が連続して増分である保証はありません。
* **dataPolicy （文字列）**: SQL フィールドで許可される値に対する承認制約を指定できます。 この属性の値は次のとおりです。

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
* **default （文字列）**：要素の動作（関数の呼び出し、デフォルト値）を定義できます。 この属性はXTK式を受け取ります。
* **desc （string）**：要素の説明を挿入できます。 この説明は、要素とその用途を理解するために使用されます。 フォームに表示できます。
* **displayAsField （boolean）**：この属性がアクティブ化されると、「リンク」タイプ `<element>`がスキーマのツリービュー（「構造」タブ）にフィールドとして表示されます。 これにより、リンクをローカルフィールドとして表示し、クエリ中に動作を変更することができます。 要素がクエリのSELECTで見つかった場合、リンクターゲットの値が使用されます。 要素がクエリのWHEREに見つかった場合、リンクの基になるキーが使用されます。
* **編集（文字列）**：この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum （string）**: フィールドにリンクされた列挙の名前を受け取ります。 列挙は、同じスキーマまたはリモートスキーマに挿入できます。
* **expr （文字列）**：この属性は、テーブルに定義が保存されていない計算フィールドを定義します。 XpathまたはXTK （文字列）式を受け取ります。
* **externalJoin （boolean）**:「link」型要素の外部結合。
* **機能（文字列）**：特性フィールドを定義します。これらのフィールドは、既存のテーブル内のデータを拡張するために使用されますが、追加テーブル内のストレージに使用されます。 使用できる値は次のとおりです。

   * 「共有」：コンテンツは、データタイプごとに共有テーブルに保存されます
   * 「専用」：コンテンツは専用テーブルに保存されます

  SQL特性テーブルは、特性タイプに基づいて自動的に作成されます。

   * 専用：`Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * 共有：`Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

  特性フィールドには2つのタイプがあります。特性に対して1つの値が許可される単純なフィールドと、特性が複数の値を含む可能性のある収集要素にリンクされる複数選択フィールドです。

  スキーマで特性が定義されている場合、このスキーマには1つのフィールドに基づくメインキーが必要です（複合キーは許可されていません）。

* **featureDate （boolean）**: 「@feature」特性フィールドにリンクされた属性。 値が「true」の場合、値が最後に更新された日時を確認できます。
* **filterPath （文字列）**：この属性はXpathを受け取り、フィールドにフィルターを定義できます。
* **folderLink （文字列）**：この属性は、エンティティを含むファイルを復元できるリンクの名前を受け取ります。
* **folderModel （文字列）**: エンティティの保存を有効にするフォルダーのタイプを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **folderProcess （文字列）**: エンティティ モデル インスタンスが保存されるリンクを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **fullLoad （ブール値）**：この属性は、フォームのフィールド選択中に、テーブル内のすべてのレコードを強制的に表示します。
* **img （文字列）**：要素にリンクされた画像のパスを受け取ります。 この属性の値は「namespace:image name」タイプです。 例：img=&quot;cus:myImage.jpg&quot;。 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **整合性（文字列）**：ターゲットテーブルに対するソーステーブルの発生の参照整合性。

  アクセス可能な値は次のとおりです。

   * &quot;define&quot;: Adobe Campaignは、リンクを介して参照されている場合、エンティティを削除しません
   * 「通常」：ソースのオカレンスを削除すると、ターゲットのオカレンス上のリンクのキーが初期化されます（デフォルトモード）。このタイプの整合性は、すべての外部キーを初期化します
   * 「own」：ソースのオカレンスを削除すると、ターゲットのオカレンスの削除がトリガーされます
   * 「owncopy」: 「own」（削除の場合）と同様または重複する（重複の場合）
   * &quot;neutral&quot;：何もしない

* **label （文字列）**：要素ラベル。
* **labelSingular （string）**: インターフェイスの一部で使用される要素のラベル（単一形式）。
* **長さ（文字列）**：最大 「文字列」タイプのSQL フィールドの値に対して許可されている文字数。
* **ローカライズ可能（ブール値）**：この属性がアクティブ化されている場合、翻訳（内部使用）用に「@label」属性の値を回復するようにコレクションツールに指示します。
* **name （MNTOKEN）**: テーブルの名前と一致する要素の内部名。 「@name」属性の値は短く、好ましくは英語で、XMLにリンクされた命名制約に準拠している必要があります。

  スキーマがデータベースに書き込まれると、Adobe Campaignによってフィールド名に接頭辞が自動的に追加されます。

   * &quot;i&quot;: &#39;integer&#39;型のプレフィックス。
   * &quot;d&quot;: &#39;double&#39;型のプレフィックス。
   * &quot;s&quot;：文字列型の接頭辞。
   * &quot;ts&quot;: &#39;date&#39; タイプのプレフィックス。

  自律的な方法でテーブルの名前を定義するには、メインスキーマ要素の定義で「@sqltable」属性を使用する必要があります。

* **noDbIndex （boolean）**：要素にインデックスを作成しないように指定できます。
* **ordered （boolean）**：属性がアクティブ化されている場合（ordered=&quot;true&quot;）、Adobe CampaignはXML コレクション要素に要素宣言シーケンスを保持します。
* **pkSequence （文字列）**：自動増分キーの計算に使用するシーケンスの名前を受け取ります。 この属性は、自動インクリメンタルキーがスキーマのルート要素で定義されている場合にのみ使用できます。
* **pkgStatus （文字列）**: パッケージの書き出し中に、この属性の値の関数として値が考慮されます：

   * &quot;always&quot;：要素は常に存在します
   * &quot;never&quot;：要素は存在しません
   * 「デフォルト（または何も）」：デフォルトのエレメントでない場合、または内部フィールドではなく、他のインスタンスと互換性がない場合を除き、エレメントは書き出されます

* **ref （文字列）**：この属性は、複数のスキーマで共有されている>要素>要素への参照（定義ファクタリング）を定義します。 定義は現在のスキーマにコピーされません。
* **必須（ブール値）**：この属性がアクティブ化されている場合（@required=&quot;true&quot;）、このフィールドはインターフェイスで強調表示されます。 フィールドのラベルはフォームで赤になります。
* **revAdvanced （boolean）**：アクティブ化すると、この属性は、反対のリンクが「詳細」リンクであることを指定します。
* **revCardinality （文字列）**：この属性は、2つのテーブル間のリンクの基数を定義します。 「リンク」タイプ `<element>`で使用されます。

  次のような値を選択できます。

   * 「シングル」：シンプルな1-1文字のリンク
   * &quot;unbound&quot;: 1-N type collection link

  デフォルトでは、リンク作成時に属性が指定されない場合、基数は1 ～ Nになります。

* **revDesc （文字列）**：この属性は、反対のリンクにリンクされた説明を受け取ります。
* **revExternalJoin （boolean）**：この属性を有効にすると、外部の結合を反対のリンクに強制的に行うことができます。
* **revIntegrity （string）**：この属性は、ターゲットスキーマの整合性を定義します。 「@integrity」属性と同じ値が許可されます。 デフォルトでは、Adobe Campaignはこの属性に「通常」の値を与えます。
* **revLabel （文字列）**：反対のリンクのラベル。
* **revLink （文字列）**：反対リンクの名前。 値が「_NONE_」の場合、宛先スキーマに反対のリンクは作成されません。
* **revTarget （文字列）**：反対リンクのターゲット。
* **sql （ブール値）**：この属性がアクティブ化されている場合（@sql=&quot;true&quot;）、要素にxml=&quot;true&quot; プロパティがある場合でも、SQL要素の格納が強制されます。
* **sqlname （文字列）**: テーブル作成時のフィールドの名前。 「@sqlname」が指定されていない場合、「@name」属性の値がデフォルトで使用されます。 スキーマをテーブルに書き込む場合、フィールドのタイプに応じて接頭辞が自動的に追加されます。
* **sqltable （string）**: スキーマのメイン要素では、この属性によって、デフォルトで生成されたSQL テーブルの名前がオーバーロードされます。 「@sqltable」が指定されていない場合、デフォルトの名前は名前空間（先頭の大文字）の後にSrcSchemaの「@name」の値が続くような構造になります。
* **tableSpace （文字列）**：この属性を使用すると、テーブルのテーブルスペースを格納する新しいデータを指定できます（ルート `<element>`で有効）。
* **tableSpaceIndex （文字列）**：この属性を使用すると、テーブルの新しいインデックスストレージ表領域を指定できます（ルート `<element>`で有効）。
* **target （MNTOKEN）**: テーブル間のリンクを作成する際に、ターゲットスキーマの名前を受け取ります。 この属性は、「リンク」タイプの要素に対してのみ有効です。
* **テンプレート（文字列）**：この属性は、複数のスキーマで共有されている`<element>`要素への参照を定義します。 定義は現在のスキーマに自動的にコピーされます。
* **translatedDefault （string）**: 「@default」属性が見つかった場合、「@translatedDefault」を使用すると、翻訳ツールで収集される@defaultで定義された式と一致するように式を再定義できます（内部使用）。
* **translatedExpr （string）**: 「@expr」属性が見つかった場合、「@translatedExpr」属性を使用すると、「@expr」で定義された式と一致する式を再定義できます。この式は、翻訳ツールで収集されます（内部使用）。
* **type （MNTOKEN）**：要素に保存されるデータのタイプを定義します。

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

* **unbound （boolean）**：属性がアクティブ化されている場合（unbound=&quot;true&quot;）、リンクは1-N基数のコレクション要素として宣言されます。
* **userEnum （文字列）**:「open」列挙の内部名を受け取ります。 列挙値は、インターフェイスでユーザーが定義できます。
* **xml （ブール値）**：このオプションが有効になっている場合、エレメントで定義されたすべての値がXMLでTEXT タイプの「mData」フィールドに格納されます。 つまり、これらのフィールドにフィルタリングや並べ替えはありません。
* **xmlChildren （ブール値）**：各子に強制的にストレージを適用します（`<element>  or  <attribute>   ) of the   <element>    element in an XML document.   </element>  </attribute> </element>`）
