---
product: campaign
title: ワークフローを使用したプロファイルリストの作成
description: ワークフローでプロファイルリストを作成する方法を説明します
audience: configuration
content-type: reference
topic-tags: use-a-custom-recipient-table
exl-id: 6b308299-4d07-4c9e-bd2f-a0860c41cf02
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---

# ワークフローを使用したプロファイルリストの作成{#creating-a-profile-list-with-a-workflow}

新しい受信者テーブルに基づいて&#x200B;**[!UICONTROL リスト]**&#x200B;タイプのリストを作成するには、リストを生成するターゲティングワークフローを作成する必要があります。

Campaignのリストの詳細については、[この節](../../platform/using/creating-and-managing-lists.md#about-lists-in-adobe-campaign)を参照してください。

![](assets/do-not-localize/how-to-video.png) [この機能をビデオで確認](../../platform/using/creating-and-managing-lists.md#create-list-in-a-wf-video)

ターゲティングワークフローを作成し、カスタム受信者テーブルの受信者を更新するには、次の手順に従います。

1. エクスプローラーの&#x200B;**[!UICONTROL プロファイルとターゲット/ジョブ/ターゲティングワークフロー]**&#x200B;ノードに移動します。
1. 新しいターゲティングワークフローを作成します。
1. **クエリ**&#x200B;アクティビティを配置し、その後に&#x200B;**リスト更新**&#x200B;アクティビティを配置します。

   ![](assets/mapping_create_list_workflow01.png)

1. 「**クエリ**」アクティビティをダブルクリックし、「**[!UICONTROL クエリを編集]**」をクリックして、新しい受信者テーブルのスキーマに基づいてターゲティングディメンションを選択します(この例では、**個別**)。 「**[!UICONTROL 完了]**」をクリックして確定します。

   ![](assets/mapping_create_list_workflow03.png)

1. **リスト更新**&#x200B;アクティビティをダブルクリックし、必要に応じて&#x200B;**[!UICONTROL リストを作成]**&#x200B;ラジオボタンを選択します。

   ![](assets/mapping_create_list_workflow02.png)

1. 新しいリストの作成フォルダーを選択します。
1. ワークフローを実行してリストを作成します。
1. **[!UICONTROL リスト更新]**&#x200B;アクティビティ中に選択したツリーのノードで結果を表示します。

   次に示すように、ダッシュボードには、リストの基になるスキーマが指定されます。

   ![](assets/mapping_list_view.png)
