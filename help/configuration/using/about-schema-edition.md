---
title: スキーマエディションについて
seo-title: スキーマエディションについて
description: スキーマエディションについて
seo-description: null
page-status-flag: never-activated
uuid: edb4d47d-b507-4d86-9873-ebd5f6acefc6
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: d5b08e4e-060c-4185-9dac-af270918e2b9
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 10%

---


# スキーマエディションについて{#about-schema-edition}

Adobe Campaignでは、次の目的でデータスキーマを使用しています。

* アプリケーション内のデータオブジェクトが基盤となるデータベーステーブルにどのように関連付けられるかの定義
* Campaign アプリケーション内での異なるデータオブジェクト間リンクの定義
* 各オブジェクトに含まれている個々のフィールドの定義と記述

キャンペーンの組み込みテーブルとその操作について詳しくは、 [Campaign Classicデータモデルを参照してください](https://helpx.adobe.com/jp/campaign/kb/acc-datamodel.html)。

## スキーマの拡張または作成 {#extending-or-creating-schemas}

受信者テーブル(nms:受信者)など、キャンペーンのコアデータスキーマの1つにフィールドやインデックスなどの要素を追加するには、そのスキーマを拡張する必要があります。 For more on this, refer to the [Extending a schema](../../configuration/using/extending-a-schema.md) section.

Adobe Campaignにあらかじめ用意されているタイプのデータをまったく新しく追加するには（例えば契約表）、カスタムスキーマを直接作成します。 For more on this, refer to the [Data schemas](../../configuration/using/data-schemas.md) section.

![](assets/schemaextension_getting_started_1.png)

作業対象のスキーマを拡張または作成したら、ベストプラクティスは、XMLコンテンツ要素を次に示すのと同じ順序で定義することです。

## 列挙 {#enumerations}

定義済みリストは、最初に、スキーマのメイン要素の前に定義されます。 特定のフィールドに対してリストが持つ選択肢を制限するために、ユーザーに値を表示できます。

例：

```
<enumeration basetype="byte" name="exTransactionTypeEnum" default="store">
<value label="Website" name="web" value="0"/>
<value label="Call Center" name="phone" value="1"/>
<value label="In Store" name="store" value="2"/>
</enumeration>
```

フィールドを定義する際、次のように定義済みリストを使用できます。

```
<attribute desc="Type of Transaction" label="Transaction Type" name="transactionType" 
type="string" enum="exTransactionTypeEnum"/>
```

>[!NOTE]
>
>また、ユーザーが管理する定義済みリスト(通常は **[!UICONTROL 管理]** / **[!UICONTROL プラットフォーム]** )を使用して、特定のフィールドの値を指定することもできます。 これらは効果的にグローバルな定義済みリストであり、作業対象の特定のスキーマ以外で定義済みリストを使用する場合は、より良い選択肢となります。

定義済みリストの詳細については、「 [定義済みリスト](../../configuration/using/schema-structure.md#enumerations) 」と「 [`<enumeration>` 要素](../../configuration/using/elements-and-attributes.md#enumeration--element) 」の節を参照してください。

## インデックス {#index}

インデックスは、スキーマのメイン要素で宣言された最初の要素です。

一意であるかどうかに関係なく、1つ以上のフィールドを参照できます。

例：

```
<dbindex name="email" unique="true">
  <keyfield xpath="@email"/>
</dbindex>
```

```
<dbindex name="lastNameAndZip">
  <keyfield xpath="@lastName"/>
  <keyfield xpath="location/@zipCode"/>
</dbindex>
```

xpath **** 属性は、スキーマ内でインデックスを作成するフィールドを指します。

>[!IMPORTANT]
>
>インデックスが提供するSQLクエリの読み取りパフォーマンスの向上には、レコードの書き込みパフォーマンスのヒットも伴うことを覚えておくことが重要です。 したがって、インデックスは用心して使用する必要があります。

インデックスの詳細については、「 [インデックス付きフィールド](../../configuration/using/database-mapping.md#indexed-fields) 」を参照してください。

## キー {#keys}

各テーブルには少なくとも1つのキーが必要です。多くの場合、 **@autopk=true** 属性を「true」に設定して、スキーマのメイン要素内に自動的に確立されます。

主キーは、 **internal** 属性を使用して定義することもできます。

例：

```
<key name="householdId" internal="true">
  <keyfield xpath="@householdId"/>
</key>
```

この例では、 **@autopk** 属性で「id」という名前のデフォルトのプライマリキーを作成する代わりに、独自の「householdId」プライマリキーを指定します。

>[!IMPORTANT]
>
>新しいスキーマを作成するときや、スキーマ拡張の際には、スキーマ全体で同じプライマリキーシーケンス値（@pkSequence）を維持する必要があります。

キーの詳細については、キーの [管理の節を参照してください](../../configuration/using/database-mapping.md#management-of-keys) 。

## 属性（フィールド） {#attributes--fields-}

属性を使用すると、データオブジェクトを構成するフィールドを定義できます。 スキーマ版ツールバーの **[!UICONTROL 挿入]** ボタンを使用して、空の属性テンプレートをXML内のカーソル位置にドロップできます。 For more on this, refer to the [Data schemas](../../configuration/using/data-schemas.md) section.

![](assets/schemaextension_getting_started_2.png)

属性の完全なリストは、「 [`<attribute>` element](../../configuration/using/elements-and-attributes.md#attribute--element) 」セクションで利用できます。 最も一般的に使用される属性の一部を以下に示します。

* **@advanced**
* **@dataPolicy**
* **@デフォルト**
* **@desc**
* **@enum**
* **@expr**
* **@label**
* **@length**
* **@name**
* **@notNull**
* **@required**
* **@ref**
* **@xml**
* **@type**

   様々なデータベース管理システム用にAdobe Campaignによって生成されたデータ・タイプのマッピングをリストした表を表示するには、「Adobe Campaign/DBMSデータのタイプの [マッピング](../../configuration/using/schema-structure.md#mapping-the-types-of-adobe-campaign-dbms-data) 」を参照してください。

各属性の詳細については、「 [属性の説明](../../configuration/using/elements-and-attributes.md#attribute-description) 」の項を参照してください。

### 例 {#examples}

デフォルト値の定義例：

```
<attribute name="transactionDate" label="Transaction Date" type="datetime" default="GetDate()"/>
```

共通属性をフィールドのテンプレートとして使用する場合の例で、必須ともマークされます。

```
<attribute name="mobile" label="Mobile" template="nms:common:phone" required="true" />
```

@advanced **** 属性を使用して非表示にする計算済みフィールドの例：

```
<attribute name="domain" label="Email domain" desc="Domain of recipient email address" expr="GetEmailDomain([@email])" advanced="true" />
```

XMLフィールドの例は、SQLフィールドにも格納され、 **@dataPolicy** 属性を持ちます。

```
<attribute name="secondaryEmail" label="Secondary email address" length="100" xml="true" sql="true" dataPolicy="email" />
```

>[!IMPORTANT]
>
>ほとんどの属性はデータベースの物理フィールドに対して1 ～ 1の基数に基づいてリンクされますが、XMLフィールドや計算済みフィールドには該当しません。\
>XMLフィールドは、テーブルのメモ型フィールド(「mData」)に格納されます。\
>ただし、計算済みフィールドは、クエリを起動するたびに動的に作成されるので、アプリケーションレイヤーにのみ存在します。

## リンク {#links}

リンクは、スキーマのメイン要素の最後の要素の一部です。 インスタンス内のすべての様々なスキーマが相互にどのように関連付けられるかを定義します。

リンク先のテーブルの **外部キー** （外部キー）を含むスキーマでリンクが宣言されています。

基数には次の3種類があります。1-1、1-N、N-N。デフォルトで使用される1-N型です。

### 例 {#examples-1}

受信者テーブル(標準搭載のスキーマ)とカスタムトランザクションのテーブル間の1-Nリンクの例を次に示します。

```
<element label="Recipient" name="lnkRecipient" revLink="lnkTransactions" target="nms:recipient" type="link"/>
```

カスタムスキーマ「Car」(「cus」名前空間内)と受信者テーブル間の1-1リンクの例を次に示します。

```
<element label="Car" name="lnkCar" revCardinality="single" revLink="recipient" target="cus:car" type="link"/>
```

受信者テーブルと、主キーではなく、電子メールアドレスに基づくアドレスのテーブルとの外部結合の例：

```
<element name="emailInfo" label="Email Info" revLink="recipient" target="nms:address" type="link" externalJoin="true">
  <join xpath-dst="@address" xpath-src="@email"/>
</element>
```

ここで、「xpath-dst」はターゲットスキーマの主キーに対応し、「xpath-src」はソーススキーマの外部キーに対応します。

## 監査記録 {#audit-trail}

スキーマの下部に含めると便利な要素の1つに、トラッキング要素（監査証跡）があります。

次の例を使用して、テーブル内のすべてのデータの作成日、データを作成したユーザー、日付、および最終変更の作成者に関するフィールドを含めます。

```
<element aggregate="xtk:common:auditTrail" name="auditTrail"/>
```

## データベース構造の更新 {#updating-the-database-structure}

変更が完了し、保存されたら、SQL構造に影響を与える可能性のある変更をデータベースに適用する必要があります。 これを行うには、データベース更新ウィザードを使用します。

![](assets/schemaextension_getting_started_3.png)

詳しくは、[データベース構造の更新](../../configuration/using/updating-the-database-structure.md)の節を参照してください。

>[!NOTE]
>
>変更がデータベース構造に影響を与えない場合は、スキーマを再生成する必要があります。 これを行うには、更新するスキーマを選択し、右クリックして、 **[!UICONTROL Actions/Regenerate selectedスキーマを選択します。]** . For more on this, refer to the [Regenerating schemas](../../configuration/using/regenerating-schemas.md) section.

