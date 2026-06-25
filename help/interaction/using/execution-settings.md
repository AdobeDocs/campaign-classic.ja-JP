---
product: campaign
title: 実行設定
description: 実行設定
feature: Interaction, Offers
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: interaction
content-type: reference
topic-tags: simulating-offers
exl-id: e2dea4a0-9ed8-47b6-a16b-eeee653d2290
TQID: https://experienceleague.adobe.com/k2-e-laXDXtVyBJnoiyKAdNHKiS3nB-t1X1cEaqeudM
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b6fcaf36-3bc4-4604-94f3-81b5d3f41ecf
subfeature_v2: []
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 171
ht-degree: 100%

---

# 実行設定{#execution-settings}



シミュレーションを作成する際には、必要に応じて実行設定を指定できます。 これらの設定を使用すると、優先度に応じて負荷が小さい時間帯にシミュレーションを実行したり、SQL クエリをログに記録したりできます。 このステージはオプションです。

実行設定は、後でシミュレーションウィンドウの「**[!UICONTROL 一般]**」タブで変更できます。

![](assets/offer_simulation_008.png)

* **[!UICONTROL 実行スケジュールを低アクティビティの時間に設定]**：Adobe Campaign のパフォーマンスを最適化するために、選択した優先順位（低、平均、高）に基づいてシミュレーションをスケジュールできます。
* **[!UICONTROL 優先順位]**：これは、スケジュールするシミュレーションに適用するレベルです。 「**[!UICONTROL 実行スケジュールを低アクティビティの時間に設定]**」オプションがオンになっている場合、アクティビティの少ない時間帯がキャンペーン開始時間として選択されます。
* **[!UICONTROL SQL クエリをログに記録]**：この機能は、エキスパートユーザー専用です。 この機能を使用すると、SQL クエリのログを表示するタブが追加され、シミュレーションがエラーで終了した場合に不具合を探すことができます。
