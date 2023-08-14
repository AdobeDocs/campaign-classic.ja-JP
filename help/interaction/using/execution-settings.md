---
product: campaign
title: 実行設定
description: 実行設定
feature: Interaction, Offers
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: interaction
content-type: reference
topic-tags: simulating-offers
exl-id: e2dea4a0-9ed8-47b6-a16b-eeee653d2290
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: ht
source-wordcount: '174'
ht-degree: 100%

---

# 実行設定{#execution-settings}



シミュレーションを作成する際には、必要に応じて実行設定を指定できます。これらの設定を使用すると、優先度に応じて負荷が小さい時間帯にシミュレーションを実行したり、SQL クエリをログに記録したりできます。
このステージはオプションです。

実行設定は、後でシミュレーションウィンドウの「**[!UICONTROL 一般]**」タブで変更できます。

![](assets/offer_simulation_008.png)

* **[!UICONTROL 実行スケジュールを低アクティビティの時間に設定]**：Adobe Campaign のパフォーマンスを最適化するために、選択した優先順位（低、平均、高）に基づいてシミュレーションをスケジュールできます。
* **[!UICONTROL 優先順位]**：これは、スケジュールするシミュレーションに適用するレベルです。「**[!UICONTROL 実行スケジュールを低アクティビティの時間に設定]**」オプションがオンになっている場合、アクティビティの少ない時間帯がキャンペーン開始時間として選択されます。
* **[!UICONTROL SQL クエリをログに記録]**：この機能は、エキスパートユーザー専用です。この機能を使用すると、SQL クエリのログを表示するタブが追加され、シミュレーションがエラーで終了した場合に不具合を探すことができます。
