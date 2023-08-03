---
product: campaign
title: スキーマ要素と属性 — キーフィールド要素
description: キーフィールド要素
feature: Schema Extension
exl-id: fb0862f9-5dcc-49f2-b99b-9822aaf3a680
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 4%

---

# キーフィールド要素 {#keyfield--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-9}

keyfield:==EMPTY

## 属性 {#attributes-9}

* @xlink (MNTOKEN)
* @xpath (MNTOKEN)

## 親 {#parents-9}

`<key>`  ,  `<dbindex />`

## 子 {#children-9}

なし

## 説明 {#description-9}

この要素は、インデックスまたはキーに統合するフィールドを定義します。

## 属性の説明 {#attribute-description-9}

* **xlink (MNTOKEN)**：リレーションテーブル（N-N リンク）の結合で定義された外部キーを自動的に参照できます。
* **xpath (MNTOKEN)**：インデックスまたはキーの定義 ( `<attribute>`  要素を選択します。 この属性は、キーまたはインデックスを定義する schema 属性へのパスを定義する Xpath を受け取ります。

## 例 {#examples-}

「@name」の Xpath を持つインデックス内の「sName」フィールドの選択：

```
<keyfield xpath="@name"/>
```
