---
product: campaign
title: スキーマ要素と属性 – メソッド要素
description: メソッド要素
feature: Schema Extension
exl-id: 0fb74318-fe09-473c-8e33-1f3afd66b4cc
TQID: https://experienceleague.adobe.com/GaT6bmWzojcbk8-XjCoqrMv2-02aoxv1cIXM0E0Y0UU
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 207
ht-degree: 1%

---

# メソッド要素 {#method--element}


## コンテンツモデル {#content-model-10}

メソッド：==（help | parameters）

## 属性 {#attributes-10}

* @_operation （文字列）
* @access （文字列）
* @const （ブール値）
* @hidden （ブール値）
* @label （文字列）
* @library （文字列）
* @name （トークン）
* @pkonly （ブール値）
* @static （ブール値）

## 親 {#parents-10}

`<methods>`  ,  `<interface />`

## 子 {#children-10}

* `<help>`
* `<parameters>`

## 説明 {#description-10}

このエレメントでは、SOAP メソッドを定義できます。

## 用途と使用状況 {#use-and-context-of-use-7}

SOAP メソッドを使用すると、アプリケーションプロセスが有効になります。

新しいメソッドを宣言するには、「@library」が必要です（非ネイティブ）。ライブラリに使用される名前空間と名前は、宣言が存在するスキーマの名前空間と名前とは独立しています。

## 属性の説明 {#attribute-description-10}

* **アクセス （文字列）**：この属性は、メソッドを使用するためのアクセス制御を定義します。 この属性が見つからない場合は、識別が必須です。 使用可能な値は、「anonymous」、「admin」、「sql」です。
* **const （boolean）**：アクティブ化されている場合、この属性は、宣言されたメソッドがエンティティを変更することを意味します
* **label （文字列）**: メソッドのラベル。
* **ライブラリ （文字列）**：このメソッドはアプリケーションにネイティブではありません。 この属性は、メソッド定義が見つかったメソッドライブラリの値を取ります（nms:mylibrary.js）。
* **name （MNTOKEN）**：一意のメソッド名。
* **静的（ブール値）**：この属性がアクティブ化されている場合、メソッドは自律的であると見なされ、呼び出されるときにすべてのパラメーターをメソッドに指定する必要があります。

## 例 {#examples-7}

標準装備の「購読」メソッドの定義：

```
 
<method name="Subscribe" static="true">
      <help>Creation of update of a recipient's subscription to an information service</help>
      <parameters>
        <param desc="Name of the information service(s) (separated with commas)"
               name="serviceName" type="string"/>
        <param desc="Recipient to subscribe and possibly create" name="recipient"
               type="DOMElement"/>
        <param desc="Create the recipient if they don't exist" name="create" type="boolean"/>
      </parameters>     
    </method>
```
