---
title: 版
seo-title: 版
description: 版
seo-description: null
page-status-flag: never-activated
uuid: df9298fc-5f62-4afb-8118-ca7e3987e81f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: navigation-hierarchy
discoiquuid: 820be231-af76-44ce-8f4d-cd5eae1eb169
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# 版{#edition}

ナビゲーション階層設定ドキュメントを作成および設定する画面は、次のノードからアクセスで **[!UICONTROL Administration > Configuration > Navigation hierarchies]** きます。

![](assets/d_ncs_integration_navigation_arbo.png)

ナビゲーション階層の設定は、複数のXMLドキュメントに分かれています。 スキーマ拡張と同じ原理に基づいて動作します。すべてのドキュメントがマージされ、設定全体を含む単一のドキュメントが生成されます。 このドキュメントは編集できず、「プレビュー」タブで表示されます。

編集フィールドには、XMLドキュメントのコンテンツが表示されます。

![](assets/d_ncs_integration_navigation_edit.png)

>[!NOTE]
>
>「名前」編集コントロールを使用すると、名前と名前空間で構成されるドキュメントキーを入力できます。 The &quot;name&quot; and &quot;namespace&quot; attributes of the **`<navtree>`** element are automatically updated in the XML edit field of the schema.

プレビューにより、次の設定を含む結合ドキュメントが自動的に生成されます。

![](assets/d_ncs_integration_navigation_preview.png)

