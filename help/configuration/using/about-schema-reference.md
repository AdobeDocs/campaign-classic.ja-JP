---
product: campaign
title: Adobe Campaignのスキーマの基本を学ぶ
description: Adobe Campaign データベースのスキーマの操作方法と概念データモデルの拡張方法について説明します
feature: Schema Extension
role: Developer
level: Intermediate, Experienced
exl-id: f36a1b01-a002-4a21-9255-ea78b5f173fe
TQID: 'https://experienceleague.adobe.com/ikQVjdkvhTM-361S7mcpRYsuhpqjHxX-Y-9wdRCYldg'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
    internal-label: Schemas
subfeature_v2:
  - id: a72a22e0-8c8d-4019-ba42-3f2644aa91a3
    internal-label: Schema extension
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
    internal-label: PI
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
source-git-commit: a97306b73a2b577841e6f24536c62b2526e9fda9
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 42%
---
# スキーマの基本を学ぶ {#about-schema-reference}

## スキーマとは {#what-is-a-schema}

この章では、Adobe Campaign データベースの概念データモデルを拡張するために、拡張スキーマを設定する方法について説明します。

Campaignの組み込みテーブルとそのインタラクションについて詳しくは、[Campaign Classic データモデル &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/datamodel){target="_blank"} （Campaign v8 ドキュメント）を参照してください。

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

Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 スキーマの構文と識別について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/schemas-forms/schemas){target=_blank}を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/schemas-forms/schemas){target=_blank}
