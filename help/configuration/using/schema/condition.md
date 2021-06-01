---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: 71e98d45-3660-4d86-a5ca-8e55ae5896eb
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
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
* @expr (string)

## 親{#parents-2}

`<sysfilter>`

## 子 {#children-2}

なし

## 説明 {#description-2}

この要素では、フィルター条件を定義できます。

## {#use-and-context-of-use-2}の使用と使用のコンテキスト

1つの`<sysfiler>`要素に複数のフィルター条件を含めることができます。

## 属性の説明{#attribute-description-2}

* **boolOperator（文字列）**:複数のが同 `<conditions>` じ要素内で定義され  `<sysfilter>` ている場合、この属性を使用して結合できます。デフォルトでは、`<condition>`要素間の論理リンクは「AND」です。 「@boolOperator」属性を使用すると、「OR」と「AND」タイプのリンクを組み合わせることができます。
* **enabledIf（文字列）**:条件のアクティブ化テスト。
* **式（文字列）**:XTK式。

## 例 {#examples-2}

```
<sysfilter>
  <condition enabledIf="hasNamedRight('admin')=false" expr="@city=[currentOperator/location/@city]" />
</sysfilter>
```
