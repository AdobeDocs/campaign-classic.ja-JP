---
product: campaign
title: スキーマ要素と属性 – パラメーター要素
description: パラメーター要素
feature: Schema Extension
exl-id: 54538c3e-3232-4bf7-a09c-dacf0f072be5
TQID: 'https://experienceleague.adobe.com/tZyI-rIbEifWdgcO80ni6lSHinH0IEeM8UrHFAUpnFs'
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
source-wordcount: '48'
ht-degree: 12%
---
# パラメーター要素 {#parameters--element}


## コンテンツモデル {#content-model-13}

パラメータ：==param

## 属性 {#attributes-13}

なし

## 親 {#parents-13}

`<method>`

## 子 {#children-13}

`<param>`

## 説明 {#description-13}

この要素は、`<parameter>`要素のグループを定義します。

## 用途と使用状況 {#use-and-context-of-use-8}

この要素は、`<method>`要素の1つの`<param>`子要素に対しても必須です。

## 属性の説明 {#attribute-description-13}

なし

## 例 {#examples-10}

```
<parameters
... //definition of one or more <param
</parameters>
```
