---
title: Message Center の処理時間
seo-title: Message Center の処理時間
description: Message Center の処理時間
seo-description: null
page-status-flag: never-activated
uuid: 06aca2c2-33c0-4839-bee4-fd838c49ce76
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: reports
discoiquuid: d1f591d2-95e8-4d99-bc60-955c96b532eb
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# Message Center の処理時間{#message-center-processing-time}

このレポートではリアルタイムキューに関する主な指標が表示されます。This report, aimed at technical administrators, can also be accessed via the **[!UICONTROL Monitoring]** universe in the control instance.

![](assets/mc_reports_2.png)

Just like for the **[!UICONTROL Message Center service level]** report, you can choose to display the overall statistics or those relative to a particular execution instance. また、チャネルおよび一定期間の検索条件を追加することもできます。セクションに表示されるインジケ **[!UICONTROL Indicators over the period]** ーターは、選択した期間に対して計算されます。

* **[!UICONTROL Average queuing time]** :message Centerでのイベントの正常な処理に要した平均時間。 処理時間のみが考慮されます。
* **[!UICONTROL Average message sending time (s)]** :message Centerでのイベントの正常な処理に要した平均時間。 MTA 配信時間のみが考慮されます。
* **[!UICONTROL Average processing time (s)]** :message Centerでのイベントの正常な処理に要した平均時間。 この計算では処理時間および MTA 送信時間が考慮されます。
* **[!UICONTROL Maximum number of queued events]** :特定の時点でMessage Centerキューに存在するイベントの最大数。
* **[!UICONTROL Minimum number of queued events]** :特定の時点でMessage Centerキューに存在するイベントの最小数。
* **[!UICONTROL Average number of queued events]** :特定の時点でMessage Centerキューに存在する平均イベント数。

>[!NOTE]
>
>警告（オレンジ）およびアラート（赤）指標のしきい値は、Adobe Campaign デプロイウィザードで設定することができます。「監視しきい値 [」を参照](../../message-center/using/monitoring-thresholds.md)。

