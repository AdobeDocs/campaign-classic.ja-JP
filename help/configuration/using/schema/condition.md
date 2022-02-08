---
product: campaign
title: スキーマ要素と属性
description: 条件要素
exl-id: 71e98d45-3660-4d86-a5ca-8e55ae5896eb
source-git-commit: 56459b188ee966cdb578c415fcdfa485dcbed355
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 5%

---

# 条件要素 {#condition--element}

![](../../../assets/v7-only.svg)

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

この要素では、フィルター条件を定義できます。

## 使用と使用のコンテキスト {#use-and-context-of-use-2}

1 `<sysfiler>`  要素には、複数のフィルター条件を含めることができます。

## 属性の説明 {#attribute-description-2}

* **boolOperator（文字列）**:複数の `<conditions>` が同じ  `<sysfilter>` 要素を使用すると、この属性を組み合わせることができます。 デフォルトでは、論理リンクは次の間にあります。 `<condition>` 要素は「AND」です。 「@boolOperator」属性を使用して、「OR」と「AND」タイプのリンクを組み合わせることができます。
* **enabledIf (string)**:条件のアクティベーションテスト。
* **expr（文字列）**:XTK 式。

## 例 {#examples-2}

```
<sysfilter>
  <condition enabledIf="hasNamedRight('admin')=false" expr="@city=[currentOperator/location/@city]" />
</sysfilter>
```
