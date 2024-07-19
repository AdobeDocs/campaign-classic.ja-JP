---
product: campaign
title: スキーマ要素と属性 – 列挙要素
description: 定義済みリスト要素
feature: Schema Extension
exl-id: 4cd67278-2623-4508-9a9f-9007c6a5f8ac
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 8%

---

# 定義済みリスト要素 {#enumeration--element}

![](../../../assets/v7-only.svg)

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

この要素を使用すると、値の列挙を定義できます。 列挙は、定義済みのスキーマに属していますが、別のスキーマを介してアクセスできます。

## 用途および使用コンテキスト {#use-and-context-of-use-4}

定義済みリストは、スキーマの開始時（メイン要素が定義される前）に定義されます。

## 属性の説明 {#attribute-description-5}

* **basetype （string）**：定義済みリストに格納される値のタイプ。

  使用可能なタイプのリスト：

   * いずれか
   * bin
   * blob
   * ブール値
   * バイト
   * CDATA
   * 日時
   * datetimetz
   * datetimenoz
   * 日付
   * DOMDocument
   * DOMElement
   * 倍精度浮動小数点数
   * 列挙
   * 浮動小数点数
   * html
   * int64
   * リンク
   * 長い
   * メモ
   * MNTOKEN
   * 割合
   * primarykey
   * 短い
   * 文字列
   * 時間
   * 期間
   * uuid

* **default （string）**：デフォルト値。 デフォルト値は、定義済みリストで定義されている値の 1 つである場合もあります。
* **desc （string）**：列挙の説明。
* **label （string）**：列挙ラベル。
* **name （string）**：定義済みリストの内部名。
* **template （文字列）**：この属性は、複数のスキーマで共有される `<enumeration>` 要素への参照を定義します。 定義は、現在のスキーマに自動的にコピーされます。

## 例 {#examples-4}

値がデータベースに格納される列挙値の例：

```
    <enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>

    <element label="Sample" name="Sample">
       <attribute dbEnum="myEnum" length="100" name="Number" required="true" type="string"/>
    </element>
```

デフォルト値を持つ定義済みリストの定義：

```
 <enumeration basetype="byte" default="email" name="canal">
    <value label="Email" name="email" value="0"/> 
    <value label="Téléphone" name="phone" value="1"/>
    <value label="Call Center" name="callcenter" value="2"/>
 </enumeration>
```
