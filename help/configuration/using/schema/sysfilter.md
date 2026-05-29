---
product: campaign
title: 要素と属性 – sysfilter要素
description: 要素と属性
feature: Schema Extension
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: a0069688-fd05-42e9-91dd-adc10bea3461
TQID: https://experienceleague.adobe.com/hjsD-JSGBPnwyj1IsLDo-tUy-63apy0-6kT9vngaaQk
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 45
ht-degree: 17%

---

# sysfilter要素 {#sysfilter--element}


## コンテンツモデル {#content-model-15}

sysFilter:==condition

## 属性 {#attributes-15}

なし

## 親 {#parents-15}

`<element>`

## 子 {#children-15}

`<condition>`

## 説明 {#description-15}

この要素を使用すると、フィルターを定義できます。

## 属性の説明 {#attribute-description-15}

この要素には属性がありません。

## 例 {#examples-12}

@name属性上の条件を持つフィルターの定義：

```
<sysFilter>
      <condition expr="@name ='Doe'"/>
  <sysFilter>
```
