---
product: campaign
title: 要素と属性 – sysfilter 要素
description: 要素と属性
feature: Schema Extension
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: a0069688-fd05-42e9-91dd-adc10bea3461
source-git-commit: 254c89490fefa5d405bcecd2f1781df46450a873
workflow-type: tm+mt
source-wordcount: '45'
ht-degree: 17%

---

# sysfilter 要素 {#sysfilter--element}


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

@name 属性に対する条件を含むフィルターの定義：

```
<sysFilter>
      <condition expr="@name ='Doe'"/>
  <sysFilter>
```
