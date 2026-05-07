---
product: campaign
title: スキーマ要素と属性 – 結合要素
description: 結合要素
feature: Schema Extension
exl-id: a7ca0300-d250-429c-8ae1-2ae7dee82cf5
source-git-commit: 254c89490fefa5d405bcecd2f1781df46450a873
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 2%

---

# 結合要素 {#join--element}


## コンテンツモデル {#content-model-7}

結合：==EMPTY

## 属性 {#attributes-7}

* @dstFilterExpr （文字列）
* @xpath-dst （文字列）
* @xpath-src （文字列）

## 親 {#parents-7}

`<element>`

## 子 {#children-7}

なし

## 説明 {#description-7}

SQL テーブル間の結合を作成するフィールドを定義できます。

## 用途と使用状況 {#use-and-context-of-use-5}

`<join>`要素は、親`<element>`要素が「link」タイプの場合にのみ使用できます。 つまり、親エレメントには「@type=link」属性を宣言する必要があります。

`<join>`要素でリモートテーブルの名前と名前空間を指定する必要はありません。 親`<element>`で指定する必要があります。

規則によって、リンクはスキーマの最後に定義されます。

リンクタイプ要素が定義されているときに`<join>`要素が指定されていない場合、リンクは両方のテーブルのプライマリキーに自動的に配置されます。

## 属性の説明 {#attribute-description-7}

* **dstFilterExpr （文字列）**：この属性を使用すると、リモート テーブル内の適格な値の数を制限できます。
* **xpath-dst （文字列）**：この属性はXpath （リモートテーブルの@name属性）を受け取ります。
* **xpath-src （文字列）**：この属性はXpath （現在のスキーマの@name属性）を受け取ります。

## 例 {#examples-6}

現在のテーブルの「email」フィールドとリモートテーブルの「@compagny-id」フィールドの間のリンク：

```
<join xpath-dst="@compagny-id" xpath-src="@email"/>
```

「EN」値を含める必要がある「@country」フィールドの内容に基づいて、「cus:Country」テーブルへのリンクをフィルタリングしました。

```
<element name="StockEN" type="link" label="MyLink" target="cus:Stock">
   <join xpath-dst="@country" xpath-src="@code" dstFilterExpr="@country = 'EN'"/>
 </element>
```
