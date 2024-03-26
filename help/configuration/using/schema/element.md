---
product: campaign
title: スキーマ要素と属性 — 要素要素
description: 要素要素
feature: Schema Extension
exl-id: 60f15ae5-b2bd-48f9-aa45-8f795a3071aa
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '2016'
ht-degree: 0%

---

# 要素要素 {#element--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-4}

element:==(attribute | compute-string | dbindex | デフォルト | 要素 | ヘルプ | join | key | sysFilter | translatedDefault)

## 属性 {#attributes-4}

_operation （文字列）, advanced （文字列）, aggregate （文字列）, applicableIf （文字列）, autopk （ブール値）, belongTo （文字列）, convDate （文字列）, dataPolicy （文字列）, dbEnum （文字列）, defOnDuplicate （ブール値）, desc （文字列）, displayAsFieldboolean)、doesNotSupportDiff(boolean)、edit(string)、emptyKeyValue(string)、enum(string)、enumImage(string)、expandSchemaTarget(string)、expr(string)、externalJoin(boolean)、feature(string)、filterPath(string)、folderLink(folder) モデル (string)、folderProcess(string)、fullLoad(boolean)、hierarchicalPath(string)、img(string)、inout(string)、integrity(string)、label(string)、length(string)、localizable(boolean)、name(MNTOKEN)、noDbIndex(boolean)、noKeyboolean)、ordered(boolean)、overflowtable(boolean)、pkSequence(string)、pkgStatus(string)、ref(string)、required(boolean)、revAdvanced(boolean)、revCardinality(string)、revExternalJoin(boolean)、revIntegrity(string)、revLink(string)), revTarget （文字列）, revVisibleIf （文字列）, sql (boolean), sqlname （文字列）, sqltable （文字列）, tableSpace （文字列）, tableSpaceIndex （文字列）, target (MNTOKEN), template （ブール値）, translatedDefault （文字列）, translatedExpr （文字列）, type ( MN)、unbound (boolean)、user (boolean)、userEnum (string)、visibleIf (string)、xml (boolean)、xmlChildren (boolean)

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

次の 4 種類の `<element>`  Adobe Campaignの要素：

* ルート `<element>`  ：スキーマと一致する SQL テーブルの名前を定義します。
* 構造 `<element>`  ：のグループを定義します  `<element>`   または   `<attribute>`    要素。
* リンク `<element>`  ：リンクを定義します。 この要素には、「@type=link」属性を含める必要があります。
* XML `<element>`  ：テキストタイプ「mData」フィールドを定義します。 この要素には、「@type=xml」属性を含める必要があります。

## 属性の説明 {#attribute-description-4}

* **_operation （文字列）**：データベースに書き込むタイプを定義します。

  この属性は、主に標準のスキーマを拡張する際に使用されます。

  アクセス可能な値は次のとおりです。

   * &quot;none&quot;：紐付けのみ。 つまり、Adobe Campaignは、更新せずに要素を復元します。要素が存在しない場合は、エラーを生成します。
   * &quot;insertOrUpdate&quot;：挿入で更新します。 つまり、Adobe Campaignは要素を更新します。要素が存在しない場合は作成します。
   * &quot;insert&quot;: insertion. つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;: update. つまり、Adobe Campaignは要素を更新します。要素が存在しない場合は、エラーを生成します。
   * &quot;delete&quot;：削除。 つまり、Adobe Campaignは要素を復元および削除します。

* **advanced (boolean)**：このオプションを有効にすると (@advanced=&quot;true&quot;)、フォーム内のリストを設定するためにアクセス可能なフィールドのリストで属性を非表示にできます。
* **aggregate（文字列）**: `<element>`  別のスキーマを使用する。 この属性は、「namespace:name」形式のスキーマ宣言を受け取ります。
* **applicableIf（文字列）**：インデックスを適用する条件。 この属性は XTK 式を受け取ります。
* **autopk (boolean)**：このオプションが有効化されている場合 (autopk=&quot;true&quot;)、一意のキーが自動的に定義されます。 このオプションは、スキーマのメイン要素でのみ使用できます。 警告： Adobe Campaignは、生成されたキーが一意であることを保証するだけです。 キーの値が連続して増分される保証はありません。
* **dataPolicy （文字列）**:「SQL」フィールドで許可する値に対して承認制約を指定できます。 この属性の値は次のとおりです。

   * &quot;none&quot;：値なし
   * &quot;smartCase&quot;：最初の文字は大文字
   * &quot;lowerCase&quot;：すべて小文字
   * &quot;upperCase&quot;：すべて大文字
   * &quot;email&quot;：メールアドレス
   * &quot;phone&quot;：電話番号
   * &quot;identifier&quot;: identifier name
   * &quot;resIdentifier&quot;：ファイル名

* **dbEnum （文字列）**:「閉じられた」列挙の内部名を受け取ります。 列挙の値は、 `<srcschema>`.
* **defOnDuplicate（ブール値）**：この属性が有効になっている場合、レコードが重複すると、(@defaultで定義されている ) デフォルト値が自動的にレコードに再適用されます。
* **default (string)**：要素の動作を定義できます（関数の呼び出し、デフォルト値）。 この属性は XTK 式を受け取ります。
* **desc （文字列）**：要素の説明を挿入できます。 この説明は、インターフェイスのステータスバーに表示されます。
* **displayAsField (boolean)**：この属性がアクティブ化されている場合、「link」タイプ `<element>`  スキーマのツリービューのフィールドとして表示されます（「構造」タブ）。 これにより、リンクをローカルフィールドとして表示し、クエリ中に動作を変更することができます。 クエリの SELECT で要素が見つかった場合は、リンクターゲットの値が使用されます。 クエリの WHERE で要素が見つかった場合、リンクの基になるキーが使用されます。
* **編集（文字列）**：この属性は、スキーマにリンクされたフォームで使用される入力のタイプを指定します。
* **enum (string)**：フィールドにリンクされている列挙の名前を受け取ります。 列挙は、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**：この属性は、テーブルに定義が格納されない計算フィールドを定義します。 Xpath 式または XTK（文字列）式を受け取ります。
* **externalJoin (boolean)**:「リンク」タイプの要素での外部結合。
* **feature （文字列）**：特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルに格納されます。 指定できる値は次のとおりです。

   * 「共有」：コンテンツは、データタイプごとに共有テーブルに保存されます
   * &quot;dedicated&quot;：コンテンツは専用のテーブルに格納されます。

  SQL 特性テーブルは、次の特性タイプに基づいて自動的に作成されます。

   * 専用： `Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * 共有済み： `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

  特性フィールドには、1 つの値が特性に対して許可される単純なフィールドと、複数選択フィールドの 2 つのタイプがあります。このフィールドでは、複数の値を含むコレクション要素に特性がリンクされます。

  スキーマ内で特性が定義される場合、このスキーマは、単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されていません）。

* **featureDate（ブール値）**:「@feature」特性フィールドにリンクされた属性。 値が「true」の場合は、値が最後に更新された日時を確認できます。
* **filterPath (string)**：この属性は Xpath を受け取り、フィールドに対してフィルターを定義できます。
* **folderLink （文字列）**：エンティティを含むファイルを復元するためのリンク名をこの属性が受け取ります。
* **folderModel (string)**：エンティティのストレージを有効にするフォルダーのタイプを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **folderProcess (string)**：エンティティモデルインスタンスが保存されるリンクを定義します。 この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **fullLoad (boolean)**：この属性は、フォームのフィールド選択時に、テーブル内のすべてのレコードを強制的に表示します。
* **img （文字列）**：要素にリンクされた画像のパスを受け取ります。 この属性の値は、「namespace:image name」タイプです。 例：img=&quot;cus:myImage.jpg&quot; 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **integrity （文字列）**：ターゲットテーブルに対するソーステーブルの出現の参照整合性。

  アクセス可能な値は次のとおりです。

   * 「定義」:Adobe Campaignは、リンクを介して参照されるエンティティを削除しません
   * &quot;normal&quot;：ソースオカレンスを削除すると、ターゲットオカレンス上のリンクのキーが初期化されます（デフォルトモード）。このタイプの整合性は、すべての外部キーを初期化します
   * &quot;own&quot;：ソースオカレンスを削除すると、ターゲットオカレンスをトリガーに削除します。
   * &quot;owncopy&quot;: &quot;own&quot; （削除の場合）または（複製の場合）重複と同様です。
   * &quot;neutral&quot;：何もしません

* **label （文字列）**：要素のラベル。
* **labelSingular （文字列）**：インターフェイスの一部で使用される要素のラベル（単数形）。
* **length （文字列）**：最大 「文字列」タイプの SQL フィールドの値に対して許可されている文字の数。
* **localizable(boolean)**：有効化されている場合、この属性は、翻訳の「@label」属性の値を復元するようコレクションツールに指示します（内部使用）。
* **名前 (MNTOKEN)**：テーブル名と一致する要素の内部名。 「@name」属性の値は短く、できれば英語で記述し、XML にリンクされた命名規則に従う必要があります。

  スキーマがデータベースに書き込まれると、Adobe Campaignによってフィールド名にプレフィックスが自動的に追加されます。

   * &quot;i&quot;: &#39;integer&#39;タイプのプレフィックス。
   * &quot;d&quot;: &#39;double&#39;型のプレフィックス。
   * &quot;s&quot;：文字列タイプのプレフィックス。
   * &quot;ts&quot;: 「日付」タイプのプレフィックス。

  自律的にテーブルの名前を定義するには、メインスキーマ要素の定義で「@sqltable」属性を使用する必要があります。

* **noDbIndex (boolean)**：要素のインデックスを作成しないように指定できます。
* **ordered（ブール値）**：属性がアクティブ化されている場合 (ordered=&quot;true&quot;)、Adobe Campaignは XML コレクション要素内に要素宣言の順序を保持します。
* **pkSequence （文字列）**：自動増分キーの計算に使用されるシーケンスの名前を受け取ります。 この属性は、スキーマのルート要素に自動増分キーが定義されている場合にのみ使用できます。
* **pkgStatus （文字列）**：パッケージの書き出し時に、値はこの属性の値の関数として考慮されます。

   * &quot;always&quot;：要素は常に存在します
   * &quot;never&quot;：要素は存在しません
   * 「default (or nothing)」：要素がデフォルトの要素でない場合、またはその要素が内部フィールドでなく、他のインスタンスと互換性がない場合を除き、エクスポートされます。

* **ref（文字列）**：この属性は、複数のスキーマ（定義のファクタリング）で共有される >element> 要素への参照を定義します。 定義は現在のスキーマにコピーされません。
* **必須（ブール値）**：この属性がアクティブ化されている場合 (@required=&quot;true&quot;)、インターフェイスでフィールドがハイライト表示されます。 フィールドのラベルは、フォームでは赤で表示されます。
* **revAdvanced（ブール値）**：有効化すると、この属性は、反対側のリンクが「詳細」リンクであることを指定します。
* **revCardinality（文字列）**:2 つのテーブル間のリンクの基数を定義します。 「リンク」タイプで使用されます `<element>`.

  次のような値を選択できます。

   * &quot;single&quot; ：シンプルな 1-1 タイプのリンク
   * &quot;unbound&quot;: 1-N タイプのコレクションリンク

  デフォルトでは、リンクの作成時に属性が指定されていない場合、基数は 1 対 N になります。

* **revDesc（文字列）**：この属性は、反対側のリンクにリンクされた説明を受け取ります。
* **revExternalJoin (boolean)**：有効化すると、この属性を使用して、反対側のリンクで外部結合を強制できます。
* **revIntegrity（文字列）**：ターゲットスキーマの整合性を定義します。 「@integrity」属性と同じ値が許可されています。 デフォルトでは、Adobe Campaignはこの属性に「通常」の値を与えます。
* **revLabel （文字列）**：反対側のリンクのラベル。
* **revLink （文字列）**：反対側のリンクの名前。 値が&#x200B;_なし_&quot;。宛先スキーマには反対のリンクは作成されません。
* **revTarget （文字列）**：反対側のリンクのターゲット。
* **sql（ブール値）**：この属性が有効になっている場合 (@sql=&quot;true&quot;)、要素に xml=&quot;true&quot;プロパティが含まれている場合でも、SQL 要素の保存を強制します。
* **sqlname （文字列）**：テーブル作成時のフィールド名。 &quot;@sqlname&quot;が指定されていない場合、&quot;@name&quot;属性の値がデフォルトで使用されます。 スキーマをテーブルに書き込む際、フィールドのタイプに応じて、プレフィックスが自動的に追加されます。
* **sqltable （文字列）**：スキーマのメイン要素の場合、この属性は、デフォルトで生成される SQL テーブルの名前をオーバーロードします。 「@sqltable」が指定されていない場合、デフォルト名は次のように構造化されます。名前空間（最初の文字は大文字）の後に SrcSchema の値「@name」が続きます。
* **tableSpace （文字列）**：この属性を使用すると、テーブル領域を格納する新しいデータを表に対して指定できます（ルートで有効）。 `<element>`) をクリックします。
* **tableSpaceIndex (string)**：この属性を使用すると、テーブルの新しいインデックス・ストレージ・テーブル領域を指定できます（ルートで有効）。 `<element>`) をクリックします。
* **ターゲット (MNTOKEN)**：テーブル間のリンクを作成する際に、ターゲットスキーマの名前を受け取ります。 この属性は、「link」タイプの要素に対してのみ有効です。
* **template （文字列）**：この属性は、 `<element>` 複数のスキーマで共有される要素。 定義は、現在のスキーマに自動的にコピーされます。
* **translatedDefault (string)**:「@default」属性が見つかった場合、「@translatedDefault」を使用して、翻訳ツールで収集される式を再定義し、@defaultで定義された式に一致させることができます（内部使用）。
* **translatedExpr (string)**:「@expr」属性が見つかった場合、「@translatedExpr」属性を使用して、「@expr」で定義された式 ( 翻訳ツール（内部使用）で収集される式 ) に一致する式を再定義できます。
* **型 (MNTOKEN)**：要素に保存されるデータのタイプを定義します。

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
   * 日付
   * 倍精度浮動小数点数
   * enum
   * 浮動小数点数
   * html
   * int64
   * リンク
   * 長い
   * メモ
   * MNTOKEN
   * 割合
   * primarykey
   * short
   * 文字列
   * 時間
   * 期間
   * uuid

* **unbound (boolean)**：属性が有効化されている場合 (unbound=&quot;true&quot;)、リンクは 1 対多の基数のコレクション要素として宣言されます。
* **userEnum (string)**:「open」列挙の内部名を受け取ります。 列挙値は、インターフェイスでユーザーが定義できます。
* **xml（ブール値）**：このオプションを有効にすると、要素で定義されたすべての値が、XML 形式の「mData」フィールド内の TEXT タイプに格納されます。 つまり、これらのフィールドにはフィルターや並べ替えは実行されません。
* **xmlChildren (boolean)**：各子 ( `<element>  or  <attribute>   ) of the   <element>    element in an XML document.   </element>  </attribute> </element>`
