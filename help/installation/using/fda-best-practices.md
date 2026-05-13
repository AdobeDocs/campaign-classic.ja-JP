---
product: campaign
title: Campaign FDAのベストプラクティスと制限
description: 外部データベース（FDA）を操作する際のベストプラクティスと制限事項について説明します
feature: Installation, Federated Data Access
audience: platform
content-type: reference
topic-tags: connectors
exl-id: f3980859-2837-416b-a0ef-2b369d2d50bd
TQID: https://experienceleague.adobe.com/o9F-VJpel6oYo-4N8nd25xW69ZAN-RpH9TaZ2jJeq-k
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 517
ht-degree: 56%

---

# ベストプラクティスと制限事項



## 外部データを利用して、メールのパーソナライゼーションを最適化 {#optimizing-email-personalization-with-external-data}

専用のワークフローで、メッセージのパーソナライゼーションを事前に処理できます。 これを実行するには、配信プロパティの「**[!UICONTROL 分析]**」タブにある「**[!UICONTROL ワークフローを使用してパーソナライズ機能データを準備]**」オプションを使用します。

このオプションを選択すると、配信を分析する際、ターゲットにリンクされているすべてのデータ（リンクされている外部データベースのテーブルのデータを含む）を一時テーブルに保存するワークフローが、自動的に作成および実行されます。

このオプションにより、パーソナライゼーション手順を実行する際のパフォーマンスが大幅に向上します。

## ワークフローでの外部データベースからのデータの使用 {#using-data-from-an-external-database-in-a-workflow}

複数のAdobe Campaign ワークフローアクティビティでは、外部データベースに保存されているデータを使用できます。

* **外部データに対するフィルター** - クエリ アクティビティを使用すると、外部データを追加し、定義されたフィルター設定で使用できます。 詳しくは、[Campaign v8 ドキュメント ]https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/wf-type/targeting-workflows.html） {target="_blank"}を参照してください。

* **サブセットを作成** – 分割アクティビティを使用すると、サブセットを作成できます。 外部データを使用して、適用するフィルタリング条件を定義できます。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/split.html?lang=ja){target="_blank"}を参照してください。

* **外部データベースを読み込む** - データ読み込み（RDBMS）アクティビティで外部データを使用できます。 詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/action-activities/data-loading-rdbms.html){target="_blank"}を参照してください。

* **情報とリンクの追加** - エンリッチメントアクティビティを使用すると、ワークフローのワークテーブルに追加データを追加したり、外部テーブルにリンクしたりできます。 こうすることで、外部データベースのデータを使用できます。 [Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/enrichment.html?lang=ja){target="_blank"}を参照してください。

## ガードレールと制限 {#fda-limitations}

FDA オプションは、ワークフローのバッチモードで外部データベースのデータを操作するように設計されています。 パフォーマンスの問題を回避するために、パーソナライゼーション、インタラクション、リアルタイムメッセージなどの単一操作のコンテキストでは、FDA モジュールを使用しないことをお勧めします。

あるデータベースのデータをターゲットにして、別のデータベースに属するフィルタリングディメンションを使用して結果をフィルタリングすることはサポートされていません。 1つのクエリで異なるデータソースにあるテーブルを結合することはできません。 ディメンションの変更などの他のワークフローアクティビティを使用して、この制限を克服できます。

Adobe Campaign と外部データベースの両方を使用する必要がある操作は、できるだけおこなわないようにします。 ベストプラクティスは次のとおりです。

* Adobe Campaign データベースを外部データベースにエクスポートし、外部データベースからのみ操作を実行して、その結果を Adobe Campaign に再インポートします。

* 外部の Adobe Campaign データベースからデータを収集し、ローカルで操作を実行します。

外部データベースのデータを使用する配信でパーソナライゼーションを実行する場合は、ワークフローで使用するデータを収集して一時テーブルに格納してから、 一時テーブルのデータを使用して配信をパーソナライズします。

FDA オプションには、使用する外部データベースシステムの制限事項が適用されます。
