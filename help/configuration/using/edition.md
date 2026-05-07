---
product: campaign
title: Campaign エクスプローラーのナビゲーションツリーの編集
description: Campaign エクスプローラーのナビゲーションツリーの編集
feature: Application Settings
role: Developer
exl-id: 204d4a24-267c-4976-90d9-7bf5bee8d116
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '135'
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
