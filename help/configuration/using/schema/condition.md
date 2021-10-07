---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: 71e98d45-3660-4d86-a5ca-8e55ae5896eb
source-git-commit: 34404fbe935e68f3cc11d937839209443ad4ca60
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 11%

---

# 条件要素 {#condition--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-2}

条件：==EMPTY

## 属性 {#attributes-2}

* @boolOperator (string)
* @enabledIf (string)
* @expr (string)

## 親 {#parents-2}

`<sysfilter>`

## 子 {#children-2}

なし

## 説明 {#description-2}

この要素では、フィルター条件を定義できます。

## 使用と使用のコンテキスト {#use-and-context-of-use-2}

1 つの `<sysfiler>` 要素に複数のフィルター条件を含めることができます。

## 属性の説明 {#attribute-description-2}

* **boolOperator（文字列）**:同じ要素内 `<conditions>` で複数が定義されて  `<sysfilter>` いる場合、この属性を使用してそれらを組み合わせることができます。デフォルトでは、論理リンクは `<condition>` 要素間は「AND」です。 「@boolOperator」属性を使用すると、「OR」と「AND」タイプのリンクを組み合わせることができます。
* **enabledIf (string)**:条件のアクティベーションテスト。
* **expr（文字列）**:XTK 式。

## 例 {#examples-2}

```
<sysfilter>
  <condition enabledIf="hasNamedRight('admin')=false" expr="@city=[currentOperator/location/@city]" />
</sysfilter>
```
