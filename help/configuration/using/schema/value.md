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
source-wordcount: '146'
ht-degree: 6%

---


# `<value>` element  {#value--element}

## コンテンツモデル{#content-model-16}

value:==help

## 属性 {#attributes-16}

* @applicableIf (string)
* @desc （文字列）
* @enabledIf (string)
* @img (string)
* @label（文字列）
* @name（文字列）
* @value（文字列）

## 親{#parents-16}

`<enumeration>`

## 子 {#children-16}

`<help>`

## 説明 {#description-16}

この要素を使用すると、定義済みリストに保存される値を定義できます。

## 属性の説明{#attribute-description-16}

* **applicableIf (string)**:この属性を使用すると、定義済みリスト値をオプションにできます。XTK式を受け取ります。
* **desc（文字列）**:定義済みリスト値の説明。
* **enabledIf (string)**:定義済みリスト値をアクティブ化する条件を指定します。
* **img （文字列）**:画像が「名前空間:image_name」フォームの定義済みリストにリンクされている。画像をアプリケーションサーバーに読み込む必要があります。
* **label (string)**:定義済みリスト値のラベル。
* **name（文字列）**:定義済みリスト値の内部名。
* **value（文字列）**:定義済みリスト値の値。値のタイプは、定義済みリストのタイプに基づいて定義されます。 定義済みリストが文字列型の場合、文字列型の値のみを含めることができます。

## 例 {#examples-13}

```
<enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>
```
