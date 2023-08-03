---
product: campaign
title: スキーマ要素と属性 — キー要素
description: キー要素
feature: Schema Extension
exl-id: 3d0ef574-27a3-40f2-91a0-70e9583d9980
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 8%

---

# キー要素 {#key--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-8}

key:==keyfield

## 属性 {#attributes-8}

* @allowEmptyPart (boolean)
* @applicableIf （文字列）
* @internal (boolean)
* @label （文字列）
* @name (MNTOKEN)
* @noDbIndex (boolean)

## 親 {#parents-8}

`<element>`

## 子 {#children-8}

`<keyfield>`

## 説明 {#description-8}

この要素を使用して、テーブル内のレコードを識別するためのキーを定義できます。

テーブルには少なくとも 1 つのキーが必要です。

## 使用と使用のコンテキスト {#use-and-context-of-use-6}

原則として、キーはスキーマのメイン要素とインデックスの後に宣言されます。

キーは、複数のフィールド（複数のフィールド）が含まれる場合は複合と呼ばれます。 `<keyfield>` 子 )。 主キーの定義に複合キーを使用しないでください。

スキーマのメイン要素に「@autopk=true」属性が含まれている場合、プライマリキーは一意です。 スキーマごとに 1 つのプライマリキーのみを持つことができます。

最初の 1,000 個の識別子が予約されているので、キーに対して値の範囲を定義する必要がある場合は、1,000 から始めます。

## 属性の説明 {#attribute-description-8}

* **allowEmptyPart（ブール値）**：複合キーの場合、この属性がアクティブ化されている場合、少なくとも 1 つのキーが空でない場合は、それらのキーが有効と見なされます。 この場合、空の概念値は「0」（ブール値またはすべてのタイプの数値データ）です。 デフォルトでは、複合キーを構成するすべてのキーを入力する必要があります。
* **applicableIf（文字列）**：この属性を使用して、キーをオプションにできます。 キー定義を適用する条件を定義します。 この属性は XTK 式を受け取ります。
* **内部（ブール値）**：アクティブ化されている場合、この属性はキーがプライマリであることをAdobe Campaignに知らせます。
* **label （文字列）**：キーのラベル。
* **名前 (MNTOKEN)**：キーの内部名。
* **noDbIndex (boolean)**：アクティブ化されている場合 (noDbIndex=&quot;true&quot;)、キーと一致するフィールドのインデックスは作成されません。

## 例 {#examples-------}

「@expr」フィールドまたは「alias」フィールドを空にすることを許可する複合キーの宣言：

```
<key name="node" allowEmptyPart="true">
  <keyfield xpath="@expr"/>
   <keyfield xpath="@alias"/>
 </key>
```

STRING 型の&quot;Name&quot;フィールドでのプライマリキーの宣言 `<srcschema>`  と一致する SQL クエリ：

```
 
<key name="PrimaryKey" internal="true">  
  <keyfield xpath="@name"/>
</key>

CREATE UNIQUE INDEX Schema_PrimaryKey ON Schema(sName);
```
