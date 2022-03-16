---
product: campaign
title: スキーマ要素と属性 — キーフィールド要素
description: キーフィールド要素
exl-id: fb0862f9-5dcc-49f2-b99b-9822aaf3a680
source-git-commit: 40da5774c8a6a228992c4aa400e2d9924215611e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 4%

---

# キーフィールド要素 {#keyfield--element}

![](../../../assets/v7-only.svg)

## Content model {#content-model-9}

keyfield:==EMPTY

## 属性 {#attributes-9}

* @xlink (MNTOKEN)
* @xpath (MNTOKEN)

## 親 {#parents-9}

`<key>`  ,  `<dbindex />`

## 子 {#children-9}

なし

## 説明 {#description-9}

この要素は、インデックスまたはキーに統合するフィールドを定義します。

## 属性の説明 {#attribute-description-9}

* **xlink (MNTOKEN)**: lets you automatically reference foreign keys defined in the join for a relation table (N-N link).
* **xpath (MNTOKEN)**: definition of an index or a key on an `<attribute>`  element. This attribute receives an Xpath which defines the path to the schema attribute that defines the key or the index.

## 例 {#examples-}

Selection of the &quot;sName&quot; field in an index with an Xpath on &quot;@name&quot;:

```
<keyfield xpath="@name"/>
```
