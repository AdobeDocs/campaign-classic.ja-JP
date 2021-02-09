---
solution: Campaign Classic
product: campaign
title: 配信の設定
description: 専用の使用例を通してA/Bテストを実行する方法を学びます。
audience: delivery
content-type: reference
topic-tags: a-b-testing
translation-type: tm+mt
source-git-commit: 177b4e74c75e4fcca70dc90b5ff2c0406181e0f7
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 93%

---


# ワークフローで配信を設定 {#step-4--configuring-the-deliveries-in-the-workflow}

次のステップで配信を設定します。設定する配信は、前のステージの[手順 2：母集団サンプルの設定](#step-2--configuring-population-samples)で作成した 3 つの母集団用のものです。最初の 2 つの配信では、母集団 A と母集団 B にそれぞれ異なるコンテンツを送信することができます。一方、3 番目の配信は、A の配信も B の配信も受信しない母集団用のものです。このコンテンツはスクリプトで割り出します。A のコンテンツと B のコンテンツのどちらかと同一のものになり、どちらのコンテンツの開封率が高いかに応じて決まります。3 番目の配信の待機期間を設定し、配信 A、配信 B の結果を特定する必要があります。そのため、3 番目の配信には「**[!UICONTROL 待機]**」アクティビティを実装します。

1. 「**[!UICONTROL 分割]**」アクティビティに移動し、母集団 A 用のトランジションを、既にワークフローにある E メール配信のトランジションとリンクします。

   ![](assets/use_case_abtesting_createdeliveries_001.png)

1. 配信をダブルクリックして開きます。
1. ドロップダウンリストで、配信 A のテンプレートを選択します。

   ![](assets/use_case_abtesting_createdeliveries_003.png)

1. 「**[!UICONTROL 続行]**」をクリックして配信を表示し、保存します。

   ![](assets/use_case_abtesting_createdeliveries_002.png)

1. 母集団 B 用の「**[!UICONTROL 分割]**」アクティビティのトランジションを 2 番目の E メール配信にリンクします。

   ![](assets/use_case_abtesting_createdeliveries_004.png)

1. 配信を開き、配信 B のテンプレートを選択し、配信を保存します。

   ![](assets/use_case_abtesting_createdeliveries_005.png)

1. その他の母集団用のトランジションを「**[!UICONTROL 待機]**」アクティビティとリンクします。

   ![](assets/use_case_abtesting_createdeliveries_006.png)

1. **[!UICONTROL 待機]**&#x200B;アクティビティを開き、5 日の待機期間を設定します。

   ![](assets/use_case_abtesting_createdeliveries_007.png)

1. 「**[!UICONTROL 待機]**」アクティビティを「**[!UICONTROL JavaScript コード]**」アクティビティとリンクします。

   ![](assets/use_case_abtesting_createdeliveries_008.png)
