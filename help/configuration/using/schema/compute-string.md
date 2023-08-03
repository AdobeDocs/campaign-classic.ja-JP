---
product: campaign
title: 要素と属性 — 計算文字列要素
description: compute-string 要素
feature: Schema Extension
exl-id: 8a079bb8-3f53-4144-a065-5bd402649cc7
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 5%

---

# compute-string 要素 {#compute-string--element}

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

The `<compute-string>` element を使用すると、XTK 式に基づいて文字列を生成し、複数の値に基づいてインターフェイスに「built」ラベルを表示できます。

## 使用と使用のコンテキスト {#use-and-context-of-use-1}

いいえの場合 `<compute-string>` が定義されている場合、 `<compute-string>` 要素は、デフォルトで、スキーマのプライマリキーの値を使用して入力されます。

## 属性の説明 {#attribute-description-1}

* **expr（文字列）**:XTK および/または Xpath 式

## 例 {#examples-1}

```
<compute-string expr="@label + Iif(@code='','', ' (' + [folder/@label] + ')')"/>  
<compute-string expr="ToString([@centralCatalog-id]) + ',' + ToString([@localOrgUnit-id])" />
```

受信者に対して計算された文字列の結果：「John Doe (john.doe@aol.com)」:

```
<element name="recipient">
<compute-string expr="@lastName + ' ' + @firstName +' (' + @email + ')'
"/>
...
</element>
```
