---
title: 配信のタイプ
seo-title: 配信のタイプ
description: 配信のタイプ
seo-description: null
page-status-flag: never-activated
uuid: a540efc7-105d-4c7f-a2ee-ade4d22b3445
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: about-deliveries-and-channels
discoiquuid: 0cbc4e92-482f-4dac-a1fb-b738e7127938
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 4ac96bf0e54268832b84b17c3cc577af038cc712

---


# 配信のタイプ{#types-of-deliveries}

キャンペーンには 3 つのタイプの配信オブジェクトがあります。

## 単一の配信 {#single-delivery}

**配信**&#x200B;は、一度だけ実行されるスタンドアロン配信オブジェクトです。レプリケートし、再度準備済みにすることはできますが、最終状態（キャンセル、停止、完了）になっている場合は再利用できません。

配信は、配信リストから作成したり、ワークフロー内で[配信](../../workflow/using/delivery.md)アクティビティを介して作成したりできます。

ワークフローには、使用するチャネルのタイプに応じた特定の配信アクティビティも用意されています。For more on these activities, refer to [this section](../../workflow/using/cross-channel-deliveries.md).

## 繰り返し配信 {#recurring-delivery}

**繰り返し配信**&#x200B;では、アクティビティを実行するたびに新しい配信を作成できます。これにより、繰り返しタスクのために新しい配信を手動で作成する必要がなくなります。

例えば、このタイプのアクティビティを月に 1 回実行した場合、1 年後の配信の数は 12 個です。

Recurring deliveries are created within workflows via the [Recurring delivery activity](../../workflow/using/recurring-delivery.md). この節では、このアクティビティの使用例を示します。ターゲ [ット設定ワークフローでの定期配信の作成](../../campaign/using/setting-up-marketing-campaigns.md#creating-a-recurring-delivery-in-a-targeting-workflow)。

## 連続配信 {#continuous-delivery}

**連続配信**&#x200B;では、既存の配信に新しい受信者を追加できるので、アクティビティを実行するたびに新しい配信を作成する必要がありません。

配信の情報（コンテンツ、名前など）を変更すると、配信の実行時に新しい配信オブジェクトが作成されます。情報を変更しなかった場合は、同じ配信オブジェクトが再利用され、同じオブジェクトに配信ログとトラッキングログが追加されます。

例えば、このタイプのアクティビティを月に 1 回実行した場合、1 年後の配信数は 1 個です（ただし、配信に変更を加えなかった場合）。

Continuous deliveries are created within workflows via the [Continuous delivery activity](../../workflow/using/continuous-delivery.md).
