---
product: campaign
title: 配信の設定
description: 専用のユースケースを通じて A/B テストを実行する方法を学ぶ
badge-v7: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7"
badge-v8: label="v8" type="Positive" tooltip="Also applies to Campaign v8"
feature: A/B Testing
exl-id: 809de30b-7d08-40de-bf3e-dc80d62eae80
source-git-commit: 6dc6aeb5adeb82d527b39a05ee70a9926205ea0b
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 100%

---

# ワークフローでの配信の設定 {#step-4--configuring-the-deliveries-in-the-workflow}



[母集団が作成されたら](a-b-testing-uc-population-samples.md)、配信を設定できます。このユースケースでは、最初の 2 つの配信によって、母集団 A と母集団 B に異なるコンテンツを送信できます。3 番目の配信はフォールバック配信です。A にも B にも属さない受信者に送信されます。そのコンテンツはスクリプトで計算され、開封率が最も高い受信者に応じて A または B のいずれかと同じになります。3 番目の配信の待機期間を設定し、配信 A、配信 B の結果を特定する必要があります。そのため、3 番目の配信には「**[!UICONTROL 待機]**」アクティビティを実装します。

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

これで、スクリプトを作成できます。 [詳細情報](a-b-testing-uc-script.md)。
