---
title: ワークフローを使用したプロファイルリストの作成
seo-title: ワークフローを使用したプロファイルリストの作成
description: ワークフローを使用したプロファイルリストの作成
seo-description: null
page-status-flag: never-activated
uuid: a30f7217-fe82-4290-b1e6-e7a126a316c1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
discoiquuid: ba42c3cf-31fc-4fbc-b230-a2b3982328c5
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 681e6ec5fc9ed8c7e46af04f0ed62927b30e1b2e

---


# ワークフローを使用したプロファイルリストの作成{#creating-a-profile-list-with-a-workflow}

新しい受信者テー **[!UICONTROL List]** ブルに基づいてタイプリストを作成するには、リストを生成するターゲット設定ワークフローを作成する必要があります。 キャンペーンのリストの詳細については、この節を参 [照してください](../../platform/using/creating-and-managing-lists.md#about-lists-in-adobe-campaign)。

1. エクスプローラ **[!UICONTROL Profiles and Targets > Jobs > Targeting workflows]** ーのノードに移動します。
1. 新しいターゲティングワークフローを作成します。
1. 「 **Query** 」アクティビティを配置し、その後に「 **List」更新アクティビティを配置します** 。

   ![](assets/mapping_create_list_workflow01.png)

1. **Query** アクティビティをダブルクリックし **[!UICONTROL Edit the query]** 、をクリックして、新しい受信者テーブルのスキーマに基づいてターゲットディメンションを選択します(例：個 **人**)。 Click **[!UICONTROL Finish]** to confirm.

   ![](assets/mapping_create_list_workflow03.png)

1. 「 **List update** 」アクティビティをダブルクリックし、ラジオボタン **[!UICONTROL Create the list if necessary (Computed name)]** を選択します。

   ![](assets/mapping_create_list_workflow02.png)

1. 新しいリストの作成フォルダを選択します。
1. ワークフローを実行してリストを作成します。
1. アクティビティ中に選択したツリーのノードに結果を表示し **[!UICONTROL List update]** ます。

   ダッシュボードでは、次に示すように、リストの基になるスキーマが指定されます。

   ![](assets/mapping_list_view.png)

>[!NOTE]
>
>「受信者のリストの作成」 [ビデオも参照できます](https://docs.adobe.com/content/help/en/campaign-learn/campaign-classic-tutorials/getting-started/creating-a-list-of-recipients.html) 。

