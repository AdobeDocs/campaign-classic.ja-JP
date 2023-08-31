---
product: campaign
title: 最終配信の定義
description: 専用のユースケースを通じて A/B テストを実行する方法を学ぶ
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: A/B Testing
role: User
exl-id: bc23a444-a872-48fb-8bba-64b301541089
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 95%

---

# A/B テスト：最終配信の定義 {#step-6--defining-the-final-delivery}

A/B テストの勝者を選択するスクリプトの作成後は、最終配信のパラメーターを定義できます。

1. 「**[!UICONTROL JavaScript コード]**」アクティビティを残りの「**[!UICONTROL 配信]**」アクティビティに接続します。
1. 「**[!UICONTROL 配信]**」アクティビティを開きます。
1. このアクティビティによってワークフローを終了するために「**[!UICONTROL アウトバウンドトランジションを生成]**」オプションをオフにします。
1. その他のオプションはデフォルト値のままにしておきます。

   ![](assets/ab_test_final_delivery.png)

（「**[!UICONTROL Javascript コード]**」アクティビティで定義された）トランジションで指定された配信を準備することで、次の手順で説明する、承認と配信の開始が可能になります。

これで、ワークフローを開始できます。[詳細情報](a-b-testing-uc-start-workflow.md)。
