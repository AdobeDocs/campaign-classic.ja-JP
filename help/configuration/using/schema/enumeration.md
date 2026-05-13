---
product: campaign
title: スキーマ要素と属性 – 列挙要素
description: 列挙要素
feature: Schema Extension
exl-id: 4cd67278-2623-4508-9a9f-9007c6a5f8ac
TQID: https://experienceleague.adobe.com/w8b-2HEtYRMOd9yHFLtvS0vS2tdLDzuIakLfrqImsGo
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 198
ht-degree: 11%

---

# 列挙要素 {#enumeration--element}


## コンテンツモデル {#content-model-5}

列挙：==（help| value）

## 属性 {#attributes-5}

* @basetype （文字列）
* @default （文字列）
* @desc （文字列）
* @label （文字列）
* @name （文字列）
* @template （文字列）

## 親 {#parents-5}

`<srcschema>`

## 子 {#children-5}

* `<help>`
* `<value>`

## 説明 {#description-5}

この要素を使用すると、値の列挙を定義できます。 列挙は、定義されているスキーマに属していますが、別のスキーマからアクセスできます。

## 用途と使用状況 {#use-and-context-of-use-4}

列挙は、スキーマの開始時（メイン要素が定義される前）に定義されます。

## 属性の説明 {#attribute-description-5}

* **basetype （文字列）**：列挙に保存されている値のタイプ。

  使用可能なタイプのリスト：

   * いずれか
   * bin
   * blob
   * ブール値
   * バイト
   * CDATA
   * 日時
   * datetime
   * datetimenotz
   * 日付
   * DOMDocument
   * DOMElement
   * 倍精度浮動小数点数
   * 列挙
   * 浮動小数点数
   * html
   * int64
   * リンク
   * 長整数
   * メモ
   * MN トークン
   * パーセント
   * primarykey
   * 短い
   * 文字列
   * 時間
   * 期間
   * uuid

* **default （string）**: Default value. デフォルト値は、列挙で定義された値のいずれかである場合もあります。
* **desc （string）**：列挙の説明。
* **label （文字列）**：列挙ラベル。
* **name （文字列）**：列挙の内部名。
* **テンプレート（文字列）**：この属性は、複数のスキーマで共有されている`<enumeration>`要素への参照を定義します。 定義は現在のスキーマに自動的にコピーされます。

## 例 {#examples-4}

値がデータベースに保存されている列挙値の例：

```
    <enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>

    <element label="Sample" name="Sample">
       <attribute dbEnum="myEnum" length="100" name="Number" required="true" type="string"/>
    </element>
```

デフォルト値を持つ列挙の定義：

```
 <enumeration basetype="byte" default="email" name="canal">
    <value label="Email" name="email" value="0"/> 
    <value label="Téléphone" name="phone" value="1"/>
    <value label="Call Center" name="callcenter" value="2"/>
 </enumeration>
```
