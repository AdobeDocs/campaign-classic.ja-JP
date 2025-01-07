---
product: campaign
title: スキーマの要素と属性 – キーフィールド要素
description: keyfield 要素
feature: Schema Extension
exl-id: fb0862f9-5dcc-49f2-b99b-9822aaf3a680
source-git-commit: 254c89490fefa5d405bcecd2f1781df46450a873
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 4%

---

# keyfield 要素 {#keyfield--element}


## コンテンツモデル {#content-model-9}

keyfield:==EMPTY

## 属性 {#attributes-9}

* @xlink （MNTOKEN）
* @xpath （MNTOKEN）

## 親 {#parents-9}

`<key>`, `<dbindex />`

## 子 {#children-9}

なし

## 説明 {#description-9}

この要素は、インデックスまたはキーに統合するフィールドを定義します。

## 属性の説明 {#attribute-description-9}

* **xlink （MNTOKEN）**：リレーションテーブル（N-N リンク）の結合で定義された外部キーを自動的に参照します。
* **xpath （MNTOKEN）**:`<attribute>` 要素上のインデックスまたはキーの定義。 この属性は、キーまたはインデックスを定義するスキーマ属性へのパスを定義する Xpath を受け取ります。

## 例 {#examples-}

「@name」に Xpath を含むインデックスの「sName」フィールドの選択：

```
<keyfield xpath="@name"/>
```
