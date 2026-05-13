---
product: campaign
title: 要素と属性 – dbindex要素
description: dbindex エレメント
feature: Schema Extension
exl-id: d7d1e427-12e0-4f07-9e01-d184dbe2ebf1
TQID: https://experienceleague.adobe.com/VWv-F5lUufsXeurPt0GMUICNvrp7cKi-AJWxFzA6wRE
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 341
ht-degree: 1%

---

# dbindex エレメント {#dbindex--element}


## コンテンツモデル {#content-model-3}

dbindex:==keyfield

## 属性 {#attributes-3}

* @_operation （文字列）
* @applicableIf （文字列）
* @label （文字列）
* @name （トークン）
* @unique （ブール値）

## 親 {#parents-3}

`<element>`

## 子 {#children-3}

`<keyfield>`

## 説明 {#description-3}

この要素を使用すると、テーブルにリンクされたインデックスを定義できます。

## 用途と使用状況 {#use-and-context-of-use-3}

複数の索引を定義できます。 1つのインデックスは、テーブルの1つ以上のフィールドを参照できます。 インデックス宣言は通常、メインスキーマ要素の定義に従います。

`<dbindex>`で定義された`<keyfield>`要素の順序は非常に重要です。 最初の`<keyfield>`は、主にクエリの基になるインデックス作成基準である必要があります。

データベース内のインデックスの名前は、テーブルの名前とインデックスの名前を連結して計算されます。 例：テーブル名「Sample」、名前空間「Cus」、インデックス名「MyIndex」 – > インデックス作成クエリ時のインデックスフィールドの名前：「CusSample_myIndex」。

## 属性の説明 {#attribute-description-3}

* **_operation （文字列）**: データベースへの書き込みの種類を定義します。

  この属性は、主にすぐに使用できるスキーマを拡張する場合に使用されます。

  アクセス可能な値は次のとおりです。

   * &quot;none&quot;：和解のみ。 つまり、Adobe Campaignはアップデートせずに復元したり、存在しない場合はエラーを発生させたりします。
   * &quot;insertOrUpdate&quot;：挿入で更新します。 つまり、Adobe Campaignがエレメントを更新するか、エレメントが存在しない場合はエレメントを作成します。
   * &quot;insert&quot;：挿入。 つまり、Adobe Campaignはエレメントが存在するかどうかを確認せずに挿入します。
   * &quot;update&quot;：更新します。 つまり、Adobe Campaignはエレメントを更新するか、エレメントが存在しない場合はエラーを生成します。
   * &quot;delete&quot;：削除。 つまり、Adobe Campaignは復元と削除を行います。

* **applicableIf （文字列）**: インデックスを考慮するための条件 – XTK式を受け取ります。
* **label （文字列）**: インデックスラベル。
* **name （MNTOKEN）**：一意のインデックス名。
* **一意（ブール値）**：このオプションがアクティブ化されている場合（@unique=&quot;true&quot;）、属性はフィールド全体でインデックスの一意性を保証します。

## 例 {#examples-3}

「id」フィールドにインデックスを作成します。 （`<dbindex>`要素トリガーの「@unique」属性は、インデックスがデータベース（クエリ）で作成されたときに「UNIQUE」 SQL キーワードを追加します）。

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

「@mail」フィールドと「@phoneNumber」フィールドでの複合インデックスの作成：

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
