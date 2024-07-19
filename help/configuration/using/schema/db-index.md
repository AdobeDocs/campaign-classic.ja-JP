---
product: campaign
title: 要素と属性 – dbindex 要素
description: dbindex 要素
feature: Schema Extension
exl-id: d7d1e427-12e0-4f07-9e01-d184dbe2ebf1
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 1%

---

# dbindex 要素 {#dbindex--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-3}

dbindex:==keyfield

## 属性 {#attributes-3}

* @_operation （文字列）
* @applicableIf （文字列）
* @label （文字列）
* @name （MNTOKEN）
* @unique （ブール値）

## 親 {#parents-3}

`<element>`

## 子 {#children-3}

`<keyfield>`

## 説明 {#description-3}

この要素を使用すると、テーブルにリンクするインデックスを定義できます。

## 用途および使用コンテキスト {#use-and-context-of-use-3}

複数のインデックスを定義できます。 1 つのインデックスで、テーブルの 1 つ以上のフィールドを参照できます。 インデックスの宣言は、通常、メインのスキーマ要素の定義に従います。

`<dbindex>` で定義される `<keyfield>` 要素の順序は非常に重要です。 最初の `<keyfield>` は、クエリが主に基づいているインデックス化条件である必要があります。

データベース内のインデックスの名前は、テーブルの名前とインデックスの名前を連結して計算されます。 例：テーブル名「Sample」、名前空間「Cus」、インデックス名「MyIndex」 – > インデックス作成のクエリ中のインデックスフィールドの名前：「CusSample_myIndex」。

## 属性の説明 {#attribute-description-3}

* **_operation （文字列）**：データベースへの書き込みのタイプを定義します。

  この属性は、主に標準スキーマを拡張する際に使用されます。

  アクセス可能な値は次のとおりです。

   * 「なし」：紐付けのみ。 つまり、Adobe Campaignは要素を更新せずに復元し、要素が存在しない場合はエラーを生成します。
   * &quot;insertOrUpdate&quot;：挿入で更新します。 つまり、Adobe Campaignは要素を更新し、存在しない場合は作成します。
   * 「挿入」：挿入。 つまり、Adobe Campaignは、存在するかどうかを確認せずに要素を挿入します。
   * 「更新」：更新。 つまり、Adobe Campaignは要素を更新するか、要素が存在しない場合はエラーを生成します。
   * 「削除」：削除。 つまり、Adobe Campaignは要素を復元して削除します。

* **applicableIf （文字列）**：インデックスを考慮する条件 – XTK 式を受け取ります。
* **label （string）**：インデックスラベル。
* **name （MNTOKEN）**：一意のインデックス名。
* **unique （boolean）**：このオプションをオンにする（@unique=&quot;true&quot;）と、フィールド全体でインデックスの一意性が属性で保証されます。

## 例 {#examples-3}

「id」フィールドでのインデックスの作成。 （`<dbindex>` 要素の「@unique」属性は、データベース（クエリ）にインデックスが作成されたときに「UNIQUE」 SQL キーワードを追加することをトリガーにします）。

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

「@mail」フィールドと「@phoneNumber」フィールドに複合インデックスを作成：

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
