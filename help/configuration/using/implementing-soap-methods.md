---
product: campaign
title: SOAP メソッドの実装
description: SOAP メソッドの実装
feature: Configuration
role: Data Engineer, Developer
exl-id: 441a0e5c-fa7f-46c8-a65a-5cca4c846d43
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 4%

---

# SOAP メソッドの実装{#implementing-soap-methods}



## はじめに {#introduction}

JavaScriptでSOAP メソッドを作成できます。 この関数は単純にアプリケーションプロセスを有効にするので、JSP の開発とフォームでの呼び出しを回避できます。

これらのSOAP メソッドは、アプリケーションでネイティブに定義されたものと同じように動作します。 静的、キーのみ、const の同じ属性がサポートされています。

## メソッドライブラリの定義 {#defining-a-method-library}

メソッドライブラリの作成には、次の 2 つの段階があります。

* SOAP メソッド宣言。
* JavaScriptの定義（または実装）。

### 宣言 {#declaration}

まず、スキーマのメソッドを宣言します（スキーマの作成および編集方法について詳しくは、[&#x200B; この節 &#x200B;](../../configuration/using/about-schema-edition.md)）を参照してください。

これらの宣言はネイティブメソッドの宣言に似ていますが、定義が配置されているメソッドライブラリの名前を指定する「library」属性を追加する必要がある点が異なります。

この名前は、「JavaScriptコード」タイプのエンティティの名前（名前空間を含む）と一致します。

例：

testLog （msg） メソッドは、nms:recipient 拡張機能で宣言されます

```
<method name="testLog" static="true" library="cus:test">
     <parameters>
       <param name="message" type="string" inout="in"/>
     </parameters>
   </method>
```

>[!NOTE]
>
>ライブラリに使用される名前空間と名前は、宣言がある名前空間とスキーマ名とは独立しています。

### 定義 {#definition}

SOAP メソッドは、ライブラリを表すスクリプトでグループ化されたJavaScript関数の形式で実装されます。

>[!NOTE]
>
>メソッドライブラリは様々なスキーマの関数をグループ化できます。逆も同様です。1 つのスキーマの関数を別のライブラリで定義することもできます。

スクリプトには、ライブラリの初期読み込み時に実行するコードを含めることができます。

**1.名前**

関数の名前は、次の形式に従う必要があります。

```
 <schema-namespace>_<schema-name>_<method-name>
```

例：

次のJavaScript関数は、上記のメソッドの実装です。 「cus:test」という名前を使用して、「JavaScript コード」タイプエンティティで定義する必要があります。

```
function nms_recipient_testLog(message)
 {
   logInfo("*** " + message)
 }
```

**2.署名**

関数のシグネチャには、宣言の各「in」または「inout」パラメーターに対する引数を含める必要があります。

具体的な状況：

* **非静的メソッド**：関数は、「xml」（E4X）タイプのオブジェクトの形式で渡される XML エンティティと一致する、追加の引数を最初に含める必要があります。
* **&quot;key only&quot; type methods**：関数には、文字列形式で渡されたキーと一致する追加の引数を最初に含める必要があります。

**3.戻り値**

関数は、「out」または「inout」タイプの各パラメーターの値を返す必要があります。 特定のケース：「static」、「key only」、「const」のいずれかの属性を持たずにメソッドが宣言された場合、最初に返される値は、変更されたエンティティの値と一致する必要があります。 新しいオブジェクトを返すことも、最初に変更されたパラメーターを返すこともできます。

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
