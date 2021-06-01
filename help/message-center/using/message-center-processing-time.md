---
product: campaign
title: Message Center の処理時間
description: 詳しくは、 Message Centerの処理時間レポートを参照してください。
audience: message-center
content-type: reference
topic-tags: reports
exl-id: c797fd94-0c8d-480b-b22a-1489ac331e77
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 89%

---

# Message Center の処理時間 {#message-center-processing-time}

このレポートではリアルタイムキューに関する主な指標が表示されます。

技術管理者向けのこのレポートは、コントロールインスタンスの「**[!UICONTROL 監視]**」タブからもアクセスできます。

![](assets/mc_reports_2.png)

**[!UICONTROL Message Center サービスレベル]**&#x200B;レポートと同じく、総合的な統計または特定の実行インスタンスに関する統計のいずれかを選択して表示することができます。また、チャネルおよび一定期間の検索条件を追加することもできます。

「**[!UICONTROL 全期間の指標]**」セクションに表示される指標は、選択した期間を対象に計算されます。

* **[!UICONTROL 平均キュー格納時間]**：Message Center が処理に成功したイベントに費やした時間。処理時間のみが考慮されます。
* **[!UICONTROL 平均メッセージ送信時間（秒）]**：Message Center が処理に成功したイベントに費やした時間。MTA 配信時間のみが考慮されます。
* **[!UICONTROL 平均処理時間（秒）]**：Message Center が処理に成功したイベントに費やした時間。この計算では処理時間および MTA 送信時間が考慮されます。
* **[!UICONTROL キュー内イベントの最大数]**：任意の時点で Message Center 内に存在したイベント数の最大値。
* **[!UICONTROL キュー内イベントの最小数]**：任意の時点で Message Center 内に存在したイベント数の最小値。
* **[!UICONTROL キュー内イベントの平均数]**：任意の時点で Message Center 内に存在したイベント数の平均値。

>[!NOTE]
>
>警告（オレンジ）およびアラート（赤）指標のしきい値は、Adobe Campaign デプロイウィザードで設定することができます。[しきい値の監視](../../message-center/using/additional-configurations.md#monitoring-thresholds)を参照してください。
