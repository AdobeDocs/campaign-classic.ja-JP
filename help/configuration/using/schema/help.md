---
product: campaign
title: スキーマ要素と属性 – ヘルプ要素
description: ヘルプ要素
feature: Schema Extension
exl-id: 8207868c-25ff-4ca9-afdd-41b324c7ac0d
TQID: 'https://experienceleague.adobe.com/R-Oa0H6l19qOU9KamHyVFrOWqBOw9uB2ISm2OYdQDrM'
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
source-wordcount: '56'
ht-degree: 23%
---
# ヘルプ要素 {#help--element}


## コンテンツモデル {#content-model-6}

help:==EMPTY

## 属性 {#attributes-6}

なし

## 親 {#parents-6}

`<srcschema>`  ,  `<element>`   ,   `<attribute>`    ,    `<enumeration>`     ,     `<value>`      ,     `<param />`,      `<method />`

## 子 {#children-6}

なし

## 説明 {#description-6}

この要素を使用すると、`<element>`または`<attribute>`要素を記述できます。 テキストのみを含めることができ、データベース内のXMLに保存されます。

## 属性の説明 {#attribute-description-6}

この要素には属性がありません。

## 例 {#examples-5}

```
<method name="CheckOperation" static="true"
      <helpchecks the validity of a campaign</help
...
</method> 
```
