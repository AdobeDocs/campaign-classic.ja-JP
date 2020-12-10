---
solution: Campaign Classic
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
translation-type: tm+mt
source-git-commit: 1818bd2aeb60689b2ce0e59cb0bd157f000de513
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 5%

---


# `<join>` element  {#join--element}

## コンテンツモデル{#content-model-7}

join:==EMPTY

## 属性 {#attributes-7}

* @dstFilterExpr（文字列）
* @xpath-dst（文字列）
* @xpath-src（文字列）

## 親{#parents-7}

`<element>`

## 子 {#children-7}

なし

## 説明 {#description-7}

SQLテーブル間の結合を作成するフィールドを定義できます。

## 使用と使用のコンテキスト{#use-and-context-of-use-5}

`<join>`要素は、親`<element>`要素が「リンク」タイプの場合にのみ使用できます。 これは、親要素で「@type=link」属性が宣言されている必要があることを意味します。

`<join>`要素でリモートテーブルの名前と名前空間を指定する必要はありません。 親`<element>`で指定する必要があります。

規則に従って、リンクはスキーマの最後に定義されます。

リンクタイプ要素が定義されているときに`<join>`要素が指定されていない場合、リンクは両方のテーブルのプライマリキーに自動的に配置されます。

## 属性の説明{#attribute-description-7}

* **dstFilterExpr (string)**:この属性を使用すると、リモート・テーブルの有効な値の数を制限できます。
* **xpath-dst (string)**:この属性は、Xpath（リモートテーブルの@name属性）を受け取ります。
* **xpath-src（文字列）**:この属性は、Xpath(現在のスキーマの@name属性)を受け取ります。

## 例 {#examples-6}

現在のテーブルの「email」フィールドとリモートテーブルの「@compagny-id」フィールド間のリンク：

```
<join xpath-dst="@compagny-id" xpath-src="@email"/>
```

「@country」フィールドの内容（「EN」値を含む必要がある）に基づいて、「cus:Country」テーブルに向けてフィルターされたリンク。

```
<element name="StockEN" type="link" label="MyLink" target="cus:Stock">
   <join xpath-dst="@country" xpath-src="@code" dstFilterExpr="@country = 'EN'"/>
 </element>
```
