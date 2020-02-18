---
title: Adobe Campaign Classicのスキーマ参照について
description: Adobe Campaign Classicデータベースの概念データモデルを拡張するための拡張スキーマの設定方法について説明します。
page-status-flag: never-activated
uuid: faddde15-59a1-4d2c-8303-5b3e470a0c51
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: schema-reference
discoiquuid: 5957b39e-c2c6-40a2-b81a-656e9ff7989c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: dbff132e3bf88c408838f91e50e4b047947ee32a

---


# スキーマ参照について{#about-schema-reference}

この章では、Adobe Campaignデータベースの概念データモデルを拡張するための拡張スキーマの設定方法について説明します。

Campaignの組み込みテーブルとそのインタラクションについて詳しくは、 [Campaign Classicデータモデルを参照してください](https://helpx.adobe.com/campaign/kb/acc-datamodel.html)。

アプリケーションに格納されるデータの物理的な構造と論理的な構造は、XMLで記述されます。 スキーマと呼ばれるAdobe Campaign固有の文法に従い **ます**。

スキーマとは、データベーステーブルに関連付けられたXMLドキュメントです。 データ構造を定義し、表のSQL定義を記述します。

* テーブルの名前
* フィールド
* 索引
* 他のテーブルとのリンク

また、データの保存に使用されるXML構造についても説明します。

* 要素と属性
* 要素の階層
* 要素と属性の種類
* デフォルト値
* ラベル、説明、およびその他のプロパティ。

スキーマを使用すると、データベース内にエンティティを定義できます。 各エンティティにスキーマがあります。

次の図に、Adobe Campaignデータシステム内のスキーマの場所を示します。

![](assets/reference_schema_intro.png)

## スキーマの構文 {#syntax-of-schemas}

スキーマのルート要素はです **`<srcschema>`**。 **とサブ要素 **`<element>`** が含 **`<attribute>`** まれます。

第1の副要 **`<element>`** 素は、エンティティのルートに一致する。

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
>エンティティのルート要素は、スキーマと同じ名前を持ちます。

![](assets/s_ncs_configuration_schema_and_entity.png)

タグは **`<element>`** エンティティ要素の名前を定義します。 **`<attribute>`** スキーマのタグは、リンク先のタグ内の属性 **`<element>`** の名前を定義します。

## スキーマのID {#identification-of-a-schema}

データスキーマは、名前と名前空間で識別されます。

名前空間を使用すると、一連のスキーマを目的の領域別にグループ化できます。 例えば、 **cus** namespaceは、顧客固有の設定(customers **)に使用さ**&#x200B;れます。

>[!IMPORTANT]
>
>標準として、名前空間の名前は簡潔で、XML命名規則に従って許可された文字のみを含める必要があります。
>
>識別子の先頭に数字を使用することはできません。

特定の名前空間は、Adobe Campaignアプリケーションの操作に必要なシステムエンティティの説明のために予約されています。

* **xtk**:プラットフォームシステムデータに関して
* **nl**:出願の全体的な使用に関して
* **nms**:配信（受信者、配信、追跡など）に関して、
* **ncm**:コンテンツ管理に関して
* **temp**:一時スキーマ用に予約済み。

The identification key of a schema is a string built using the namespace and the name separated by a colon; for example: **cus:recipient**.
