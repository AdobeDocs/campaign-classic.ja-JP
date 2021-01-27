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
source-wordcount: '338'
ht-degree: 2%

---


# dbindex要素{#dbindex--element}

## コンテンツモデル{#content-model-3}

dbindex:==keyfield

## 属性 {#attributes-3}

* @_operation（文字列）
* @applicableIf (string)
* @label（文字列）
* @name (MNTOKEN)
* @unique（ブール値）

## 親{#parents-3}

`<element>`

## 子 {#children-3}

`<keyfield>`

## 説明 {#description-3}

この要素を使用すると、テーブルにリンクされたインデックスを定義できます。

## 使用と使用のコンテキスト{#use-and-context-of-use-3}

複数のインデックスを定義できます。 1つのインデックスで、テーブルの1つ以上のフィールドを参照できます。 インデックス宣言は、通常、メインスキーマ要素の定義に従います。

`<dbindex>`に定義される`<keyfield>`要素の順序は非常に重要です。 最初の`<keyfield>`は、クエリが主に基づくインデクション基準にする必要があります。

データベース内のインデックスの名前は、テーブルの名前とインデックスの名前を連結して計算されます。 次に例を示します。インデックス作成クエリ中の、テーブル名「Sample」、名前空間「Cus」、インデックス名「MyIndex」 —>インデックスフィールドの名前：&quot;CusSample_myIndex&quot;.

## 属性の説明{#attribute-description-3}

* **_operation (string)**:データベースに書き込むタイプを定義します。

   この属性は主に、標準搭載されたスキーマを拡張する場合に使用します。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:和解のみ。 つまり、Adobe Campaignは、要素を更新せずに回復します。要素が存在しない場合はエラーが発生します。
   * &quot;insertOrUpdate&quot;:挿入時に更新します。 つまり、Adobe Campaignは、要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入。 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 これは、Adobe Campaignが要素を更新するか、存在しない場合はエラーを生成することを意味します。
   * &quot;delete&quot;:削除。 つまり、Adobe Campaignは要素を回復および削除します。

* **applicableIf (string)**:インデックスを考慮する条件 — XTK式を受け取ります。
* **label (string)**:indexラベル。
* **name (MNTOKEN)**:一意のインデックス名。
* **unique (boolean)**:このオプションが有効な場合(@unique=&quot;true&quot;)、属性はフィールド全体でのインデックスの一意性を保証します。

## 例 {#examples-3}

「id」フィールドでのインデックスの作成。 (`<dbindex>`要素トリガーの「@unique」属性は、データベース(クエリ)にインデックスが作成されたときに「UNIQUE」SQLキーワードを追加します)。

```
<element label="Sample" name="Sample">
  <dbindex name="myIndex" label="My index on the ID field" unique="true" applicableIf="HasPackage('nms:social')">
      <keyfield xpath="@id"/>
  </dbindex>
    <attribute name="id" type="long"/>
</element>          
```

```
ALTER TABLE CusSample ADD iSampleId INTEGER;
UPDATE CusSample SET iSampleId = 0;
ALTER TABLE CusSample ALTER COLUMN iSampleId SET Default 0;
ALTER TABLE CusSample ALTER COLUMN iSampleId SET NOT NULL; 
CREATE UNIQUE INDEX CusSample_myIndex ON CusSample(iSampleId);
```

「@mail」フィールドと「@phoneNumber」フィールドに複合インデックスを作成します。

```
<element label="NewSchemaUser" name="NewSchemaUser">
  <dbindex name="myIndex" label="My composite index">
         <keyfield xpath="@email"/>
         <keyfield xpath="@phone"/>
  </dbindex>
  
  <attribute name="email" type="string"/>
  <attribute name="phone" type="string"/>
</element>      
```

```
CREATE INDEX DocNewSchemaUser_myIndex ON DocNewSchemaUser(sEmail, sPhone);
```
