---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: 8a079bb8-3f53-4144-a065-5bd402649cc7
source-git-commit: 34404fbe935e68f3cc11d937839209443ad4ca60
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 12%

---

# 計算文字列要素 {#compute-string--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-1}

compute-string:==EMPTY

## 属性 {#attributes-1}

@expr

## 親 {#parents-1}

`<element>`

## 子 {#children-1}

なし

## 説明 {#description-1}

`<compute-string>` 要素を使用すると、XTK 式に基づいて文字列を生成し、複数の値に基づいて「built」ラベルをインターフェイスに表示できます。

## 使用と使用のコンテキスト {#use-and-context-of-use-1}

`<compute-string>` が定義されていない場合は、デフォルトで `<compute-string>` 要素が入力され、スキーマのプライマリキーの値が設定されます。

## 属性の説明 {#attribute-description-1}

* **expr（文字列）**:XTK や Xpath の式

## 例 {#examples-1}

```
<compute-string expr="@label + Iif(@code='','', ' (' + [folder/@label] + ')')"/>  
<compute-string expr="ToString([@centralCatalog-id]) + ',' + ToString([@localOrgUnit-id])" />
```

受信者に対して計算された文字列の結果：&quot;John Doe (john.doe@aol.com)&quot;:

```
<element name="recipient">
<compute-string expr="@lastName + ' ' + @firstName +' (' + @email + ')'
"/>
...
</element>
```
