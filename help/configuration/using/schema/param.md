---
product: campaign
title: スキーマ要素と属性 — パラメーター要素
description: パラメーター要素
feature: Schema Extension
exl-id: d8960a2e-6900-4346-9f06-e7dd9d7b5139
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 9%

---

# パラメーター要素 {#param--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-12}

param:==help

## 属性 {#attributes-12}

* @_operation （文字列）
* @desc （文字列）
* @enum （文字列）
* @inout （文字列）
* @label （文字列）
* @localizable （文字列）
* @name (MNTOKEN)
* @namespace (MNTOKEN)
* @type （文字列）

## 親 {#parents-12}

`<parameters>`

## 子 {#children-12}

`<help>`

## 説明 {#description-12}

この要素を使用して、SOAP メソッドを呼び出すためのパラメーターを定義できます。

## 属性の説明 {#attribute-description-12}

* **desc （文字列）**：に関する説明 `<param>` 要素を選択します。
* **inout （文字列）**：この属性は、パラメーターが SOAP 呼び出しの入力 (in) または出力 (out) にあるかどうかを定義します。 この属性が指定されていない場合、デフォルトのパラメーターは入力されます (&quot;@inout=in&quot;)。
* **label （文字列）**: `<param>` ラベル
* **localizable（文字列）**：有効化されている場合、この属性は、翻訳の「@label」属性の値を復元するようコレクションツールに指示します（内部使用）。
* **名前 (MNTOKEN)**：の内部名 `<param>`
* **type (string)**：この属性は、 `<param>` 要素

  使用可能なタイプのリスト：

   * いずれか
   * bin
   * blob
   * ブール値
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

## 例 {#examples-9}

文字列タイプの「serviceName」受信設定の定義：

```
<param desc="Name of the information service(s) (separated with commas)"
               name="serviceName" type="string" inout="in"/>
```
