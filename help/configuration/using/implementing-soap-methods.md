---
title: SOAP メソッドの実装
seo-title: SOAP メソッドの実装
description: SOAP メソッドの実装
seo-description: null
page-status-flag: never-activated
uuid: c9366f4e-460d-4087-88f7-9cc6d0de597a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: api
discoiquuid: 76984d9d-7759-4e0f-a275-09cca27589fa
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# SOAP メソッドの実装{#implementing-soap-methods}

## はじめに {#introduction}

JavaScriptでSOAPメソッドを作成できます。 この関数は、アプリケーションプロセスを単に有効にするだけで、フォーム内でのJSPの開発と呼び出しを回避できます。

これらのSOAPメソッドは、アプリケーションでネイティブに定義されたメソッドと同じように動作します。 同じ属性がサポートされています。静的、キーのみ、定数

## メソッドライブラリの定義 {#defining-a-method-library}

メソッドライブラリの作成には、次の2つの段階があります。

* SOAPメソッド宣言、
* JavaScriptの定義（または実装）。

### 申告 {#declaration}

スキーマ内でメソッドを宣言することによる開始(スキーマの作成および編集方法の詳細については、 [この節を参照](../../configuration/using/about-schema-edition.md))。

この宣言はネイティブメソッドの宣言と似ていますが、定義が存在するメソッドライブラリの名前を指定する&#39;library&#39;属性を追加する必要がある点が異なります。

この名前は、「JavaScriptコード」型エンティティの名前(名前空間付き)と一致します。

例：

testLog(msg)メソッドは、nms:受信者拡張子で宣言されています

```
<method name="testLog" static="true" library="cus:test">
     <parameters>
       <param name="message" type="string" inout="in"/>
     </parameters>
   </method>
```

>[!NOTE]
>
>ライブラリに使用される名前空間と名前は、宣言が見つかった名前空間とスキーマの名前とは独立しています。

### 定義 {#definition}

SOAPメソッドは、JavaScript関数の形式で実装され、ライブラリを表すスクリプトにグループ化されています。

>[!NOTE]
>
>メソッドライブラリは、様々なスキーマの関数をグループ化したり、その逆をグループ化したりできます。1つのスキーマの関数は、別々のライブラリに定義できます。

スクリプトには、初回のライブラリの読み込み中に実行するコードを含めることができます。

**1.名前**

関数の名前は、次の形式に従う必要があります。

```
 <schema-namespace>_<schema-name>_<method-name>
```

例：

次のJavaScript関数は、上記のメソッドの実装です。 この変数は、&#39;cus:test&#39;という名前を使用して&#39;JavaScriptコード&#39;型エンティティで定義する必要があります。

```
function nms_recipient_testLog(message)
 {
   logInfo("*** " + message)
 }
```

**2.署名**

関数のシグネチャには、宣言の各&#39;in&#39;または&#39;inout&#39;パラメータに対する引数を含める必要があります。

具体的なケース：

* **非静的メソッド**:この関数には、最初に、&#39;xml&#39;(E4X)型のオブジェクトの形式で渡されるXMLエンティティと一致する追加の引数を含める必要があります。
* **&quot;key only&quot;型のメソッド**:この関数には、最初に、文字列の形式で渡されるキーと一致する追加の引数を含める必要があります。

**3.戻り値**

この関数は、&#39;out&#39;型または&#39;inout&#39;型の各パラメーターの値を返す必要があります。 具体的なケース：メソッドが&#39;static&#39;、&#39;key only&#39;、または&#39;const&#39;属性なしで宣言されている場合、最初の戻り値は変更されたエンティティと一致する必要があります。 新しいオブジェクトを返したり、最初に変更されたパラメータを返したりできます。

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

