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
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '171'
ht-degree: 100%

---


# AND 結合{#and-join}

結合は、先行するすべてのアクティビティが完了しているなど、すべてのインバウンドトランジションが有効化されている場合にのみ、アウトバウンドトランジションをトリガーします。これにより、ワークフローを続行する前に、特定のアクティビティを確実に完了させるようにできます。

例えば、コンテンツの作成と配信の自動送信のコンテキストで AND 結合アクティビティを使用して、ターゲットのクエリとコンテンツの更新手順が完了した後にのみ配信が開始されるようにできます。該当する使用例については、[この節](../../delivery/using/automating-via-workflows.md#creating-the-delivery-and-its-content)を参照してください。

![](assets/and-join-usage.png)

アウトバウンドに送られるアクティビティの母集団は、アクティビティ内のインバウンドトランジション間のメインセットを選択することで、決定されます。

アウトバウンドトランジションには、インバウンドトランジションの母集団の 1 つのみを含むことができます。アクティビティが設定されていない場合、アウトバウンドトランジションにより、インバウンド母集団のいずれかがランダムに選択されます。

>[!CAUTION]
>
>「**AND 結合**」タイプアクティビティの場合、イベント変数は結合されますが、同じ変数を 2 回定義した場合、競合が生じ、値が未確定になります。詳しくは、[](../../workflow/using/javascript-scripts-and-templates.md#event-variables) を参照してください。
