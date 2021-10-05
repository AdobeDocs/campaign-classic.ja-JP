---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: 60f15ae5-b2bd-48f9-aa45-8f795a3071aa
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '2012'
ht-degree: 1%

---

# 要素要素 {#element--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-4}

element:==(attribute | compute-string | dbindex | default |要素 |ヘルプ | join |キー | sysFilter | translatedDefault)

## 属性 {#attributes-4}

_operation （文字列）、advanced (boolean)、 aggregate （文字列）、 applicableIf （文字列）、 autopk (boolean)、 belongsTo （文字列）、 convDate （文字列）、 dataPolicy （文字列）、 dataSource （文字列）、 defOnDuplicate (boolean)、 desc （文字列）、 displayAsFieldboolean)、doesNotSupportDiff(boolean)、edit(string)、emptyKeyValue(string)、enum(string)、enumImage(string)、expandSchemaTarget(string)、expr(string)、externalJoin(boolean)、feature(string)、filterPath(string)、folderLink(for) モデル（文字列）、 folderProcess （文字列）、 fullLoad （ブール値）、 hierarchicalPath （文字列）、 img （文字列）、 inout （文字列）、整合性（文字列）、ラベル（文字列）、長さ（文字列）、ローカライズ可能（ブール値）、名前 (MNTOKEN)、noDbIndex （ブール値）、noKey ブール値 )、順序付け済み（ブール値）、オーバーフロー可能（ブール値）、pkSequence（文字列）、pkgStatus（文字列）、ref（文字列）、必須（ブール値）、revAdvanced（ブール値）、revCardinality（文字列）、revDesc（文字列）、revExternalJoin（ブール値）、revIntegrity（文字列）、revLink), revTarget （文字列）, revVisibleIf （文字列）, sql (boolean), sqlname （文字列）, sqltable （文字列）, tableSpace （文字列）, tableSpaceIndex （文字列）, target (MNTOKEN), template （文字列）, templarateTable （ブール値）, translatedExpr （文字列）, type ( MNTOKEN)、unbound (boolean)、user (boolean)、userEnum (string)、visibleIf (string)、xml (boolean)、xmlChildren (boolean)

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

Adobe Campaignには 4 種類の `<element>` 要素があります。

* ルート `<element>` :は、スキーマに一致する SQL テーブルの名前を定義します。
* 構造 `<element>` :`<element>` のグループを定義します。   または   `<attribute>`    要素
* リンク `<element>` :リンクを定義します。 この要素には、「@type=link」属性を含める必要があります。
* XML `<element>` :テキストタイプ「mData」フィールドを定義します。 この要素には、「@type=xml」属性を含める必要があります。

## 属性の説明 {#attribute-description-4}

* **_operation （文字列）**:データベースに書き込むタイプを定義します。

   この属性は、主に標準のスキーマを拡張する際に使用されます。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:紐付けのみ。 つまり、Adobe Campaignは、更新せずに要素を回復します。要素が存在しない場合は、エラーを生成します。
   * &quot;insertOrUpdate&quot;:を挿入して更新します。 つまり、Adobe Campaignは要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 つまり、Adobe Campaignは要素を更新するか、存在しない場合はエラーを生成します。
   * &quot;delete&quot;:削除します。 つまり、Adobe Campaignは要素を復元および削除します。

* **advanced (boolean)**:このオプションを有効にすると (@advanced=&quot;true&quot;)、フォームでリストを設定するためにアクセス可能なフィールドのリストの属性を非表示にできます。
* **集計（文字列）**:を使用すると、別のスキーマでの定 `<element>`  義をコピーできます。この属性は、「namespace:name」の形式でスキーマ宣言を受け取ります。
* **applicableIf (string)**:インデックスを適用する条件。この属性は XTK 式を受け取ります。
* **autopk（ブール値）**:このオプションが有効な場合 (autopk=&quot;true&quot;)、一意のキーが自動的に定義されます。このオプションは、スキーマのメイン要素でのみ使用できます。 警告： Adobe Campaignは、生成されたキーが一意であることを保証するだけです。 キー値が連続して増分される保証はありません。
* **dataPolicy （文字列）**:では、「SQL」フィールドで許可する値に対する承認制約を指定できます。この属性の値は次のとおりです。

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
* **デフォルト（文字列）**:では、要素の動作（関数の呼び出し、デフォルト値）を定義できます。この属性は XTK 式を受け取ります。
* **desc （文字列）**:要素の説明を挿入できます。この説明は、インターフェイスのステータスバーに表示されます。
* **displayAsField (boolean)**:この属性が有効になっている場合、「リンク」タイプ `<element>`  は、スキーマのツリービュー（「構造」タブ）のフィールドとして表示されます。これにより、リンクをローカルフィールドとして表示し、クエリ中に動作を変更することができます。 クエリの SELECT に要素が見つかると、リンクターゲットの値が使用されます。 クエリの WHERE で要素が見つかると、リンクの基になるキーが使用されます。
* **編集（文字列）**:この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum (string)**:は、フィールドにリンクされている列挙の名前を受け取ります。列挙は、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**:この属性は、テーブルに定義が格納されない計算フィールドを定義します。Xpath または XTK（文字列）式を受け取ります。
* **externalJoin (boolean)**:「リンク」タイプ要素の外部結合。
* **機能（文字列）**:特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルに格納されます。指定できる値は次のとおりです。

   * &quot;shared&quot;:コンテンツは、データタイプごとに共有テーブルに格納されます
   * &quot;dedicated&quot;:コンテンツは専用のテーブルに格納されます。

   SQL 特性テーブルは、特性タイプに基づいて自動的に作成されます。

   * 専用：`Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

   次の 2 種類の特性フィールドがあります。単一の値が特性に対して許可される単純なフィールドと、複数選択フィールド。複数の選択フィールドでは、特性が複数の値を含むコレクション要素にリンクされます。

   スキーマ内で特性が定義される場合、このスキーマは、単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されません）。

* **featureDate（ブール値）**:属性は「@feature」特性フィールドにリンクされています。値が「true」の場合は、値が最後に更新された日時を確認できます。
* **filterPath（文字列）**:この属性は Xpath を受け取り、フィールドに対してフィルターを定義できます。
* **folderLink （文字列）**:この属性は、エンティティを含むファイルを復元するためのリンクの名前を受け取ります。
* **folderModel（文字列）**:エンティティの保存を有効にするフォルダーのタイプを定義します。この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **folderProcess (string)**:エンティティモデルインスタンスを保存するリンクを定義します。この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **fullLoad (boolean)**:この属性は、フォーム内のフィールド選択時に、テーブル内のすべてのレコードを強制的に表示します。
* **img （文字列）**:は、要素にリンクされた画像のパスを受け取ります。この属性の値は、「namespace:image name」タイプです。 例：img=&quot;cus:myImage.jpg&quot;. 物理的には、イメージをアプリケーションサーバーにインポートする必要があります。
* **整合性（文字列）**:ターゲット・テーブルに対するソース・テーブルの出現の参照整合性。

   アクセス可能な値は次のとおりです。

   * &quot;define&quot;:Adobe Campaignでは、リンクを介して参照されているエンティティは削除されません
   * &quot;normal&quot;:ソースオカレンスを削除すると、ターゲットオカレンス上のリンクのキーが初期化されます（デフォルトモード）。この整合性タイプは、すべての外部キーを初期化します
   * &quot;own&quot;:ソースオカレンスの削除トリガーターゲットオカレンスの削除
   * &quot;owncopy&quot;:「own」（削除の場合）または（複製の場合）重複の発生と同様
   * &quot;neutral&quot;:何もしない

* **label （文字列）**:要素のラベル。
* **labelSingular（文字列）**:インターフェイスの一部で使用される要素のラベル（単数形）。
* **length （文字列）**:最大「文字列」タイプの SQL フィールドの値に対して許可されている文字の数。
* **localizable（ブール値）**:この属性が有効な場合、この属性は、翻訳（内部使用）の「@label」属性の値を復元するように収集ツールに指示します。
* **名前 (MNTOKEN)**:テーブルの名前と一致する要素の内部名。「@name」属性の値は短く、できれば英語で記述し、XML にリンクされた命名規則に従う必要があります。

   スキーマがデータベースに書き込まれると、Adobe Campaignによってフィールド名にプレフィックスが自動的に追加されます。

   * &quot;i&quot;:プレフィックスを「integer」型に設定します。
   * &quot;d&quot;:「double」型のプレフィックス。
   * &quot;s&quot;:プレフィックスを使用します。
   * &quot;ts&quot;:プレフィックスを使用して、「日付」タイプを指定します。

   自律的な方法でテーブルの名前を定義するには、メインスキーマ要素の定義で「@sqltable」属性を使用する必要があります。

* **noDbIndex (boolean)**:要素のインデックスを作成しないように指定できます。
* **ordered（ブール値）**:属性が有効化 (ordered=&quot;true&quot;) されている場合、Adobe Campaignは XML コレクション要素内に要素宣言の順序を保持します。
* **pkSequence（文字列）**:は、自動増分キーの計算に使用されるシーケンスの名前を受け取ります。この属性は、スキーマのルート要素に自動増分キーが定義されている場合にのみ使用できます。
* **pkgStatus （文字列）**:パッケージの書き出し時に、値はこの属性の値の関数として考慮されます。

   * &quot;always&quot;:要素は常に存在します
   * &quot;never&quot;:要素は存在しない
   * &quot;default （または nothing）&quot;:要素は、デフォルトの要素である場合や、内部フィールドでなく、他のインスタンスと互換性がない場合を除き、エクスポートされます。

* **ref（文字列）**:この属性は、複数のスキーマ（定義ファクタリング）で共有される >element> 要素への参照を定義します。定義は現在のスキーマにコピーされません。
* **必須（ブール値）**:この属性が有効な場合 (@required=&quot;true&quot;)、インターフェイスでフィールドがハイライト表示されます。フィールドのラベルは、フォームでは赤で表示されます。
* **revAdvanced（ブール値）**:この属性を有効にすると、反対側のリンクが「詳細」リンクになります。
* **revCardinality（文字列）**:この属性は、2 つのテーブル間のリンクの基数を定義します。これは「リンク」タイプ `<element>` で使用されます。

   次のような値を選択できます。

   * &quot;single&quot; :単純な 1-1 タイプのリンク
   * &quot;unbound&quot;:1-N 型収集リンク

   デフォルトでは、リンクの作成時に属性が指定されない場合、基数は 1 対 N になります。

* **revDesc（文字列）**:この属性は、反対側のリンクにリンクされた説明を受け取ります。
* **revExternalJoin（ブール値）**:このアトリビュートを有効にすると、反対側のリンクで外部結合を強制できます。
* **revIntegrity（文字列）**:この属性は、ターゲット・スキーマの整合性を定義します。「@integrity」属性と同じ値が許可されます。 デフォルトでは、Adobe Campaignはこの属性に「通常」値を与えます。
* **revLabel（文字列）**:反対側のリンクのラベル。
* **revLink（文字列）**:反対のリンクの名前。値が「_NONE_」の場合、反対側のリンクは宛先スキーマに作成されません。
* **revTarget（文字列）**:反対のリンクのターゲット。
* **sql（ブール値）**:この属性が有効になっている場合 (@sql=&quot;true&quot;)、要素に xml=&quot;true&quot;プロパティが含まれていても、SQL 要素の保存が強制されます。
* **sqlname （文字列）**:テーブル作成時のフィールドの名前。「@sqlname」を指定しない場合、「@name」属性の値がデフォルトで使用されます。 スキーマをテーブルに書き込む際、フィールドのタイプに応じてプレフィックスが自動的に追加されます。
* **sqltable（文字列）**:スキーマのメイン要素に対して、この属性は、デフォルトで生成された SQL テーブルの名前をオーバーロードします。「@sqltable」を指定しない場合、デフォルトの名前は次のように構造化されます。namespace （最初の文字は大文字）の後に SrcSchema &quot;@name&quot;の値が続く。
* **tableSpace (string)**:この属性を使用すると、表の表領域を格納する新しいデータを指定できます ( ルートで有効 `<element>`)。
* **tableSpaceIndex (string)**:この属性を使用すると、テーブルの新しいインデックス・ストレージ・テーブルスペースを指定できます ( ルートで有効 `<element>`)。
* **ターゲット (MNTOKEN)**:は、テーブル間のリンクを作成する際にターゲットスキーマの名前を受け取ります。この属性は、「リンク」タイプの要素に対してのみ有効です。
* **template （文字列）**:この属性は、複数のスキーマで共有さ `<element>` れる要素への参照を定義します。定義は、現在のスキーマに自動的にコピーされます。
* **translatedDefault（文字列）**:「@default」属性が見つかった場合、「@translatedDefault」を使用して、翻訳ツールで収集される式を@defaultで定義した式に一致するように再定義できます（内部使用）。
* **translatedExpr (string)**:「@expr」属性が見つかった場合、「@translatedExpr」属性を使用して、「@expr」で定義された式と一致し、翻訳ツール（内部使用）で収集される式を再定義できます。
* **型 (MNTOKEN)**:は、要素に格納されるデータのタイプを定義します。

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

* **unbound（ブール値）**:属性が有効な場合 (unbound=&quot;true&quot;)、リンクは 1-N 基数のコレクション要素として宣言されます。
* **userEnum (string)**:は、「開いている」列挙の内部名を受け取ります。列挙の値は、インターフェイスでユーザーが定義できます。
* **xml（ブール値）**:このオプションを有効にすると、要素で定義されたすべての値が XML 形式の「mData」フィールドに格納されます。つまり、これらのフィールドにはフィルターや並べ替えは適用されません。
* **xmlChildren (boolean)**:各子に対して強制的に保存します (  `<element>  or  <attribute>   ) of the   <element>    element in an XML document.   </element>  </attribute> </element>`
