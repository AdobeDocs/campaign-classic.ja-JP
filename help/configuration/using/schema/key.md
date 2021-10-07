---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: 3d0ef574-27a3-40f2-91a0-70e9583d9980
source-git-commit: 34404fbe935e68f3cc11d937839209443ad4ca60
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 3%

---

# キー要素 {#key--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-8}

key:==keyfield

## 属性 {#attributes-8}

* @allowEmptyPart (boolean)
* @applicableIf (string)
* @internal (boolean)
* @label (string)
* @name (MNTOKEN)
* @noDbIndex (boolean)

## 親 {#parents-8}

`<element>`

## 子 {#children-8}

`<keyfield>`

## 説明 {#description-8}

この要素を使用して、テーブル内のレコードを識別するためのキーを定義できます。

テーブルには、少なくとも 1 つのキーが必要です。

## 使用と使用のコンテキスト {#use-and-context-of-use-6}

原則として、キーは、スキーマのメイン要素とインデックスの後に宣言されます。

キーは、複数のフィールド（例：複数の `<keyfield>` 子）が含まれる場合、複合と呼ばれます。 複合キーを使用して主キーを定義しないでください。

スキーマのメイン要素に「@autopk=true」属性が含まれている場合、プライマリキーは一意です。 1 つのスキーマにつき 1 つのプライマリキーのみを持つことができます。

最初の 1000 個の識別子は予約されているので、キーに対して値の範囲を定義する必要がある場合は、1000 から始めます。

## 属性の説明 {#attribute-description-8}

* **allowEmptyPart (boolean)**:複合キーの場合、この属性が有効な場合、少なくとも 1 つのキーが空でない場合、それらのキーは有効と見なされます。この場合、空の概念値は「0」（ブール値またはすべてのタイプの数値データ）です。 デフォルトでは、複合キーを構成するすべてのキーを入力する必要があります。
* **applicableIf (string)**:この属性を使用すると、キーをオプションにできます。キー定義を適用する条件を定義します。 この属性は XTK 式を受け取ります。
* **内部（ブール値）**:有効化されている場合、この属性はキーがプライマリであることをAdobe Campaignに知らせます。
* **label （文字列）**:キーのラベル。
* **名前 (MNTOKEN)**:キーの内部名。
* **noDbIndex (boolean)**:有効化された場合 (noDbIndex=&quot;true&quot;)、キーと一致するフィールドのインデックスは作成されません。

## 例 {#examples-------}

「@expr」フィールドまたは「alias」フィールドを空にすることを許可する複合キーの宣言：

```
<key name="node" allowEmptyPart="true">
  <keyfield xpath="@expr"/>
   <keyfield xpath="@alias"/>
 </key>
```

`<srcschema>` 内の STRING 型の「Name」フィールドでのプライマリキーの宣言と、一致する SQL クエリ：

```
 
<key name="PrimaryKey" internal="true">  
  <keyfield xpath="@name"/>
</key>

CREATE UNIQUE INDEX Schema_PrimaryKey ON Schema(sName);
```
