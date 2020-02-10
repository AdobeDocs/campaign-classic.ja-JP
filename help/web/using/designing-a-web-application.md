---
title: Web アプリケーションの設計
seo-title: Web アプリケーションの設計
description: Web アプリケーションの設計
seo-description: null
page-status-flag: never-activated
uuid: 29c11154-f056-4047-849a-739ba0a2c615
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: web-applications
discoiquuid: 08efa472-d090-404d-9ad7-47adb3489c30
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c9c9d5f96856ce9e19571bad032d2bf04eaa60bd

---


# Web アプリケーションの設計{#designing-a-web-application}

Web applications are created and managed according to the same principle as [online surveys](../../web/using/about-surveys.md).

ただし、機能的な違いは次のとおりです。

* Web アプリケーションは、アーカイブされたフィールドを使用しません。データは、そのため、データベースフィールドまたはローカル変数にのみ格納されます。
* Webアプリケーションに関する組み込みレポートはありません。
* 追加のフィールドは、主にテーブルやグラフを作成する場合に使用します。

>[!CAUTION]
>
>Web アプリケーション構築プロセスで早期にエラーを検出するために、適用した設定を継続的にチェックすることを強くお勧めします。To check the rendering of a modification, save the application, then click the **[!UICONTROL Preview]** sub-tab.
>
>Web アプリケーションがパブリッシュされるまで、変更はエンドユーザーには表示されません。

## Web アプリケーションへのグラフの追加 {#inserting-charts-in-a-web-application}

Web アプリケーションにグラフを含めることができます。そのためには、ツールバーにあるグラフのドロップダウンリストを使用して、挿入するグラフのタイプを選択します。

![](assets/s_ncs_admin_webapps_bar_graph.png)

メニューを選択することもで **[!UICONTROL Add a chart]** きます。

![](assets/s_ncs_admin_webapps_graph.png)

## Web アプリケーションへのテーブルの追加 {#inserting-tables-in-a-web-application}

テーブルを追加するには、ツールバーにあるテーブルのドロップダウンリストを使用して、使用するテーブルのタイプを選択します。

![](assets/s_ncs_admin_webapps_bar_table.png)

また、ドロップダウンメニューでテーブルのタイプを選択することもできます。

![](assets/s_ncs_admin_webapps_table.png)

## 概要タイプの Web アプリケーション {#overview-type-web-applications}

Adobe Campaign インターフェイスは、受信者、配信、キャンペーン、在庫などのアクセス、管理、操作に、多くの Web アプリケーションを使用します。

それらは、1 ページのみのダッシュボードの形のインターフェイスで表示されます。

そのまま使用できるWebアプリケーションは、ノードに保存され **[!UICONTROL Administration > Configuration > Web applications]** ます。

## フォームタイプのWebアプリケーションの編集 {#edit-forms-type-web-applications}

エクストラネット用のフォームを編集 Web アプリケーションには、次の特徴があります。

* プリロードボックス

   ほとんどの場合、表示されるデータは、プリロードされる必要があります。これらのフォームにアクセスするユーザーは識別される（アクセス制御で）ので、プリロードは暗号化される必要はありません。

* 保存ボックス
* ページの追加

   すべての「概要」タイプの Web アプリケーションは単一ページなのに対して、編集フォームは、特定の条件（テスト、選択肢、関係するオペレーターのプロファイルなど）に基づいた一連のページを提供できます。

このタイプの Web アプリケーションの操作は、**調査**&#x200B;に似ていますが、履歴管理またはフィールドのアーカイブがありません。ユーザーは、通常、自己を証明する必要があるログインページを使用してアクセスします。
