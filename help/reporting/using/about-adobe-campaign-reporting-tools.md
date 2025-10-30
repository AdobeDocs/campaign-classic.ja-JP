---
product: campaign
title: Adobe Campaign のレポートツールについて
description: 組み込みレポートまたはカスタマイズされたレポートでキャンペーンの成果を分析します
feature: Reporting, Monitoring
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
exl-id: 1ef30004-e1b0-4dde-8104-0ee9e8aa9d8b
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: ht
source-wordcount: '347'
ht-degree: 100%

---

# レポートの基本を学ぶ {#about-adobe-campaign-reporting-tools}



Adobe Campaign では、[ビルトインレポート](../../reporting/using/about-campaign-built-in-reports.md)のほかにも、様々なコンテキストで様々なニーズに応えるレポートを生成できます。
このドキュメントでは、使用モードと実装モードの基本事項について詳しく説明します。

Adobe Campaign は、レポート専用ツールではありません。Adobe Campaign で作成されたレポートを使用すると、主に集計データを表示できます。Adobe Campaign のレポートは、データの分析および表示専用であり、データベースエクスポート用には設計されていません。

Adobe Campaign データベースからデータをエクスポートするには、ワークフローを作成して、データエクスポートアクティビティを使用する必要があります。詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/action-activities/action-activities.html?lang=ja){target="_blank"}を参照してください。

Adobe Campaign には、いくつかのレポートツールが用意されています。

1. **ビルトインレポート**：配信、キャンペーン、プラットフォームアクティビティ、オプション機能などに関する一連のレポートが用意されています。
これらのレポートは、関連する様々な機能を通じて使用できます。具体的なニーズに合わせてレポートをカスタマイズすることもできます。

   詳しくは、[この節](../../reporting/using/about-campaign-built-in-reports.md)を参照してください。

1. **記述的データ分析**：データベース内のデータに関する統計情報を生成できる視覚的なツールが用意されています。専用のアシスタントを使用して記述的な分析レポートを作成し、ニーズに応じてコンテンツやレイアウトをカスタマイズできます。

   詳しくは、[この節](../../reporting/using/about-descriptive-analysis.md)を参照してください。

1. **パーソナライズされたレポート**：データベース内のデータに関するレポートを作成できます。作成されたレポートは、適切なコンテキストで参照可能になります。

   複雑なクエリや計算が必要な場合や、データ量が多い場合には、レポートで分析されるデータをクエリによって収集し、リスト（「データ管理」タイプのワークフロー）やキューブ（マーケティング分析を使用）で事前集計することもできます。データはピボットテーブルまたはグループリストの形式で表示されます。

   詳しくは、[この節](../../reporting/using/about-reports-creation-in-campaign.md)を参照してください。

1. **分析レポート**：マーケティング分析を使用すれば、直観的なデータ調査が可能になります。

   詳しくは、[この節](../../reporting/using/ac-cubes.md)を参照してください。

>[!CAUTION]
>
>表示や操作が簡単になるように、また、エクスポートを効率的におこなえるように、レポートの行数は 1,000 行を超えないようにしてください。
