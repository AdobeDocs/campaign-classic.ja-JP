---
product: campaign
title: ターゲットマッピング
description: ターゲットマッピングの作成方法を説明します
feature: Application Settings
role: Data Engineer, Developer
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 38333669-5598-4811-a121-b677c1413f56
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---

# ターゲットマッピング{#target-mapping}



次の 2 つの場合に、ターゲットマッピングの作成が必要です。

* Adobe Campaignで提供される受信者テーブル以外の受信者テーブルを使用する場合、
* ターゲットマッピング画面で標準ターゲティングディメンションとは異なるフィルタリングディメンションを設定した場合。

ターゲットマッピング作成ウィザードは、カスタムテーブルを使用するために必要なすべてのスキーマを作成するのに役立ちます。

## カスタムテーブルにリンクされたスキーマの作成と設定 {#creating-and-configuring-schemas-linked-to-the-custom-table}

ターゲットマッピングを作成する前に、Adobe Campaignが新しい受信者データスキーマで動作するようにいくつかの設定が必要です。

それには、次の手順に従います。

1. 使用するカスタムテーブルのフィールドを統合する新しいデータスキーマを作成します。

   詳しくは、を参照してください。 [スキーマリファレンス（xtk:srcSchema）](../../configuration/using/about-schema-reference.md).

   この例では、顧客スキーマを作成します。これは、ID、名、姓、メールアドレス、携帯電話番号のフィールドを含む非常に単純なテーブルです。 目的は、このテーブルに保存されている個人にメールまたは SMS アラートを送信できるようにすることです。

   スキーマの例（cus:individual）

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

1. =&quot;true&quot;属性を使用して、スキーマを外部ビューとして宣言します。 こちらを参照してください [ビュー属性](../../configuration/using/schema-characteristics.md#the-view-attribute).

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

1. 「」をクリックします **[!UICONTROL 管理/ キャンペーン管理/ ターゲットマッピング]** ノード。
1. 「」をクリックします **新規** ボタンをクリックして、ターゲットマッピング作成ウィザードを開きます。
1. を入力 **ラベル** 「」フィールドに移動し、で作成したスキーマを選択します。 **ターゲティングディメンション** フィールド。

   ![](assets/mapping_diffusion_wizard_1.png)

1. が含まれる **住所フォームの編集** ウィンドウで、様々な配信アドレスに一致するスキーマのフィールドを選択します。 ここでは、をマッピングできます **@email** および **@mobile** フィールド。

   ![](assets/mapping_diffusion_wizard_2.png)

1. 次の場合 **ストレージ** ウィンドウで、 **拡張スキーマのサフィックス** Adobe Campaignが提供する標準スキーマから新しいスキーマを区別するためのフィールド。

   クリック **[!UICONTROL 新しい追加フィールドの定義]** 配信のターゲットにするディメンションを選択します。

   デフォルトでは、除外管理はメッセージと同じテーブルに保存されます。

   を確認します **トラッキング用のストレージスキーマの生成** ターゲットマッピングにリンクされたトラッキングのストレージを設定する場合は、ボックスに設定します。

   ![](assets/mapping_diffusion_wizard_3.png)

   >[!IMPORTANT]
   >
   >Adobe Campaignは、ターゲティングスキーマと呼ばれる、同じ broadlog スキーマや trackinglog スキーマにリンクされた複数の受信者スキーマをサポートしていません。 そうしないと、後でデータの紐付けに異常が生じる可能性があります。 詳細については、を参照してください [推奨事項と制限事項](../../configuration/using/about-custom-recipient-table.md) ページ。

1. が含まれる **拡張機能** ウィンドウで、生成するオプションのスキーマを選択します（使用可能なスキーマのリストは、Adobe Campaign プラットフォームにインストールされているモジュールによって異なります）。

   ![](assets/mapping_diffusion_wizard_4.png)

1. 「」をクリックします **保存** ボタンをクリックしてウィザードを閉じます。

   ウィザードでは、開始スキーマを使用して、新しいターゲットマッピングを機能させるために必要な他のすべてのスキーマを作成します。

   ![](assets/mapping_schema_list.png)

## ターゲットマッピングの使用 {#using-target-mapping}

配信のターゲットとして新しいスキーマを使用する方法は 2 つあります。

* マッピングに基づいて 1 つ以上の配信テンプレートを作成
* 以下に示すように、配信の作成時に、ターゲット選択時にマッピングを直接選択します。

![](assets/mapping_selection_ciblage.png)
