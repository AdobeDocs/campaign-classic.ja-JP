---
title: レポートのリスト
seo-title: レポートのリスト
description: レポートのリスト
seo-description: null
page-status-flag: never-activated
uuid: 79a914d0-7828-4fe1-b1b7-b055d4bf1f82
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: accessing-built-in-reports
discoiquuid: 3e593527-5580-44ea-93dc-9084d862537e
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: f7655cd93a7dc8ecd35cd379da350ad279cae725

---


# レポートのリスト{#list-of-reports}

## 配信に関するレポート {#reports-on-deliveries}

以下の表に、Adobe Campaign によって提供される組み込みレポートを示します。

これらのレポートの内容について詳しくは、[この節](../../reporting/using/delivery-reports.md)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベルと内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
   <td> <strong>スキーマ</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> ユーザーアクティビティ（recipientActivity）<br /> </td> 
   <td> 開封数、クリック数およびトランザクション数の時間別の分類。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信スループット（throughput）<br /> </td> 
   <td> メッセージ数/時間および M ビット/秒の配信スループットのグラフ。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信不能件数とバウンス数（errors）<br /> </td> 
   <td> 原因別ドメイン別バウンス数と配信不能件数<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> トラッキング指標（deliveryFeedback）<br /> </td> 
   <td> 受信者の行動をトラッキングするための主要指標の概要。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> トラッキング指標（mobileAppDeliveryFeedback）<br /> </td> 
   <td> モバイルアプリケーションへの配信のトラッキング指標。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> ブラウザー（browserStatistics）<br /> </td> 
   <td> メッセージをクリックした受信者が使用するブラウザーに関する統計。<br /> </td> 
   <td> xtk:none<br /> </td> 
  </tr> 
  <tr> 
   <td> ソーシャルネットワークへの共有（deliveryForward）<br /> </td> 
   <td> 共有アクティビティとメール開封に関する統計。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> ホットクリック（hoturls）<br /> </td> 
   <td> メッセージとクリック率を重ねて表示。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> 仮説レポート（deliveryHypothesis）<br /> </td> 
   <td> 配信仮説に関する測定の概要の表示。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信統計（statisticsPerDelivery）<br /> </td> 
   <td> E メールドメインごとの統計（処理メッセージ数、配信メッセージ数、ハードバウンス数、ソフトバウンス数、クリック数、購読解除数）。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> 共有アクティビティの統計（forwardActivities）<br /> </td> 
   <td> 期間ごとの共有アクティビティ数、開封数および購読数の分析。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> トラッキング統計（trackingStatistics）<br /> </td> 
   <td> 開封率、クリック率、トランザクション率に関するレポート。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信の概要（deliverySending）<br /> </td> 
   <td> 配信概要の指標：ターゲット数、除外数および送信メッセージ数。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信の概要（deliveryStatistics）<br /> </td> 
   <td> 選択した配信の概要テーブル : ターゲット、除外および送信されたメッセージ。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> オペレーティングシステム（osStatistics）<br /> </td> 
   <td> メッセージをクリックした受信者が使用するオペレーティングシステムに関する統計。<br /> </td> 
   <td> xtk:none<br /> </td> 
  </tr> 
  <tr> 
   <td> 反応率（deliveryFeedbackSocial）<br /> </td> 
   <td> 配信の反応率および反応の分類。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
  <tr> 
   <td> URL とクリックスループット（topUrlDelivery）<br /> </td> 
   <td> 最も反応の良い URL および関連するクリックストリーム。<br /> </td> 
   <td> nms:delivery<br /> </td> 
  </tr> 
 </tbody> 
</table>

## キャンペーンに関するレポート {#reports-on-campaigns}

キャンペーンに関するレポートは **nms:operation** テーブル内のデータに関係します。

以下の表に、Adobe Campaign によって提供される組み込みレポートを示します。

これらのレポートの内容について詳しくは、[この節](../../campaign/using/designing-marketing-campaigns.md)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベルと内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> ユーザーアクティビティ（operationRecipientActivity）<br /> </td> 
   <td> 開封数、クリック数およびトランザクション数の時間別の分類（Campaign に依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信スループット（operationThroughput）<br /> </td> 
   <td> メール数/時間および M ビット/秒の配信スループットのグラフ（Campaign に依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> キャンペーン費用（budgetOperationExpenses）<br /> </td> 
   <td> キャンペーンのライン項目の詳細を表示（Campaign に依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信不能件数とバウンス数（operationErrors）<br /> </td> 
   <td> 原因別およびドメイン別バウンス数と配信不能件数（Campaign に依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> コストラインの調査（budgetExplorerOperation）<br /> </td> 
   <td> コストラインの記述的分析（MRM に依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> トラッキング指標（operationFeedback）<br /> </td> 
   <td> 主要追跡インジケーターの概要：開封数、クリック数およびトランザクション数はキャンペーンに依存します。<br /> </td> 
  </tr> 
  <tr> 
   <td> ソーシャルネットワークへの共有（operationForward）<br /> </td> 
   <td> 共有アクティビティとメール開封に関する統計（Campaign に依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> 仮説レポート（operationHypothesis）<br /> </td> 
   <td> キャンペーン配信の仮説測定の概要を表示（Campaign に依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> 共有アクティビティの統計（forwardActivityOpt）<br /> </td> 
   <td> 期間ごとの共有アクティビティ数、開封数および購読数の分析（Campaign に依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> 配信の概要（operationStatistics）<br /> </td> 
   <td> キャンペーン配信の概要グラフ : ターゲット数、除外数および送信メッセージ数。<br /> </td> 
  </tr> 
  <tr> 
   <td> URL とクリックスループット（operationTopUrlDelivery）<br /> </td> 
   <td> 最も反応の良い URL および関連するクリックストリーム（Campaign に依存）。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## サービスに関するレポート {#reports-on-services}

サービスに関するレポートは **nms:service** テーブル内のデータに関係します。

以下の表に、Adobe Campaign によって提供される組み込みレポートを示します。

これらのレポートの内容について詳しくは、関連するガイドを参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベルと内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> ファン獲得（socialAcquisitionsByWebapp）<br /> </td> 
   <td> 見込み客の獲得を有効にした Web アプリケーションの分析。ソーシャルマーケティングのアドオンに依存します。<br /> </td> 
  </tr> 
  <tr> 
   <td> 購読の分類（mobileAppDistribution）<br /> </td> 
   <td> モバイルアプリケーションごとのアクティブな購読の分類（モバイルアプリチャネルのアドオンに依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> 購読トラッキング（subscriptionsProgress）<br /> </td> 
   <td> 情報サービスの購読数の変化。<br /> </td> 
  </tr> 
  <tr> 
   <td> 反応率（socialReactionRate）<br /> </td> 
   <td> 最新の配信の反応率。ソーシャルマーケティングのアドオンに依存します。<br /> </td> 
  </tr> 
  <tr> 
   <td> 反応率（mobileAppReactivityRate）<br /> </td> 
   <td> 最新の配信の反応率（モバイルアプリチャネルのアドオンに依存）。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 予算レポート {#budget-reports}

以下の表に、Adobe Campaign によって提供される組み込みレポートを示します。

これらのレポートの内容について詳しくは、[この節](../../campaign/using/designing-marketing-campaigns.md)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベルと内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
   <td> <strong>スキーマ</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> プログラムに関連するコスト（budgetProgramCost）<br /> </td> 
   <td> プログラムコストの内訳。<br /> </td> 
   <td> nms:program<br /> </td> 
  </tr> 
  <tr> 
   <td> 予算の変化（budgetEvolution）<br /> </td> 
   <td> コミットメントレベル別の予算コストの変化。<br /> </td> 
   <td> nms:budget<br /> </td> 
  </tr> 
  <tr> 
   <td> 予算の累積変化（budgetCumulativeEvolution）<br /> </td> 
   <td> Evolution of the cumulated budget costs broken down by commi<br /> tment level. </td> 
   <td> nms:budget<br /> </td> 
  </tr> 
  <tr> 
   <td> コストラインの調査（budgetExplorerBudget）<br /> </td> 
   <td> コストラインの記述的分析。<br /> </td> 
   <td> nms:budget<br /> </td> 
  </tr> 
  <tr> 
   <td> コストラインの調査（budgetExplorer）<br /> </td> 
   <td> コストラインの記述的分析。<br /> </td> 
   <td> nms:costLine<br /> </td> 
  </tr> 
  <tr> 
   <td> コストラインの調査（budgetExplorerPlan）<br /> </td> 
   <td> コストラインの記述的分析。<br /> </td> 
   <td> nms:plan<br /> </td> 
  </tr> 
  <tr> 
   <td> コストラインの調査（budgetExplorerProgram）<br /> </td> 
   <td> コストラインの記述的分析。<br /> </td> 
   <td> nms:program<br /> </td> 
  </tr> 
  <tr> 
   <td> 予算の概要（budget）<br /> </td> 
   <td> メインコスト、費用カテゴリおよび予算のスナップショット。<br /> </td> 
   <td> nms:budget<br /> </td> 
  </tr> 
 </tbody> 
</table>

## シミュレーションに関するレポート {#reports-on-simulations}

シミュレーションに関するレポートは **nms:simulation** テーブル内のデータに関係します。

以下の表に、Adobe Campaign によって提供される組み込みレポートを示します。

これらのレポートの内容について詳しくは、関連するガイドを参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベルと内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> シミュレーションの除外の詳細（dlvSimuLossesDetail）<br /> </td> 
   <td> 除外のすべての原因の詳細テーブル。<br /> </td> 
  </tr> 
  <tr> 
   <td> オファーのランク別分類（offerSimulationRanking）<br /> </td> 
   <td> シミュレーションでのオファーの分類（ランク別）。<br /> </td> 
  </tr> 
  <tr> 
   <td> シミュレーションの概要（dlvSimuLossesSummary）<br /> </td> 
   <td> シミュレーションの規模と除外条件の概要。<br /> </td> 
  </tr> 
  <tr> 
   <td> 重複統計情報（dlvSimuOverlapping）<br /> </td> 
   <td> 配信ターゲットの重複数。<br /> </td> 
  </tr> 
  <tr> 
   <td> シミュレーションによる除外の概要（dlvSimuLossesSimu）<br /> </td> 
   <td> シミュレーションによる除外のテーブル。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Web アプリケーションに関するレポート {#reports-on-web-applications}

Web アプリケーションに関するレポートは **nms:WebApp** テーブル内のデータに関係します。

以下の表に、Adobe Campaign によって提供される組み込みレポートを示します。

これらのレポートの内容について詳しくは、[この節](../../web/using/about-web-applications.md)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベルと内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> ドキュメント（surveyDictionary）<br /> </td> 
   <td> 調査の構造の説明（調査マネージャーのアドオンに依存）。<br /> </td> 
  </tr> 
  <tr> 
   <td> メイン（surveyProperties）<br /> </td> 
   <td> 調査のプロパティ。<br /> </td> 
  </tr> 
  <tr> 
   <td> 回答の分類（surveyDistribution）<br /> </td> 
   <td> 質問に対する回答の分類。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## その他の標準レポート {#other-ootb-reports}

次の組み込みレポートも用意されています。詳しくは、それぞれが関係する機能についてのドキュメントを参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベルと内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
   <td> <strong>スキーマ</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> オファー分析（offerAnalysis）<br /> </td> 
   <td> 日付別およびチャネル別のオファー分析（インタラクションのアドオンに依存）。<br /> </td> 
   <td> nms:offer<br /> </td> 
  </tr> 
  <tr> 
   <td> リマーケティングの効率（remarketingEffect）<br /> </td> 
   <td> リマーケティングの効率の測定。<br /> </td> 
   <td> nms:webEvent<br /> </td> 
  </tr> 
  <tr> 
   <td> ソーシャル見込み客の獲得履歴（socialVisitorStatistics）<br /> </td> 
   <td> Twitter および Facebook の見込み客獲得履歴（ソーシャルマーケティングのアドオンに依存）。<br /> </td> 
   <td> nms:visitor<br /> </td> 
  </tr> 
  <tr> 
   <td> 最近の提案トラッキング（recentPropositions）<br /> </td> 
   <td> リアルタイム提案トラッキング。<br /> </td> 
   <td> nms:propositionRcp<br /> </td> 
  </tr> 
 </tbody> 
</table>

