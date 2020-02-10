---
title: データの更新
seo-title: データの更新
description: データの更新
seo-description: null
page-status-flag: never-activated
uuid: 3a192934-215a-4a0a-a141-956b5c229f5b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: profile-management
discoiquuid: 1e196989-b8c1-473a-89c9-bbeb68b98419
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 51e4d72abf3a1f48700ca38566dbf06dd24594b8

---


# データの更新{#updating-data}

受信者のプロファイルにリンクされているデータは、手動または自動で更新できます。

## 自動更新の設定 {#setting-up-an-automatic-update}

自動更新は、ワークフローを使用して設定できます。詳しくは、[この節](../../workflow/using/update-data.md)を参照してください。

## 一括更新の実行 {#performing-a-mass-update}

To perform manual updates, right-click the selected recipient(s) to use the **[!UICONTROL Actions]** shortcut menu, or use the **[!UICONTROL Actions]** icon.

![](assets/s_ncs_user_action_icon.png)

更新には、一連の受信者の一括更新と、2 つのプロファイル間のデータ結合の 2 種類があります。各アクションについて、ウィザードに従って更新を設定できます。

### 一括更新 {#mass-update}

一括更新の場合は、を使用しま **[!UICONTROL Action > Mass update of selected lines...]**&#x200B;す。 ウィザードを使用して、更新を設定および実行することができます。

ウィザードの最初の手順では、更新するフィールドを指定します。

ウィザードの左側のセクションに、使用可能フィールドのリストが表示されます。Use the **[!UICONTROL Find]** field to run a search of these fields. **Enter** キーを押してリストを参照します。次に示すように、入力内容に一致するフィールド名が太字で表示されます。

更新するフィールドをダブルクリックすると、それらのフィールドがウィザードの右側のセクションに表示されます。

![](assets/s_ncs_user_update_wizard01_1.png)

In the event of an error, use the **[!UICONTROL Delete]** button to delete a field from the list of fields to be updated.

更新するプロファイルに適用する値を選択するか、入力します。

![](assets/s_ncs_user_update_wizard01_12.png)

You can click **[!UICONTROL Distribution of values]** to display the distribution of values of the selected field for the recipients present in the current folder (not only the recipients affected by the update).

![](assets/s_ncs_user_update_wizard01_2.png)

このウィンドウで値の配分を表示するためのフィルターを定義したり、現在のフォルダーを変更して別のフォルダーの値の配分を表示したりできます。これらは読み取り専用のアクションであり、定義する更新の設定に影響を与えることはありません。

![](assets/s_ncs_user_update_wizard01_3.png)

Close this window and click **[!UICONTROL Next]** to display the second update wizard step. In this step, you can launch the update by clicking **[!UICONTROL Start]**.

![](assets/s_ncs_user_update_wizard01_4.png)

更新の実行に関する情報がウィザードの上部セクションに表示されます。

The **[!UICONTROL Stop]** lets you cancel the update, but certain records might have been updated, and stopping the process will not cancel these updates. プログレスバーに操作の進捗状況が表示されます。

### データの結合 {#merge-data}

2つの受 **[!UICONTROL Merge selected lines...]** 信者プロファイルの結合を開始する場合に選択します。 オプションを選択する前に、結合するプロファイルを選択する必要があります。結合の設定および実行には、ウィザードを使用します。

ウィザードには、いずれかのソースプロファイルで入力された各フィールドについて取得する値が表示されます。If one or more fields in the profiles to be merged have different values, they are displayed in the **[!UICONTROL List of conflicts]** section. その場合、次の例に示すように、リストの下のラジオボタンを使用してデフォルトプロファイルを選択できます。

![](assets/s_ncs_user_merge_wizard01_1.png)

Click **[!UICONTROL Compute]** to display the result of your choice.

![](assets/s_ncs_user_merge_wizard01_2.png)

Check the **[!UICONTROL Result]** columns of both sections of the window, and click **[!UICONTROL Finish]** to run the merge.

## データのエクスポート {#exporting-data}

リストのコンテンツをエクスポートできます。エクスポートを設定して実行するには、以下の手順に従います。

1. エクスポートするレコードを選択します。
1. Right-click and select **[!UICONTROL Export...]**.

   ![](assets/s_ncs_user_export_list.png)

1. 次に、抽出するデータを選択します。デフォルトでは、表示されているすべての列が出力列に追加されます。

   ![](assets/s_ncs_user_export_list_start.png)

   For more on how to configure the export wizard, refer to [Export wizard](../../platform/using/exporting-data.md#export-wizard).

## サービスの購読登録 {#subscribing-to-a-service}

ほとんどの場合、受信者は専用のランディングページからニュースレターを購読します。詳しくは、[この節](../../delivery/using/managing-subscriptions.md)を参照してください。一方で、フィルターを適用した受信者のプロファイルを、手動でサービス（ニュースレターやバイラルサービス）に購読登録することもできます。手順は次のとおりです。

1. 購読登録する受信者を選択して、右クリックします。
1. 選択 **[!UICONTROL Actions > Subscribe selection to a service]**.

   ![](assets/s_ncs_user_selection_subscribe_service.png)

1. Select the desired service and click **[!UICONTROL Next]**:

   ![](assets/s_ncs_user_selection_subscribe_service_2.png)

   >[!NOTE]
   >
   >This editor lets you create a new service: click the **[!UICONTROL Create]** button.

1. 受信者にアク **[!UICONTROL Send a confirmation message]** セスできます。 このメッセージのコンテンツは、選択したサービスにリンクされた購読シナリオで設定できます。
1. Click the **[!UICONTROL Start]** button to run the subscription process.

   ![](assets/s_ncs_user_selection_subscribe_service_3.png)

ウィンドウの上部セクションで実行プロセスを監視できます。The **[!UICONTROL Stop]** button lets you stop the process. ただし、既に処理された受信者は購読登録されます。

このオプションのチェ **[!UICONTROL Do not keep a trace of this job in the database]** ックを外すと、このプロセスの情報を保存する実行フォルダーを選択（または作成）できます。

To check on the process, go to the **[!UICONTROL Subscriptions]** tab on the profiles of the recipients concerned by this operation, or to the **[!UICONTROL Subscriptions]** tab accessed via the **[!UICONTROL Profiles and Targets > Services and Subscriptions]** node.

![](assets/s_ncs_user_selection_subscribe_service_4.png)

>[!NOTE]
>
>情報サービスの作成と設定について詳しくは、[このページ](../../delivery/using/managing-subscriptions.md)を参照してください。

