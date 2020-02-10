---
title: ターゲットマッピング
seo-title: ターゲットマッピング
description: ターゲットマッピング
seo-description: null
page-status-flag: never-activated
uuid: a7dad8eb-c191-4f10-b7d8-63e0699603b7
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
discoiquuid: ff7e6f72-7605-41ee-b25a-1e4618e674d7
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 8b3ab02d1fd90c3f14314508a8fa7d99df82436c

---


# ターゲットマッピング{#target-mapping}

ターゲットマッピングの作成は、次の2つの場合に必要です。

* adobe Campaignで提供されるテーブル以外の受信者テーブルを使用する場合、
* ターゲットマッピング画面で標準のターゲットディメンションと異なるフィルターディメンションを設定する場合。

ターゲット・マッピング作成ウィザードは、カスタム表を使用するために必要なすべてのスキーマの作成に役立ちます。

## カスタム表にリンクされたスキーマの作成と設定 {#creating-and-configuring-schemas-linked-to-the-custom-table}

ターゲットマッピングを作成する前に、Adobe Campaignが新しい受信者データスキーマを使用して動作するためには、いくつかの設定が必要です。

それには、次の手順に従います。

1. 使用するカスタムテーブルのフィールドを統合する新しいデータスキーマを作成します。

   詳しくは、 [Schema reference (xtk:srcSchema)を参照してください](../../configuration/using/about-schema-reference.md)。

   この例では、次のフィールドを含む非常に単純なテーブルである顧客スキーマを作成します。ID、名、姓、電子メールアドレス、携帯電話番号。 このテーブルに保存された個人に電子メールやSMSアラートを送信できるようにすることを目的としています。

   スキーマの例(cus:individual)

   ```
   <srcSchema name="individual" namespace="cus" label="Individuals">
     <element name="individual">
       <key name="id" internal="true">
         <keyfield xpath="@id"/>
       </key>
       <attribute name="id" type="long" length="32"/>
       <attribute name="lastName" type="string" length="100"/>
       <attribute name="firstName" type="string" length="100"/>
       <attribute name="email" type="string" length="100"/>
       <attribute name="mobile" type="string" length="100"/>
     </element>
   </srcSchema>
   ```

1. =&quot;true&quot;属性を使用して、スキーマを外部ビューとして宣言します。 ビュー属 [性を参照](../../configuration/using/schema-characteristics.md#the-view-attribute)。

   ```
    <srcSchema desc="External recipient table" namespace="cus" view="true"....>
      ...
    </srcSchema>
   ```

1. ダイレクトメールアドレスを追加する必要がある場合は、次の種類の構造を使用してください。

   ```
   <element advanced="true" name="postalAddress" template="nms:common:postalAddress">
        <attribute expr="SubString(JuxtWords(Smart([../infos/@firstname]), Upper([../infos/@name])), 1, 80)"
                   name="line1"/>
        <attribute expr="Upper([../address/@line2])" name="line2"/>
        <attribute expr="Upper([../address/@line])" name="line3"/>
        <attribute expr="Upper([../address/@line])" name="line4"/>
        <attribute expr="Upper([../address/@line])" name="line5"/>
        <attribute expr="Upper([../address/@line])" name="line6"/>
        <attribute _operation="delete" name="line7"/>
        <attribute _operation="delete" name="addrErrorCount"/>
        <attribute _operation="delete" name="addrQuality"/>
        <attribute _operation="delete" name="addrLastCheck"/>
        <element expr="@line1+'n'+@line2+'n'+@line3+'n'+@line4+'n'+@line5+'n'+@line6"
                 name="serialized"/>
        <attribute expr="AllNonNull2([../address/@line], [../infos/@name])" name="addrDefined"/>
      </element>
   ```

1. ノードをクリッ **[!UICONTROL Administration > Campaign management > Target mappings]** クします。
1. 「 **New** 」ボタンをクリックして、ターゲット・マッピング作成ウィザードを開きます。
1. 「ラベル **」フィールドを入力し、「ターゲットディメンション」フィールドで作成したスキ** ーマを選択します **** 。

   ![](assets/mapping_diffusion_wizard_1.png)

1. 「 **Edit address forms** 」ウィンドウで、様々な配信アドレスと一致するスキーマのフィールドを選択します。 ここで、「@email」フィールドと「 **@mobile** 」フィールドをマッ **プできます** 。

   ![](assets/mapping_diffusion_wizard_2.png)

1. 次の「 **Storage** 」ウィンドウで、「 **Suffix of the extension schemas** 」フィールドに新しいスキーマとAdobe Campaignが提供する追加設定なしのスキーマを区別します。

   クリッ **[!UICONTROL Define new additional fields]** クして、配信のターゲットにするディメンションを選択します。

   デフォルトでは、除外管理はメッセージと同じテーブルに保存されます。 ターゲットマ **ッピングにリンクされたトラッキングのストレージを設定する場合は、** 「トラッキング用のストレージスキーマを生成」ボックスを選択します。

   ![](assets/mapping_diffusion_wizard_3.png)

   >[!CAUTION]
   >
   >Adobe Campaignは、複数の受信者スキーマ（ターゲティングスキーマ）をサポートしません。同じブロードログスキーマまたはトラッキングログスキーマにリンクされています。 そうでないと、後でデータ調整の異常が発生する可能性があります。 この詳細については、「推奨と制限」ページ [を参照してください](../../configuration/using/about-custom-recipient-table.md) 。

1. 「拡張」ウ **ィンドウで** 、生成するオプションのスキーマを選択します（使用可能なスキーマのリストは、Adobe Campaignプラットフォームにインストールされているモジュールによって異なります）。

   ![](assets/mapping_diffusion_wizard_4.png)

1. Click the **Save** button to close the wizard.

   ウィザードでは、開始スキーマを使用して、新しいターゲット・マッピングを機能させるために必要なその他すべてのスキーマを作成します。

   ![](assets/mapping_schema_list.png)

## ターゲットマッピングの使用 {#using-target-mapping}

新しいスキーマを配信のターゲットとして使用する方法は2つあります。

* マッピングに基づいて1つ以上の配信テンプレートを作成する
* 配信の作成時に、ターゲット選択時に直接マッピングを選択します。次に例を示します。

![](assets/mapping_selection_ciblage.png)

**関連トピック**

* [顧客の要求に迅速に対応し、データにアクセス](https://helpx.adobe.com/campaign/kb/simplifying-campaign-management-acc.html#Quicklyrespondtocustomerrequeststoaccesstheirdata)