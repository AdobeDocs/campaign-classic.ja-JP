---
product: campaign
title: スキーマ要素と属性 – キー要素
description: キー要素
feature: Schema Extension
exl-id: 3d0ef574-27a3-40f2-91a0-70e9583d9980
TQID: https://experienceleague.adobe.com/5LDW8-4YjfDebSOFq6ON8c0ulQQsGGjmRbek67G4Ml4
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 322
ht-degree: 8%

---

# キー要素 {#key--element}


## コンテンツモデル {#content-model-8}

key:==keyfield

## 属性 {#attributes-8}

* @allowEmptyPart （ブール値）
* @applicableIf （文字列）
* @internal （ブール値）
* @label （文字列）
* @name （トークン）
* @noDbIndex （ブール値）

## 親 {#parents-8}

`<element>`

## 子 {#children-8}

`<keyfield>`

## 説明 {#description-8}

この要素では、テーブル内のレコードを識別するためのキーを定義できます。

テーブルには少なくとも 1 つのキーが必要です。

## 用途と使用状況 {#use-and-context-of-use-6}

原則として、キーはスキーマのメイン要素とインデックスの後に宣言されます。

キーに複数のフィールドが含まれる場合（つまり、複数の`<keyfield>`個の子フィールドが含まれる場合）は、複合キーと呼ばれます。 複合キーを使用してプライマリキーを定義しないでください。

スキーマのメイン要素に「@autopk=true」属性が含まれている場合、プライマリキーは一意です。 スキーマごとに1つのプライマリキーのみを持つことができます。

最初の1000個の識別子は予約されているので、キーの値の範囲を定義する必要がある場合は、1000から開始してください。

## 属性の説明 {#attribute-description-8}

* **allowEmptyPart （boolean）**：複合キーの場合、この属性がアクティブ化されている場合、少なくとも1つのキーが空でない場合、これらのキーは有効であると見なされます。 この場合、空の概念の値は「0」（ブール値またはすべての種類の数値データ）になります。 デフォルトでは、合成キーを構成するすべてのキーを入力する必要があります。
* **applicableIf （文字列）**：この属性を使用すると、キーをオプションにできます。 キー定義が適用される条件を定義します。 この属性はXTK式を受け取ります。
* **内部（ブール値）**：アクティブ化されている場合、この属性はAdobe Campaignにキーがプライマリであることを知らせます。
* **label （文字列）**: キーのラベル。
* **name （MNTOKEN）**: キーの内部名。
* **noDbIndex （boolean）**：アクティブ化されている場合（noDbIndex=&quot;true&quot;）、キーに一致するフィールドはインデックス化されません。

## 例 {#examples-------}

「@expr」フィールドまたは「alias」フィールドを空にすることを許可する複合キーの宣言：

```
<key name="node" allowEmptyPart="true">
  <keyfield xpath="@expr"/>
   <keyfield xpath="@alias"/>
 </key>
```

`<srcschema>`のSTRING タイプの「名前」フィールドと一致するSQL クエリに対するプライマリキーの宣言：

```
 
<key name="PrimaryKey" internal="true">  
  <keyfield xpath="@name"/>
</key>

CREATE UNIQUE INDEX Schema_PrimaryKey ON Schema(sName);
```
