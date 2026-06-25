---
product: campaign
title: AND 結合
description: AND 結合
feature: Workflows
hide: true
exl-id: 8b6d5c03-e104-4cf0-82ab-a08467e3e478
TQID: https://experienceleague.adobe.com/L6SmrK6xHkRqZI69OepbB4drLPfrX-cmvi6h6su3LYk
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2: id: ee25c34b-ea50-427b-9369-ba0a160f7d70id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22fid: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 197
ht-degree: 100%

---

# AND 結合{#and-join}



結合は、先行するすべてのアクティビティが完了しているなど、すべてのインバウンドトランジションが有効化されている場合にのみ、アウトバウンドトランジションをトリガーします。 これにより、ワークフローを続行する前に、特定のアクティビティを確実に完了させるようにできます。

例えば、コンテンツの作成と配信の自動送信のコンテキストで AND 結合アクティビティを使用して、ターゲットのクエリとコンテンツの更新手順が完了した後にのみ配信が開始されるようにできます。 該当する使用例については、[この節](../../delivery/using/automating-via-workflows.md#creating-the-delivery-and-its-content)を参照してください。

![](assets/and-join-usage.png)

>[!NOTE]
>
>異なるターゲティングディメンションで設定されたインバウンドトランジションは、**[!UICONTROL AND-join]** アクティビティを使用して結合できません。

アウトバウンドに送られるアクティビティの母集団は、アクティビティ内のインバウンドトランジション間のメインセットを選択することで、決定されます。

アウトバウンドトランジションには、インバウンドトランジションの母集団の 1 つのみを含むことができます。 アクティビティが設定されていない場合、アウトバウンドトランジションにより、インバウンド母集団のいずれかがランダムに選択されます。

>[!CAUTION]
>
>「**AND 結合**」タイプアクティビティの場合、イベント変数は結合されますが、同じ変数を 2 回定義した場合、競合が生じ、値が未確定になります。 詳しくは、[この節](javascript-scripts-and-templates.md#event-variables)を参照してください。
