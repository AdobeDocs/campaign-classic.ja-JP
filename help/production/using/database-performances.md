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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 8%

---


# データベースのパフォーマンス{#database-performances}

パフォーマンスの問題のほとんどは、データベースのメンテナンスに関連しています。 パフォーマンスの低下の原因を特定する際に役立つ主な4つのリードを示します。

* 設定,
* Adobe Campaignプラットフォームのインストールと設定、
* データベースのメンテナンス,
* リアルタイム診断。

## 設定 {#configuration}

最初のAdobe Campaignプラットフォーム設定が引き続き有効であることを確認し、必要に応じて、配信品質やデータベースサイズの観点からお客様のニーズを再評価します。 また、完全なハードウェアチェック（CPU、RAM、IOシステム）を実行することをお勧めします。

>[!NOTE]
>
>インサイトについては、『 [Adobe Campaignハードウェアサイズガイド](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html) 』を参照してください。

## プラットフォームの設定 {#platform-configuration}

不適切な設定は、プラットフォームのパフォーマンスに影響を与える可能性があります。 ネットワーク設定、プラットフォームの配信品質オプション、およびMTA設定を **serverConf.xml** ファイルで確認することをお勧めします。

## データベースメンテナンス {#database-maintenance}

**データベースのクリーンアップタスク**

データベースのクリーンアップタスクが動作していることを確認してください。 これを行うには、ログファイルにエラーが含まれているかどうかを確認する表示を行います。 詳しくは、[この節](../../production/using/database-cleanup-workflow.md)を参照してください。

**保守計画**

データベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 これを行うには、データベース管理者に問い合わせて、次の情報を確認してください。

* 彼らのメンテナンススケジュール
* 以前に実行した保守計画
* スクリプトログの表示。

詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

>[!CAUTION]
>
>ミッドソーシング設定を使用する場合は、データベースを定期的に管理する必要があります。 マーケティングプラットフォーム上の配信を分析する際、マーケティングインスタンスはミッドソーシングインスタンスに情報を送信します。 プロセスの速度が遅くなると、マーケティングインスタンスに影響が出ます。

**作業テーブルの管理**

作業用テーブルの数とサイズを確認してください。 一定のサイズを超えると、データベースのパフォーマンスが低下します。 これらのテーブルはワークフローと配信によって作成されます。 ワークフローと配信がアクティブな間は、データベースに残ります。 作業テーブルのサイズを制限するには、次の操作を実行します。

* 次のステータスの配信を停止または削除します。 **[!UICONTROL 失敗]** 、 **[!UICONTROL 進行中]** 、配信 **[!UICONTROL の準備完了]** 、または **[!UICONTROL 一時停止]** 。
* エラーが原因で一時停止されたワークフローの停止または削除、
* エン **[!UICONTROL ド]** アクティビティを含まないテストで使用され、ステータスが「 **[!UICONTROL 一時停止」のままのワークフローをすべて停止します]** 。

>[!CAUTION]
>
>操作に長い時間がかかり、大量のスペースが解放される場合は、インデックスの再構築など、十分なメンテナンスが必要になります。 詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

**Adobe Campaignプロセスの監視**

Adobe Campaignのインストール設定に応じて、プラットフォーム監視には次の2つのツールを使用できます。

* インスタンスの実稼働ページ。 For more on this, refer to [Manual monitoring](../../production/using/monitoring-processes.md#manual-monitoring).
* netreportスクリプト。 詳しくは、「Adobe Campaignスクリプトを使用した [自動監視](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts)」を参照してください。

## Specifics {#specifics}

問題の原因を特定するために、リアルタイム診断を実行する必要が生じる場合があります。 開始を行うには、プロセスおよびプラットフォームのログファイルを確認し、問題の再作成中にデータベースのアクティビティを監視します。 特に、次の点に注意してください。

* 保守実施計画
* 実行中のSQLクエリ、
* 外部プロセスが同時に実行されているかどうか(クレンジング、インポート、集計の計算など)。

