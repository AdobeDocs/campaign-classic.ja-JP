---
product: campaign
title: 要素と属性 – 値要素
description: 要素と属性
feature: Schema Extension
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: bad7fb4b-43d9-4033-ae0d-cf191d89114b
TQID: 'https://experienceleague.adobe.com/rGaA--VHVGxCBHX5SgZUQQ9AwMgOTYWqMYGpYWU4-WY'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
    internal-label: Schemas
subfeature_v2:
  - id: a72a22e0-8c8d-4019-ba42-3f2644aa91a3
    internal-label: Schema extension
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%
---
# 値要素 {#value--element}


## コンテンツモデル {#content-model-16}

value:==help

## 属性 {#attributes-16}

* @applicableIf （文字列）
* @desc （文字列）
* @enabledIf （文字列）
* @img （文字列）
* @label （文字列）
* @name （文字列）
* @value （文字列）

## 親 {#parents-16}

`<enumeration>`

## 子 {#children-16}

`<help>`

## 説明 {#description-16}

この要素では、列挙に格納される値を定義できます。

## 属性の説明 {#attribute-description-16}

* **applicableIf （文字列）**：この属性を使用すると、列挙値をオプションにできます。 XTK式を受け取ります。
* **desc （文字列）**：列挙値の説明。
* **enabledIf （文字列）**：列挙値をアクティブ化するための条件。
* **img （文字列）**: 「名前空間:image_name」フォームの列挙にリンクされた画像。 画像はアプリケーションサーバーに読み込む必要があります。
* **label （文字列）**：列挙値のラベル。
* **name （文字列）**：列挙値の内部名。
* **値（文字列）**：列挙値の値。 値のタイプは、列挙のタイプに基づいて定義されます。 列挙が文字列型の場合、文字列型の値のみを含めることができます。

## 例 {#examples-13}

```
<enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>
```
