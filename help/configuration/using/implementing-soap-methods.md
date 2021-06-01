---
product: campaign
title: SOAP メソッドの実装
description: SOAP メソッドの実装
audience: configuration
content-type: reference
topic-tags: api
exl-id: 441a0e5c-fa7f-46c8-a65a-5cca4c846d43
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 4%

---

# SOAP メソッドの実装{#implementing-soap-methods}

## はじめに {#introduction}

JavaScriptでSOAPメソッドを作成できます。 この関数は、単にアプリケーションプロセスを有効にするだけで、フォーム内でJSPを開発したり、JSPを呼び出したりするのを回避できます。

これらのSOAPメソッドは、アプリケーションでネイティブに定義されたメソッドと同じように動作します。 同じ属性がサポートされています。静的、キーのみ、および定数。

## メソッドライブラリ{#defining-a-method-library}の定義

メソッドライブラリの作成には、次の2つの段階があります。

* SOAPメソッド宣言
* JavaScriptでの定義（または実装）。

### 宣言 {#declaration}

最初に、スキーマでメソッドを宣言します（スキーマの作成および編集方法について詳しくは、[この節](../../configuration/using/about-schema-edition.md)を参照してください）。

この宣言は、ネイティブメソッドの宣言と似ていますが、定義が存在するメソッドライブラリの名前を指定する「library」属性を追加する必要がある点が異なります。

この名前は、「JavaScriptコード」タイプエンティティの名前（名前空間）と一致します。

例：

testLog(msg)メソッドは、 nms:recipient拡張で宣言します。

```
<method name="testLog" static="true" library="cus:test">
     <parameters>
       <param name="message" type="string" inout="in"/>
     </parameters>
   </method>
```

>[!NOTE]
>
>ライブラリに使用される名前空間と名前は、宣言が見つかる名前空間とスキーマ名とは独立しています。

### 定義 {#definition}

SOAPメソッドは、ライブラリを表すスクリプトにグループ化されたJavaScript関数の形式で実装されます。

>[!NOTE]
>
>メソッドライブラリは、様々なスキーマの関数をグループ化できます。また、その逆も可能です。1つのスキーマの関数は、別々のライブラリで定義できます。

スクリプトには、ライブラリの初回読み込み時に実行するコードを含めることができます。

**1.名前**

関数の名前は、次の形式に従う必要があります。

```
 <schema-namespace>_<schema-name>_<method-name>
```

例：

次のJavaScript関数は、上記のメソッドの実装です。 これは、「cus:test」名を使用して「JavaScriptコード」タイプエンティティで定義する必要があります。

```
function nms_recipient_testLog(message)
 {
   logInfo("*** " + message)
 }
```

**2.署名**

関数のシグネチャには、宣言の各&#39;in&#39;または&#39;inout&#39;パラメーターの引数を含める必要があります。

具体的なケース：

* **非静的メソッド**:関数には、まず、「xml」(E4X)型のオブジェクトの形式で渡されるXMLエンティティと一致する追加の引数を含める必要があります。
* **「キーのみ」タイプメソッド**:関数には、まず、文字列の形式で渡されたキーと一致する追加の引数を含める必要があります。

**3.戻り値**

この関数は、「out」型または「inout」型の各パラメーターの値を返す必要があります。 具体的なケース：メソッドが&#39;static&#39;、&#39;key only&#39;、または&#39;const&#39;属性を含めずに宣言されている場合、最初に返される値は変更されたエンティティと一致する必要があります。 新しいオブジェクトを返したり、最初に変更されたパラメータを返したりできます。

例：

```
function nms_recipient_setLastName(self, name)
 {
   self.@lastName = name
   return self
 }
```

複数の値が返される場合は、テーブルに表示する必要があります。

例：

```
function nms_recipient_getKey(self)
 {
   return [self.@firstName, self.@lastName]
 }
```
