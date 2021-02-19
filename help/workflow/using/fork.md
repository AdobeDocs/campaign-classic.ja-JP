---
solution: Campaign Classic
product: campaign
title: 分岐
description: 分岐ワークフローアクティビティの詳細を説明します
audience: workflow
content-type: reference
topic-tags: flow-control-activities
translation-type: tm+mt
source-git-commit: e5f718908d0bb6893e54c51700865ecda09c80db
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---


# 分岐{#fork}

**[!UICONTROL 分岐]**&#x200B;アクティビティを使用すると、同じワークフロー内で複数のアクティビティを個別に実行するために、複数のアウトバウンドトランジションを作成できます。

例えば、クエリの後にアクティビティを使用して、2 つの操作を並行して実行できます。

* クエリの結果をオーディエンスに保存し、
* 複数の配信を送信するために、結果に対してセグメントを実行します。

例えば、コンテンツの作成と配信の自動送信のコンテキストでアクティビティを使用して、ターゲットの計算とコンテンツの作成を同時に開始することもできます。該当する使用例については、[この節](../../delivery/using/automating-via-workflows.md#creating-the-delivery-and-its-content)を参照してください。

>[!IMPORTANT]
>
>**[!UICONTROL 分岐]**&#x200B;アクティビティの後に追加されたアウトバウンドトランジションは、同時には実行&#x200B;**されません**。この動作は、ワークフローのパフォーマンスに影響を与える可能性があります。 複数のアクティビティを個別に実行し、最終的にそれらを結合してから残りのワークフローを実行する必要がある場合は、このアクティビティを使用します。

**[!UICONTROL 分岐]**&#x200B;アクティビティを設定するには、アクティビティを開き、該当するアウトバウンドトランジションの番号とラベルを定義します。

![](assets/s_user_segmentation_fork.png)

その後、必要に応じて、各アウトバウンドトランジションを設定し、[AND 結合](../../workflow/using/and-join.md)アクティビティを使用して結合できます。 このようにして、残りのワークフローは、**[!UICONTROL 分岐]**&#x200B;アクティビティのアウトバウンドトランジションが終了した場合にのみ実行されます。
