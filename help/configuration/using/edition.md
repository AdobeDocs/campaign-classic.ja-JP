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

ナビゲーション階層の設定ドキュメントを作成および設定する画面は、**[!UICONTROL 管理/設定/ナビゲーション階層]**&#x200B;ノードからアクセスできます。

![](assets/d_ncs_integration_navigation_arbo.png)

ナビゲーション階層の設定は、複数のXMLドキュメントに分かれています。 これは、スキーマ拡張と同様の原則に基づいて動作します。すべてのドキュメントが結合され、設定全体を含む単一のドキュメントが生成されます。 このドキュメントは編集できず、「プレビュー」タブに表示されます。

編集フィールドには、XMLドキュメントのコンテンツが表示されます。

![](assets/d_ncs_integration_navigation_edit.png)

>[!NOTE]
>
>「名前」編集コントロールを使用すると、名前と名前空間で構成されるドキュメントキーを入力できます。 **`<navtree>`**&#x200B;要素の「name」と「名前空間」属性は、スキーマのXML編集フィールドで自動的に更新されます。

プレビューは、次の設定を含む結合ドキュメントを自動的に生成します。

![](assets/d_ncs_integration_navigation_preview.png)

