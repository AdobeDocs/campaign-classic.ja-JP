---
solution: Campaign Classic
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
translation-type: tm+mt
source-git-commit: 922257b157f8d76d6e703b0510ff689d1aa4d067
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

この要素を使用して、フィルターを定義できます。

## 属性の説明{#attribute-description-15}

この要素には属性がありません。

## 例 {#examples-12}

@name属性の条件を含むフィルターの定義：

```
<sysFilter>
      <condition expr="@name ='Doe'"/>
  <sysFilter>
```
