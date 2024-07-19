---
product: campaign
title: ワークフローを使用したプロファイルリストの作成
description: ワークフローでプロファイルリストを作成する方法を説明します
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Workflows, Profiles
role: User
exl-id: 6b308299-4d07-4c9e-bd2f-a0860c41cf02
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 17%

---

# ワークフローを使用したプロファイルリストの作成{#creating-a-profile-list-with-a-workflow}


新しい受信者テーブルに基づいて **[!UICONTROL リスト]** タイプのリストを作成するには、リストを生成するターゲティングワークフローを作成する必要があります。

Campaign のリストについて詳しくは、[ この節 ](../../platform/using/creating-and-managing-lists.md#about-lists-in-adobe-campaign) を参照してください。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](../../platform/using/creating-and-managing-lists.md#create-list-in-a-wf-video)

ターゲティングワークフローを作成し、カスタム受信者テーブルで受信者を更新するには、次の手順に従います。

1. エクスプローラーの **[!UICONTROL プロファイルとターゲット/ジョブ/ターゲティングワークフロー]** ノードに移動します。
1. 新しいターゲティングワークフローを作成します。
1. **クエリ** アクティビティを配置し、その後に **リスト更新** アクティビティを配置します。

   ![](assets/mapping_create_list_workflow01.png)

1. 「**クエリ**」アクティビティをダブルクリックし、「**[!UICONTROL クエリを編集]**」をクリックして、新しい受信者テーブルのスキーマに基づいてターゲティングディメンションを選択します（この例では、「**個人**」）。 「**[!UICONTROL 完了]**」をクリックして確定します。

   ![](assets/mapping_create_list_workflow03.png)

1. **リスト更新** アクティビティをダブルクリックし、「**[!UICONTROL 必要に応じてリストを作成（名前を自動生成）]**」ラジオボタンを選択します。

   ![](assets/mapping_create_list_workflow02.png)

1. 新しいリストの作成フォルダーを選択します。
1. ワークフローを実行してリストを作成します。
1. **[!UICONTROL リスト更新]** アクティビティで選択したツリーのノードに結果を表示します。

   ダッシュボードは、次に示すように、リストの基になるスキーマを指定します。

   ![](assets/mapping_list_view.png)
