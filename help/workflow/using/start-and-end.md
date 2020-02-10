---
title: 開始および終了
seo-title: 開始および終了
description: 開始および終了
seo-description: null
page-status-flag: never-activated
uuid: ec0c818c-c307-4f50-908c-507bce0ea27b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: flow-control-activities
discoiquuid: 8b239d5e-2317-42c8-9fee-7d40bea624da
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# 開始および終了{#start-and-end}

The **[!UICONTROL Start]** and **[!UICONTROL End]** activities allow you to graphically mark the start and end of a workflow. これらのアクティビティは、機能上の影響はないので、省略可能です。

* **[!UICONTROL Start]**

   ワークフローの実行は、インバウンドトランジションのないアクティビティと、「開始」タイプアクティビティから開始します。

   ![](assets/s_user_segmentation_start_stop.png)

* **[!UICONTROL End]**

   You can configure the **[!UICONTROL End]** activity to interrupt all tasks that are in progress. それには、アクティビティをダブルクリックしてプロパティを標示し、適切なオプションを選択します。

   ![](assets/s_user_segmentation_end.png)

   作業用テーブル内のデータは、「終了」アクティビティが有効になると自動的に削除されます。データを削除する必要がなく、不要な負荷を避けたい場合は、最後のアクティビティ出力でトランジションを無効にすることもできます。例えば、配信出力でプロセスが何もスケジュールされていない場合、次に示す関連オプションのチェックを外します。

   ![](assets/s_advuser_delivery_option_no_output.png)

