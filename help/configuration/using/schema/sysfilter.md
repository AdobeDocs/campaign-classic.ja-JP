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
source-wordcount: '42'
ht-degree: 26%

---


# `<sysfilter>` element  {#sysfilter--element}

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
