---
product: campaign
title: 要素と属性 – 文字列計算要素
description: 計算文字列要素
feature: Schema Extension
exl-id: 8a079bb8-3f53-4144-a065-5bd402649cc7
source-git-commit: 254c89490fefa5d405bcecd2f1781df46450a873
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 5%

---

# 計算文字列要素 {#compute-string--element}


## コンテンツモデル {#content-model-1}

compute-string:==EMPTY

## 属性 {#attributes-1}

@expr

## 親 {#parents-1}

`<element>`

## 子 {#children-1}

なし

## 説明 {#description-1}

`<compute-string>` 要素を使用すると、XTK 式に基づいて文字列を生成し、複数の値に基づいて「ビルド」ラベルをインターフェイスに表示できます。

## 用途および使用コンテキスト {#use-and-context-of-use-1}

`<compute-string>` が定義されていない場合、デフォルトでは、スキーマのプライマリキーの値を使用して `<compute-string>` 要素が入力されます。

## 属性の説明 {#attribute-description-1}

* **expr （文字列）**:XTK や Xpath 式

## 例 {#examples-1}

```
<compute-string expr="@label + Iif(@code='','', ' (' + [folder/@label] + ')')"/>  
<compute-string expr="ToString([@centralCatalog-id]) + ',' + ToString([@localOrgUnit-id])" />
```

受信者で計算された文字列の結果：「John Doe （john.doe@aol.com）」:

```
<element name="recipient">
<compute-string expr="@lastName + ' ' + @firstName +' (' + @email + ')'
"/>
...
</element>
```
