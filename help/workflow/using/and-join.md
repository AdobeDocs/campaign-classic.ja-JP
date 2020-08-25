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
source-git-commit: f7ed7e59be2cfbde467b0c80d21cfbf52016a2b8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 56%

---


# AND 結合{#and-join}

結合は、先行するすべてのアクティビティが完了しているなど、すべてのインバウンドトランジションが有効化されている場合にのみ、アウトバウンドトランジションをトリガーします。これにより、ワークフローを続行する前に、特定のアクティビティを確実に完了させるようにできます。

例えば、コンテンツの作成と自動送信配信のコンテキストでAND結合アクティビティを使用して、配信のクエリとコンテンツの更新の手順が完了した後にのみターゲットが開始されるようにできます。 このセクションでは、専用の使用例を紹介 [します。](../../delivery/using/automating-via-workflows.md#creating-the-delivery-and-its-content)

![](assets/and-join-usage.png)

アウトバウンドに送られるアクティビティの母集団は、アクティビティ内のインバウンドトランジション間のメインセットを選択することで、決定されます。

アウトバウンドトランジションには、インバウンドトランジションの母集団の 1 つのみを含むことができます。アクティビティが設定されていない場合、アウトバウンドトランジションにより、インバウンド母集団のいずれかがランダムに選択されます。

>[!CAUTION]
>
>**** AND結合型のアクティビティの場合、イベント変数は結合されますが、同じ変数が2回定義された場合は競合が発生し、値は未確定のままです。 詳しくは、[](../../workflow/using/javascript-scripts-and-templates.md#event-variables)を参照してください。
