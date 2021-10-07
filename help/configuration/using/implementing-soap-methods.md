---
product: campaign
title: SOAP メソッドの実装
description: SOAP メソッドの実装
audience: configuration
content-type: reference
topic-tags: api
exl-id: 441a0e5c-fa7f-46c8-a65a-5cca4c846d43
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 4%

---

# SOAP メソッドの実装{#implementing-soap-methods}

![](../../assets/v7-only.svg)

## はじめに {#introduction}

JavaScript で SOAP メソッドを作成できます。 この関数は、単にアプリケーションプロセスを有効にするだけで、フォーム内で JSP を開発したり JSP を呼び出したりするのを避けることができます。

これらの SOAP メソッドは、アプリケーションでネイティブに定義されたメソッドと同じように動作します。 同じ属性がサポートされています。静的、キーのみ、および定数。

## メソッドライブラリの定義 {#defining-a-method-library}

メソッドライブラリの作成には、次の 2 つの段階があります。

* SOAP メソッドの宣言
* JavaScript での定義（または実装）。

### 宣言 {#declaration}

まず、スキーマでメソッドを宣言します（スキーマの作成および編集方法について詳しくは、[ この節 ](../../configuration/using/about-schema-edition.md) を参照してください）。

この宣言は、ネイティブメソッドの宣言と似ていますが、定義が存在するメソッドライブラリの名前を指定する&#39;library&#39;属性を追加する必要がある点が異なります。

この名前は、「JavaScript コード」タイプエンティティの名前（名前空間）と一致します。

例：

testLog(msg) メソッドは、 nms:recipient 拡張で宣言します。

```
<method name="testLog" static="true" library="cus:test">
     <parameters>
       <param name="message" type="string" inout="in"/>
     </parameters>
   </method>
```

>[!NOTE]
>
>ライブラリに使用する名前空間と名前は、宣言が見つかる名前空間とスキーマ名とは独立しています。

### 定義 {#definition}

SOAP メソッドは、ライブラリを表すスクリプトにグループ化された JavaScript 関数の形式で実装されます。

>[!NOTE]
>
>メソッドライブラリは、様々なスキーマの関数をグループ化したり、その逆をおこなうことができ、1 つのスキーマの関数を別々のライブラリで定義したりできます。

スクリプトには、ライブラリの初回読み込み時に実行するコードを含めることができます。

**1.名前**

関数の名前は、次の形式に従う必要があります。

```
 <schema-namespace>_<schema-name>_<method-name>
```

例：

次の JavaScript 関数は、上記のメソッドの実装です。 「cus:test」という名前を使用して、「JavaScript コード」タイプのエンティティで定義する必要があります。

```
function nms_recipient_testLog(message)
 {
   logInfo("*** " + message)
 }
```

**2.署名**

関数のシグネチャには、宣言の各&#39;in&#39;または&#39;inout&#39;パラメータの引数を含める必要があります。

具体的な事例：

* **非静的メソッド**:関数には、まず、「xml」(E4X) 型のオブジェクトの形式で渡される XML エンティティと一致する追加の引数を含める必要があります。
* **「キーのみ」タイプメソッド**:関数には、文字列の形式で渡されたキーと一致する、最初に追加の引数を含める必要があります。

**3.戻り値**

この関数は、各&#39;out&#39;型または&#39;inout&#39;型パラメータの値を返す必要があります。 具体的なケース：メソッドが&#39;static&#39;、&#39;key only&#39;、または&#39;const&#39;属性を含まずに宣言されている場合、最初に返される値は変更されたエンティティと一致する必要があります。 新しいオブジェクトを返したり、最初に変更されたパラメータを返すことができます。

例：

```
function nms_recipient_setLastName(self, name)
 {
   self.@lastName = name
   return self
 }
```

複数の値を返す場合は、テーブルに表示する必要があります。

例：

```
function nms_recipient_getKey(self)
 {
   return [self.@firstName, self.@lastName]
 }
```
