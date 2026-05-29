---
product: campaign
title: スキーマ要素と属性 – パラメーター要素
description: パラメーター要素
feature: Schema Extension
exl-id: d8960a2e-6900-4346-9f06-e7dd9d7b5139
TQID: https://experienceleague.adobe.com/fiMkJtGU90FP-G6BJhTnIrgBJ39uIJaakqKD49EhXS0
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 177
ht-degree: 12%

---

# パラメーター要素 {#param--element}


## コンテンツモデル {#content-model-12}

param:==help

## 属性 {#attributes-12}

* @_operation （文字列）
* @desc （文字列）
* @enum （文字列）
* @inout （文字列）
* @label （文字列）
* @localizable （文字列）
* @name （トークン）
* @namespace （トークン）
* @type （文字列）

## 親 {#parents-12}

`<parameters>`

## 子 {#children-12}

`<help>`

## 説明 {#description-12}

このエレメントでは、SOAP メソッドを呼び出すためのパラメーターを定義できます。

## 属性の説明 {#attribute-description-12}

* **desc （文字列）**: `<param>`要素に関する説明。
* **inout （文字列）**：この属性は、パラメーターがSOAP呼び出しの入力（in）または出力（out）のどちらに位置しているかを定義します。 この属性が指定されていない場合、デフォルトのパラメーターは入力（&quot;@inout=in&quot;）になります。
* **label （文字列）**: `<param>` ラベル
* **ローカライズ可能（文字列）**：この属性がアクティブ化されている場合、翻訳（内部使用）用に「@label」属性の値を回復するようにコレクションツールに指示します。
* **name （MNTOKEN）**: `<param>`の内部名
* **type （string）**：この属性は`<param>`要素の型を定義します

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

## 例 {#examples-9}

文字列タイプの「serviceName」インバウンド設定の定義：

```
<param desc="Name of the information service(s) (separated with commas)"
               name="serviceName" type="string" inout="in"/>
```
