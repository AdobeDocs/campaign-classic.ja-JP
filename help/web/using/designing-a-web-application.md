---
product: campaign
title: web アプリケーションの設計
description: web アプリケーションの設計
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Web Apps
exl-id: dcdf6afc-321e-4027-a350-fff6bbf22e71
TQID: https://experienceleague.adobe.com/8HdoOgOBgZgI3-Kxnn-I0kW5zyTSBfUtM0IoLGBvHag
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: c5474392-5419-4296-9e41-f6f4ce4f6e9bid: a4671286-a59f-47e3-b97b-90627a1977d5
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
subfeature_v2: id: f391046b-0cf3-4e76-bd3b-97fe06654506id: ed29abcd-b6a8-4d4b-ab8b-b7e746973281id: d7be2b01-dc9c-40f7-aace-a151707504ed
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 309
ht-degree: 100%

---

# Web アプリケーションの設計{#designing-a-web-application}



Web アプリケーションは、[web フォーム](about-web-forms.md)と同じ原則に従って作成および管理されます。

>[!CAUTION]
>
>「**[!UICONTROL プレビュー]**」サブタブを使用すると、web アプリケーションの設計時にエラーを確認できます。 Web アプリケーションのプレビューに使用するプロファイルテストは、**[!UICONTROL web アプリケーションエージェント]**&#x200B;のオペレーターの&#x200B;**[!UICONTROL アクセス権]**&#x200B;があるフォルダーに置く必要があることに注意してください。 </br>Web アプリケーションが公開されるまで、変更はエンドユーザーには公開されません。

## Web アプリケーションへのグラフの挿入 {#inserting-charts-in-a-web-application}

Web アプリケーションにグラフを含めることができます。 そのためには、ツールバーにあるグラフのドロップダウンリストを使用して、挿入するグラフのタイプを選択します。

![](assets/s_ncs_admin_webapps_bar_graph.png)

また、**[!UICONTROL グラフを追加]**&#x200B;メニューを選択することもできます。

![](assets/s_ncs_admin_webapps_graph.png)

## Web アプリケーションへのテーブルの挿入 {#inserting-tables-in-a-web-application}

テーブルを追加するには、ツールバーにあるテーブルのドロップダウンリストを使用して、使用するテーブルのタイプを選択します。

![](assets/s_ncs_admin_webapps_bar_table.png)

また、ドロップダウンメニューでテーブルのタイプを選択することもできます。

![](assets/s_ncs_admin_webapps_table.png)

## 概要タイプの Web アプリケーション {#overview-type-web-applications}

Adobe Campaign インターフェイスは、受信者、配信、キャンペーン、在庫などのアクセス、管理、操作に、多くの Web アプリケーションを使用します。

それらは、1 ページのみのダッシュボードの形のインターフェイスで表示されます。

標準の Web アプリケーションは、**[!UICONTROL 管理／設定／Web アプリケーション]**&#x200B;ノードに格納されています。

## フォームタイプの Web アプリケーションの編集 {#edit-forms-type-web-applications}

エクストラネット用のフォームを編集 Web アプリケーションには、次の特徴があります。

* プリロードボックス

  ほとんどの場合、表示されるデータは、プリロードされる必要があります。 これらのフォームにアクセスするユーザーは識別される（アクセス制御で）ので、プリロードは暗号化される必要はありません。

* 保存ボックス
* ページの追加

  すべての「概要」タイプの Web アプリケーションは単一ページなのに対して、編集フォームは、特定の条件（テスト、選択肢、関係するオペレーターのプロファイルなど）に基づいた一連のページを提供できます。

