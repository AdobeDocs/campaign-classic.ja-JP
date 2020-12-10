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
source-wordcount: '204'
ht-degree: 4%

---


# `<method>` element  {#method--element}

## コンテンツモデル{#content-model-10}

method:==( help) |パラメーター)

## 属性 {#attributes-10}

* @_operation（文字列）
* @access (string)
* @const (boolean)
* @hidden（ブール値）
* @label（文字列）
* @library (string)
* @name (MNTOKEN)
* @pkonly (boolean)
* @static（ブール値）

## 親{#parents-10}

`<methods>`  ,   `<interface />`

## 子 {#children-10}

* `<help>`
* `<parameters>`

## 説明 {#description-10}

この要素を使用して、SOAPメソッドを定義できます。

## 使用と使用のコンテキスト{#use-and-context-of-use-7}

SOAPメソッドを使用すると、アプリケーションプロセスが有効になります。

「@library」は、新しいメソッド（非ネイティブ）を宣言するために必要です。ライブラリに使用される名前空間と名前は、宣言が含まれるスキーマの名前空間と名前とは独立しています。

## 属性の説明{#attribute-description-10}

* **access (string)**:この属性は、メソッドを使用するアクセス制御を定義します。この属性がない場合は、識別は必須です。 次の値を指定できます。&#39;anonymous&#39;、&#39;admin&#39;、および&#39;sql&#39;。
* **const(boolean)**:この属性がアクティブ化された場合、宣言されたメソッドがエンティティを変更することを意味します
* **label (string)**:メソッドのラベル。
* **library (string)**:このメソッドは、アプリケーションに固有のメソッドではありません。この属性は、メソッド定義が見つかったメソッドライブラリの値を取ります(nms:mylibrary.js)。
* **name (MNTOKEN)**:一意のメソッド名。
* **static (boolean)**:この属性が有効になっている場合、メソッドは自律型であると見なされ、呼び出し時にメソッドにすべてのパラメーターを指定する必要があります。

## 例 {#examples-7}

初期設定の「購読」メソッドの定義：

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
