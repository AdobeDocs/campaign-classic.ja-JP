---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: d7d1e427-12e0-4f07-9e01-d184dbe2ebf1
source-git-commit: 34404fbe935e68f3cc11d937839209443ad4ca60
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# dbindex 要素 {#dbindex--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-3}

dbindex:==keyfield

## 属性 {#attributes-3}

* @_operation (string)
* @applicableIf (string)
* @label (string)
* @name (MNTOKEN)
* @unique (boolean)

## 親 {#parents-3}

`<element>`

## 子 {#children-3}

`<keyfield>`

## 説明 {#description-3}

この要素を使用して、テーブルにリンクするインデックスを定義できます。

## 使用と使用のコンテキスト {#use-and-context-of-use-3}

複数のインデックスを定義できます。 1 つのインデックスは、テーブルの 1 つ以上のフィールドを参照できます。 インデックス宣言は、通常、メインスキーマ要素の定義に従います。

`<dbindex>` で定義されている `<keyfield>` 要素の順序は非常に重要です。 最初の `<keyfield>` は、クエリの主な基になるインデクス基準である必要があります。

データベース内のインデックスの名前は、テーブルの名前とインデックスの名前を連結して計算されます。 例：テーブル名「Sample」、名前空間「Cus」、インデックス名「MyIndex」 —> インデックス作成時のインデックスフィールドの名前：&quot;CusSample_myIndex&quot;.

## 属性の説明 {#attribute-description-3}

* **_operation （文字列）**:データベースに書き込むタイプを定義します。

   この属性は、主に標準のスキーマを拡張する際に使用されます。

   アクセス可能な値は次のとおりです。

   * &quot;none&quot;:紐付けのみ。 つまり、Adobe Campaignは、更新せずに要素を回復します。要素が存在しない場合は、エラーを生成します。
   * &quot;insertOrUpdate&quot;:を挿入して更新します。 つまり、Adobe Campaignは要素を更新するか、存在しない場合は作成します。
   * &quot;insert&quot;:挿入 つまり、Adobe Campaignは、要素が存在するかどうかを確認せずに要素を挿入します。
   * &quot;update&quot;:更新。 つまり、Adobe Campaignは要素を更新するか、存在しない場合はエラーを生成します。
   * &quot;delete&quot;:削除します。 つまり、Adobe Campaignは要素を復元および削除します。

* **applicableIf (string)**:インデックスを考慮する条件 — XTK 式を受け取ります。
* **label （文字列）**:インデックスのラベル。
* **名前 (MNTOKEN)**:一意のインデックス名。
* **一意（ブール値）**:このオプションが有効な場合 (@unique=&quot;true&quot;)、属性はフィールド全体でインデックスの一意性を保証します。

## 例 {#examples-3}

「id」フィールドでのインデックスの作成。 (`<dbindex>` 要素トリガーの「@unique」属性。データベース（クエリ）でインデックスが作成されたときに「UNIQUE」 SQL キーワードを追加します )。

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

「@mail」フィールドと「@phoneNumber」フィールドの複合インデックスの作成：

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
