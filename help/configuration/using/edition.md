---
product: campaign
title: Campaign エクスプローラーのナビゲーションツリーを編集
description: Campaign エクスプローラーのナビゲーションツリーを編集
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
exl-id: 204d4a24-267c-4976-90d9-7bf5bee8d116
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Campaign エクスプローラーのナビゲーションツリーを編集{#edition}

ナビゲーション階層設定ドキュメントを作成および設定する画面には、 **[!UICONTROL 管理/設定/ナビゲーション階層]** ノード：

![](assets/d_ncs_integration_navigation_arbo.png)

ナビゲーション階層の設定は、複数の XML ドキュメントに分かれています。 この関数は、スキーマ拡張と同様の原則に基づいて動作します。設定全体を含む単一のドキュメントを生成するために、すべてのドキュメントがマージされます。 このドキュメントは編集できず、「プレビュー」タブで表示されます。

編集フィールドは、XML ドキュメントのコンテンツを提供します。

![](assets/d_ncs_integration_navigation_edit.png)

>[!NOTE]
>
>「名前」編集コントロールを使用して、名前と名前空間で構成されるドキュメントキーを入力できます。 の「name」属性と「namespace」属性 **`<navtree>`** 要素は、スキーマの XML 編集フィールドで自動的に更新されます。

プレビューにより、完全な設定を含む結合ドキュメントが自動的に生成されます。

![](assets/d_ncs_integration_navigation_preview.png)
