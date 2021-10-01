---
product: campaign
title: ターゲティングワークフローの作成
description: 専用の使用例を通してA/Bテストを実行する方法を学びます。
audience: delivery
content-type: reference
topic-tags: a-b-testing
exl-id: aa21fa33-aef9-484a-b454-0cd5a6868a98
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: ht
source-wordcount: '163'
ht-degree: 100%

---

# ターゲティングワークフローの作成 {#step-1--creating-a-targeting-workflow}

![](../../assets/common.svg)

キャンペーンの「**[!UICONTROL ターゲティングとワークフロー]**」タブでワークフローを作成する必要があります。このワークフローは、1 つの「**[!UICONTROL クエリ]**」アクティビティ、2 つの「**[!UICONTROL E メール配信]**」アクティビティとリンクした 1 つの「**[!UICONTROL 分割]**」アクティビティ、1 つの「**[!UICONTROL 待機]**」アクティビティ、1 つの「**[!UICONTROL JavaScript コード]**」アクティビティ、1 つの「**[!UICONTROL 配信]**」アクティビティから構成されます。

1. まだ作成していない場合は、キャンペーンを作成します（詳しくは、[この節](../../campaign/using/setting-up-marketing-campaigns.md#creating-a-campaign)を参照してください）。

   ![](assets/use_case_abtesting_targetwkfl_001.png)

1. 「**[!UICONTROL ターゲティングとワークフロー]**」タブに移動します。

   ![](assets/use_case_abtesting_targetwkfl_002.png)

1. 既存のワークフローのラベルを変更するか、「**[!UICONTROL 追加]**」をクリックして新しいラベルを作成します（詳しくは、[この節](../../campaign/using/marketing-campaign-deliveries.md#selecting-the-target-population)を参照してください）。

   ![](assets/use_case_abtesting_targetwkfl_003.png)

1. マウスを使用してワークフローダイアグラムにアクティビティをドラッグ＆ドロップします。対象となるアクティビティには、1 つの&#x200B;**[!UICONTROL クエリ]**&#x200B;アクティビティ（「**[!UICONTROL ターゲット]**」タブ）、1 つの&#x200B;**[!UICONTROL 分割]**&#x200B;アクティビティ（「**[!UICONTROL ターゲット]**」タブ）、2 つの **[!UICONTROL E メール配信]**&#x200B;アクティビティ（「**[!UICONTROL 配信]**」タブ）、1 つの&#x200B;**[!UICONTROL 待機]**&#x200B;アクティビティ（「**[!UICONTROL フロー制御]**」タブ）、1 つの **[!UICONTROL JavaScript コード]**&#x200B;アクティビティ（「**[!UICONTROL アクション]**」タブ）、1 つの&#x200B;**[!UICONTROL 配信]**&#x200B;アクティビティ（「**[!UICONTROL アクション]**」タブ）などがあります。

![](assets/use_case_abtesting_targetwkfl_004.png)

これで、母集団サンプルを設定できます。 [詳細情報](a-b-testing-uc-population-samples.md)。
