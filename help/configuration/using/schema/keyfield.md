---
product: campaign
title: スキーマ要素と属性
description: キーフィールド要素
exl-id: fb0862f9-5dcc-49f2-b99b-9822aaf3a680
source-git-commit: 56459b188ee966cdb578c415fcdfa485dcbed355
workflow-type: tm+mt
source-wordcount: '101'
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

* **xlink (MNTOKEN)**:では、リレーションテーブル（N-N リンク）の結合で定義された外部キーを自動的に参照できます。
* **xpath (MNTOKEN)**:インデックスまたはキーの定義 `<attribute>`  要素。 この属性は、キーまたはインデックスを定義する schema 属性へのパスを定義する Xpath を受け取ります。

## 例 {#examples-}

「@name」の Xpath を持つインデックス内の「sName」フィールドの選択：

```
<keyfield xpath="@name"/>
```
