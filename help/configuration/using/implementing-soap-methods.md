---
product: campaign
title: SOAP メソッドの実装
description: SOAP メソッドの実装
feature: Configuration
role: Developer
exl-id: 441a0e5c-fa7f-46c8-a65a-5cca4c846d43
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 4%

---

# SOAP メソッドの実装{#implementing-soap-methods}



## はじめに {#introduction}

JavaScriptでSOAP メソッドを作成できます。 この関数は、アプリケーションプロセスを有効にするだけで、JSPの開発とフォームでの呼び出しを回避できます。

これらのSOAP メソッドは、アプリケーションでネイティブに定義されているものと同じように動作します。 同じ属性がサポートされています。static、key only、constです。

## メソッドライブラリの定義 {#defining-a-method-library}

メソッドライブラリの作成には、次の2つの段階があります。

* SOAP方式の宣言，
* JavaScriptの定義（または実装）。

### 宣言 {#declaration}

最初に、スキーマ内のメソッドを宣言します（スキーマの作成および編集方法について詳しくは、[この節](../../configuration/using/about-schema-edition.md)を参照してください）。

その宣言はネイティブメソッドの宣言と似ていますが、定義が配置されているメソッドライブラリの名前を指定する「library」属性を追加する必要があります。

この名前は、「JavaScript Code」型エンティティの名前（名前空間）と一致します。

例：

testLog （msg） メソッドがnms:recipient拡張機能で宣言されています

```
<method name="testLog" static="true" library="cus:test">
     <parameters>
       <param name="message" type="string" inout="in"/>
     </parameters>
   </method>
```

>[!NOTE]
>
>ライブラリに使用される名前空間と名前は、宣言が見つかった名前空間とスキーマ名とは独立しています。

### 定義 {#definition}

SOAP メソッドは、ライブラリを表すスクリプトにグループ化されたJavaScript関数の形式で実装されます。

>[!NOTE]
>
>メソッドライブラリは、様々なスキーマの関数をグループ化できます。また、その逆も可能です。1つのスキーマの関数は、個別のライブラリで定義できます。

スクリプトには、最初のライブラリ読み込み中に実行されるコードを含めることができます。

**1. 名前**

関数の名前は、次の形式に準拠している必要があります。

```
 <schema-namespace>_<schema-name>_<method-name>
```

例：

以下のJavaScript関数は、上記のメソッドの実装です。 これは、「cus:test」名を使用して、「JavaScript コード」型エンティティで定義する必要があります。

```
function nms_recipient_testLog(message)
 {
   logInfo("*** " + message)
 }
```

**2. 署名**

関数の署名には、宣言の各「in」または「inout」パラメーターの引数を含める必要があります。

具体的な事例：

* **非静的メソッド**：関数には、最初に追加の引数を含める必要があります。これは、「xml」（E4X）型オブジェクトの形式で渡されるXML エンティティと一致します。
* **&quot;key only&quot; type methods**：関数には、最初に追加の引数を含める必要があり、文字列形式で渡されるキーと一致する必要があります。

**3. 返された値**

関数は、「out」または「inout」タイプの各パラメーターの値を返す必要があります。 特定のケース：メソッドが「static」、「key only」、「const」属性のいずれも指定せずに宣言されている場合、最初に返される値は変更されたエンティティと一致する必要があります。 新しいオブジェクトを返したり、最初に変更されたパラメーターを返したりできます。

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
