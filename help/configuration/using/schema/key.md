---
product: campaign
title: スキーマの要素と属性 – キー要素
description: 主要な要素
feature: Schema Extension
exl-id: 3d0ef574-27a3-40f2-91a0-70e9583d9980
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 1%

---

# 主要な要素 {#key--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-8}

key:==keyfield

## 属性 {#attributes-8}

* @allowEmptyPart （ブール値）
* @applicableIf （文字列）
* @internal （ブール値）
* @label （文字列）
* @name （MNTOKEN）
* @noDbIndex （ブール値）

## 親 {#parents-8}

`<element>`

## 子 {#children-8}

`<keyfield>`

## 説明 {#description-8}

この要素を使用すると、テーブル内のレコードを識別するためのキーを定義できます。

テーブルには少なくとも 1 つのキーが必要です。

## 用途および使用コンテキスト {#use-and-context-of-use-6}

原則として、キーはスキーマのメイン要素とインデックスの後に宣言されます。

キーに複数のフィールド（つまり、複数の `<keyfield>` の子）が含まれる場合、キーは複合キーと呼ばれます。 プライマリキーの定義に複合キーを使用しないでください。

スキーマのメイン要素に「@autopk=true」属性が含まれている場合、プライマリキーは一意です。 スキーマごとに 1 つのプライマリキーのみを持つことができます。

最初の 1000 個の識別子は予約されているので、キーに対して値の範囲を定義する必要がある場合は、1000 から開始します。

## 属性の説明 {#attribute-description-8}

* **allowEmptyPart （ブール値）**：複合キーの場合、この属性が有効な場合、少なくとも 1 つのキーが空でない場合、それらのキーが有効であると見なされます。 その場合、空の概念の値は「0」（ブール値またはすべてのタイプの数値データの場合）になります。 デフォルトでは、複合キーを構成するすべてのキーを入力する必要があります。
* **applicableIf （string）**：この属性を使用すると、キーをオプションにすることができます。 キー定義が適用される条件を定義します。 この属性は XTK 式を受け取ります。
* **internal （boolean）**：有効な場合、この属性を使用してAdobe Campaignにキーがプライマリであることを知らせます。
* **label （文字列）**：キーのラベル。
* **name （MNTOKEN）**：キーの内部名。
* **noDbIndex （ブール値）**：有効になっている場合（noDbIndex=&quot;true&quot;）、キーに一致するフィールドのインデックスは作成されません。

## 例 {#examples-------}

「@expr」フィールドまたは「エイリアス」フィールドのいずれかを空にすることを許可する複合キーの宣言。

```
<key name="node" allowEmptyPart="true">
  <keyfield xpath="@expr"/>
   <keyfield xpath="@alias"/>
 </key>
```

`<srcschema>` および一致する SQL クエリの文字列タイプの「名前」フィールドにおけるプライマリキーの宣言：

```
 
<key name="PrimaryKey" internal="true">  
  <keyfield xpath="@name"/>
</key>

CREATE UNIQUE INDEX Schema_PrimaryKey ON Schema(sName);
```
