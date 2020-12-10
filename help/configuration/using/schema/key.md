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
source-wordcount: '316'
ht-degree: 3%

---


# `<key>` element  {#key--element}

## コンテンツモデル{#content-model-8}

key:==keyfield

## 属性 {#attributes-8}

* @allowEmptyPart (boolean)
* @applicableIf (string)
* @internal (boolean)
* @label（文字列）
* @name (MNTOKEN)
* @noDbIndex (boolean)

## 親{#parents-8}

`<element>`

## 子 {#children-8}

`<keyfield>`

## 説明 {#description-8}

この要素では、テーブル内のレコードを識別するためのキーを定義できます。

テーブルには少なくとも1つのキーが必要です。

## 使用と使用のコンテキスト{#use-and-context-of-use-6}

原則として、キーはスキーマのメイン要素とインデックスの後に宣言されます。

キーに複数のフィールド（例：複数の`<keyfield>`子）が含まれる場合は、複合キーと呼ばれます。 主キーの定義に複合キーを使用しないでください。

スキーマのメイン要素に「@autopk=true」属性が含まれている場合、プライマリキーは一意です。 スキーマ1人につき1つの主キーしか持つことができません。

最初の1000個の識別子は予約されているので、キーに対して値の範囲を定義する必要がある場合、開始は1000になります。

## 属性の説明{#attribute-description-8}

* **allowEmptyPart (boolean)**:複合キーの場合、この属性が有効な場合、そのキーの少なくとも1つが空でないと、そのキーは有効と見なされます。この場合、空の概念の値は「0」です（ブール値またはすべてのタイプの数値データ）。 デフォルトでは、複合キーを構成するすべてのキーを入力する必要があります。
* **applicableIf (string)**:この属性を使用すると、キーをオプションにできます。キー定義を適用する条件を定義します。 この属性はXTK式を受け取ります。
* **internal (boolean)**:この属性は、アクティブ化された場合に、キーがプライマリであることをAdobe Campaignに知らせます。
* **label (string)**:キーのラベル。
* **name (MNTOKEN)**:キーの内部名。
* **noDbIndex (boolean)**:アクティブ化された場合(noDbIndex=&quot;true&quot;)、キーに一致するフィールドのインデックスは作成されません。

## 例 {#examples-------}

「@expr」または「alias」フィールドを空にすることを許可する複合キーの宣言：

```
<key name="node" allowEmptyPart="true">
  <keyfield xpath="@expr"/>
   <keyfield xpath="@alias"/>
 </key>
```

`<srcschema>`内のSTRING型の&quot;Name&quot;フィールドでの主キーの宣言と、一致するSQLクエリ:

```
 
<key name="PrimaryKey" internal="true">  
  <keyfield xpath="@name"/>
</key>

CREATE UNIQUE INDEX Schema_PrimaryKey ON Schema(sName);
```
