---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: a7ca0300-d250-429c-8ae1-2ae7dee82cf5
source-git-commit: 34404fbe935e68f3cc11d937839209443ad4ca60
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 5%

---

# 結合要素 {#join--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-7}

join:==EMPTY

## 属性 {#attributes-7}

* @dstFilterExpr (string)
* @xpath-dst (string)
* @xpath-src (string)

## 親 {#parents-7}

`<element>`

## 子 {#children-7}

なし

## 説明 {#description-7}

SQL テーブル間の結合を作成するフィールドを定義できます。

## 使用と使用のコンテキスト {#use-and-context-of-use-5}

`<join>` 要素は、親の `<element>` 要素が「link」タイプの場合にのみ使用できます。 つまり、親要素には「@type=link」属性を宣言する必要があります。

`<join>` 要素でリモート・テーブルの名前と名前空間を指定する必要はありません。 親 `<element>` で指定する必要があります。

慣例により、リンクはスキーマの最後に定義されます。

リンクタイプ要素の定義時に `<join>` 要素が指定されていない場合、リンクは両方のテーブルのプライマリキーに自動的に配置されます。

## 属性の説明 {#attribute-description-7}

* **dstFilterExpr（文字列）**:この属性を使用すると、リモート・テーブルの有効な値の数を制限できます。
* **xpath-dst（文字列）**:この属性は Xpath( リモート・テーブルの@name属性 ) を受け取る。
* **xpath-src（文字列）**:この属性は Xpath を受け取ります ( 現在のスキーマの@name属性 )。

## 例 {#examples-6}

現在のテーブルの「email」フィールドとリモートテーブルの「@compagny-id」フィールド間のリンク：

```
<join xpath-dst="@compagny-id" xpath-src="@email"/>
```

「EN」値を含む「@country」フィールドの内容に基づいて、「cus:Country」テーブルに対するフィルターされたリンク：

```
<element name="StockEN" type="link" label="MyLink" target="cus:Stock">
   <join xpath-dst="@country" xpath-src="@code" dstFilterExpr="@country = 'EN'"/>
 </element>
```
