---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: a0069688-fd05-42e9-91dd-adc10bea3461
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 25%

---

# sysfilter要素{#sysfilter--element}

## コンテンツモデル{#content-model-15}

sysFilter:==condition

## 属性 {#attributes-15}

なし

## 親{#parents-15}

`<element>`

## 子 {#children-15}

`<condition>`

## 説明 {#description-15}

この要素では、フィルターを定義できます。

## 属性の説明{#attribute-description-15}

この要素には属性がありません。

## 例 {#examples-12}

@name属性の条件を持つフィルターの定義：

```
<sysFilter>
      <condition expr="@name ='Doe'"/>
  <sysFilter>
```
