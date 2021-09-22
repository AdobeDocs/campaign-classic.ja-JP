---
product: campaign
title: ターゲットマッピング
description: ターゲットマッピングの作成方法を説明します
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
exl-id: 38333669-5598-4811-a121-b677c1413f56
source-git-commit: ed43a632a962747c9402ff8d5f0ce442c2cc6490
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# ターゲットマッピング{#target-mapping}

![](../../assets/v7-only.svg)

ターゲットマッピングの作成は、次の2つの場合に必要です。

* Adobe Campaignで指定された受信者テーブル以外の受信者テーブルを使用する場合、
* ターゲットマッピング画面の標準ターゲティングディメンションとは異なるフィルタリングディメンションを設定する場合。

ターゲットマッピング作成ウィザードは、カスタムテーブルを使用するために必要なすべてのスキーマを作成するのに役立ちます。

## カスタムテーブルにリンクされたスキーマの作成と設定 {#creating-and-configuring-schemas-linked-to-the-custom-table}

Adobe Campaignが新しい受信者データスキーマを使用して操作するには、ターゲットマッピングを作成する前に、いくつかの設定が必要です。

それには、次の手順に従います。

1. 使用するカスタムテーブルのフィールドを統合する新しいデータスキーマを作成します。

   詳しくは、[スキーマリファレンス(xtk:srcSchema)](../../configuration/using/about-schema-reference.md)を参照してください。

   この例では、顧客スキーマを作成し、次のフィールドを含む非常にシンプルなテーブルを作成します。ID、名、姓、電子メールアドレス、携帯電話番号。 目的は、このテーブルに格納された個人にEメールまたはSMSアラートを送信することです。

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

1. =&quot;true&quot;属性を使用して、スキーマを外部ビューとして宣言します。 [ビュー属性](../../configuration/using/schema-characteristics.md#the-view-attribute)を参照してください。

   ```
    <srcSchema desc="External recipient table" namespace="cus" view="true"....>
      ...
    </srcSchema>
   ```

1. ダイレクトメールアドレスを追加する必要がある場合は、次のタイプの構造を使用してください。

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

1. **[!UICONTROL 管理/キャンペーン管理/ターゲットマッピング]**&#x200B;ノードをクリックします。
1. 「**新規**」ボタンをクリックして、ターゲットマッピング作成ウィザードを開きます。
1. 「**ラベル**」フィールドに入力し、「**ターゲティングディメンション**」フィールドで作成したスキーマを選択します。

   ![](assets/mapping_diffusion_wizard_1.png)

1. **アドレスフォームを編集**&#x200B;ウィンドウで、様々な配信アドレスと一致するスキーマのフィールドを選択します。 ここでは、**@email**&#x200B;フィールドと&#x200B;**@mobile**&#x200B;フィールドをマッピングします。

   ![](assets/mapping_diffusion_wizard_2.png)

1. 次の&#x200B;**ストレージ**&#x200B;ウィンドウで、「拡張スキーマの&#x200B;**サフィックス**」フィールドに新しいスキーマをAdobe Campaignが提供する標準のスキーマと区別するために入力します。

   「**[!UICONTROL 新しい追加フィールドを定義]**」をクリックして、配信のターゲットにするディメンションを選択します。

   デフォルトでは、除外管理はメッセージと同じテーブルに保存されます。

   ターゲットマッピングにリンクされたトラッキングのストレージを設定する場合は、「**トラッキングのストレージスキーマを生成**」ボックスをオンにします。

   ![](assets/mapping_diffusion_wizard_3.png)

   >[!IMPORTANT]
   >
   >Adobe Campaignは、同じbroadlogスキーマやtrackinglogスキーマにリンクされた、複数の受信者スキーマをサポートしていません。 それ以外の場合は、後でデータの紐付けに異常が生じる可能性があります。 詳しくは、[推奨と制限](../../configuration/using/about-custom-recipient-table.md)ページを参照してください。

1. **拡張機能**&#x200B;ウィンドウで、生成するオプションのスキーマを選択します(使用可能なスキーマのリストは、Adobe Campaignプラットフォームにインストールされているモジュールによって異なります)。

   ![](assets/mapping_diffusion_wizard_4.png)

1. 「**保存**」ボタンをクリックして、ウィザードを閉じます。

   ウィザードでは、開始スキーマを使用して、新しいターゲットマッピングを機能させるために必要なその他すべてのスキーマを作成します。

   ![](assets/mapping_schema_list.png)

## ターゲットマッピングの使用 {#using-target-mapping}

新しいスキーマを配信のターゲットとして使用する方法は2つあります。

* マッピングに基づいて1つ以上の配信テンプレートを作成する
* 配信の作成時に、ターゲットの選択時に直接マッピングを選択します（下図を参照）。

![](assets/mapping_selection_ciblage.png)

**関連トピック**

* [顧客の要求に迅速に応じて、データにアクセス](https://helpx.adobe.com/campaign/kb/simplifying-campaign-management-acc.html#Quicklyrespondtocustomerrequeststoaccesstheirdata)
