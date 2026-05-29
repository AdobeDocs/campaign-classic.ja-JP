---
product: campaign
title: スキーマ要素と属性 – ヘルプ要素
description: ヘルプ要素
feature: Schema Extension
exl-id: 8207868c-25ff-4ca9-afdd-41b324c7ac0d
TQID: https://experienceleague.adobe.com/R-Oa0H6l19qOU9KamHyVFrOWqBOw9uB2ISm2OYdQDrM
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 49
ht-degree: 12%

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
