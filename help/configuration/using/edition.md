---
product: campaign
title: エディション
description: エディション
audience: configuration
content-type: reference
topic-tags: navigation-hierarchy
exl-id: 204d4a24-267c-4976-90d9-7bf5bee8d116
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 1%

---

# Campaignエクスプローラーのナビゲーションツリーを編集{#edition}

ナビゲーション階層設定ドキュメントを作成および設定する画面には、**[!UICONTROL 管理/設定/ナビゲーション階層]**&#x200B;ノードからアクセスできます。

![](assets/d_ncs_integration_navigation_arbo.png)

ナビゲーション階層の設定は、複数のXMLドキュメントに分割されます。 これは、スキーマ拡張と同様の原則に基づいて動作します。設定全体を含む単一のドキュメントを生成するために、すべてのドキュメントが結合されます。 このドキュメントは編集できず、「プレビュー」タブに表示されます。

編集フィールドは、XMLドキュメントのコンテンツを提供します。

![](assets/d_ncs_integration_navigation_edit.png)

>[!NOTE]
>
>「名前」編集コントロールを使用して、名前と名前空間で構成されるドキュメントキーを入力できます。 **`<navtree>`**&#x200B;要素の「name」属性と「namespace」属性は、スキーマのXML編集フィールドで自動的に更新されます。

プレビューは、完全な設定を含む結合ドキュメントを自動的に生成します。

![](assets/d_ncs_integration_navigation_preview.png)
