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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 22%

---


# ワークフローを使用したプロファイルリストの作成{#creating-a-profile-list-with-a-workflow}

新しいリストテーブルに基づいて **** リストタイプの受信者を作成するには、リストを生成するターゲットワークフローを作成する必要があります。 キャンペーンのリストの詳細については、 [この節を参照してください](../../platform/using/creating-and-managing-lists.md#about-lists-in-adobe-campaign)。

1. エクスプローラーの **[!UICONTROL プロファイルとターゲット/ジョブ/ワークフローのターゲット設定]** (Targeting Jobs)ノードに移動します。
1. 新しいターゲティングワークフローを作成します。
1. **クエリ** アクティビティを配置し、その後に **リスト更新** アクティビティを追加します。

   ![](assets/mapping_create_list_workflow01.png)

1. クエリ **アクティビティを重複クリックし、「** クエリの **** 編集」をクリックして、新しい受信者テーブルのスキーマに基づいてターゲティングディメンションを選択します(例： **個人**)。 「**[!UICONTROL 完了]**」をクリックして確定します。

   ![](assets/mapping_create_list_workflow03.png)

1. 重複で **リスト更新** アクティビティをクリックし、「必要に応じてリストを **[!UICONTROL 作成」（計算済み名）ラジオボタンを選択します]** 。

   ![](assets/mapping_create_list_workflow02.png)

1. 新しいリストの作成フォルダーを選択します。
1. ワークフローを実行してリストを作成します。
1. 表示の更新 **[!UICONTROL アクティビティで選択したツリーのノードに結果を]** リストします。

   ダッシュボードは、次に示すように、リストの基になるスキーマを指定します。

   ![](assets/mapping_list_view.png)

>[!NOTE]
>
>また、受信者のリストの [作成のビデオを参照することもできます](https://docs.adobe.com/content/help/ja-JP/campaign-classic-learn/tutorials/getting-started/creating-a-list-of-recipients.html) 。

