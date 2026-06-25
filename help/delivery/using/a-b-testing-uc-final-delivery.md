---
product: campaign
title: 最終配信の定義
description: 専用のユースケースを通じて A/B テストを実行する方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: A/B Testing
role: User
exl-id: bc23a444-a872-48fb-8bba-64b301541089
TQID: https://experienceleague.adobe.com/P0oI4PhLZB-iBFDrEJ2Qy7eIOPYWSWYu5s6j3yCN6j0
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
feature_v2: id: b631758a-142d-425f-b9aa-f756d85cb979id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2: id: d5bbe3da-ba85-4242-817e-54f7c4b943e0id: e739ee2b-6228-412e-878f-45de0791417d
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 129
ht-degree: 100%

---

# A/B テスト：最終配信の定義 {#step-6--defining-the-final-delivery}

A/B テストの勝者を選択するスクリプトの作成後は、最終配信のパラメーターを定義できます。

1. 「**[!UICONTROL JavaScript コード]**」アクティビティを残りの「**[!UICONTROL 配信]**」アクティビティに接続します。
1. 「**[!UICONTROL 配信]**」アクティビティを開きます。
1. このアクティビティによってワークフローを終了するために「**[!UICONTROL アウトバウンドトランジションを生成]**」オプションをオフにします。
1. その他のオプションはデフォルト値のままにしておきます。

   ![](assets/ab_test_final_delivery.png)

（「**[!UICONTROL Javascript コード]**」アクティビティで定義された）トランジションで指定された配信を準備することで、次の手順で説明する、承認と配信の開始が可能になります。

これで、ワークフローを開始できます。 [詳細情報](a-b-testing-uc-start-workflow.md)。
