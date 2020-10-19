---
title: レポートのベストプラクティス
description: キャンペーンレポートのベストプラクティス
page-status-flag: never-activated
uuid: 09de6a17-b3a7-4543-b672-b0a21653aa75
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: reporting-in-adobe-campaign
discoiquuid: 904961e0-7dff-4350-8d5d-e4bdd368b3ff
translation-type: tm+mt
source-git-commit: 2a82493deada11cb22ef37d215b6eae8274ce890
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 81%

---


# レポートのベストプラクティス{#best-practices-reporting}

## ニーズの分析{#analyzing-needs}

レポートツールの使用は、操作するデータの量、複雑さ、セットアップするレポートの種類によって左右されます

レポートの作成、使用、永続性を最適化するには、対応しようとしているニーズを十分に把握する必要があります。この最初の分析では、作成するレポートの種類と最適な作成モードを特定しますレポートを作成するには、次の手順に従います。

1. ニーズの特定

   最初の手順は、ニーズ、つまり、レポートに表示する内容とその目的（監視、分析、データのエクスポートなど）を明確に特定することです。

   Adobe Campaign には、様々なレポート機能が用意されています。最適な機能を特定するには、ニーズを分析することが重要です。

   例えば、次のようなことが可能です。

   * データベース内のデータを調べ、測定値を定義します。 Learn more [in this section](../../reporting/using/about-cubes.md)
   * 既存追加のレポートに対するインジケーター。 Learn more [in this section](../../reporting/using/about-reports-creation-in-campaign.md)
   * データベース内のデータを表示します。 Learn more [in this section](../../reporting/using/about-descriptive-analysis.md)
   * 新しい配信レポートを作成します。 Learn more [in this section](../../reporting/using/about-reports-creation-in-campaign.md)),
   * Export data from the Adobe Campaign database (via a workflow, refer to [this section](../../workflow/using/about-workflows.md)
   * ピボットテーブルを作成します。Learn more [in this section](../../reporting/using/creating-a-table.md#creating-a-breakdown-or-pivot-table)
   * 集計データを表示します。 Learn more [in this section](../../reporting/using/about-cubes.md)
   * ウィザードを使用してデータを分析します。 Learn more [in this section](../../reporting/using/about-descriptive-analysis.md)
   * 大量のデータを分析する。 Learn more [in this section](../../reporting/using/about-reports-creation-in-campaign.md)

1. ターゲット母集団の特定

   次に、作成したいレポートのターゲットを割り出して、誰にレポートを表示させるかという公開の種類とレポートの表示モード（ブラウザーで、Adobe Campaign で、特定のオブジェクト向け、プラットフォーム全体向けなど）を把握する必要があります。

   また、次のオペレーター向けにレポートを作成できます。

   * すべての Adobe Campaign オペレーター
   * マーケティングキャンペーンへのアクセス権のみを持つオペレーター
   * 一時使用のための単一オペレーター
   * Web にアクセスしているすべてのオペレーターなど

   これらを検討する際には、アクセス権とセキュリティに関する問題も考慮に入れる必要があります。

1. コンテンツの定義

   次に、配信指標、データベースプロファイルに関するレポートなど、表示したいデータのタイプを割り出す必要があります。

   また、このデータの特性（単純、計算結果、重要など）、データの場所（Adobe Campaign 内、サードパーティシステム内）、計算周期を定義するためのデータ更新頻度（毎日、毎週、不定期）およびデータ量も把握する必要があります。

   データの量と更新に関する問題を慎重に検討して、レポートの表示上の問題、特に時間的な問題を回避する必要があります。そのため、集計を作成して、一部のデータをレポートの処理とは別に事前計算しておくことをお勧めします。トラッキングログと配信ログのテーブルには、何百万ものレコードを格納できます。これは、データをワークフローで集計してレポートで使用できるようにする必要があることを意味します。

## レポート作成の最適化{#optimizing-report-creation}

### データ量 {#data-volume}

最適なパフォーマンスを保証するには、操作対象のデータの量が多すぎてはいけません。

つまり、

* レポートの計算時間が 5 分を超えないようにしてください。

   同様に、設計フェーズで少量のデータに対してレポートの計算時間が 60 秒を超える場合は、計算方法を変更する必要があります。

* Marketing Analyticsモジュールを使用する場合、レポートデータは1,000万行を超えてはなりません。

また、集計の計算を夜間におこない、その集計データを直接レポートで使用することをお勧めします。これらの集計は、専用のデータ管理ワークフロー（SQL クエリ）で作成する必要があります。

また、レポートの計算を夜間におこない、データベースに過大な負荷をかけることなくいつでも表示できる履歴を自動的に作成することもできます。

### クエリ {#queries}

できる限り SQL クエリを使用し、JavaScript による後処理を避けることをお勧めします。必要な場合は、ワークフローでスクリプトアクティビティを使用し、計算に使用されたデータを削除します。また、アーカイブしたデータを使用して、処理時間を短縮することもできます。

その場合は、次の構文を使用する必要があります。

```
if(string(ctx@_historyId)!==""))
```

レポートに表示するデータを収集できるクエリは、複雑すぎないものにしてください。特に、データベース内のすべてのデータに適用する場合は注意が必要です。パフォーマンスを向上させるには、これらのクエリを実行する前にデータをフィルターすると役に立つことがあります。つまり、データの一部のみを計算の対象とすることになります。

### パフォーマンス {#performances}

上記の推奨事項に従うことで、レポートの計算を最適化できます。

さらに、Adobe Campaign では、次の改善を推奨します。

* データモデルの操作：インデックス付きフィールドは、主に数式の改善に使用する必要があります。

   インデックス付きのフィールドをすばやく見つけるには、Adobe Campaign のインターフェイスで列の名前に注目します。フィールドにインデックスが付いている場合、並べ替え矢印に赤の下線が付いています。

   For more on indexes, refer to [this section](../../configuration/using/data-model-best-practices.md#indexes).

* レポートの拡張性が高いことを確認します。時間の経過とともに、データ量が大幅に増加する可能性があります。

   同様に、テストフェーズで操作するデータの量は、本番での実際のデータ量と異なる場合があります。テストフェーズが重要なのは、そのためです。

   最後に、データパージの遅延を認識して、データが操作しやすくなるように、必要に応じて遅延を調整する必要があります。

   クリーンアップとデータ保持の詳細については、 [このセクションを参照してください](../../configuration/using/data-model-best-practices.md#data-retention)。

### レポートのエクスポート {#exporting-reports}

レポートのエクスポートに特有の推奨事項について詳しくは、[この節](../../reporting/using/actions-on-reports.md#exporting-a-report)を参照してください。
