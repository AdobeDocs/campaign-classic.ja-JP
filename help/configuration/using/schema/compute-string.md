---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: 8a079bb8-3f53-4144-a065-5bd402649cc7
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 12%

---

# 計算文字列要素{#compute-string--element}

## コンテンツモデル{#content-model-1}

compute-string:==EMPTY

## 属性 {#attributes-1}

@expr

## 親{#parents-1}

`<element>`

## 子 {#children-1}

なし

## 説明 {#description-1}

`<compute-string>`要素を使用して、XTK式に基づいて文字列を生成し、複数の値に基づいてインターフェイスに「built」ラベルを表示できます。

## {#use-and-context-of-use-1}の使用と使用のコンテキスト

`<compute-string>`が定義されていない場合、デフォルトでは、スキーマ内のプライマリキーの値を持つ`<compute-string>`要素が入力されます。

## 属性の説明{#attribute-description-1}

* **式（文字列）**:XTKやXpathの式

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
