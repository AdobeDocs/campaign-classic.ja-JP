---
product: campaign
title: ターゲットマッピング
description: ターゲットマッピングの作成方法を説明します
feature: Application Settings
badge-v7: label="v7" type="Informative" tooltip="Campaign Classicv7 に適用"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 38333669-5598-4811-a121-b677c1413f56
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---

# ターゲットマッピング{#target-mapping}



ターゲットマッピングの作成は、次の 2 つの場合に必要です。

* Adobe Campaignで提供される受信者テーブル以外の受信者テーブルを使用する場合、
* 「ターゲットマッピング」画面の標準ターゲティングディメンションとは異なるフィルタリングディメンションを設定する場合。

ターゲットマッピング作成ウィザードは、カスタムテーブルを使用するために必要なすべてのスキーマを作成するのに役立ちます。

## カスタムテーブルにリンクされたスキーマの作成と設定 {#creating-and-configuring-schemas-linked-to-the-custom-table}

Adobe Campaignが新しい受信者データスキーマで動作するには、ターゲットマッピングを作成する前に、いくつかの設定が必要です。

それには、次の手順に従います。

1. 使用するカスタムテーブルのフィールドを統合する新しいデータスキーマを作成します。

   詳しくは、 [スキーマ参照 (xtk:srcSchema)](../../configuration/using/about-schema-reference.md).

   この例では、ID、名、姓、E メールアドレス、携帯電話番号の各フィールドを含む非常にシンプルなテーブルで顧客スキーマを作成します。 その目的は、このテーブルに格納された個人に E メールまたは SMS アラートを送信できるようにすることです。

   スキーマの例 (cus:individual)

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

1. =&quot;true&quot;属性を使用して、スキーマを外部ビューとして宣言します。 参照： [ビュー属性](../../configuration/using/schema-characteristics.md#the-view-attribute).

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

1. 次をクリック： **[!UICONTROL 管理/キャンペーン管理/ターゲットマッピング]** ノード。
1. 次をクリック： **新規** ボタンをクリックして、ターゲットマッピング作成ウィザードを開きます。
1. 次を入力します。 **ラベル** フィールドに値を入力し、 **ターゲティングディメンション** フィールドに入力します。

   ![](assets/mapping_diffusion_wizard_1.png)

1. Adobe Analytics の **アドレスフォームを編集** ウィンドウで、様々な配信アドレスと一致するスキーマのフィールドを選択します。 ここで、 **@email** および **@mobile** フィールド。

   ![](assets/mapping_diffusion_wizard_2.png)

1. 次の場合： **ストレージ** ウィンドウで、 **拡張スキーマのサフィックス** 新しいスキーマをAdobe Campaignが提供する標準のスキーマと区別するためのフィールド。

   クリック **[!UICONTROL 新しい追加フィールドを定義する]** をクリックして、配信でターゲットにするディメンションを選択します。

   デフォルトでは、除外管理はメッセージと同じテーブルに格納されます。

   次を確認します。 **トラッキング用のストレージスキーマを生成** 」ボックスをオンにします。

   ![](assets/mapping_diffusion_wizard_3.png)

   >[!IMPORTANT]
   >
   >Adobe Campaignは、同じ broadlog スキーマや trackinglog スキーマにリンクされた、複数の受信者スキーマ（ターゲティングスキーマと呼ばれる）をサポートしていません。 それ以外の場合は、後でデータの紐付けが異常になる可能性があります。 詳しくは、 [レコメンデーションと制限事項](../../configuration/using/about-custom-recipient-table.md) ページに貼り付けます。

1. Adobe Analytics の **拡張機能** ウィンドウで、生成するオプションのスキーマを選択します ( 使用可能なスキーマのリストは、Adobe Campaignプラットフォームにインストールされているモジュールによって異なります )。

   ![](assets/mapping_diffusion_wizard_4.png)

1. 次をクリック： **保存** ボタンをクリックしてウィザードを閉じます。

   ウィザードでは、開始スキーマを使用して、新しいターゲットマッピングを機能させるために必要なその他すべてのスキーマを作成します。

   ![](assets/mapping_schema_list.png)

## ターゲットマッピングの使用 {#using-target-mapping}

新しいスキーマを配信のターゲットとして使用する方法は 2 つあります。

* マッピングに基づいて 1 つ以上の配信テンプレートを作成
* 配信の作成時に、ターゲットの選択時に直接マッピングを選択します（下図を参照）。

![](assets/mapping_selection_ciblage.png)
