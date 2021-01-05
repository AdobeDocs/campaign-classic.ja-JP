---
solution: Campaign Classic
product: campaign
title: 分岐
description: 分岐ワークフローアクティビティの詳細を説明します
audience: workflow
content-type: reference
topic-tags: flow-control-activities
translation-type: tm+mt
source-git-commit: 3eecc16442a11849c12819cf83392f60c5b82a13
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 16%

---


# 分岐{#fork}

**[!UICONTROL Fork]**&#x200B;アクティビティを使用すると、同じワークフロー内で複数のアクティビティを個別に実行するために、複数の送信トランジションを作成できます。

例えば、クエリの後にアクティビティを使用して、2つの操作を並行して実行できます。

* クエリの結果をオーディエンスに保存し、
* 複数の配信を送信するために、結果に対してセグメントを実行します。

また、ターゲットの計算とコンテンツの作成を並行して開始するために、コンテンツの作成と自動送信の配信のコンテキストでこのアクティビティを使用することもできます。 該当する使用例については、[この節](../../delivery/using/automating-via-workflows.md#creating-the-delivery-and-its-content)を参照してください。

>[!WARNING]
>
>Forkアクティビティの後に追加された送信トランジションは、同時に実行されないことに注意してください。
>
>したがって、ワークフローのパフォーマンスを向上させるためではなく、複数のアクティビティを個別に実行し、最終的にそれらを結合してからワークフローの残りの部分を実行するためにアクティビティを使用する必要があります。

分岐アクティビティを設定するには、分岐アクティビティを開き、該当するアウトバウンドトランジションの番号とラベルを定義します。

![](assets/s_user_segmentation_fork.png)

その後、必要に応じて、各送信トランジションを設定し、[AND-join](../../workflow/using/and-join.md)アクティビティを使用して結合することができます。 このようにして、残りのワークフローは、**[!UICONTROL Fork]**&#x200B;アクティビティの送信トランジションが終了した場合にのみ実行されます。
