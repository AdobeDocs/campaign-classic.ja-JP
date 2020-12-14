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
source-wordcount: '196'
ht-degree: 10%

---


# 定義済みリスト要素{#enumeration--element}

## コンテンツモデル{#content-model-5}

定義済みリスト:==(help| value)

## 属性 {#attributes-5}

* @basetype（文字列）
* @default（文字列）
* @desc （文字列）
* @label（文字列）
* @name（文字列）
* @template (string)

## 親{#parents-5}

`<srcschema>`

## 子 {#children-5}

* `<help>`
* `<value>`

## 説明 {#description-5}

この要素を使用して、値の定義済みリストを定義できます。 定義済みリストは、で定義されているスキーマに属していますが、別のスキーマを介してアクセスできます。

## 使用と使用のコンテキスト{#use-and-context-of-use-4}

定義済みリストは、スキーマの開始時（メイン要素が定義される前）に定義されます。

## 属性の説明{#attribute-description-5}

* **basetype (string)**:定義済みリストに格納される値のタイプ。

   使用可能なタイプのリスト:

   * いずれか
   * bin
   * blob
   * boolean
   * バイト
   * CDATA
   * datetime
   * datetimetz
   * datetimenotz
   * 日付
   * DOMDocument
   * DOMElement
   * 重複
   * 列挙
   * float
   * html
   * int64
   * link
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

* **default（文字列）**:デフォルト値。デフォルト値は、定義済みリストで定義されている値の1つでもかまいません。
* **desc（文字列）**:定義済みリストの説明。
* **label (string)**:定義済みリストラベル
* **name（文字列）**:定義済みリストの内部名。
* **template (string)**:この属性は、複数のスキーマが共有する `<enumeration>` 要素への参照を定義します。定義は自動的に現在のスキーマにコピーされます。

## 例 {#examples-4}

データベースに値が格納される定義済みリスト値の例：

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
