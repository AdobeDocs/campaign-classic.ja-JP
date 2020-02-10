---
title: 列挙の管理
seo-title: 列挙の管理
description: 列挙の管理
seo-description: null
page-status-flag: never-activated
uuid: 23ad4cae-237f-48e5-b111-cfe88cf0b864
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: administration-basics
discoiquuid: 7674c856-2b64-4a85-9ffa-3e14a142028e
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# 列挙の管理{#managing-enumerations}

## 列挙について {#about-enumerations}

列挙（「定義済みリスト」とも呼ばれます）とは、特定のフィールドへの入力候補としてシステムによって表示される値のリストです。列挙を利用することでフィールドの値を統一することができ、データ入力時やクエリでの利用に便利です。

値のリストはドロップダウンリストとして表示され、値を選択すると、その値がフィールドに入力されます。また、このドロップダウンリストには予測入力機能があり、オペレーターが最初の数文字を入力すると続きが自動的に補完されます。

コンソールの一部のフィールドは、この種の列挙を使用して定義されています。フィールドに値を直接入力してリストに追加できるタイプの列挙は、「オープン」な列挙と呼ばれます。

## 値に対するアクセス {#access-to-values}

The values for this type of field are defined and overall administration of these fields (adding/deleting a value) is performed via the **[!UICONTROL Administration > Platform > Enumerations]** node of the tree.

![](assets/s_ncs_user_itemized_list_node.png)

* 上部セクションには、定義済みリストが設定されているフィールドのリストが表示されます。
* 下部セクションには、値の選択肢のリストが表示されます。これらの値は、そのフィールドを使用するエディター内にも重複して表示されます。

   ![](assets/s_ncs_user_itemized_list_values.png)

   To create a new enumeration value, click **[!UICONTROL Add]**.

   ![](assets/s_ncs_user_itemized_list.png)

   If the **[!UICONTROL Open]** option is selected, the user can add a new itemized list value directly in the corresponding field. 値を作成してよいかどうか確かめる確認メッセージが表示されます。

   ![](assets/s_ncs_user_itemized_list_new_value.png)

* If the **[!UICONTROL Closed]** option is selected, users will not be able to create new values, but merely choose from the values available.

## データの標準化 {#standardizing-data}

### エイリアスクレンジングについて {#about-alias-cleansing}

定義済みリストフィールドには、列挙に含まれていない値を入力できます。それらの値は、そのまま格納することも、クレンジング処理を適用することもできます。

>[!CAUTION]
>
>データクレンジングは、データベース内のデータに大きな影響を及ぼす重大なプロセスです。Adobe Campaign の大規模なデータ更新が実行され、場合によっては一部の値が削除される結果になることもあります。したがって、この操作はエキスパートユーザー向け機能として予約されています。

入力値は次のいずれかの方法で使用できます。

* Added to the itemized list values: in this case the **[!UICONTROL Open]** option must be selected,
* または、対応するエイリアスに自動的に置き換えられます。この場合、このケースは項目別リストのタブで定 **[!UICONTROL Alias]** 義する必要があります。
* エイリアスのリストに格納：エイリアスの割り当ては後で実行します。

   >[!NOTE]
   >
   >If you need to use data cleansing capabilities, select the **[!UICONTROL Alias cleansing]** option in the itemized list.

### エイリアスの利用 {#using-aliases}

The option **[!UICONTROL Alias cleansing]** makes it possible to use aliases for the selected itemized list. When this option is selected, the **[!UICONTROL Alias]** tab is displayed at the bottom of the window.

![](assets/s_ncs_user_itemized_list_alias_option.png)

#### エイリアスの作成 {#creating-an-alias}

To create an alias, click **[!UICONTROL Add]**.

![](assets/s_ncs_user_itemized_list_alias_create.png)

変換元となるエイリアスと、適用する値を入力し、「**[!UICONTROL Ok]**」をクリックします。

![](assets/s_ncs_user_itemized_list_alias_create_2.png)

この操作を確定する前にパラメーターを確認します。

>[!CAUTION]
>
>この段階が完了すると、以前に入力されていた値は置き換えられます。以前の値を復元することはできません。

![](assets/s_ncs_user_itemized_list_alias_create_3.png)

その後、ユーザーが（Adobe Campaign コンソールまたはフォームの）会社フィールドに **NEILSEN** と入力すると、**NIELSEN Ltd** という値に自動置換されます。値の置換は&#x200B;**エイリアスクレンジング**&#x200B;ワークフローによって実行されます。データクレンジ [ングの実行を参照](#running-data-cleansing)。

![](assets/s_ncs_user_itemized_list_alias_use.png)

#### 値のエイリアスへの変換 {#converting-values-into-aliases}

To convert an enumeration value into an alias, right-click in the list of values and choose **[!UICONTROL Convert values into aliases...]**.

![](assets/s_ncs_user_itemized_list_alias_detail.png)

Choose the values you want to convert and click **[!UICONTROL Next]**.

![](assets/s_ncs_user_itemized_list_alias_transform.png)

Click **[!UICONTROL Start]** to run the conversion.

![](assets/s_ncs_user_itemized_list_alias_detail1.png)

実行が完了すると、エイリアスのリストに新しいエイリアスが追加されます。

![](assets/s_ncs_user_itemized_list_alias_detail2.png)

#### エイリアスのヒット数の取得 {#retrieving-alias-hits}

ユーザーによって入力された値をエイリアスに変換することもできます。In effect, when the user enters a value that is not included in the itemized list, the value is stored in the **[!UICONTROL Alias]** tab.

入力値は&#x200B;**エイリアスクレンジング**&#x200B;テクニカルワークフローによって毎晩復元され、定義済みリストに反映されます。実行中のデータク [レンジングを参照](#running-data-cleansing)

If necessary, the **[!UICONTROL Hits]** column can display the number of times this value was entered. ただし、この値を計算するために長い時間と大量のメモリが必要となる場合があります。この詳細については、「エントリオカレンスの [計算」を参照してくださ](#calculating-entry-occurrences)い。

### データクレンジングの実行 {#running-data-cleansing}

Data cleansing is performed by the **[!UICONTROL Alias cleansing]** technical workflow. 列挙用に定義された設定は、実行時に適用されます。エイリアスのクレンジ [ングワークフローを参照してくださ](#alias-cleansing-workflow)い。

Cleansing can be triggered via the **[!UICONTROL Cleanse values...]** link.

![](assets/s_ncs_user_itemized_list_alias_start_normalize.png)

The **[!UICONTROL Advanced parameters...]** link lets you set the date starting from which collected values are taken into account.

![](assets/s_ncs_user_itemized_list_alias_normalize.png)

Click the **[!UICONTROL Start]** button to run data cleansing.

#### 入力の発生回数の計算 {#calculating-entry-occurrences}

The **[!UICONTROL Alias]** sub-tab of an itemized list can display the number of occurrences of an alias among all the values entered. This information is an estimate and will be displayed in the **[!UICONTROL Hits]** column.

>[!CAUTION]
>
>エイリアスの入力回数を計算するには、長い時間が必要となる場合があります。この機能を使用する際には注意してください。

You can run hit calculation manually via the **[!UICONTROL Cleanse values...]** link. To do this, click the **[!UICONTROL Advanced parameters...]** link and select the desired option(s).

![](assets/s_ncs_user_itemized_list_alias_hits.png)

* **[!UICONTROL Update the number of alias hits]**:これにより、入力した日付に基づいて既に計算済みのヒットを更新できます。
* **[!UICONTROL Recalculate the number of alias hits from the start]**:adobe Campaignプラットフォーム全体で計算を実行できます。

指定した期間について計算を自動実行する（例：週に 1 回）ための専用ワークフローを作成することもできます。

To do this, create a copy of the **[!UICONTROL Alias cleansing]** workflow, change the scheduler and use the following settings in the **[!UICONTROL Enumeration value cleansing]** activity:

* **-updateHits**：エイリアスのヒット数を更新する場合
* **-updateHits:full**：エイリアスのヒット数をすべて再計算する場合

#### エイリアスクレンジングワークフロー {#alias-cleansing-workflow}

**エイリアスクレンジング**&#x200B;ワークフローは、列挙値のクレンジングを実行します。デフォルトでは毎日実行されます。

ノードを介してアクセスさ **[!UICONTROL Administration > Production > Technical workflows]** れます。

![](assets/s_ncs_user_itemized_list_alias_wf.png)

