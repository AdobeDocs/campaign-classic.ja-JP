---
product: campaign
title: スキーマの要素と属性 – 結合要素
description: 要素を結合
feature: Schema Extension
exl-id: a7ca0300-d250-429c-8ae1-2ae7dee82cf5
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 2%

---

# 要素を結合 {#join--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-7}

結合：==空

## 属性 {#attributes-7}

* @dstFilterExpr （文字列）
* @xpath-dst （文字列）
* @xpath-src （文字列）

## 親 {#parents-7}

`<element>`

## 子 {#children-7}

なし

## 説明 {#description-7}

SQL テーブル間に結合を作成するフィールドを定義できます。

## 用途および使用コンテキスト {#use-and-context-of-use-5}

`<join>` 要素は、親 `<element>` 要素が「link」タイプの場合にのみ使用できます。 つまり、親要素には「@type=link」属性が宣言されている必要があります。

`<join>` 要素内のリモートテーブルの名前と名前空間を指定する必要はありません。 親 `<element>` で指定する必要があります。

慣例により、リンクはスキーマの最後に定義されます。

リンクタイプ要素の定義時に `<join>` 要素が指定されていない場合、リンクは両方のテーブルのプライマリキーに自動的に配置されます。

## 属性の説明 {#attribute-description-7}

* **dstFilterExpr （文字列）**：この属性を使用すると、リモートテーブル内の適格な値の数を制限できます。
* **xpath-dst （文字列）**：この属性は Xpath （リモートテーブルの@name 属性）を受け取ります。
* **xpath-src （string）**：この属性は、Xpath （現在のスキーマの@name 属性）を受け取ります。

## 例 {#examples-6}

現在のテーブルの「電子メール」フィールドとリモートテーブルの「@compagny-id」フィールド間のリンク：

```
<join xpath-dst="@compagny-id" xpath-src="@email"/>
```

「@country」フィールドのコンテンツに基づいて「cus:Country」テーブルへのリンクをフィルタリングしました。このフィールドには「EN」値を含める必要があります。

```
<element name="StockEN" type="link" label="MyLink" target="cus:Stock">
   <join xpath-dst="@country" xpath-src="@code" dstFilterExpr="@country = 'EN'"/>
 </element>
```
