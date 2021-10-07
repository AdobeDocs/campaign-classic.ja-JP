---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: 4cd67278-2623-4508-9a9f-9007c6a5f8ac
source-git-commit: 34404fbe935e68f3cc11d937839209443ad4ca60
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 10%

---

# 列挙要素 {#enumeration--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-5}

列挙：==(help| value)

## 属性 {#attributes-5}

* @basetype (string)
* @default (string)
* @desc (string)
* @label (string)
* @name (string)
* @template (string)

## 親 {#parents-5}

`<srcschema>`

## 子 {#children-5}

* `<help>`
* `<value>`

## 説明 {#description-5}

この要素を使用して、値の列挙を定義できます。 列挙は、定義されているスキーマに属していますが、別のスキーマからアクセスできます。

## 使用と使用のコンテキスト {#use-and-context-of-use-4}

列挙は、スキーマの開始時（メイン要素の定義前）に定義されます。

## 属性の説明 {#attribute-description-5}

* **basetype （文字列）**:列挙に保存される値のタイプ。

   使用可能なタイプのリスト：

   * いずれか
   * bin
   * blob
   * boolean
   * バイト
   * CDATA
   * 日時
   * datetimetz
   * datetimenotz
   * date
   * DOMDocument
   * DOMElement
   * 重複
   * enum
   * float
   * html
   * int64
   * リンク
   * 長い
   * メモ
   * MNTOKEN
   * percent
   * primarykey
   * short
   * 文字列
   * 時間
   * 間隔
   * uuid

* **デフォルト（文字列）**:デフォルト値。デフォルト値は、列挙で定義された値の 1 つでもかまいません。
* **desc （文字列）**:列挙の説明。
* **label （文字列）**:列挙ラベル
* **名前（文字列）**:列挙の内部名。
* **template （文字列）**:この属性は、複数のスキーマで共有さ `<enumeration>` れる要素への参照を定義します。定義は、現在のスキーマに自動的にコピーされます。

## 例 {#examples-4}

データベースに値が格納される列挙値の例：

```
    <enumeration name="myEnum">
       <value name="One" value="1"/>
       <value name="Two" value="2"/>
    </enumeration>

    <element label="Sample" name="Sample">
       <attribute dbEnum="myEnum" length="100" name="Number" required="true" type="string"/>
    </element>
```

デフォルト値の列挙の定義：

```
 <enumeration basetype="byte" default="email" name="canal">
    <value label="Email" name="email" value="0"/> 
    <value label="Téléphone" name="phone" value="1"/>
    <value label="Call Center" name="callcenter" value="2"/>
 </enumeration>
```
