---
solution: Campaign Classic
product: campaign
title: エディション
description: エディション
audience: configuration
content-type: reference
topic-tags: navigation-hierarchy
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 2%

---


# エディション{#edition}

ナビゲーション階層設定ドキュメントを作成および設定する画面は、 **[!UICONTROL 管理/設定/ナビゲーション階層]** ノードからアクセスできます。

![](assets/d_ncs_integration_navigation_arbo.png)

ナビゲーション階層の設定は、複数のXMLドキュメントに分かれています。 これは、スキーマ拡張と同様の原則に基づいて動作します。すべてのドキュメントが結合され、設定全体を含む単一のドキュメントが生成されます。 このドキュメントは編集できず、「プレビュー」タブに表示されます。

編集フィールドには、XMLドキュメントのコンテンツが表示されます。

![](assets/d_ncs_integration_navigation_edit.png)

>[!NOTE]
>
>「名前」編集コントロールを使用すると、名前と名前空間で構成されるドキュメントキーを入力できます。 The &quot;name&quot; and &quot;namespace&quot; attributes of the **`<navtree>`** element are automatically updated in the XML edit field of the schema.

プレビューは、次の設定を含む結合ドキュメントを自動的に生成します。

![](assets/d_ncs_integration_navigation_preview.png)

