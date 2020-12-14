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
source-wordcount: '2012'
ht-degree: 1%

---


# 要素要素{#element--element}

## コンテンツモデル{#content-model-4}

element:=(attribute) | compute-string | dbindex |デフォルト |要素 |ヘルプ |結合 | key | sysFilter | translatedDefault)

## 属性 {#attributes-4}

_operation (string)、advanced (boolean)、集計(string)、applicableIf (string)、autopk (boolean)、belonsTo (string)、convDate (string)、dataSource (string)、defOnDuplicate (boolean)、desc (string)、displayAsField(boolean)、doesNotSupportDiff (boolean)、edit (string)、emptyKeyValue (string)、enum (string)、enumImage (string)、expandSchemaTarget (string)、expr (string)、externalJoin (boolean)、featureDate (boolean)、filerPath (string)、folderLink (string)folderModel（文字列）、folderProcess（文字列）、fullLoad（ブール値）、hierarchical（ブール値）、hierarchicalPath（文字列）、img（文字列）、inout（文字列）、integrity（文字列）、label（文字列）、length（文字列）、localizable（ブール値）、name(MNTOKEN)、noDbIndex（ブール値）（ブール値）、順序付き（ブール値）、オーバーフローテーブル（ブール値）、pkSequence（文字列）、pkgStatus（文字列）、ref（文字列）、revAdvanced（ブール値）、revCardinality（文字列）、revDesc（ブール値）、revExternalJoin（ブール値）、revIntegrity（文字列）、revLinLink文字列)、revTarget （文字列）、revVisibleIf （文字列）、sql （ブール値）、sqlname （文字列）、sqltable （文字列）、tableSpace （文字列）、tableSpaceIndex （文字列）、ターゲット(MNTOKEN)、template （文字列）、templateDefault （ブール値）、translatedExpr （文字列）、type （文字列）トークン)、連結されていない（ブール値）、ユーザー（ブール値）、userEnum（文字列）、visibleIf（文字列）、xml（ブール値）、xmlChildren（ブール値）

## 親{#parents-4}

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

Adobe Campaignには4種類の`<element>`要素があります。

* ルート`<element>` :スキーマに一致するSQLテーブルの名前を定義します。
* 構造`<element>` :`<element>`のグループを定義   または   `<attribute>`    エレメント。
* リンク`<element>`:リンクを定義します。 この要素には「@type=link」属性を含める必要があります。
* XML `<element>` :テキストタイプ「mData」フィールドを定義します。 この要素には「@type=xml」属性を含める必要があります。

## 属性の説明{#attribute-description-4}

* **_operation (string)**:データベースに書き込むタイプを定義します。

   この属性は主に、標準搭載されたスキーマを拡張する場合に使用します。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:和解のみ。 つまり、Adobe Campaignは、要素を更新せずに回復します。要素が存在しない場合はエラーが発生します。
   * &quot;insertOrUpdate&quot;:挿入時に更新します。 つまり、Adobe Campaignは、要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 これは、Adobe Campaignが要素を更新するか、存在しない場合はエラーを生成することを意味します。
   * &quot;delete&quot;:削除。 つまり、Adobe Campaignは要素を回復および削除します。

* **advanced(boolean)**:このオプションをアクティブ化すると(@advanced=&quot;true&quot;)、フォーム内のリストの設定にアクセスできるフィールドのリスト上で属性を非表示にできます。
* **集計（文字列）**:別のスキーマを `<element>`  介しての定義をコピーできます。この属性は、「名前空間：名前」の形式のスキーマ宣言を受け取ります。
* **applicableIf (string)**:インデックスを適用する条件。この属性はXTK式を受け取ります。
* **autopk (boolean)**:このオプションが有効な場合(autopk=&quot;true&quot;)、一意のキーが自動的に定義されます。このオプションは、スキーマのメイン要素でのみ使用できます。 警告：Adobe Campaignは、生成されたキーが一意であることを保証するだけです。 キー値が連続していて増分的であることは保証されません。
* **dataPolicy (string)**:「SQL」フィールドで許可される値に対して、承認制約を指定できます。この属性の値は次のとおりです。

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
* **default（文字列）**:要素の動作（関数の呼び出し、デフォルト値）を定義できます。この属性はXTK式を受け取ります。
* **desc（文字列）**:要素の説明を挿入できます。この説明は、インターフェイスのステータスバーに表示されます。
* **displayAsField (boolean)**:この属性がアクティブ化されると、「リンク」タイプ `<element>`  がスキーマのツリー表示（「構造」タブ）にフィールドとして表示されます。これにより、リンクをローカルフィールドとして表示し、クエリ中に動作を変更することができます。 クエリのSELECTに要素が見つかると、リンクターゲットの値が使用されます。 クエリのWHEREに要素が見つかると、リンクの基になるキーが使用されます。
* **編集（文字列）**:この属性は、スキーマにリンクされたフォームで使用される入力の種類を指定します。
* **enum（文字列）**:は、フィールドにリンクされている定義済みリストの名前を受け取ります。定義済みリストは、同じスキーマまたはリモートスキーマに挿入できます。
* **expr（文字列）**:この属性は、テーブルに定義が格納されていない計算済みフィールドを定義します。XpathまたはXTK （文字列）式を受け取ります。
* **externalJoin (boolean)**:「リンク」型要素の外部結合。
* **機能（文字列）**:特性フィールドを定義します。これらのフィールドは、既存のテーブルのデータを拡張するために使用されますが、別のテーブルのストレージと共に使用されます。指定できる値は次のとおりです。

   * &quot;共有&quot;:コンテンツは、データ型ごとに共有テーブルに保存されます
   * &quot;dedicated”:コンテンツは専用のテーブルに格納される

   SQL特性テーブルは、次の特性タイプに基づいて自動的に作成されます。

   * 専用：`Ft_[name_of_the_schema_containing_the_characteristic]_[name_of_the_characteristic]`
   * shared: `Ft_[type_of_key_of_the_schema_containing_the_characteristic]_[type_of_the_characteristic]`

   次の2種類の特性フィールドがあります。単一の値が特性に対して承認される単純なフィールドと、複数の選択フィールド。複数の値を含むコレクション要素に特性がリンクされるフィールドです。

   特性がスキーマで定義される場合、このスキーマは、単一のフィールドに基づくメインキーを持つ必要があります（複合キーは許可されません）。

* **featureDate (boolean)**:属性が「@feature」特性フィールドにリンクされている。値が「true」の場合は、値が最後に更新された日時を確認できます。
* **filterPath (string)**:この属性はXpathを受け取り、フィールドに対してフィルターを定義できます。
* **folderLink (string)**:この属性は、エンティティを含むファイルを回復するためのリンクの名前を受け取ります。
* **folderModel (string)**:エンティティストレージを有効にするフォルダーのタイプを定義します。この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **folderProcess (string)**:エンティティモデルインスタンスが保存されるリンクを定義します。この属性は、「@folderLink」が存在する場合にのみ定義されます。
* **fullLoad (boolean)**:この属性は、フォーム内のフィールド選択時に、テーブル内のすべてのレコードを強制的に表示します。
* **img （文字列）**:は、要素にリンクされた画像のパスを受け取ります。この属性の値は、「名前空間：画像名」タイプです。 次に例を示します。img=&quot;cus:myImage.jpg&quot;. 物理的には、画像をアプリケーションサーバーに読み込む必要があります。
* **整合性（文字列）**:ターゲットテーブルに対するソーステーブルのオカレンスの参照整合性。

   アクセス可能な値は次のとおりです。

   * &quot;define&quot;:Adobe Campaignがリンクを介して参照されている場合、エンティティは削除されません。
   * &quot;normal&quot;:ソースオカレンスを削除すると、ターゲットオカレンス上のリンクのキーが初期化されます（デフォルトモード）。このタイプの整合性は、すべての外部キーを初期化します
   * &quot;own&quot;:ソースオカレンスの削除によって、ターゲットオカレンスの削除がトリガされます
   * &quot;owncopy&quot;:「own」（削除の場合）または重複（複製の場合）に似ている
   * &quot;neutral&quot;:何もしない

* **label (string)**:要素のラベル。
* **labelSingular (string)**:インターフェイスの一部で使用される要素のラベル（単数形）。
* **length (string)**:最大「string」型のSQLフィールドの値に対して承認された文字数。
* **localizable (boolean)**:この属性がアクティブ化されている場合、収集ツールに対して翻訳用の「@label」属性の値を復元するよう指示します（内部使用）。
* **name (MNTOKEN)**:テーブルの名前と一致する要素の内部名。「@name」属性の値は、短く、できれば英語で指定する必要があり、XMLにリンクされた命名の制約に従ってください。

   スキーマがデータベースに書き込まれると、フィールド名にプリフィックスがAdobe Campaignによって自動的に追加されます。

   * &quot;i&quot;:プレフィックスの値を指定します。
   * &quot;d&quot;:プレフィックスが表示されます。
   * &quot;s&quot;:のプレフィックスを指定します。
   * &quot;ts&quot;:プレフィックスに値を入力します。

   自律的な方法でテーブルの名前を定義するには、メインのスキーマ要素の定義で「@sqltable」属性を使用する必要があります。

* **noDbIndex (boolean)**:要素のインデックスを作成しないように指定できます。
* **ordered (boolean)**:属性がアクティブ化された場合(ordered=&quot;true&quot;)、Adobe Campaignは要素宣言のシーケンスをXMLコレクション要素内に保持します。
* **pkSequence （文字列）**:は、自動増分キーの計算に使用されるシーケンスの名前を受け取ります。この属性は、スキーマのルート要素で自動増分キーが定義されている場合にのみ使用できます。
* **pkgStatus (string)**:パッケージのエクスポート時に、値はこの属性の値の関数として考慮されます。

   * &quot;always&quot;:要素は常に存在します
   * &quot;never&quot;:要素が存在しない
   * &quot;default (or nothing)&quot;:要素は、デフォルトの要素でない場合、または内部フィールドでなく、他のインスタンスと互換性がない場合を除き、エクスポートされます

* **ref （文字列）**:この属性は、複数のスキーマ（定義のファクタリング）が共有する>element>要素への参照を定義します。定義は現在のスキーマにコピーされません。
* **required (boolean)**:この属性がアクティブ化された場合(@required=&quot;true&quot;)、インターフェイスでフィールドがハイライト表示されます。フィールドのラベルは、フォームでは赤で表示されます。
* **revAdvanced （ブール値）**:この属性を有効にすると、反対側のリンクが「アドバンス」リンクであることを指定します。
* **revCardinality（文字列）**:この属性は、2つのテーブル間のリンクのカーディナリティを定義します。これは「リンク」型`<element>`で使用されます。

   次のような値を選択できます。

   * &quot;single&quot; :単純な1-1タイプのリンク
   * &quot;unbound&quot;:1-N型収集リンク

   デフォルトでは、リンクの作成時に属性が指定されていない場合、基数は1 ～ Nになります。

* **revDesc （文字列）**:この属性は、反対のリンクにリンクされた説明を受け取ります。
* **revExternalJoin （ブール値）**:この属性を有効にすると、反対のリンクに外部結合を強制できます。
* **revIntegrity （文字列）**:この属性は、ターゲットスキーマの整合性を定義します。「@integrity」属性と同じ値が許可されます。 デフォルトでは、Adobe Campaignはこの属性に「normal」値を与えます。
* **revLabel（文字列）**:反対のリンクのラベル。
* **revLink （文字列）**:反対側のリンクの名前。値が「_NONE_」の場合、反対側のリンクは宛先スキーマに作成されません。
* **revTarget （文字列）**:反対のリンクのターゲット。
* **sql (boolean)**:この属性がアクティブ化される(@sql=&quot;true&quot;)と、xml=&quot;true&quot;プロパティが含まれている場合でも、SQL要素のストレージが強制されます。
* **sqlname （文字列）**:テーブル作成時のフィールドの名前。「@sqlname」を指定しない場合、「@name」属性の値がデフォルトで使用されます。 テーブルにスキーマを書き込むとき、フィールドの種類に応じてプリフィックスが自動的に追加されます。
* **sqltable （文字列）**:スキーマのメイン要素の場合、この属性は、デフォルトで生成されるSQLテーブルの名前をオーバーロードします。「@sqltable」を指定しない場合、デフォルトの名前は次のように構造化されます。名前空間（大文字の最初の文字）の後にSrcSchema &quot;@name&quot;の値が続く。
* **tableSpace (string)**:この属性を使用すると、テーブルの新しいデータ格納テーブルスペースを指定できます(ルートで有効 `<element>`)。
* **tableSpaceIndex (string)**:この属性を使用すると、テーブルの新しいインデックス・ストレージ表領域を指定できます(ルートで有効 `<element>`)。
* **ターゲット(MNTOKEN)**:は、テーブル間のリンクを作成する際に、ターゲットスキーマの名前を受け取ります。この属性は、「リンク」タイプの要素に対してのみ有効です。
* **template (string)**:この属性は、複数のスキーマが共有する `<element>` 要素への参照を定義します。定義は自動的に現在のスキーマにコピーされます。
* **translatedDefault(string)**:「@default」属性が見つかった場合、「@translatedDefault」を使用すると、式を再定義して、翻訳ツールによって収集される@defaultで定義されているのと一致させることができます（内部使用）。
* **translatedExpr (string)**:「@expr」属性が見つかった場合、「@translatedExpr」属性を使用すると、「@expr」で定義された式と一致する翻訳を再定義でき、翻訳ツールによって収集されます（内部使用）。
* **type (MNTOKEN)**:要素に格納するデータのタイプを定義します。

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

* **unbound (boolean)**:属性がアクティブ化された場合(unbound=&quot;true&quot;)、そのリンクは1-N個のカーディナリティのコレクション要素として宣言されます。
* **userEnum (string)**:は、「open」定義済みリストの内部名を受け取ります。定義済みリスト値は、インターフェイスでユーザーが定義できます。
* **xml（ブール値）**:このオプションを有効にすると、要素で定義されたすべての値がXMLのTEXTタイプ「mData」フィールドに格納されます。これは、これらのフィールドにフィルタや並べ替えが設定されないことを意味します。
* **xmlChildren (boolean)**:各子のストレージを強制(  `<element>  or  <attribute>   ) of the   <element>    element in an XML document.   </element>  </attribute> </element>`
