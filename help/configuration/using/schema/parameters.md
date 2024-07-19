---
product: campaign
title: スキーマ要素と属性 – パラメーター要素
description: parameters 要素
feature: Schema Extension
exl-id: 54538c3e-3232-4bf7-a09c-dacf0f072be5
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '48'
ht-degree: 12%

---

# parameters 要素 {#parameters--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-13}

パラメータ：==param

## 属性 {#attributes-13}

なし

## 親 {#parents-13}

`<method>`

## 子 {#children-13}

`<param>`

## 説明 {#description-13}

この要素は、要素のグループ `<parameter>` 定義します。

## 用途および使用コンテキスト {#use-and-context-of-use-8}

`<method>` 要素の単一の `<param>` 子要素の場合でも、この要素は必須です。

## 属性の説明 {#attribute-description-13}

なし

## 例 {#examples-10}

```
<parameters
... //definition of one or more <param
</parameters>
```
