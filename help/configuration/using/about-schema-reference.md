---
product: campaign
title: Adobe Campaignのスキーマの基本を学ぶ
description: Adobe Campaign データベースのスキーマの操作方法と概念データモデルの拡張方法について説明します
feature: Schema Extension
role: Developer
level: Intermediate, Experienced
exl-id: f36a1b01-a002-4a21-9255-ea78b5f173fe
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 49%

---

# スキーマの基本を学ぶ {#about-schema-reference}

## スキーマとは {#what-is-a-schema}

この章では、Adobe Campaign データベースの概念データモデルを拡張するために、拡張スキーマを設定する方法について説明します。

Campaignの組み込みテーブルとそのインタラクションについて詳しくは、[Campaign Classic データモデル &#x200B;](about-data-model.md)を参照してください。

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
