---
title: '"使用例：条件によるシードアドレスの選択"'
seo-title: '"使用例：条件によるシードアドレスの選択"'
description: '"使用例：条件によるシードアドレスの選択"'
seo-description: null
page-status-flag: never-activated
uuid: 6af39893-6ef3-4204-8b53-0c16e35bac8f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: using-seed-addresses
discoiquuid: fa8aab62-e182-4388-aa23-c255b0dbd42e
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 209ac4d81d2d27c264ee6b288bcb7fcb1900ffc5

---


# 使用例：条件によるシードアドレスの選択{#use-case-selecting-seed-addresses-on-criteria}

In the framework of a delivery or a campaign, the **[!UICONTROL Edit the dynamic condition...]** link lets you choose seed addresses based on specific selection criteria.

この使用例では、**My online library** というサイトが、顧客の読み物の好みに応じてニュースレターのコンテンツをパーソナライズするとします。

配信責任者は、警察を題材とする小説を購入した会員向けのニュースレターを、購買部門と共同で作成しました。

配信責任者は、完成したニュースレターを購買部門の協力者にも読んでもらえるよう、シードアドレスとして購買部門のメンバーを配信先に追加することにしました。このような場合、動的条件を使用すると、アドレスの設定や更新作業の手間を省くことができます。

動的条件を使用するには、次の条件が揃っている必要があります。

* 配信の送信準備ができていること。
* 使用するシードアドレスが、共通の値を持っていること。その値は、Adobe Campaign にあらかじめ存在するフィールドの値でかまいません。この例では、すべてのシードアドレスの「部門」フィールドに「購買」という値が含まれるものとします。これは、Adobe Campaign にデフォルトで用意されているフィールドではありません。

## 手順 1 - 配信の作成 {#step-1---creating-a-delivery}

配信の作成手順について詳しくは、「電子メール配信の [作成」の節を参照してください](../../delivery/using/creating-an-email-delivery.md) 。

この例では、配信責任者がニュースレターを作成し、受信者を選択します。

![](assets/dlv_seeds_usecase_01.png)

## 手順 2 - 共通値の作成 {#step-2---creating-a-common-value}

シードアドレス間に共通する値（この例では「部門」フィールドの「購買」）を作成するには、まず、使用するシードアドレスの&#x200B;**データスキーマ**&#x200B;を拡張し、スキーマに関連付けられた入力フォームを編集する必要があります。

### データスキーマの拡張 {#extending-the-data-schema}

スキーマの拡張について詳しくは、[設定ガイド](../../configuration/using/data-schemas.md)を参照してください。

1. ノードで、 **[!UICONTROL Administration > Configuration > Data schemas]** アイコンをクリック **[!UICONTROL New]** します。
1. ウィンドウ **[!UICONTROL Creation of a data schema]** で、オプションを選択 **[!UICONTROL Extension of a schema]** し、をクリックしま **[!UICONTROL Next]**&#x200B;す。

   ![](assets/dlv_seeds_usecase_09.png)

1. ソーススキーマ **[!UICONTROL Seed addresses]** を選択し、「 **doc** 」と入力してをク **[!UICONTROL Namespace]** リックしま **[!UICONTROL Ok]**&#x200B;す。

   ![](assets/dlv_seeds_usecase_10.png)

1. クリック **[!UICONTROL Save]**.
1. 次に示すコードをコピーし、スキーマ編集ウィンドウで、下のスクリーンショットの場所に貼り付けます。

   ```
     <element name="common">
       <element label="Recipient" name="custom_nms_recipient">
         <attribute label="Department" length="80" name="workField" template="nms:recipient:recipient/@company"
                    type="string" userEnum="workField"/>
       </element>
     </element>
   ```

   ![](assets/dlv_seeds_usecase_20.png)

   次に、次の行をコピーして要素の下に貼り付け **[!UICONTROL Seed to insert in the export files]** ます。

   ```
       <element aggregate="doc:seedMember:common">
     </element>
   ```

   ![](assets/dlv_seeds_usecase_29.png)

   In this case, you are specifying that a new enumeration named **[!UICONTROL Department]** has been created in the seed address table, and it is based on the standard **[!UICONTROL @company]** enumeration template (labeled under the name **Company** in the seed address form).

1. クリック **[!UICONTROL Save]**.
1. メニューで、 **[!UICONTROL Tools > Advanced]** オプションを選択 **[!UICONTROL Update database structure]** します。

   ![](assets/dlv_seeds_usecase_12.png)

1. When the update wizard is displayed, click the **[!UICONTROL Next]** button to access the Edit tables window: changes carried out in the seed address data schema require a structure update.

   ![](assets/dlv_seeds_usecase_13.png)

1. ウィザードの指示に従って、更新を実行するページが表示されるまで操作を進めます。ボタンをクリッ **[!UICONTROL Start]** クします。

   ![](assets/dlv_seeds_usecase_14.png)

   更新が完了したら、ウィザードを閉じます。

1. Adobe Campaign との接続を一旦切断し、再接続します。これで、シードアドレスのデータスキーマに加えた変更が有効になります。In order for them to be visible from the seed address screen, you must update the associated **[!UICONTROL Input form]**. 「入力フォーム [の更新」の節を参照](#updating-the-input-form) 。

#### リンクされたテーブルに基づくデータスキーマの拡張 {#extending-the-data-schema-from-a-linked-table}

シードアドレスのデータスキーマでは、受信者データスキーマ「受信者」（nms）にリンクされたテーブル内の値を使用できます。

For example, the user would like to integrate the **[!UICONTROL Internet Extension]** found in the **[!UICONTROL Country]** table that is linked to the recipients schema.

![](assets/dlv_seeds_usecase_06.png)

その場合、の節で説明されている方法で、シードアドレスのデータスキーマを拡張する必要があります。ただし、**手順 4** では次のコードを組み込みます。

```
<element name="country">
      <attribute label="Internet Extension" length="2" name="iana" type="string"/>
      <attribute label="Country ISO" length="2" name="countryIsoA2" type="string"/>
    </element>
```

![](assets/dlv_seeds_usecase_11.png)

この記述は次のことを示しています。

* that the user wants to create a new element named **[!UICONTROL Internet Extension]**,
* that this element comes from the **[!UICONTROL Country]** table.

>[!CAUTION]
>
>リンクされたテーブル名には、そのリンク先テーブルの **xpath-dst** を指定する必要があります。
>
>This can be found in the **[!UICONTROL Country]** element in the recipients table.

![](assets/dlv_seeds_usecase_07.png)

The user can then follow from **step 5** of the section, and update the **[!UICONTROL Input form]** of the seed addresses.

「入力フォーム [の更新」の節を参照](#updating-the-input-form) 。

#### 入力フォームの更新 {#updating-the-input-form}

1. ノードで、 **[!UICONTROL Administration > Configuration > Input forms]** 入力フォームのシードアドレスを探します。

   ![](assets/dlv_seeds_usecase_19.png)

1. Edit the form and insert the following line in the **[!UICONTROL Recipient]** container.

   ```
   <input xpath="@workField"/>
   ```

   ![](assets/dlv_seeds_usecase_21.png)

1. 変更を保存します。
1. いずれかのシードアドレスを開きます。フィールド **[!UICONTROL Department]** がテーブルに表示 **[!UICONTROL Recipient]** されます。

   ![](assets/dlv_seeds_usecase_22.png)

1. Edit the seed addresses that you want to use for the delivery and enter **Purchasing** as the value in the **[!UICONTROL Department]** field.

## 手順 3 - 条件の定義 {#step-3---defining-the-condition}

配信のシードアドレスに動的条件を指定できます。手順は次のとおりです。

1. 配信を開きます。

   ![](assets/dlv_seeds_usecase_01.png)

1. リンクをクリ **[!UICONTROL To]** ックし、タブをク **[!UICONTROL Seed addresses]** リックしてリンクにアクセス **[!UICONTROL Edit the dynamic condition...]** します。

   ![](assets/dlv_seeds_usecase_02.png)

1. 目的に合ったシードアドレスを抽出するための式を選択します。ここで、ユーザーが式を選 **[!UICONTROL Department (@workField)]** 択します。

   ![](assets/dlv_seeds_usecase_03.png)

1. 使用する値を選択します。この例の場合は、ドロップダウンリストから「**購買**」という部門名を選択します。

   ![](assets/dlv_seeds_usecase_17.png)

   >[!NOTE]
   >
   >先ほど作成したスキーマ拡張は&#x200B;**受信者**&#x200B;スキーマに基づいており、上図の画面に表示されている値は、**受信者**&#x200B;スキーマの列挙値に基づくものです。

1. クリック **[!UICONTROL Ok]**.

   The query is displayed in the **[!UICONTROL Select target]** window.

   ![](assets/dlv_seeds_usecase_04.png)

1. 「**[!UICONTROL Ok]**」をクリックして、クエリを承認します。
1. Analyze your delivery then click on the **[!UICONTROL Delivery]** tab to access the delivery logs.

   購買部門のシードアドレスは、受信者や他のシードアドレスと同じように、配信待ちとして表示されます。

   ![](assets/dlv_seeds_usecase_05.png)

1. Click the **[!UICONTROL Send]** button to start the delivery.

   購買部門のメンバーはこの配信のシードアドレスに含まれているので、購買部門の各メンバーの E メール受信ボックスにも配信が届きます。

   ![](assets/dlv_seeds_usecase_18.png)
