---
product: campaign
title: ワークフローを使用したプロファイルリストの作成
description: ワークフローでプロファイルリストを作成する方法を説明します
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
exl-id: 6b308299-4d07-4c9e-bd2f-a0860c41cf02
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---

# ワークフローを使用したプロファイルリストの作成{#creating-a-profile-list-with-a-workflow}

![](../../assets/v7-only.svg)

新しい受信者テーブルに基づいて **[!UICONTROL リスト]** タイプのリストを作成するには、リストを生成するターゲティングワークフローを作成する必要があります。

Campaign のリストの詳細については、[ この節 ](../../platform/using/creating-and-managing-lists.md#about-lists-in-adobe-campaign) を参照してください。

![](assets/do-not-localize/how-to-video.png) [動画でこの機能を確認する](../../platform/using/creating-and-managing-lists.md#create-list-in-a-wf-video)

ターゲティングワークフローを作成し、カスタム受信者テーブルの受信者を更新するには、次の手順に従います。

1. エクスプローラーの **[!UICONTROL プロファイルとターゲット/ジョブ/ターゲティングワークフロー]** ノードに移動します。
1. 新しいターゲティングワークフローを作成します。
1. **クエリ** アクティビティを追加し、その後に **リスト更新** アクティビティを追加します。

   ![](assets/mapping_create_list_workflow01.png)

1. 「**クエリ**」アクティビティをダブルクリックし、「**[!UICONTROL クエリを編集]**」をクリックして、新しい受信者テーブルのスキーマに基づいてターゲティングディメンションを選択します ( この例では&#x200B;**個々の**)。 「**[!UICONTROL 完了]**」をクリックして確定します。

   ![](assets/mapping_create_list_workflow03.png)

1. 「**リストの更新**」アクティビティをダブルクリックし、「**[!UICONTROL 必要に応じてリストを作成（計算済みの名前）]**」ラジオボタンを選択します。

   ![](assets/mapping_create_list_workflow02.png)

1. 新しいリストの作成フォルダーを選択します。
1. ワークフローを実行して、リストを作成します。
1. **[!UICONTROL リスト更新]** アクティビティ中に選択したツリーのノードで結果を表示します。

   次に示すように、ダッシュボードには、リストの基になるスキーマが指定されます。

   ![](assets/mapping_list_view.png)
