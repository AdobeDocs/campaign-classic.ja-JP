---
title: ワークフローを使用したプロファイルリストの作成
description: ワークフローでプロファイルリストを作成する方法を説明します
page-status-flag: never-activated
uuid: a30f7217-fe82-4290-b1e6-e7a126a316c1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
discoiquuid: ba42c3cf-31fc-4fbc-b230-a2b3982328c5
translation-type: tm+mt
source-git-commit: c2c0609619e0cc81444d089850add6dec5de93fd
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---


# ワークフローを使用したプロファイルリストの作成{#creating-a-profile-list-with-a-workflow}

新しいリストテーブルに基づいて **** リストタイプの受信者を作成するには、リストを生成するターゲットワークフローを作成する必要があります。

キャンペーンのリストの詳細については、 [この節を参照してください](../../platform/using/creating-and-managing-lists.md#about-lists-in-adobe-campaign)。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](../../platform/using/creating-and-managing-lists.md#create-list-in-a-wf-video)

ターゲットワークフローを作成し、カスタム受信者テーブルの受信者を更新するには、次の手順に従います。

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


