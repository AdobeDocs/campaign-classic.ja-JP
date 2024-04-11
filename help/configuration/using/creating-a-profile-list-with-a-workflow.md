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
ht-degree: 15%

---

# ワークフローを使用したプロファイルリストの作成{#creating-a-profile-list-with-a-workflow}


を作成するには **[!UICONTROL リスト]** タイプ list 新しい受信者テーブルに基づいて、リストを生成するターゲティングワークフローを作成する必要があります。

Campaign のリストについて詳しくは、次を参照してください。 [この節](../../platform/using/creating-and-managing-lists.md#about-lists-in-adobe-campaign).

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](../../platform/using/creating-and-managing-lists.md#create-list-in-a-wf-video)

ターゲティングワークフローを作成し、カスタム受信者テーブルで受信者を更新するには、次の手順に従います。

1. に移動します **[!UICONTROL プロファイルとターゲット/ジョブ/ターゲティングワークフロー]** エクスプローラーのノード。
1. 新しいターゲティングワークフローを作成します。
1. 場所 a **クエリ** アクティビティの後に **リストの更新** アクティビティ。

   ![](assets/mapping_create_list_workflow01.png)

1. をダブルクリックします **クエリ** アクティビティを選択してから、 **[!UICONTROL クエリを編集します]** 新しい受信者テーブルのスキーマに基づいてターゲティングディメンションを選択するには、次の例を参照してください。 **個人**）に設定します。 「**[!UICONTROL 完了]**」をクリックして確定します。

   ![](assets/mapping_create_list_workflow03.png)

1. をダブルクリックします **リストの更新** アクティビティを選択してから、 **[!UICONTROL 必要に応じてリストを作成（名前を自動生成）]** ラジオボタン。

   ![](assets/mapping_create_list_workflow02.png)

1. 新しいリストの作成フォルダーを選択します。
1. ワークフローを実行してリストを作成します。
1. で選択したツリーのノードに結果を表示します。 **[!UICONTROL リストの更新]** アクティビティ。

   ダッシュボードは、次に示すように、リストの基になるスキーマを指定します。

   ![](assets/mapping_list_view.png)
