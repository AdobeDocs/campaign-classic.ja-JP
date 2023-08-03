---
product: campaign
title: スキーマ要素と属性 — メソッド要素
description: メソッド要素
feature: Schema Extension
exl-id: 0fb74318-fe09-473c-8e33-1f3afd66b4cc
source-git-commit: fd5e4bbc87a48f029a09b14ab1d927b9afe4ac52
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# メソッド要素 {#method--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-10}

method:==( help |パラメーター )

## 属性 {#attributes-10}

* @_operation （文字列）
* @access （文字列）
* @const (boolean)
* @hidden (boolean)
* @label （文字列）
* @library （文字列）
* @name (MNTOKEN)
* @pkonly (boolean)
* @static (boolean)

## 親 {#parents-10}

`<methods>`  ,  `<interface />`

## 子 {#children-10}

* `<help>`
* `<parameters>`

## 説明 {#description-10}

この要素を使用して、SOAP メソッドを定義できます。

## 使用と使用のコンテキスト {#use-and-context-of-use-7}

SOAP メソッドを使用すると、アプリケーションプロセスが有効になります。

新しいメソッド（非ネイティブ）を宣言するには、「@library」が必要です。ライブラリに使用される名前空間と名前は、宣言が存在するスキーマの名前空間と名前とは独立しています。

## 属性の説明 {#attribute-description-10}

* **access (string)**：この属性は、メソッドを使用するためのアクセス制御を定義します。 この属性がない場合は、識別が必須です。 使用できる値は「匿名」、「管理者」、「SQL」です。
* **const (boolean)**：有効化されている場合、この属性は、宣言されたメソッドによってエンティティが変更されることを意味します
* **label （文字列）**：メソッドのラベル。
* **ライブラリ（文字列）**：このメソッドは、アプリケーションのネイティブではありません。 この属性は、メソッド定義が見つかったメソッドライブラリの値を取ります (nms:mylibrary.js)。
* **名前 (MNTOKEN)**：一意のメソッド名。
* **static（ブール値）**：この属性が有効になっている場合、メソッドは autonomous と見なされ、呼び出し時に、すべてのパラメーターをメソッドに指定する必要があります。

## 例 {#examples-7}

標準提供の「購読」メソッドの定義：

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
