---
product: campaign
title: ワークフローを使用したプロファイルリストの作成
description: ワークフローでプロファイルリストを作成する方法を説明します
feature: Workflows
exl-id: 6b308299-4d07-4c9e-bd2f-a0860c41cf02
source-git-commit: 8fa50d17a9ff36ccc310860ac93771590cfd76fd
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---

# ワークフローを使用したプロファイルリストの作成{#creating-a-profile-list-with-a-workflow}

![](../../assets/common.svg)

を作成するには、以下を実行します。 **[!UICONTROL リスト]** 新しい受信者テーブルに基づいて「リスト」と入力する場合は、リストを生成するターゲティングワークフローを作成する必要があります。

Campaign のリストについて詳しくは、 [この節](../../platform/using/creating-and-managing-lists.md#about-lists-in-adobe-campaign).

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](../../platform/using/creating-and-managing-lists.md#create-list-in-a-wf-video)

ターゲティングワークフローを作成し、カスタム受信者テーブルで受信者を更新するには、次の手順に従います。

1. 次に移動： **[!UICONTROL プロファイルとターゲット/ジョブ/ターゲティングワークフロー]** エクスプローラーのノード。
1. 新しいターゲティングワークフローを作成します。
1. 場所 a **クエリ** アクティビティの後に **リスト更新** アクティビティ。

   ![](assets/mapping_create_list_workflow01.png)

1. 次をダブルクリックします。 **クエリ** 「 」アクティビティに移動し、「 」をクリックします。 **[!UICONTROL クエリを編集]** 新しい受信者テーブルのスキーマに基づいてターゲティングディメンションを選択するには ( この例では： **個人**) をクリックします。 「**[!UICONTROL 完了]**」をクリックして確定します。

   ![](assets/mapping_create_list_workflow03.png)

1. 次をダブルクリックします。 **リスト更新** 「 」アクティビティで、 **[!UICONTROL 必要に応じてリストを作成（名前を自動生成）]** ラジオボタン。

   ![](assets/mapping_create_list_workflow02.png)

1. 新しいリストの作成フォルダーを選択します。
1. ワークフローを実行してリストを作成します。
1. 結果を、 **[!UICONTROL リスト更新]** アクティビティ。

   次に示すように、ダッシュボードには、リストの基になるスキーマが指定されます。

   ![](assets/mapping_list_view.png)
