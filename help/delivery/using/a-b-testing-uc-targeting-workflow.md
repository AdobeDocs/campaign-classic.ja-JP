---
product: campaign
title: ターゲティングワークフローの作成
description: 専用のユースケースを通じて A/B テストを実行する方法を学ぶ
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: A/B Testing
role: User
exl-id: aa21fa33-aef9-484a-b454-0cd5a6868a98
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 100%

---

# A/B テスト：ターゲティングワークフローを作成 {#step-1--creating-a-targeting-workflow}

キャンペーンの「**[!UICONTROL ターゲティングとワークフロー]**」タブでワークフローを作成する必要があります。このワークフローは、1 つの「**[!UICONTROL クエリ]**」アクティビティ、2 つの「**[!UICONTROL メール配信]**」アクティビティとリンクした 1 つの「**[!UICONTROL 分割]**」アクティビティ、1 つの「**[!UICONTROL 待機]**」アクティビティ、1 つの「**[!UICONTROL JavaScript コード]**」アクティビティ、1 つの「**[!UICONTROL 配信]**」アクティビティから構成されます。

1. まだ作成していない場合は、キャンペーンを作成します（詳しくは、[この節](../../campaign/using/setting-up-marketing-campaigns.md#creating-a-campaign)を参照してください）。

   ![](assets/use_case_abtesting_targetwkfl_001.png)

1. 「**[!UICONTROL ターゲティングとワークフロー]**」タブに移動します。

   ![](assets/use_case_abtesting_targetwkfl_002.png)

1. 既存のワークフローのラベルを変更するか、「**[!UICONTROL 追加]**」をクリックして新しいラベルを作成します（詳しくは、[この節](../../campaign/using/marketing-campaign-deliveries.md#selecting-the-target-population)を参照してください）。

   ![](assets/use_case_abtesting_targetwkfl_003.png)

1. マウスを使用してワークフローダイアグラムにアクティビティをドラッグ＆ドロップします。対象となるアクティビティには、1 つの「**[!UICONTROL クエリ]**」アクティビティ（「**[!UICONTROL ターゲット]**」タブ）、1 つの「**[!UICONTROL 分割]**」アクティビティ（「**[!UICONTROL ターゲット]**」タブ）、2 つの「**[!UICONTROL メール配信]**」アクティビティ（「**[!UICONTROL 配信]**」タブ）、1 つの「**[!UICONTROL 待機]**」アクティビティ（「**[!UICONTROL フロー制御]**」タブ）、1 つの「**[!UICONTROL JavaScript コード]**」アクティビティ（「**[!UICONTROL アクション]**」タブ）、1 つの「**[!UICONTROL 配信]**」アクティビティ（「**[!UICONTROL アクション]**」タブ）などがあります。

![](assets/use_case_abtesting_targetwkfl_004.png)

これで、母集団サンプルを設定できます。 [詳細情報](a-b-testing-uc-population-samples.md)。
