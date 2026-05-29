---
product: campaign
title: A/B テストの設定
description: Campaign で A/B テストを設定する方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: A/B Testing
role: User
exl-id: 6adf2e75-63b1-44ad-8925-03beb3bc0bdd
TQID: https://experienceleague.adobe.com/PHIsuJZ-o5mBRAPggyVYdzS7PBXL9GYCBc6Fr56ur5Q
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
feature_v2:
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2:
  - id: e95a583b-fcfa-4524-8666-46a29c828119
  - id: c8da4fdd-eb94-4751-a43c-f82733fb2d6e
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: f4da0e76-df77-451e-ad61-21afb7bd8810
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 264
ht-degree: 100%

---

# A/B テストの設定 {#configuring-a-b-testing}

この節では、A/B テストを実行するワークフローを構築する方法について説明します。

1. 新しいワークフローを作成し、目的の母集団をターゲットに設定するクエリアクティビティを設定します。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/query.html?lang=ja){target="_blank"}を参照してください。

1. 分割アクティビティを追加して、ターゲット母集団を複数のサブセットに分割します。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/split.html?lang=ja){target="_blank"}を参照してください。

1. アクティビティを開き、必要に応じて各サブセットを設定します。 **[!UICONTROL 分割]**&#x200B;アクティビティの設定方法の詳細については、[こちらの節](../../workflow/using/split.md)を参照してください。

   この例では、ニュースレター用の 2 つの新しい件名を、それぞれターゲット母集団の 10%に提示して、テストをおこないます。

   ![](assets/ab-testing-split.png)

1. その他の母集団に、現在の件名でニュースレターを送信するためにトランジションを追加します。 これをおこなうには、「**[!UICONTROL 一般]**」タブの「**[!UICONTROL 補集合を生成]**」オプションを有効にします。

   ![](assets/ab-testing-complement.png)

1. サブセットごとに、テストする配信のバージョンを追加します。

   ![](assets/ab-testing-delivery.png)

これで、ワークフローを開始できます。 配信が送信されると、3 つのサブセットの動作を配信ログでトラッキングして、どの件名が最も成功したかを確認できます。

また、ワークフローを使用すると、プロセスの自動化が可能です。より良いパフォーマンスを示した配信バリアントを自動的に識別して、その他の母集団に送信できます。 詳しくは、この専用の[ユースケース](a-b-testing-use-case.md)を参照してください。
