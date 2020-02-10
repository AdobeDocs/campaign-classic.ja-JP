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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 58b69ae83d0ff2bece26cb3ff0604cd92e3c20f4

---


# スキーマエディションについて{#about-schema-edition}

Adobe Campaignでは、データスキーマを使用して次のことを行います。

* アプリケーション内のデータオブジェクトが基盤となるデータベーステーブルにどのように関連付けられるかの定義
* Campaign アプリケーション内での異なるデータオブジェクト間リンクの定義
* 各オブジェクトに含まれている個々のフィールドの定義と記述

Campaignの組み込みテーブルとそのインタラクションについて詳しくは、 [Campaign Classicデータモデルを参照してください](https://helpx.adobe.com/campaign/kb/acc-datamodel.html)。

## スキーマの拡張または作成 {#extending-or-creating-schemas}

受信者テーブル(nms:recipient)など、キャンペーンのコアデータスキーマの1つにフィールドやインデックスなどの要素を追加するには、そのスキーマを拡張する必要があります。 この詳細については、「スキーマの拡張」の節 [を参照してくださ](../../configuration/using/extending-a-schema.md) い。

Adobe Campaignにあらかじめ用意されていない、まったく新しいタイプのデータを追加する（例えば契約表）には、カスタムスキーマを直接作成できます。 For more on this, refer to the [Data schemas](../../configuration/using/data-schemas.md) section.

![](assets/schemaextension_getting_started_1.png)

作業対象のスキーマを拡張または作成した後は、XMLコンテンツ要素を次に示すのと同じ順序で定義することをお勧めします。

## 列挙 {#enumerations}

列挙は、最初に、スキーマのメイン要素の前に定義されます。 リストに値を表示して、特定のフィールドに対するユーザーの選択を制限できます。

例：

```
<enumeration basetype="byte" name="exTransactionTypeEnum" default="store">
<value label="Website" name="web" value="0"/>
<value label="Call Center" name="phone" value="1"/>
<value label="In Store" name="store" value="2"/>
</enumeration>
```

フィールドを定義する際に、次のようにこの列挙を使用できます。

```
<attribute desc="Type of Transaction" label="Transaction Type" name="transactionType" 
type="string" enum="exTransactionTypeEnum"/>
```

>[!NOTE]
>
>また、ユーザー管理の列挙(通常は>の下 **[!UICONTROL Administration]** )を使用し **[!UICONTROL Platform]** て、特定のフィールドの値を指定できます。 これらは効果的にグローバルな列挙であり、作業対象の特定のスキーマ以外で列挙を使用できる場合は、より良い選択肢となります。

列挙の詳細については、「列挙」と「要素」の節を [参照し](../../configuration/using/schema-structure.md#enumerations) て [`<enumeration>` ください](../../configuration/using/elements-and-attributes.md#enumeration--element) 。

## インデックス {#index}

インデックスは、スキーマのメイン要素で宣言された最初の要素です。

一意である場合とない場合があり、1つ以上のフィールドを参照します。

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

xpath属 **性は** 、インデックスを作成するスキーマ内のフィールドを指します。

>[!CAUTION]
>
>インデックスによって提供されるSQLクエリの読み取りパフォーマンスの向上には、レコードの書き込みに対するパフォーマンスの低下も伴う点に注意してください。 したがって、インデックスは用心して使用する必要があります。

インデックスの詳細については、「インデックス付きフィール [ド」の節を参照してください](../../configuration/using/database-mapping.md#indexed-fields) 。

## キー {#keys}

各テーブルには少なくとも1つのキーが必要で、多くの場合、 **@autopk=true** 属性を「true」に設定して、スキーマのメイン要素で自動的に確立されます。

主キーは、 **internal属性を使用して定義することもで** きます。

例：

```
<key name="householdId" internal="true">
  <keyfield xpath="@householdId"/>
</key>
```

この例では、 **** @autopk属性で「id」という名前のデフォルトの主キーを作成する代わりに、独自の「householdId」主キーを指定します。

>[!CAUTION]
>
>新しいスキーマを作成するときや、スキーマ拡張の際には、スキーマ全体で同じプライマリキーシーケンス値（@pkSequence）を維持する必要があります。

キーの詳細については、「キーの管理」の節 [を参照してください](../../configuration/using/database-mapping.md#management-of-keys) 。

## 属性（フィールド） {#attributes--fields-}

属性を使用すると、データオブジェクトを構成するフィールドを定義できます。 スキーマ編集ツールバー **[!UICONTROL Insert]** のボタンを使用して、空の属性テンプレートをXMLのカーソル位置にドロップできます。 For more on this, refer to the [Data schemas](../../configuration/using/data-schemas.md) section.

![](assets/schemaextension_getting_started_2.png)

属性の完全なリストは、「要素」セクションで使用で [`<attribute>` きます](../../configuration/using/elements-and-attributes.md#attribute--element) 。 最も一般的に使用される属性の一部を以下に示します。

* **@advanced**
* **@dataPolicy**
* **@default**
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

   様々なデータベース管理システム用にAdobe Campaignで生成されたデータ型のマッピングの一覧表を表示するには、「 [Adobe Campaign/DBMSデータ型のマッピング](../../configuration/using/schema-structure.md#mapping-the-types-of-adobe-campaign-dbms-data) 」を参照してください。

各属性の詳細については、「属性の説明」の節を参照 [してください](../../configuration/using/elements-and-attributes.md#attribute-description) 。

### 例 {#examples}

デフォルト値の定義例：

```
<attribute name="transactionDate" label="Transaction Date" type="datetime" default="GetDate()"/>
```

共通属性を必須としてマークされたフィールドのテンプレートとして使用する例を次に示します。

```
<attribute name="mobile" label="Mobile" template="nms:common:phone" required="true" />
```

@advanced属性を使用して非表示にする計算済みフィー **ルドの例** :

```
<attribute name="domain" label="Email domain" desc="Domain of recipient email address" expr="GetEmailDomain([@email])" advanced="true" />
```

XMLフィールドの例は、SQLフィールドにも格納され、 **@dataPolicy属性を持ちます** 。

```
<attribute name="secondaryEmail" label="Secondary email address" length="100" xml="true" sql="true" dataPolicy="email" />
```

>[!CAUTION]
>
>ほとんどの属性は、1 ～ 1の基数に従ってデータベースの物理フィールドにリンクされますが、XMLフィールドや計算済みフィールドには該当しません。\
>XMLフィールドは、テーブルのメモ型フィールド(「mData」)に格納されます。\
>ただし、計算済みフィールドは、クエリーが開始されるたびに動的に作成されるので、アプリケーション層にのみ存在します。

## リンク {#links}

リンクは、スキーマのメイン要素の最後の要素の一部です。 インスタンス内のすべての異なるスキーマが相互に関連付けられる方法を定義します。

リンク先のテーブルの外部キーを含むス **キーマで** 、リンクが宣言されています。

基数には次の3種類があります。1-1、1-N、N-N。デフォルトで使用される1-Nタイプです。

### 例 {#examples-1}

受信者テーブル（あらかじめ用意されているスキーマ）とカスタムトランザクションのテーブル間の1-Nリンクの例を次に示します。

```
<element label="Recipient" name="lnkRecipient" revLink="lnkTransactions" target="nms:recipient" type="link"/>
```

カスタムスキーマ「Car」（「cus」名前空間内）と受信者テーブルの間の1-1リンクの例を次に示します。

```
<element label="Car" name="lnkCar" revCardinality="single" revLink="recipient" target="cus:car" type="link"/>
```

受信者テーブルと、主キーではなく電子メールアドレスに基づくアドレステーブルとの間の外部結合の例：

```
<element name="emailInfo" label="Email Info" revLink="recipient" target="nms:address" type="link" externalJoin="true">
  <join xpath-dst="@address" xpath-src="@email"/>
</element>
```

ここで、「xpath-dst」はターゲットスキーマの主キーに対応し、「xpath-src」はソーススキーマの外部キーに対応します。

## Audit trail {#audit-trail}

スキーマの下部に含めると便利な要素の1つに、トラッキング要素（監査証跡）があります。

次の例を使用して、テーブル内のすべてのデータの作成日、データを作成したユーザー、日付、および最終変更の作成者に関するフィールドを含めます。

```
<element aggregate="xtk:common:auditTrail" name="auditTrail"/>
```

## データベース構造の更新 {#updating-the-database-structure}

変更が完了して保存されたら、SQL構造に影響を与える可能性のある変更をデータベースに適用する必要があります。 これを行うには、データベース更新ウィザードを使用します。

![](assets/schemaextension_getting_started_3.png)

詳しくは、「データベース構造の更新 [」の節を参照してください](../../configuration/using/updating-the-database-structure.md) 。

>[!NOTE]
>
>変更がデータベース構造に影響を与えない場合は、スキーマを再生成する必要があります。 これを行うには、更新するスキーマを選択し、右クリックしてを選択します **[!UICONTROL Actions > Regenerate selected schemas...]** 。 For more on this, refer to the [Regenerating schemas](../../configuration/using/regenerating-schemas.md) section.

