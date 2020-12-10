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
source-wordcount: '46'
ht-degree: 26%

---


# `<help>` element  {#help--element}

## コンテンツモデル{#content-model-6}

help:=EMPTY

## 属性 {#attributes-6}

なし

## 親{#parents-6}

`<srcschema>`  ,   `<element>`   ,    `<attribute>`    ,     `<enumeration>`     ,      `<value>`      ,      `<param />`,       `<method />`

## 子 {#children-6}

なし

## 説明 {#description-6}

この要素では、`<element>`または`<attribute>`   エレメント。 テキストのみを含めることができ、データベースのXMLに保存されます。

## 属性の説明{#attribute-description-6}

この要素には属性がありません。

## 例 {#examples-5}

```
<method name="CheckOperation" static="true"
      <helpchecks the validity of a campaign</help
...
</method> 
```
