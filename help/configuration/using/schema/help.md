---
product: campaign
title: スキーマ要素と属性
description: ヘルプ要素
exl-id: 8207868c-25ff-4ca9-afdd-41b324c7ac0d
source-git-commit: 56459b188ee966cdb578c415fcdfa485dcbed355
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 12%

---

# ヘルプ要素 {#help--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-6}

help:==EMPTY

## 属性 {#attributes-6}

なし

## 親 {#parents-6}

`<srcschema>`  ,  `<element>`   ,   `<attribute>`    ,    `<enumeration>`     ,     `<value>`      ,     `<param />`,      `<method />`

## 子 {#children-6}

なし

## 説明 {#description-6}

この要素では、 `<element>`  または  `<attribute>`   要素。 テキストのみを含めることができ、XML 形式でデータベースに格納されます。

## 属性の説明 {#attribute-description-6}

この要素には属性がありません。

## 例 {#examples-5}

```
<method name="CheckOperation" static="true"
      <helpchecks the validity of a campaign</help
...
</method> 
```
