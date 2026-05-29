---
product: campaign
title: 配信テンプレートの作成
description: 専用のユースケースを通じて A/B テストを実行する方法を学ぶ
role: User
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: A/B Testing
exl-id: 77b3a906-b76e-49e1-b524-b6f1ae537259
TQID: https://experienceleague.adobe.com/eble-fTf8Rk7fFGnKNh5pLUhMaLdZlJrG-vjrhbHx1I
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
feature_v2:
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2:
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: e739ee2b-6228-412e-878f-45de0791417d
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 100%

---

# A/B テスト：配信テンプレートを作成 {#step-3--creating-two-delivery-templates}

ここでは、2 つの配信テンプレートを作成します。 各テンプレートは、「**[!UICONTROL 分割]**」アクティビティとリンクした「**[!UICONTROL メール配信]**」アクティビティで参照されます。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-templates.html?lang=ja){target="_blank"}を参照してください。

1. **[!UICONTROL リソース／配信テンプレート]**&#x200B;フォルダーを参照します。
1. 「**[!UICONTROL メール]**」配信テンプレートを複製します。

   ![](assets/use_case_abtesting_deliverymodel_001.png)

1. 配信 A に使用するコンテンツを作成します。

   ![](assets/use_case_abtesting_deliverymodel_002.png)

1. この手順を繰り返し、配信 B のテンプレートも作成します。

   ![](assets/use_case_abtesting_deliverymodel_003.png)

これで、ワークフローに配信を設定できるようになりました。 [詳細情報](a-b-testing-uc-configuring-deliveries.md)。
