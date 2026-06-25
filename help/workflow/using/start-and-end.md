---
product: campaign
title: 開始および終了
description: 「開始および終了」ワークフローアクティビティの詳細を説明します
feature: Workflows
hide: true
exl-id: 56dfbaf3-93de-4ade-b4ad-9b54d239c7a5
TQID: https://experienceleague.adobe.com/Vw3JK6VyMf4HrEkvYk4-34dGTp0e3e1xPZ8jG0bAxz8
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
  - id: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: c35995a47788db080636c66827a4bd6dc98806cf
workflow-type: tm+mt
source-wordcount: 140
ht-degree: 100%

---

# 開始と終了{#start-and-end}



「**[!UICONTROL 開始]**」アクティビティおよび「**[!UICONTROL 終了]**」アクティビティを使用して、ワークフローの開始と終了を視覚的に示します。 これらのアクティビティは、機能上の影響はないので、省略可能です。

* **[!UICONTROL 開始]**

  ワークフローの実行は、インバウンドトランジションのないアクティビティと、「開始」タイプアクティビティから開始します。

  ![](assets/s_user_segmentation_start_stop.png)

* **[!UICONTROL 終了]**

  進行中のすべてのタスクを中断する「**[!UICONTROL 終了]**」アクティビティを設定できます。 それには、アクティビティをダブルクリックしてプロパティを表示し、適切なオプションを選択します。

  ![](assets/s_user_segmentation_end.png)

  ワークテーブル内のデータは、「終了」アクティビティが有効になると自動的に削除されます。 データを削除する必要がなく、不要な負荷を避けたい場合は、最後のアクティビティ出力でトランジションを無効にすることもできます。 例えば、配信出力でプロセスが何もスケジュールされていない場合、次に示す関連オプションのチェックを外します。

  ![](assets/s_advuser_delivery_option_no_output.png)

