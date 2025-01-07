---
product: campaign
title: スキーマ要素と属性 – 条件要素
description: 条件要素
feature: Schema Extension
exl-id: 71e98d45-3660-4d86-a5ca-8e55ae5896eb
source-git-commit: 254c89490fefa5d405bcecd2f1781df46450a873
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 5%

---

# 条件要素 {#condition--element}


## コンテンツモデル {#content-model-2}

条件：==EMPTY

## 属性 {#attributes-2}

* @boolOperator （文字列）
* @enabledIf （文字列）
* @expr （文字列）

## 親 {#parents-2}

`<sysfilter>`

## 子 {#children-2}

なし

## 説明 {#description-2}

この要素を使用すると、フィルター条件を定義できます。

## 用途および使用コンテキスト {#use-and-context-of-use-2}

1 つの `<sysfiler>` 要素に、複数のフィルター条件を含めることができます。

## 属性の説明 {#attribute-description-2}

* **boolOperator （文字列）**：同じ `<sysfilter>` 要素内で複数の `<conditions>` が定義されている場合、この属性を使用してそれらを組み合わせることができます。 デフォルトでは、`<condition>` 要素間の論理リンクは「AND」です。 「@boolOperator」属性を使用すると、「OR」タイプと「AND」タイプのリンクを組み合わせることができます。
* **enabledIf （string）**：条件のアクティベーションテスト。
* **expr （string）**:XTK 式。

## 例 {#examples-2}

```
<sysfilter>
  <condition enabledIf="hasNamedRight('admin')=false" expr="@city=[currentOperator/location/@city]" />
</sysfilter>
```
