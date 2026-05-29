---
product: campaign
title: ワークフローを使用したプロファイルリストの作成
description: ワークフローでプロファイルリストを作成する方法を説明します
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Workflows, Profiles
role: User
exl-id: 6b308299-4d07-4c9e-bd2f-a0860c41cf02
TQID: https://experienceleague.adobe.com/km2D2qnUAdgDCauLUYcWSC-J567twPEyvaZBsLDAOKA
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 214
ht-degree: 17%

---

# ワークフローを使用したプロファイルリストの作成{#creating-a-profile-list-with-a-workflow}


新しい受信者テーブルに基づいて&#x200B;**[!UICONTROL リスト]**&#x200B;型リストを作成するには、リストを生成するターゲティングワークフローを作成する必要があります。

Campaignのリストについて詳しくは、[この節](../../platform/using/creating-and-managing-lists.md#about-lists-in-adobe-campaign)を参照してください。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](../../platform/using/creating-and-managing-lists.md#create-list-in-a-wf-video)

ターゲティングワークフローを作成し、カスタム受信者テーブルで受信者を更新するには、次の手順に従います。

1. エクスプローラーの&#x200B;**[!UICONTROL プロファイルとターゲット/ジョブ/ターゲティングワークフロー]** ノードに移動します。
1. 新しいターゲティングワークフローを作成します。
1. **クエリ** アクティビティを配置し、その後&#x200B;**リスト更新** アクティビティを配置します。

   ![](assets/mapping_create_list_workflow01.png)

1. **クエリ** アクティビティをダブルクリックし、**[!UICONTROL クエリを編集]**&#x200B;をクリックして、新しい受信者テーブルのスキーマに基づいてターゲティングディメンションを選択します（この例では&#x200B;**個人**）。 「**[!UICONTROL 完了]**」をクリックして確定します。

   ![](assets/mapping_create_list_workflow03.png)

1. 「**リストの更新**」アクティビティをダブルクリックし、「必要に応じてリストを作成（計算名） **」ラジオボタンを選択します。**

   ![](assets/mapping_create_list_workflow02.png)

1. 新しいリストの作成フォルダーを選択します。
1. ワークフローを実行してリストを作成します。
1. **[!UICONTROL リスト更新]** アクティビティ中に選択したツリーのノードの結果を表示します。

   ダッシュボードでは、次に示すように、リストの基となるスキーマを指定します。

   ![](assets/mapping_list_view.png)
