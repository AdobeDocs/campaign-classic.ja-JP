---
product: campaign
title: データスキーマでのキー管理
description: データスキーマのキー管理について
feature: Configuration, Instance Settings
role: Developer
exl-id: faf63c8f-9d10-43c1-a990-91361594af9f
TQID: 'https://experienceleague.adobe.com/dErbfzRabMls-5x1S3eRZO94Kqcz9LRh3PaUhVD5zAU'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
    internal-label: Schemas
  - id: 7f0a1ee5-eeb8-5478-a9cd-b1896f033118
    internal-label: Instance Settings
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: a72a22e0-8c8d-4019-ba42-3f2644aa91a3
    internal-label: Schema extension
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
    internal-label: PI
  - id: a14877cc-63b1-41d9-bf0b-5f97cadd0417
    internal-label: Configuration guidelines
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a97306b73a2b577841e6f24536c62b2526e9fda9
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 28%
---
# スキーマでのキー管理 {#management-of-keys}

データスキーマに関連付けられた各テーブルには、テーブル内のレコードを識別するためのキーが少なくとも 1 つ必要です。 このページでは、Campaign Classic v7 テーブルで使用される自動インクリメンタルキーについて説明します。

Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 キー管理について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/schemas-forms/database-keys){target=_blank}を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/schemas-forms/database-keys){target=_blank}

## 自動インクリメンタルキー {#auto-incremental-key}

ほとんどのAdobe Campaign テーブルの主キーは、データベースエンジンによって自動生成される32 ビットの長い整数です。 キー値の計算は、データベース全体で一意の数値を生成するシーケンス（デフォルトでは&#x200B;**XtkNewId** SQL関数）によって異なります。 キーの内容は、レコードの挿入時に自動的に入力されます。

増分キーの利点は、テーブル間の結合に変更不可能なテクニカルキーを提供できることです。 さらに、このキーは2 バイトの整数を使用するため、メモリをあまり消費しません。

ソーススキーマで、**pkSequence**&#x200B;属性で使用するシーケンスの名前を指定できます。 この属性がソーススキーマで指定されていない場合、**XtkNewId**&#x200B;のデフォルトシーケンスが使用されます。 このアプリケーションは、最も多くのレコードを含むテーブルであるため、**nms:broadLog**&#x200B;および&#x200B;**nms:trackingLog** スキーマ （**NmsBroadLogId**&#x200B;および&#x200B;**NmsTrackingLogId**）に専用シーケンスを使用します。

ACC 18.10以降、**XtkNewId**&#x200B;は、標準スキーマのシーケンスのデフォルト値ではなくなりました。 専用のシーケンスを使用して、スキーマを構築したり、既存のスキーマを拡張したりできるようになりました。

>[!IMPORTANT]
>
>スキーマを新しく作成するときや、スキーマを拡張するときは、スキーマ全体で同じプライマリキーのシーケンス値（@pkSequence）を保持する必要があります。

Adobe Campaign スキーマで参照されているシーケンス（**NmsTrackingLogId**&#x200B;など）は、パラメーター内のIDの数をコンマで区切って返すSQL関数に関連付ける必要があります。 この関数は&#x200B;**GetNew** XXX **Ids**&#x200B;と呼ぶ必要があります。ここで、**XXX**&#x200B;はシーケンスの名前です（**GetNewNmsTrackingLogIds**&#x200B;例）。 **datakit/nms/eng/sql/** ディレクトリのアプリケーションに付属している&#x200B;**postgres-nms.sql**、**mssql-nms.sql**&#x200B;または&#x200B;**oracle-nms.sql** ファイルを表示して、各データベースエンジンの「NmsTrackingLogId」シーケンス作成例を復元します。

一意のキーを宣言するには、データスキーマのメイン要素に&#x200B;**autopk**&#x200B;属性（値「true」）を入力します。

**例**：

ソーススキーマでの増分キーの宣言：

```sql
<srcSchema name="recipient" namespace="cus">
  <element name="recipient" autopk="true">
  ...
  </element>
</srcSchema>
```

生成されたスキーマ：

```sql
<schema mappingType="sql" name="recipient" namespace="cus" xtkschema="xtk:schema">  
  <element name="recipient" autopk="true" pkSequence="XtkNewId" sqltable="CusRecipient"> 
    <dbindex name="id" unique="true">
      <keyfield xpath="@id"/>
    </dbindex>

    <key internal="true" name="id">
      <keyfield xpath="@id"/>
    </key>

    <attribute desc="Internal primary key" label="Primary key" name="id" sqlname="iRecipientId" type="long"/>
  </element>
</schema>
```

キーとそのインデックスの定義に加えて、自動生成されたプライマリキーを格納するために、「id」という数値フィールドが拡張スキーマに追加されました。

>[!IMPORTANT]
>
>プライマリキーが 0 に設定されたレコードは、テーブルの作成時に自動的に挿入されます。 このレコードは、外部結合を避けるために使用されます。外部結合はボリュームテーブルでは有効ではありません。 デフォルトでは、外部キーはすべて値 0 で初期化されるので、データ項目が入力されていない場合でも常に、結合時に結果を返します。


## 詳細情報

詳細については、次のリンクを参照してください。

* [スキーマの基本を学ぶ](about-schema-reference.md)
* [スキーマの構造](schema-structure.md)
* [データベースマッピング](database-mapping.md)
* [&#x200B; リンク管理](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/developer/schemas-forms/database-links){target="_blank"} （Campaign v8 ドキュメント）
* [Campaign データモデル &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/datamodel){target="_blank"} （Campaign v8 ドキュメント）
