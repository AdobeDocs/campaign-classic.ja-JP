---
product: campaign
title: オファーエンジン
description: オファーエンジン
feature: Workflows, Interaction
exl-id: 8db4b04f-7754-4a49-ab72-afc916888ebb
source-git-commit: 381538fac319dfa075cac3db2252a9cc80b31e0f
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# オファーエンジン{#offer-engine}

![](../../assets/v7-only.svg)

**[!UICONTROL オファーエンジン]**&#x200B;アクティビティを使用して、配信に先立つオファーエンジンの呼び出しを定義できます。

このアクティビティは、エンリッチメントアクティビティと同じ原則でエンジン呼び出しによって作動します。つまり、配信の前に、インバウンド母集団のデータを、エンジンによって自動生成されたオファーでエンリッチメントします。

![](assets/int_offerengine_activity2.png)

クエリを設定した後におこなう作業（この[節](query.md)を参照）：

1. 「**[!UICONTROL オファーエンジン]**」アクティビティを追加し、開きます。
1. 使用可能な各種フィールドに入力して、オファーエンジンパラメーター（オファースペース、カテゴリまたはテーマ、コンタクト日、保持するオファー数）への呼び出しを指定します。エンジンは、これらのパラメーターに基づいて、追加するオファーを自動的に計算します。

   >[!CAUTION]
   >
   >このアクティビティを使用する場合、配信に使用されたオファーの提案のみが格納されます。

   ![](assets/int_offerengine_activity1.png)

1. 次に、選択したチャネルに対応する配信アクティビティを設定します。[クロスチャネル配信](cross-channel-deliveries.md)を参照してください。
