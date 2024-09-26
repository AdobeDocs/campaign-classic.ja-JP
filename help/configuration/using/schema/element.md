---
product: campaign
title: スキーマの要素と属性 – 要素
description: element
feature: Schema Extension
exl-id: 60f15ae5-b2bd-48f9-aa45-8f795a3071aa
source-git-commit: 728848eab059fc669c241346a2ff1feebd79222c
workflow-type: tm+mt
source-wordcount: '2029'
ht-degree: 0%

---

# element {#element--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-4}

要素：==（attribute | compute-string | dbindex |既定値 |要素 | ヘルプ |結合 | キー | sysFilter | translatedDefault）

## 属性 {#attributes-4}

_operation （string）、advanced （boolean）、aggregate （string）、applicableIf （string）、autopk （boolean）、belongsTo （string）、convDate （string）、dataPolicy （string）、dataSource （string）、dbEnum （string）、defOnDuplicate （boolean）、default （string）、desc （string）、displayAsField （boolean）、doesNotSupportDiff （boolean）、edit （string）、emptyKeyValue （string）、enum （string）、enumImage （string）、enumImage （string）、expand schemaTarget （string）、expr （string）、externalJoin （boolean）、feature （string）、featureDate （boolean）、filterPath （string）、folderLink （string）、folderModel （string）、folderProcess （string）、fullLoad （boolean）、hierarchicalPath （string）、img （string）、inout （string）、integrity （string）、label （string）、labelSingular （string）、length （string）、localizable （boolean）、name （MNTOKEN）、noDbIndex （boolean）、no key （boolean）、ordered （boolean）、overflowtable （boolean）、pkSequence （string）、pkgStatus （string）、ref （string）、required （boolean）、revAdvanced （boolean）、revCardinality （string）、revDesc （string）、revExternalJoin （boolean）、revIntegrity （string）、revLabel （string）、revLink （string）、revVisibleIf （string）、sql （boolean）、sqlname （string）、sqltable （string）、tableSpace, tableSpaceIndex （string）, target （MNTOKEN）, template （string）, temporaryTable （boolean）, translatedDefault （string）, translatedExpr （string）, type （MNTOKEN）, unbound （boolean）, user （boolean）, userEnum （string）, visibleIf （string）, xml （boolean）, xmlChildren （boolean）

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

Adobe Campaignには、次の 4 種類の `<element>` 要素があります。

* ルート `<element>`：スキーマに一致する SQL テーブルの名前を定義します。
* 構造 `<element>` :`<element>` のグループを定義します。   または   `<attribute>`    要素。
* リンク `<element>`：リンクを定義します。 この要素には、「@type=link」属性を含める必要があります。
* XML `<element>`：テキストタイプ「mData」フィールドを定義します。 この要素には、「@type=xml」属性を含める必要があります。

## 属性の説明 {#attribute-description-4}

* **_operation （文字列）**：データベースへの書き込みのタイプを定義します。

  この属性は、主に標準スキーマを拡張する際に使用されます。

  アクセス可能な値は次のとおりです。

   * 「なし」：紐付けのみ。 つまり、Adobe Campaignは要素を更新せずに復元し、要素が存在しない場合はエラーを生成します。
   * &quot;insertOrUpdate&quot;：挿入で更新します。 つまり、Adobe Campaignは要素を更新し、存在しない場合は作成します。
   * 「挿入」：挿入。 つまり、Adobe Campaignは、存在するかどうかを確認せずに要素を挿入します。
   * 「更新」：更新。 つまり、Adobe Campaignは要素を更新するか、要素が存在しない場合はエラーを生成します。
   * 「削除」：削除。 つまり、Adobe Campaignは要素を復元して削除します。

* **詳細（ブール値）**：このオプションを有効にすると（@advanced=&quot;true&quot;）、フォームでのリストの設定にアクセスできる使用可能なフィールドのリストで属性を非表示にできます。
* **集計（文字列）**：別のスキーマを使用して `<element>` の定義をコピーできます。 この属性は、「namespace:name」の形式でスキーマ宣言を受け取ります。
* **applicableIf （string）**：インデックスを適用する条件。 この属性は XTK 式を受け取ります。
* **autopk （boolean）**：このオプションをオンにする（autopk=&quot;true&quot;）と、一意のキーが自動的に定義されます。 このオプションは、スキーマのメイン要素でのみ使用できます。 警告：Adobe Campaignでは、生成されたキーが一意であることのみが保証されます。 キー値が連続して増分されるということは保証されません。
* **dataPolicy （文字列）**:SQL フィールドで許可される値に対して承認制約を指定できます。 この属性の値は次のとおりです。

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
* **default （string）**：要素の動作（関数の呼び出し、デフォルト値）を定義できます。 この属性は XTK 式を受け取ります。
* **desc （string）**：要素の説明を挿入できます。 この説明は、要素の概要と用途を理解するために使用されます。 フォームに表示できます。
* **displayAsField （ブール値）**：この属性をアクティブ化すると、「リンク」タイプの `<element>` がスキーマのツリービュー（「構造」タブ）にフィールドとして表示されます。 これにより、リンクをローカルフィールドとして表示し、クエリ中に動作を変更できます。 クエリの SELECT 内に要素が見つかると、リンクターゲットの値が使用されます。 クエリの WHERE 内に要素が見つかった場合は、基になるリンクのキーが使用されます。
* **edit （string）**：この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum （string）**：フィールドにリンクされた定義済みリストの名前を受け取ります。 定義済みリストは、同じスキーマまたはリモートスキーマに挿入できます。
* **expr （文字列）**：この属性は、テーブルに定義が保存されない計算フィールドを定義します。 Xpath または XTK （文字列）式を受け取ります。
* **externalJoin （ブール）**:「link」タイプの要素での外部結合。
* **feature （string）**：特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルへの格納は保持されます。 指定できる値は次のとおりです。

   * 「共有」：コンテンツは、データタイプごとに共有テーブルに保存されます
   * 「dedicated」：コンテンツは専用テーブルに保存されます

  SQL 特性テーブルは、特性タイプに基づいて自動的に作成されます。

   * 専用：`Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * 共有：`Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

  特性フィールドには、特性に対して単一の値が許可される単純なフィールドと、特性が複数の値を含むことができるコレクション要素にリンクされる複数選択フィールドの 2 種類があります。

  スキーマ内で特性が定義される場合、このスキーマには、単一のフィールドに基づくメインキーが必要です（複合キーは許可されていません）。

* **featureDate （ブール値）**:「@feature」特性フィールドにリンクされた属性。 値が「true」の場合は、値が最後に更新された日時を調べることができます。
* **filterPath （string）**：この属性は Xpath を受け取り、フィールドにフィルターを定義できます。
* **folderLink （string）**：この属性は、エンティティを含んだファイルを回復できるリンクの名前を受け取ります。
* **folderModel （文字列）**：エンティティストレージを有効にするフォルダーのタイプを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **folderProcess （文字列）**：エンティティモデルインスタンスが格納されるリンクを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **fullLoad （ブール値）**：この属性は、フォームでのフィールド選択時に、テーブル内のすべてのレコードを強制的に表示します。
* **img （string）**：要素にリンクされた画像のパスを受け取ります。 この属性の値は、「namespace:image name」タイプです。 例：img=&quot;cus:myImage.jpg&quot;。 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **integrity （string）**：ターゲットテーブルに対するソーステーブルのオカレンスの参照整合性。

  アクセス可能な値は次のとおりです。

   * 「define」：リンク経由で参照されている場合、Adobe Campaignがエンティティを削除しない
   * 「normal」：ソースオカレンスを削除すると、ターゲットオカレンス（デフォルトモード）上のリンクのキーが初期化され、このタイプの整合性によってすべての外部キーが初期化されます
   * &quot;own&quot;：ソースオカレンスを削除すると、ターゲットオカレンスの削除がトリガーされます
   * 「owncopy」:「own」（削除の場合）や重複オカレンス（複製の場合）に似ています。
   * &quot;neutral&quot;：何も実行しない

* **label （string）**：要素のラベル。
* **labelSingular （string）**: インターフェイスの一部で使用される要素のラベル（単数形）。
* **length （string）**：最大 「文字列」タイプの SQL フィールドの値に使用できる文字数。
* **localizable （boolean）**：有効な場合、この属性は、翻訳の「@label」属性の値を復元するようにコレクションツールに指示します（内部使用）。
* **name （MNTOKEN）**：テーブル名に一致する要素の内部名。 「@name」属性の値は短く（できれば英語）、XML にリンクされた命名制約に準拠する必要があります。

  スキーマがデータベースに書き込まれると、Adobe Campaignによって、フィールド名にプレフィックスが自動的に追加されます。

   * 「i」:「integer」タイプのプレフィックス。
   * &quot;d&quot;: 「double」タイプのプレフィックス。
   * 「s」：文字列タイプのプレフィックス。
   * 「ts」:「日付」タイプのプレフィックス。

  自律的にテーブルの名前を定義するには、メインのスキーマ要素の定義で「@sqltable」属性を使用する必要があります。

* **noDbIndex （ブール値）**：要素にインデックスを作成しないことを指定できます。
* **ordered （boolean）**：属性がアクティブになっている場合（ordered=&quot;true&quot;）、Adobe Campaignは XML コレクション要素で要素宣言のシーケンスを保持します。
* **pkSequence （string）**：自動増分キーの計算に使用するシーケンスの名前を受け取ります。 この属性は、自動増分キーがスキーマのルート要素で定義されている場合にのみ使用できます。
* **pkgStatus （string）**：パッケージのエクスポート中、値はこの属性の値の関数として考慮されます。

   * 「常に」：要素は常に存在します
   * 「なし」：要素は存在しません
   * 「default （or nothing）」：要素は、デフォルトの要素である場合や、内部フィールドではなく他のインスタンスとの互換性がない場合を除いて、書き出されます

* **ref （string）**：この属性は、複数のスキーマ（定義ファクタリング）で共有される >element> 要素への参照を定義します。 定義は現在のスキーマにコピーされません。
* **必須（ブール値）**：この属性をアクティブにする（@required=&quot;true&quot;）と、インターフェイスでフィールドがハイライト表示されます。 フォームではフィールドのラベルは赤になります。
* **revAdvanced （boolean）**：有効にすると、この属性は反対側のリンクが「詳細」リンクであることを指定します。
* **revCardinality （文字列）**：この属性は、2 つのテーブル間のリンクのカーディナリティを定義します。 「リンク」タイプの `<element>` で使用されます。

  次のような値を選択できます。

   * 「single」：シンプルな 1-1 タイプのリンク
   * 「unbound」:1-N タイプのコレクションリンク

  デフォルトでは、リンクの作成時に属性が指定されていない場合、カーディナリティは 1-N になります。

* **revDesc （文字列）**：この属性は、反対側のリンクにリンクされた説明を受け取ります。
* **revExternalJoin （boolean）**：有効にすると、この属性を使用して反対側のリンクに外部結合を強制できます。
* **revIntegrity （string）**：この属性は、ターゲットスキーマの整合性を定義します。 「@integrity」属性と同じ値が許可されます。 デフォルトでは、Adobe Campaignはこの属性に「normal」値を付与します。
* **revLabel （文字列）**：反対のリンクのラベル。
* **revLink （文字列）**：反対のリンクの名前。 値が「_NONE_」の場合、宛先スキーマに反対のリンクは作成されません。
* **revTarget （文字列）**：反対のリンクのターゲット。
* **sql （ブール値）**：この属性がアクティブ化されている場合（@sql=&quot;true&quot;）、要素に xml=&quot;true&quot; プロパティがある場合でも、SQL 要素のストレージを強制します。
* **sqlname （string）**: テーブル作成中のフィールドの名前。 「@sqlname」を指定しない場合、「@name」属性の値がデフォルトで使用されます。 スキーマをテーブルに書き込む場合、フィールドのタイプに応じて、プレフィックスが自動的に追加されます。
* **sqltable （string）**：スキーマのメイン要素に対して、この属性は、デフォルトで生成される SQL テーブルの名前をオーバーロードします。 「@sqltable」を指定しない場合、デフォルトの名前は、名前空間（最初の文字は大文字）の後に SrcSchema 「@name」の値が続くように構成されます。
* **tableSpace （string）**：この属性を使用すると、テーブルの新しいデータ保存用のテーブル領域（ルート `<element>` ージで有効）を指定できます。
* **tableSpaceIndex （string）**：この属性を使用すると、テーブルの新しいインデックスストレージのテーブルスペースを指定できます（ルート `<element>` で有効）。
* **target （MNTOKEN）**：テーブル間のリンクを作成する際に、ターゲットスキーマの名前を受け取ります。 この属性は、「リンク」タイプの要素に対してのみアクティブです。
* **template （文字列）**：この属性は、複数のスキーマで共有される `<element>` 要素への参照を定義します。 定義は、現在のスキーマに自動的にコピーされます。
* **translatedDefault （string）**:「@default」属性が見つかった場合、「@translatedDefault」を使用すると、@default で定義された式と一致し、翻訳ツールによって収集される式を再定義できます（内部使用）。
* **translatedExpr （文字列）**:「@expr」属性が見つかった場合、「@translatedExpr」属性を使用すると、「@expr」で定義された式と一致し、翻訳ツールによって収集される式を再定義できます（内部使用）。
* **type （MNTOKEN）**：要素に保存されるデータのタイプを定義します。

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

* **unbound （ブール値）**：属性がアクティブになっている（unbound=&quot;true&quot;）場合、リンクは 1 対多のカーディナリティのコレクション要素として宣言されます。
* **userEnum （文字列）**:「開いている」列挙の内部名を受け取ります。 定義済みリストの値は、ユーザーがインターフェイスで定義できます。
* **xml （ブール値）**：このオプションを有効にすると、要素で定義されたすべての値が、TEXT タイプの「mData」フィールドの XML に保存されます。 つまり、これらのフィールドに対してフィルタリングや並べ替えは行われません。
* **xmlChildren （ブール値）**：子ごとに強制的にストレージを設定します（`<element>  or  <attribute>   ) of the   <element>    element in an XML document.   </element>  </attribute> </element>`
