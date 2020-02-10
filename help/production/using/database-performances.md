---
title: データベースのパフォーマンス
seo-title: データベースのパフォーマンス
description: データベースのパフォーマンス
seo-description: null
page-status-flag: never-activated
uuid: 47ff7532-1fe7-47c2-bc3b-0f46d3a4a288
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: 6358c8fd-2b75-4462-acd1-887ee44d3110
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 34cd6e6cf5652c9e2163848c2b1ef32f53ee6ca4

---


# データベースのパフォーマンス{#database-performances}

ほとんどのパフォーマンスの問題は、データベースのメンテナンスに関連しています。 パフォーマンスの低下の原因を見つけるための主な4つのリードを示します。

* 設定,
* Adobe Campaignプラットフォームのインストールと設定、
* データベースメンテナンス,
* リアルタイム診断。

## 設定 {#configuration}

最初のAdobe Campaignプラットフォームの設定が引き続き有効であることを確認し、必要に応じて、配信品質やデータベースサイズの観点から顧客のニーズを再評価します。 また、完全なハードウェアチェック（CPU、RAM、IOシステム）を実行することをお勧めします。

>[!NOTE]
>
>インサイトについては、 [Adobe Campaign Harware Sizing Guideを参照してください](https://helpx.adobe.com/campaign/kb/hardware-sizing-guide.html) 。

## プラットフォーム設定 {#platform-configuration}

不適切な設定は、プラットフォームのパフォーマンスに影響を与える可能性があります。 ネットワーク設定、プラットフォームの配信品質オプション、およびMTA設定を **serverConf.xmlファイルで確認することをお勧めします** 。

## データベースメンテナンス {#database-maintenance}

**データベースのクリーンアップタスク**

データベースのクリーンアップタスクが動作していることを確認してください。 これを行うには、ログファイルを表示して、エラーが含まれているかどうかを確認します。 詳しくは、[この節](../../production/using/database-cleanup-workflow.md)を参照してください。

**メンテナンスプラン**

データベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 これを行うには、データベース管理者に問い合わせて、次の情報を確認してください。

* 彼らのメンテナンススケジュール
* 以前に実施された保守計画
* スクリプトログを表示します。

詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

>[!CAUTION]
>
>中間ソーシング設定を使用する場合は、データベースを定期的に保守する必要があります。 マーケティングプラットフォーム上の配信を分析する際、マーケティングインスタンスは中間ソーシングインスタンスに情報を送信します。 プロセスの速度が低下すると、マーケティングインスタンスに影響が及びます。

**作業テーブルの管理**

作業用テーブルの数とサイズを確認してください。 特定のサイズを超えると、データベースのパフォーマンスが低下します。 これらのテーブルはワークフローと配信によって作成されます。 ワークフローと配信がアクティブな間は、データベースに残ります。 作業テーブルのサイズを制限するには、次の操作を実行します。

* 次のステータスの配信を停止または削除します。 **[!UICONTROL Failed]** 、 **[!UICONTROL In progress]** 、 **[!UICONTROL Ready for delivery]** 、ま **[!UICONTROL Paused]** たは
* エラーが原因で一時停止したワークフローを停止または削除します。
* アクティビティを含まず、ステータスが残るテストに使用されるすべて **[!UICONTROL End]** のワークフローを停止しま **[!UICONTROL Paused]** す。

>[!CAUTION]
>
>操作に時間がかかり、大量のスペースが解放される場合は、インデックスの再構築など、詳細なメンテナンスが必要です。 詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

**Adobe Campaignプロセス監視**

Adobe Campaignのインストール設定に応じて、プラットフォーム監視には次の2つのツールを使用できます。

* インスタンス実稼働ページ。 For more on this, refer to [Manual monitoring](../../production/using/monitoring-processes.md#manual-monitoring).
* netreportスクリプト。 詳しくは、「Adobe Campaignスクリプトを使用し [た自動監視」を参照してください](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts)。

## 詳細 {#specifics}

問題の原因を特定するために、リアルタイム診断を実行する必要が生じる場合があります。 まず、プロセスおよびプラットフォームのログファイルを確認し、問題の再作成中にデータベースのアクティビティを監視します。 特に、以下の点に注意してください。

* 整備計画
* 実行中のSQLクエリ、
* 外部プロセスが同時に実行されているかどうか（クレンジング、インポート、集計計算など）。

