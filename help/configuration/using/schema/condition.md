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
source-wordcount: '93'
ht-degree: 11%

---


# 条件要素{#condition--element}

## コンテンツモデル{#content-model-2}

条件：==EMPTY

## 属性 {#attributes-2}

* @boolOperator (string)
* @enabledIf (string)
* @expr（文字列）

## 親{#parents-2}

`<sysfilter>`

## 子 {#children-2}

なし

## 説明 {#description-2}

この要素を使用して、フィルター条件を定義できます。

## 使用と使用のコンテキスト{#use-and-context-of-use-2}

1つの`<sysfiler>`要素に複数のフィルター条件を含めることができます。

## 属性の説明{#attribute-description-2}

* **boolOperator (string)**:複数 `<conditions>` が同じ  `<sysfilter>` 要素内で定義されている場合、この属性を使用すると、それらを組み合わせることができます。デフォルトでは、論理リンクは`<condition>`要素間の「AND」です。 「@boolOperator」属性を使用すると、「OR」と「AND」タイプのリンクを組み合わせることができます。
* **enabledIf (string)**:条件アクティベーションテスト。
* **expr（文字列）**:XTK式。

## 例 {#examples-2}

```
<sysfilter>
  <condition enabledIf="hasNamedRight('admin')=false" expr="@city=[currentOperator/location/@city]" />
</sysfilter>
```
