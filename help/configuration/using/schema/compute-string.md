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

`<compute-string>`要素を使用すると、XTK式に基づく文字列を生成し、いくつかの値に基づいて「組み込み」ラベルをインターフェイスに表示できます。

## 使用と使用のコンテキスト{#use-and-context-of-use-1}

`<compute-string>`が定義されていない場合、デフォルトでは、スキーマの主キーの値を使用して`<compute-string>`要素が入力されます。

## 属性の説明{#attribute-description-1}

* **expr（文字列）**:XTKやXpathの式

## 例 {#examples-1}

```
<compute-string expr="@label + Iif(@code='','', ' (' + [folder/@label] + ')')"/>  
<compute-string expr="ToString([@centralCatalog-id]) + ',' + ToString([@localOrgUnit-id])" />
```

受信者で計算された文字列の結果：&quot;John Doe (john.doe@aol.com)&quot;:

```
<element name="recipient">
<compute-string expr="@lastName + ' ' + @firstName +' (' + @email + ')'
"/>
...
</element>
```
