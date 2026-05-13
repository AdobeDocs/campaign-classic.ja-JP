---
product: campaign
title: Adobe Campaignのスキーマの基本を学ぶ
description: Adobe Campaign データベースのスキーマの操作方法と概念データモデルの拡張方法について説明します
feature: Schema Extension
role: Developer
level: Intermediate, Experienced
exl-id: f36a1b01-a002-4a21-9255-ea78b5f173fe
TQID: https://experienceleague.adobe.com/ikQVjdkvhTM-361S7mcpRYsuhpqjHxX-Y-9wdRCYldg
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2: id: a72a22e0-8c8d-4019-ba42-3f2644aa91a3id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 372
ht-degree: 49%

---

# スキーマの基本を学ぶ {#about-schema-reference}

## スキーマとは {#what-is-a-schema}

この章では、Adobe Campaign データベースの概念データモデルを拡張するために、拡張スキーマを設定する方法について説明します。

Campaignの組み込みテーブルとそのインタラクションについて詳しくは、[Campaign Classic データモデル ](about-data-model.md)を参照してください。

Adobe Campaignでは、アプリケーションに格納されるデータの物理構造と論理構造をXMLで記述します。 **スキーマ**&#x200B;は、データベーステーブルに関連付けられたXML ドキュメントです。 この中でデータ構造を定義し、表の SQL 定義を記述します。

* テーブルの名前
* フィールド
* 索引
* 他のテーブルとのリンク

また、データの格納に使用する XML 構造についても説明します。

* 要素と属性
* 要素の階層
* 要素と属性の種類
* デフォルト値
* ラベル、説明およびその他のプロパティ。

スキーマを使用すると、データベース内にエンティティを定義できます。 エンティティごとにスキーマがあります。

次の図は、Adobe Campaign データシステム内のスキーマの場所を示しています。

![](assets/reference_schema_intro.png)

## スキーマの構文 {#syntax-of-schemas}

スキーマのルート要素は **`<srcschema>`** です。 **`<element>`** と **`<attribute>`** のサブ要素が含まれます。

最初の **`<element>`** サブ要素は、エンティティのルートに一致します。

```
<srcSchema name="recipient" namespace="cus">
  <element name="recipient">  
    <attribute name="lastName"/>
    <attribute name="email"/>
    <element name="location">
      <attribute name="city"/>
   </element>
  </element>
</srcSchema>
```

>[!NOTE]
>
>エンティティのルート要素はスキーマと同じ名前を持ちます。

![](assets/s_ncs_configuration_schema_and_entity.png)

**`<element>`** タグはエンティティ要素の名前を定義します。 スキーマの **`<attribute>`** タグは、リンク先の **`<element>`** タグの属性の名前を定義します。

## スキーマの ID {#identification-of-a-schema}

データスキーマは、名前と名前空間で識別されます。

名前空間を使用すると、一連のスキーマを目標領域別にグループ化できます。 例えば、**cus** 名前空間は、顧客固有の設定（**customers**）に使用します。

スキーマの識別キーは、名前空間と名前をコロンで区切った文字列です。例：**cus:recipient**。

>[!IMPORTANT]
>
>* 名前空間の名前は簡潔で、XML命名ルールに従って許可された文字のみを含める必要があります。
>
>* 識別子の先頭を数字にすることはできません。
>
>* 次の名前空間は、Adobe Campaign アプリケーションの操作に必要なシステム エンティティの説明用に予約されており、使用しないでください。**xtk**、**nl**、**nms**、**ncm**、**temp**、**ncl**、**crm**、**xxl**。
>
