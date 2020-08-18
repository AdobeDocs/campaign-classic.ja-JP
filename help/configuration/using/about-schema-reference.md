---
title: Adobe Campaign Classicのスキーマリファレンスについて
description: Adobe Campaign Classicデータベースの概念データモデルを拡張するための拡張スキーマの構成方法を学びます。
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
source-git-commit: d4ebaaf90d88cbec9a4d24d79eaf7c46890d933a
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 7%

---


# スキーマリファレンスについて{#about-schema-reference}

この章では、Adobe Campaignデータベースの概念的データモデルを拡張するための拡張スキーマの設定方法について説明します。

キャンペーンの組み込みテーブルとその操作について詳しくは、 [Campaign Classicデータモデルを参照してください](https://helpx.adobe.com/jp/campaign/kb/acc-datamodel.html)。

アプリケーションに格納されるデータの物理的および論理的構造は、XML で記述されます。It obeys a grammar specific to Adobe Campaign, called a **schema**.

スキーマは、データベーステーブルに関連付けられたXMLドキュメントです。 データ構造を定義し、表のSQL定義を説明します。

* テーブルの名前
* フィールド
* インデックス
* 他のテーブルとのリンク

また、データの格納に使用するXML構造についても説明します。

* 要素と属性
* 要素の階層
* 要素と属性の種類
* デフォルト値
* ラベル、説明、およびその他のプロパティ。

スキーマを使用すると、データベース内にエンティティを定義できます。 エンティティごとにスキーマがあります。

次の図に、Adobe Campaignデータシステム内のスキーマの場所を示します。

![](assets/reference_schema_intro.png)

## スキーマの構文 {#syntax-of-schemas}

スキーマのルート要素はで **`<srcschema>`**&#x200B;す。 サブ要素 **`<element>`** とサブ要素が含まれ **`<attribute>`** ます。

第1の **`<element>`** 副要素は、エンティティのルートに一致します。

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
>エンティティのルートスキーマは、要素と同じ名前を持ちます。

![](assets/s_ncs_configuration_schema_and_entity.png)

タグは、エンティティ要素の名前を定義します。 **`<element>`** **`<attribute>`** スキーマのタグは、リンク先の **`<element>`** タグの属性の名前を定義します。

## スキーマの識別 {#identification-of-a-schema}

データスキーマは、名前と名前空間で識別されます。

名前空間を使用すると、スキーマのセットを目標領域別にグループ化できます。 例えば、 **cus** 名前空間は、顧客固有の設定(**customers**)に使用されます。

>[!IMPORTANT]
>
>標準として、名前空間名は簡潔にし、XML命名規則に従って、許可された文字のみを含める必要があります。
>
>識別子の先頭を数字にすることはできません。

特定の名前空間は、Adobe Campaignアプリケーションの操作に必要なシステムエンティティの説明のために予約されています。

* **xtk**:プラットフォームシステムデータについて
* **nl**:出願の全体的な使用に関して
* **nms**:配信(受信者、配信、追跡等)に関する
* **ncm**:コンテンツ管理に関して
* **temp**:一時スキーマ用に予約。

The identification key of a schema is a string built using the namespace and the name separated by a colon; for example: **cus:recipient**.
