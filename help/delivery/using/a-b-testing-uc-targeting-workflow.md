---
product: campaign
title: ターゲティングワークフローの作成
description: 専用のユースケースを通じて A/B テストを実行する方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: A/B Testing
role: User
exl-id: aa21fa33-aef9-484a-b454-0cd5a6868a98
TQID: https://experienceleague.adobe.com/D4O223FYCiIwT-P4WCXa1gYjxB56lCGVIuGL3x-fDRo
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
subfeature_v2:
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: e739ee2b-6228-412e-878f-45de0791417d
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 198
ht-degree: 100%

---

# A/B テスト：ターゲティングワークフローを作成 {#step-1--creating-a-targeting-workflow}

キャンペーンの「**[!UICONTROL ターゲティングとワークフロー]**」タブでワークフローを作成する必要があります。 このワークフローは、1 つの「**[!UICONTROL クエリ]**」アクティビティ、2 つの「**[!UICONTROL メール配信]**」アクティビティとリンクした 1 つの「**[!UICONTROL 分割]**」アクティビティ、1 つの「**[!UICONTROL 待機]**」アクティビティ、1 つの「**[!UICONTROL JavaScript コード]**」アクティビティ、1 つの「**[!UICONTROL 配信]**」アクティビティから構成されます。

1. まだキャンペーンを作成していない場合は、作成します。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/set-up-campaigns.html?lang=ja){target=_blank}を参照してください。

   ![](assets/use_case_abtesting_targetwkfl_001.png)

1. 「**[!UICONTROL ターゲティングとワークフロー]**」タブに移動します。

   ![](assets/use_case_abtesting_targetwkfl_002.png)

1. 既存のワークフローのラベルを変更するか、「**[!UICONTROL 追加]**」をクリックして、新しいラベルを作成します（詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/marketing-campaign-target.html?lang=ja){target="_blank"}を参照してください）。

   ![](assets/use_case_abtesting_targetwkfl_003.png)

1. マウスを使用してワークフローダイアグラムにアクティビティをドラッグ＆ドロップします。対象となるアクティビティには、1 つの「**[!UICONTROL クエリ]**」アクティビティ（「**[!UICONTROL ターゲット]**」タブ）、1 つの「**[!UICONTROL 分割]**」アクティビティ（「**[!UICONTROL ターゲット]**」タブ）、2 つの「**[!UICONTROL メール配信]**」アクティビティ（「**[!UICONTROL 配信]**」タブ）、1 つの「**[!UICONTROL 待機]**」アクティビティ（「**[!UICONTROL フロー制御]**」タブ）、1 つの「**[!UICONTROL JavaScript コード]**」アクティビティ（「**[!UICONTROL アクション]**」タブ）、1 つの「**[!UICONTROL 配信]**」アクティビティ（「**[!UICONTROL アクション]**」タブ）などがあります。

![](assets/use_case_abtesting_targetwkfl_004.png)

これで、母集団サンプルを設定できます。 [詳細情報](a-b-testing-uc-population-samples.md)。
