---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: fb0862f9-5dcc-49f2-b99b-9822aaf3a680
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 10%

---

# keyfield要素{#keyfield--element}

## コンテンツモデル{#content-model-9}

keyfield:==EMPTY

## 属性 {#attributes-9}

* @xlink (MNTOKEN)
* @xpath (MNTOKEN)

## 親{#parents-9}

`<key>`  ,  `<dbindex />`

## 子 {#children-9}

なし

## 説明 {#description-9}

この要素は、インデックスまたはキーに統合するフィールドを定義します。

## 属性の説明{#attribute-description-9}

* **xlink (MNTOKEN)**:では、リレーションテーブル（N-Nリンク）の結合で定義された外部キーを自動的に参照できます。
* **xpath (MNTOKEN)**:要素のインデックスまたはキーの `<attribute>`  定義。この属性は、キーまたはインデックスを定義するスキーマ属性へのパスを定義するXpathを受け取ります。

## 例 {#examples-}

「@name」のXpathを持つインデックス内の「sName」フィールドの選択：

```
<keyfield xpath="@name"/>
```
