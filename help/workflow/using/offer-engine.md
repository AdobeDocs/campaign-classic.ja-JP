---
title: オファーエンジン
seo-title: オファーエンジン
description: オファーエンジン
seo-description: null
page-status-flag: never-activated
uuid: a8f6056a-80e6-4f9f-81f5-563c98d11d28
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: targeting-activities
discoiquuid: 08987595-e80c-4197-ad1e-9aa7cfc7c3eb
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# オファーエンジン{#offer-engine}

**[!UICONTROL オファーエンジン]**&#x200B;アクティビティを使用して、配信に先立つオファーエンジンの呼び出しを定義できます。

このアクティビティは、エンリッチメントアクティビティと同じ原則でエンジン呼び出しによって作動します。つまり、配信の前に、インバウンド母集団のデータを、エンジンによって自動生成されたオファーでエンリッチメントします。

![](assets/int_offerengine_activity2.png)

クエリを設定した後におこなう作業（この[節](../../workflow/using/query.md)を参照）：

1. 「**[!UICONTROL オファーエンジン]**」アクティビティを追加し、開きます。
1. 使用可能な各種フィールドに入力して、オファーエンジンパラメーター（オファースペース、カテゴリまたはテーマ、コンタクト日、保持するオファー数）への呼び出しを指定します。エンジンは、これらのパラメーターに基づいて、追加するオファーを自動的に計算します。

   >[!CAUTION]
   >
   >このアクティビティを使用する場合、配信に使用されたオファーの提案のみが格納されます。

   ![](assets/int_offerengine_activity1.png)

1. 次に、選択したチャネルに対応する配信アクティビティを設定します。[クロスチャネル配信](../../workflow/using/cross-channel-deliveries.md)を参照してください。

