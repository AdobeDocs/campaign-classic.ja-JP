---
product: campaign
title: 配信テンプレートの作成
description: 専用のユースケースを通して A/B テストを実行する方法を説明します。
audience: delivery
content-type: reference
topic-tags: a-b-testing
exl-id: 77b3a906-b76e-49e1-b524-b6f1ae537259
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 100%

---

# 配信テンプレートの作成 {#step-3--creating-two-delivery-templates}

ここでは、2 つの配信テンプレートを作成します。各テンプレートは、「**[!UICONTROL 分割]**」アクティビティとリンクした「**[!UICONTROL E メール配信]**」アクティビティで参照されます。詳しくは、[この節](../../delivery/using/about-templates.md)を参照してください。

1. **[!UICONTROL リソース／配信テンプレート]**&#x200B;フォルダーへ移動します。
1. 「**[!UICONTROL E メール]**」配信テンプレートを複製します。

   ![](assets/use_case_abtesting_deliverymodel_001.png)

1. 配信 A に使用するコンテンツを作成します。

   ![](assets/use_case_abtesting_deliverymodel_002.png)

1. この手順を繰り返し、配信 B のテンプレートも作成します。

   ![](assets/use_case_abtesting_deliverymodel_003.png)

これで、ワークフロー内の配信を設定できます（[手順 4：ワークフローでの配信の設定](../../delivery/using/a-b-testing-uc-configuring-deliveries.md)を参照）。
