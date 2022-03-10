---
product: campaign
title: 最終配信の定義
description: 専用のユースケースを通じて A/B テストを実行する方法を学ぶ
feature: A/B Testing
exl-id: bc23a444-a872-48fb-8bba-64b301541089
source-git-commit: 9839dbacda475c2a586811e3c4f686b1b1baab05
workflow-type: ht
source-wordcount: '118'
ht-degree: 100%

---

# 最終配信の定義 {#step-6--defining-the-final-delivery}

![](../../assets/common.svg)

A/B テストの勝者を選択するスクリプトの作成後は、最終配信のパラメーターを定義できます。

1. 「**[!UICONTROL JavaScript コード]**」アクティビティを残りの「**[!UICONTROL 配信]**」アクティビティに接続します。
1. 「**[!UICONTROL 配信]**」アクティビティを開きます。
1. このアクティビティによってワークフローを終了するために「**[!UICONTROL アウトバウンドトランジションを生成]**」オプションをオフにします。
1. その他のオプションはデフォルト値のままにしておきます。

   ![](assets/ab_test_final_delivery.png)

（「**[!UICONTROL Javascript コード]**」アクティビティで定義された）トランジションで指定された配信を準備することで、次の手順で説明する、承認と配信の開始が可能になります。

これで、ワークフローを開始できます。[詳細情報](a-b-testing-uc-start-workflow.md)。
