---
product: campaign
title: AND 結合
description: AND 結合
feature: Workflows
exl-id: 8b6d5c03-e104-4cf0-82ab-a08467e3e478
source-git-commit: b94c4bfd478b4a8fbcefe6341608dd6a14bb31d3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 100%

---

# AND 結合{#and-join}

![](../../assets/common.svg)

結合は、先行するすべてのアクティビティが完了しているなど、すべてのインバウンドトランジションが有効化されている場合にのみ、アウトバウンドトランジションをトリガーします。これにより、ワークフローを続行する前に、特定のアクティビティを確実に完了させるようにできます。

例えば、コンテンツの作成と配信の自動送信のコンテキストで AND 結合アクティビティを使用して、ターゲットのクエリとコンテンツの更新手順が完了した後にのみ配信が開始されるようにできます。該当する使用例については、[この節](../../delivery/using/automating-via-workflows.md#creating-the-delivery-and-its-content)を参照してください。

![](assets/and-join-usage.png)

>[!NOTE]
>
>異なるターゲティングディメンションで設定されたインバウンドトランジションは、**[!UICONTROL AND-join]** アクティビティを使用して結合できません。

アウトバウンドに送られるアクティビティの母集団は、アクティビティ内のインバウンドトランジション間のメインセットを選択することで、決定されます。

アウトバウンドトランジションには、インバウンドトランジションの母集団の 1 つのみを含むことができます。アクティビティが設定されていない場合、アウトバウンドトランジションにより、インバウンド母集団のいずれかがランダムに選択されます。

>[!CAUTION]
>
>「**AND 結合**」タイプアクティビティの場合、イベント変数は結合されますが、同じ変数を 2 回定義した場合、競合が生じ、値が未確定になります。詳しくは、[この節](javascript-scripts-and-templates.md#event-variables)を参照してください。
