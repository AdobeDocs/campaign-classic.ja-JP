---
product: campaign
title: Campaign エクスプローラーナビゲーションツリーの編集
description: Campaign エクスプローラーナビゲーションツリーの編集
feature: Application Settings
role: Data Engineer, Developer
exl-id: 204d4a24-267c-4976-90d9-7bf5bee8d116
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Campaign エクスプローラーナビゲーションツリーの編集{#edition}

ナビゲーション階層設定ドキュメントを作成および設定する画面には、 **[!UICONTROL 管理/設定/ナビゲーション階層]** ノード：

![](assets/d_ncs_integration_navigation_arbo.png)

ナビゲーション階層の設定は、複数の XML ドキュメントに分かれています。 これは、スキーマ拡張と同様の原則で動作します。すべてのドキュメントが結合されて、設定全体を含む単一のドキュメントが生成されます。 このドキュメントは編集できず、[ プレビュー ] タブで表示されます。

編集フィールドには、XML ドキュメントのコンテンツが表示されます。

![](assets/d_ncs_integration_navigation_edit.png)

>[!NOTE]
>
>「名前」編集コントロールを使用すると、名前と名前空間で構成されるドキュメントキーを入力できます。 の「name」属性と「namespace」属性 **`<navtree>`** 要素は、スキーマの XML 編集フィールドで自動的に更新されます。

プレビューでは、完全な設定を含む結合ドキュメントが自動的に生成されます。

![](assets/d_ncs_integration_navigation_preview.png)
