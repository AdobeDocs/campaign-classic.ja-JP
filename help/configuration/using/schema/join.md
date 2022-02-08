---
product: campaign
title: スキーマ要素と属性
description: 結合要素
exl-id: a7ca0300-d250-429c-8ae1-2ae7dee82cf5
source-git-commit: 56459b188ee966cdb578c415fcdfa485dcbed355
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 2%

---

# 結合要素 {#join--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-7}

join:==EMPTY

## 属性 {#attributes-7}

* @dstFilterExpr （文字列）
* @xpath-dst （文字列）
* @xpath-src （文字列）

## 親 {#parents-7}

`<element>`

## 子 {#children-7}

なし

## 説明 {#description-7}

SQL テーブル間で結合を作成するフィールドを定義できます。

## 使用と使用のコンテキスト {#use-and-context-of-use-5}

A `<join>`  要素は親の場合にのみ使用できます  `<element>`  要素のタイプが「リンク」です。 つまり、親要素には「@type=link」属性を宣言する必要があります。

リモートテーブルの名前と名前空間を `<join>`  要素。 親で指定する必要があります  `<element>`.

慣例により、リンクはスキーマの末尾で定義されます。

この `<join>` 要素が指定されていない場合、リンクは自動的に両方のテーブルのプライマリキーに配置されます。

## 属性の説明 {#attribute-description-7}

* **dstFilterExpr (string)**:この属性を使用すると、リモートテーブルの有効な値の数を制限できます。
* **xpath-dst （文字列）**:この属性は Xpath ( リモートテーブルの@name属性 ) を受け取ります。
* **xpath-src (string)**:この属性は Xpath( 現在のスキーマの@name属性 ) を受け取ります。

## 例 {#examples-6}

現在のテーブルの「email」フィールドとリモートテーブルの「@compagny-id」フィールド間のリンク：

```
<join xpath-dst="@compagny-id" xpath-src="@email"/>
```

「EN」値を含む「@country」フィールドの内容に基づいて、「cus:Country」テーブルに対するフィルターされたリンク。

```
<element name="StockEN" type="link" label="MyLink" target="cus:Stock">
   <join xpath-dst="@country" xpath-src="@code" dstFilterExpr="@country = 'EN'"/>
 </element>
```
