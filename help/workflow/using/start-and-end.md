---
title: 開始および終了
description: 開始およびエンドワークフローのアクティビティの詳細
page-status-flag: never-activated
uuid: ec0c818c-c307-4f50-908c-507bce0ea27b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: flow-control-activities
discoiquuid: 8b239d5e-2317-42c8-9fee-7d40bea624da
translation-type: tm+mt
source-git-commit: 6be6c353c3464839a74ba857d8d93d0f68bc8865
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 94%

---


# 開始および終了{#start-and-end}

「**[!UICONTROL 開始]**」アクティビティおよび「**[!UICONTROL 終了]**」アクティビティを使用して、ワークフローの開始と終了を視覚的に示します。これらのアクティビティは、機能上の影響はないので、省略可能です。

* **[!UICONTROL 開始]**

   ワークフローの実行は、インバウンドトランジションのないアクティビティと、「開始」タイプアクティビティから開始します。

   ![](assets/s_user_segmentation_start_stop.png)

* **[!UICONTROL 終了]**

   進行中のすべてのタスクを中断する「**[!UICONTROL 終了]**」アクティビティを設定できます。それには、アクティビティをダブルクリックしてプロパティを標示し、適切なオプションを選択します。

   ![](assets/s_user_segmentation_end.png)

   作業用テーブル内のデータは、「終了」アクティビティが有効になると自動的に削除されます。データを削除する必要がなく、不要な負荷を避けたい場合は、最後のアクティビティ出力でトランジションを無効にすることもできます。例えば、配信出力でプロセスが何もスケジュールされていない場合、次に示す関連オプションのチェックを外します。

   ![](assets/s_advuser_delivery_option_no_output.png)

