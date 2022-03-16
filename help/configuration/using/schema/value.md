---
product: campaign
title: 要素と属性 — 値要素
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: bad7fb4b-43d9-4033-ae0d-cf191d89114b
source-git-commit: 40da5774c8a6a228992c4aa400e2d9924215611e
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 4%

---

# 値要素 {#value--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-16}

値：==help

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

この要素を使用すると、列挙に保存された値を定義できます。

## 属性の説明 {#attribute-description-16}

* **applicableIf（文字列）**:この属性を使用すると、列挙値をオプションにできます。 XTK 式を受け取ります。
* **desc （文字列）**:列挙値の説明。
* **enabledIf (string)**:列挙値を有効化する条件。
* **img （文字列）**:画像は、「namespace:image_name」フォームの列挙にリンクされています。 イメージをアプリケーションサーバーにインポートする必要があります。
* **label （文字列）**:列挙値のラベル。
* **name（文字列）**:列挙値の内部名。
* **値（文字列）**:列挙値の値。 値のタイプは、列挙のタイプに基づいて定義されます。 列挙が文字列タイプの場合は、文字列タイプの値のみを含めることができます。

## 例 {#examples-13}

```
<enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>
```
