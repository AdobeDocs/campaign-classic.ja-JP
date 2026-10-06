---
product: campaign
title: スキーマ要素と属性 – キーフィールド要素
description: keyfield要素
feature: Schema Extension
exl-id: fb0862f9-5dcc-49f2-b99b-9822aaf3a680
TQID: 'https://experienceleague.adobe.com/tVWLlgg97dREZZHvUW81FhDVhS-uNvUHlbhH0YBrAdY'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
    internal-label: Schemas
subfeature_v2:
  - id: a72a22e0-8c8d-4019-ba42-3f2644aa91a3
    internal-label: Schema extension
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 6%
---
# keyfield要素 {#keyfield--element}


## コンテンツモデル {#content-model-9}

keyfield:==EMPTY

## 属性 {#attributes-9}

* @xlink （トークン）
* @xpath （トークン）

## 親 {#parents-9}

`<key>`  ,  `<dbindex />`

## 子 {#children-9}

なし

## 説明 {#description-9}

この要素は、インデックスまたはキーに統合するフィールドを定義します。

## 属性の説明 {#attribute-description-9}

* **xlink （MNTOKEN）**：関係テーブル （N-N リンク）の結合で定義された外部キーを自動的に参照できます。
* **xpath （MNTOKEN）**: `<attribute>`要素のインデックスまたはキーの定義。 この属性は、キーまたはインデックスを定義するスキーマ属性へのパスを定義するXpathを受け取ります。

## 例 {#examples-}

「@name」にXpathが設定されたインデックスの「sName」フィールドの選択：

```
<keyfield xpath="@name"/>
```
