---
product: campaign
title: 要素と属性 – compute-string要素
description: compute-string要素
feature: Schema Extension
exl-id: 8a079bb8-3f53-4144-a065-5bd402649cc7
TQID: https://experienceleague.adobe.com/vLSA9oDdBg-0sElc6QlusY-YviNyRU8Fq6yXRrFrN1g
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 95
ht-degree: 5%

---

# compute-string要素 {#compute-string--element}


## コンテンツモデル {#content-model-1}

compute-string:==EMPTY

## 属性 {#attributes-1}

@expr

## 親 {#parents-1}

`<element>`

## 子 {#children-1}

なし

## 説明 {#description-1}

`<compute-string>`要素を使用すると、XTK式に基づいて文字列を生成し、複数の値に基づいてインターフェイスに「ビルドされた」ラベルを表示できます。

## 用途と使用状況 {#use-and-context-of-use-1}

`<compute-string>`が定義されていない場合、デフォルトでは`<compute-string>`要素がスキーマのプライマリキーの値で入力されます。

## 属性の説明 {#attribute-description-1}

* **expr （string）**: XTKまたはXpath式

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
