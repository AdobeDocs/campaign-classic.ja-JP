---
product: campaign
title: Campaign エクスプローラーのナビゲーションツリーの編集
description: Campaign エクスプローラーのナビゲーションツリーの編集
feature: Application Settings
role: Developer
exl-id: 204d4a24-267c-4976-90d9-7bf5bee8d116
TQID: https://experienceleague.adobe.com/k8LhZvPSYchAxnQew5eknkDbxHDznzPefl032auuYLc
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 135
ht-degree: 0%

---

# Campaign エクスプローラーのナビゲーションツリーの編集{#edition}

ナビゲーション階層設定ドキュメントを作成および設定する画面には、**[!UICONTROL 管理/設定/ナビゲーション階層]** ノードからアクセスできます。

![](assets/d_ncs_integration_navigation_arbo.png)

ナビゲーション階層設定は、複数のXML ドキュメントに分割されます。 これは、スキーマ拡張と同様の原則に基づいて動作します。すべてのドキュメントが結合され、設定全体を含む単一のドキュメントが生成されます。 このドキュメントは編集できず、「プレビュー」タブで表示されます。

編集フィールドには、XML ドキュメントのコンテンツが表示されます。

![](assets/d_ncs_integration_navigation_edit.png)

>[!NOTE]
>
>「名前」編集コントロールを使用すると、名前と名前空間で構成されるドキュメントキーを入力できます。 **`<navtree>`**&#x200B;要素の「name」属性と「namespace」属性は、スキーマのXML編集フィールドで自動的に更新されます。

プレビューでは、コンフィギュレーション全体を含む結合ドキュメントが自動的に生成されます。

![](assets/d_ncs_integration_navigation_preview.png)
