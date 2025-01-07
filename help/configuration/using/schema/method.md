---
product: campaign
title: スキーマ要素と属性 – メソッド要素
description: メソッド要素
feature: Schema Extension
exl-id: 0fb74318-fe09-473c-8e33-1f3afd66b4cc
source-git-commit: 254c89490fefa5d405bcecd2f1781df46450a873
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# メソッド要素 {#method--element}


## コンテンツモデル {#content-model-10}

メソッド：==（help | パラメーター）

## 属性 {#attributes-10}

* @_operation （文字列）
* @access （文字列）
* @const （ブール値）
* @hidden （ブール値）
* @label （文字列）
* @library （文字列）
* @name （MNTOKEN）
* @pkonly （ブール値）
* @static （ブール値）

## 親 {#parents-10}

`<methods>`, `<interface />`

## 子 {#children-10}

* `<help>`
* `<parameters>`

## 説明 {#description-10}

この要素を使用すると、SOAP メソッドを定義できます。

## 用途および使用コンテキスト {#use-and-context-of-use-7}

SOAP メソッドを使用すると、アプリケーションプロセスを実行できます。

「@library」は、新しいメソッド（ネイティブ以外）を宣言するために必要です。ライブラリに使用される名前空間と名前は、宣言があるスキーマの名前空間と名前とは独立しています。

## 属性の説明 {#attribute-description-10}

* **access （string）**：この属性は、メソッドを使用するためのアクセス制御を定義します。 この属性がない場合、識別は必須です。 使用できる値は、「anonymous」、「admin」、「sql」です。
* **const （boolean）**：有効な場合、この属性は、宣言されたメソッドがエンティティを変更することを意味します
* **label （string）**: メソッドのラベル。
* **library （string）**：このメソッドは、アプリケーションにネイティブではありません。 この属性は、メソッド定義が見つかったメソッドライブラリの値を取得します（nms:mylibrary.js）。
* **name （MNTOKEN）**：一意のメソッド名。
* **static （boolean）**：この属性が有効な場合、メソッドは自律的であると見なされ、呼び出し時にすべてのパラメーターをメソッドに指定する必要があります。

## 例 {#examples-7}

デフォルトの「購読」メソッドの定義：

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
