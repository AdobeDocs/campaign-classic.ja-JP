---
product: campaign
title: スキーマ要素と属性 – 条件要素
description: 条件要素
feature: Schema Extension
exl-id: 71e98d45-3660-4d86-a5ca-8e55ae5896eb
TQID: https://experienceleague.adobe.com/Jx8bLCt1UEqAZDm0cSuexx25js-e5xTsvkeSMzVCUHw
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 95
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

この要素では、フィルタリング条件を定義できます。

## 用途と使用状況 {#use-and-context-of-use-2}

1つの`<sysfiler>`要素に複数のフィルター条件を含めることができます。

## 属性の説明 {#attribute-description-2}

* **boolOperator （string）**：同じ`<sysfilter>`要素内で複数の`<conditions>`が定義されている場合、この属性を使用すると、それらを組み合わせることができます。 デフォルトでは、論理リンクは`<condition>`要素の間にある「AND」です。 「@boolOperator」属性を使用すると、「OR」と「AND」タイプのリンクを組み合わせることができます。
* **enabledIf （文字列）**：条件のアクティベーション テスト。
* **expr （文字列）**: XTK式。

## 例 {#examples-2}

```
<sysfilter>
  <condition enabledIf="hasNamedRight('admin')=false" expr="@city=[currentOperator/location/@city]" />
</sysfilter>
```
