---
solution: Campaign Classic
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
translation-type: tm+mt
source-git-commit: 1818bd2aeb60689b2ce0e59cb0bd157f000de513
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 11%

---


# `<param>` element  {#param--element}

## コンテンツモデル{#content-model-12}

param:==help

## 属性 {#attributes-12}

* @_operation（文字列）
* @desc （文字列）
* @enum （文字列）
* @inout （文字列）
* @label（文字列）
* @localizable (string)
* @name (MNTOKEN)
* @名前空間(MNTOKEN)
* @type (string)

## 親{#parents-12}

`<parameters>`

## 子 {#children-12}

`<help>`

## 説明 {#description-12}

この要素では、SOAPメソッドを呼び出すためのパラメーターを定義できます。

## 属性の説明{#attribute-description-12}

* **desc（文字列）**: `<param>` 要素に関する説明。
* **inout (string)**:この属性は、SOAP呼び出しの入力(in)または出力(out)にパラメーターが存在するかどうかを定義します。この属性を指定しない場合、デフォルトのパラメーターは入力(「@inout=in」)になります。
* **label (string)**: `<param>` label
* **localizable (string)**:この属性がアクティブ化されている場合、収集ツールに対して翻訳用の「@label」属性の値を復元するよう指示します（内部使用）。
* **name (MNTOKEN)**:内部名  `<param>`
* **type (string)**:この属性は、 `<param>` 要素のタイプを定義します

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

## 例 {#examples-9}

文字列タイプの&quot;serviceName&quot;受信設定の定義：

```
<param desc="Name of the information service(s) (separated with commas)"
               name="serviceName" type="string" inout="in"/>
```
