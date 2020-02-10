---
title: AND 結合
seo-title: AND 結合
description: AND 結合
seo-description: null
page-status-flag: never-activated
uuid: 8234d6cd-0e9b-4187-9ddf-9e1f86aa1b9a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: flow-control-activities
discoiquuid: 075206aa-ff7b-4fa8-a05d-14a29fb119ba
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# AND 結合{#and-join}

結合は、先行するすべてのアクティビティが完了しているなど、すべてのインバウンドトランジションが有効化されている場合にのみ、アウトバウンドトランジションをトリガーします。これにより、ワークフローを続行する前に、特定のアクティビティを確実に完了させるようにできます。

アウトバウンドに送られるアクティビティの母集団は、アクティビティ内のインバウンドトランジション間のメインセットを選択することで、決定されます。

アウトバウンドトランジションには、インバウンドトランジションの母集団の 1 つのみを含むことができます。アクティビティが設定されていない場合、アウトバウンドトランジションにより、インバウンド母集団のいずれかがランダムに選択されます。
