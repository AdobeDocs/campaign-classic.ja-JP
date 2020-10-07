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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# ターゲットマッピング{#target-mapping}

ターゲットマッピングの作成は、次の2つの場合に必要です。

* adobe campaignが提供するもの以外の受信者テーブルを使用する場合、
* ターゲットマッピング画面の標準ターゲティングディメンションと異なるフィルタリングディメンションを設定する場合。

ターゲットマッピングの作成ウィザードは、カスタムテーブルを使用するのに必要なすべてのスキーマを作成する際に役立ちます。

## カスタムテーブルにリンクされたスキーマの作成と設定 {#creating-and-configuring-schemas-linked-to-the-custom-table}

ターゲットマッピングを作成する前に、Adobe Campaignが新しい受信者データスキーマで動作するために、いくつかの設定が必要です。

それには、次の手順に従います。

1. 使用するカスタムテーブルのフィールドを統合する新しいデータスキーマを作成します。

   詳細は、 [スキーマリファレンス(xtk:srcSchema)を参照してください](../../configuration/using/about-schema-reference.md)。

   この例では、次のフィールドを含む非常に単純なテーブル、顧客スキーマを作成します。ID、名、姓、電子メールアドレス、携帯電話番号。 この表に保存されている個人に電子メールやSMSのアラートを送信できるようにすることが目的です。

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

1. =&quot;true&quot;属性を使用して、スキーマを外部表示として宣言します。 「表示 [属性](../../configuration/using/schema-characteristics.md#the-view-attribute)」を参照してください。

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

1. **[!UICONTROL 管理/キャンペーン管理/ターゲットマッピング]** ノードをクリックします。
1. 「 **新規** 」ボタンをクリックして、ターゲットマッピング作成ウィザードを開きます。
1. 「 **ラベル** 」フィールドに値を入力し、作成したスキーマを「 **ターゲティングディメンション** 」フィールドで選択します。

   ![](assets/mapping_diffusion_wizard_1.png)

1. 「アドレスフォームの **編集** 」ウィンドウで、様々な配信アドレスと一致するスキーマのフィールドを選択します。 ここで、 **@email** 、@mobile **** の各フィールドをマッピングできます。

   ![](assets/mapping_diffusion_wizard_2.png)

1. 次の **ストレージ** ・ウィンドウで、拡張スキーマ **** ・フィールドのサフィックスを入力して、新しいスキーマとAdobe Campaignが提供する標準のスキーマを区別します。

   「 **[!UICONTROL 新しい追加フィールドを定義]** 」をクリックして、配信でターゲットするディメンションを選択します。

   デフォルトでは、除外管理はメッセージと同じテーブルに保存されます。 ターゲットマッピングにリンクされた追跡の **ストレージを設定する場合は、「追跡用のストレージスキーマを** 生成します」ボックスをオンにします。

   ![](assets/mapping_diffusion_wizard_3.png)

   >[!IMPORTANT]
   >
   >Adobe Campaignは、同じブロードローグやトラッキングログのスキーマにリンクされた複数の受信者スキーマ(ターゲットスキーマ)をサポートしていません。 そうでない場合は、後でデータ調整の異常が発生する可能性があります。 この詳細については、「 [推奨と制限](../../configuration/using/about-custom-recipient-table.md) 」ページを参照してください。

1. 「 **拡張機能** 」ウィンドウで、生成するオプションのスキーマを選択します(使用可能なスキーマのリストは、Adobe Campaignプラットフォームにインストールされているモジュールに応じて異なります)。

   ![](assets/mapping_diffusion_wizard_4.png)

1. Click the **Save** button to close the wizard.

   ウィザードは、開始スキーマを使用して、新しいターゲットマッピングを動作させるために必要なその他のスキーマをすべて作成します。

   ![](assets/mapping_schema_list.png)

## ターゲットマッピングの使用 {#using-target-mapping}

新しいスキーマを配信のターゲットとして使用する方法は2つあります。

* マッピングに基づいて1つ以上の配信テンプレートを作成
* 次に示すように、配信を作成する際に、ターゲットの選択時に直接マッピングを選択します。

![](assets/mapping_selection_ciblage.png)

**関連トピック**

* [顧客の要求に迅速に対応し、データにアクセス](https://helpx.adobe.com/campaign/kb/simplifying-campaign-management-acc.html#Quicklyrespondtocustomerrequeststoaccesstheirdata)