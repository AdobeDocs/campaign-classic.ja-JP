---
product: campaign
title: 要素と属性 – 値要素
description: 要素と属性
feature: Schema Extension
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: bad7fb4b-43d9-4033-ae0d-cf191d89114b
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '148'
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

この要素を使用すると、列挙に格納された値を定義できます。

## 属性の説明 {#attribute-description-16}

* **applicableIf （string）**：この属性を使用すると、列挙値をオプションにすることができます。 XTK 式を受け取ります。
* **desc （string）**：列挙値の説明。
* **enabledIf （string）**：列挙値をアクティブ化するための条件。
* **img （string）**:「namespace:image_name」フォームの列挙にリンクされた画像。 画像をアプリケーションサーバーに読み込む必要があります。
* **label （string）**：定義済みリスト値のラベル。
* **name （string）**：定義済みリスト値の内部名。
* **value （string）**：定義済みリストの値。 値のタイプは、列挙のタイプに基づいて定義されます。 列挙が文字列タイプの場合、文字列タイプの値のみを含めることができます。

## 例 {#examples-13}

```
<enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>
```
