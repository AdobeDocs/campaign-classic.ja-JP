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

`<key>`  ,   `<dbindex />`

## 子 {#children-9}

なし

## 説明 {#description-9}

この要素は、インデックスまたはキーに統合するフィールドを定義します。

## 属性の説明{#attribute-description-9}

* **xlink (MNTOKEN)**:リレーションテーブル（N-Nリンク）のジョインで定義された外部キーを自動的に参照できます。
* **xpath (MNTOKEN)**: `<attribute>`  要素のインデックスまたはキーの定義。この属性は、キーまたはインデックスを定義するスキーマ属性へのパスを定義するXpathを受け取ります。

## 例 {#examples-}

「@name」上のXpathを持つインデックス内の「sName」フィールドの選択：

```
<keyfield xpath="@name"/>
```
