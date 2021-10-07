---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: d8960a2e-6900-4346-9f06-e7dd9d7b5139
source-git-commit: 34404fbe935e68f3cc11d937839209443ad4ca60
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 11%

---

# param 要素 {#param--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-12}

param:==help

## 属性 {#attributes-12}

* @_operation (string)
* @desc (string)
* @enum (string)
* @inout (string)
* @label (string)
* @localizable (string)
* @name (MNTOKEN)
* @namespace (MNTOKEN)
* @type (string)

## 親 {#parents-12}

`<parameters>`

## 子 {#children-12}

`<help>`

## 説明 {#description-12}

この要素を使用して、SOAP メソッドを呼び出すためのパラメーターを定義できます。

## 属性の説明 {#attribute-description-12}

* **desc （文字列）**:要素に関する説 `<param>` 明。
* **inout （文字列）**:この属性は、パラメーターが SOAP 呼び出しの入力 (in) または出力 (out) にあるかどうかを定義します。この属性を指定しない場合、デフォルトのパラメーターは入力 (「@inout=in」) です。
* **label （文字列）**: `<param>` label
* **ローカライズ可能（文字列）**:この属性が有効な場合、この属性は、翻訳（内部使用）の「@label」属性の値を復元するように収集ツールに指示します。
* **名前 (MNTOKEN)**:内部名  `<param>`
* **型（文字列）**:この属性は、要素のタイプを定義し `<param>` ます

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

## 例 {#examples-9}

文字列タイプの「serviceName」受信設定の定義：

```
<param desc="Name of the information service(s) (separated with commas)"
               name="serviceName" type="string" inout="in"/>
```
