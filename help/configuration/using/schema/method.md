---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: 0fb74318-fe09-473c-8e33-1f3afd66b4cc
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 4%

---

# メソッド要素{#method--element}

## コンテンツモデル{#content-model-10}

method:==( help |パラメーター)

## 属性 {#attributes-10}

* @_operation (string)
* @access (string)
* @const (boolean)
* @hidden (boolean)
* @label (string)
* @library (string)
* @name (MNTOKEN)
* @pkonly (boolean)
* @static (boolean)

## 親{#parents-10}

`<methods>`  ,  `<interface />`

## 子 {#children-10}

* `<help>`
* `<parameters>`

## 説明 {#description-10}

この要素を使用して、SOAPメソッドを定義できます。

## {#use-and-context-of-use-7}の使用と使用のコンテキスト

SOAPメソッドを使用すると、アプリケーションプロセスが有効になります。

新しいメソッド（非ネイティブ）を宣言するには、「@library」が必要です。ライブラリに使用される名前空間と名前は、宣言が含まれるスキーマの名前空間と名前とは独立しています。

## 属性の説明{#attribute-description-10}

* **アクセス（文字列）**:この属性は、メソッドを使用するためのアクセス制御を定義します。この属性がない場合は、識別が必須です。 使用できる値は次のとおりです。「anonymous」、「admin」、「sql」。
* **const (boolean)**:有効になっている場合、この属性は宣言されたメソッドによってエンティティが変更されることを意味します。
* **label（文字列）**:メソッドのラベル。
* **ライブラリ（文字列）**:このメソッドは、アプリケーションにネイティブではありません。この属性は、メソッド定義が見つかったメソッドライブラリの値を取ります(nms:mylibrary.js)。
* **名前(MNTOKEN)**:一意のメソッド名。
* **static (boolean)**:この属性が有効になっている場合、メソッドは自律型と見なされ、呼び出される際に、すべてのパラメータをメソッドに指定する必要があります。

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
