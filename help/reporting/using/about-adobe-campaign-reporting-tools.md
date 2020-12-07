---
solution: Campaign Classic
product: campaign
title: Adobe Campaign のレポートツールについて
description: 組み込みレポートまたはカスタマイズされたレポートでキャンペーンの成果を分析します。
audience: reporting
content-type: reference
topic-tags: reporting-in-adobe-campaign
translation-type: ht
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: ht
source-wordcount: '334'
ht-degree: 100%

---


# レポートの概要{#about-adobe-campaign-reporting-tools}

Adobe Campaign では、[組み込みレポート](../../reporting/using/about-campaign-built-in-reports.md)のほかにも、様々なコンテキストで様々なニーズに応えるレポートを生成できます。このドキュメントでは、使用モードと実装モードの基本事項について詳しく説明します。

Adobe Campaign は、レポート専用ツールではありません。Adobe Campaign で作成されたレポートを使用すると、主に集計データを表示できます。Adobe Campaign のレポートは、データの分析および表示専用であり、データベースエクスポート用には設計されていません。

Adobe Campaign データベースからデータをエクスポートするには、ワークフローを作成して、データエクスポートアクティビティを使用する必要があります。詳しくは、[この節](../../workflow/using/about-action-activities.md)を参照してください。

Adobe Campaign には、いくつかのレポートツールが用意されています。

1. **組み込みレポート**：配信、キャンペーン、プラットフォームアクティビティ、オプション機能などに関する一連のレポートが用意されています。これらのレポートは、関連する様々な機能を通じて使用できます。具体的なニーズに合わせてレポートをカスタマイズすることもできます。

   詳しくは、[この節](../../reporting/using/about-campaign-built-in-reports.md)を参照してください。

1. **記述的データ分析**：データベース内のデータに関する統計情報を生成できる視覚的なツールが用意されています。専用のウィザードを使用して記述的分析レポートを作成でき、そのコンテンツやレイアウトをニーズに応じてカスタマイズできます。

   詳しくは、[この節](../../reporting/using/about-descriptive-analysis.md)を参照してください。

1. **パーソナライズされたレポート**：データベース内のデータに関するレポートを作成できます。作成されたレポートは、適切なコンテキストで参照可能になります。

   複雑なクエリや計算が必要な場合や、データ量が多い場合には、レポートで分析されるデータをクエリによって収集し、リスト（「データ管理」タイプのワークフロー）やキューブ（マーケティング分析を使用）で事前集計することもできます。データはピボットテーブルまたはグループリストの形式で表示されます。

   詳しくは、[この節](../../reporting/using/about-reports-creation-in-campaign.md)を参照してください。

1. **分析レポート**：マーケティング分析を使用すれば、直観的なデータ調査が可能になります。

   詳しくは、[この節](../../reporting/using/about-cubes.md)を参照してください。

>[!CAUTION]
>
>表示や操作が簡単になるように、また、エクスポートを効率的におこなえるように、レポートの行数は 1,000 行を超えないようにしてください。