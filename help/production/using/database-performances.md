---
product: campaign
title: データベース性能
description: データベース性能
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 33dcfd4b-51fd-44f4-98e0-23eafb79d7da
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 13%

---

# データベースのパフォーマンス{#database-performances}



パフォーマンスの問題の多くは、データベースのメンテナンスに関連しています。 パフォーマンスが低下する原因を特定するのに役立つ、主な4つのリードを紹介します。

* 設定
* Adobe Campaign プラットフォームのインストールと設定
* データベースのメンテナンス
* リアルタイム診断

## 設定 {#configuration}

Adobe Campaignの初期設定が引き続き有効であることを確認し、必要に応じて、配信品質やデータベースのサイズに関するお客様のニーズを再評価します。 また、ハードウェアチェック（CPU、RAM、IO システム）を実行することをお勧めします。

>[!NOTE]
>
>詳しくは、[Adobe Campaign ハードウェアのサイズ変更ガイド &#x200B;](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)を参照してください。

## プラットフォーム設定 {#platform-configuration}

不適切な設定は、プラットフォームのパフォーマンスに影響を与える可能性があります。 **serverConf.xml** ファイルで、ネットワーク設定、プラットフォーム配信オプション、およびMTA設定を確認することをお勧めします。

## データベースのメンテナンス {#database-maintenance}

**データベースのクリーンアップ タスク**

データベースのクリーンアップ タスクが有効であることを確認してください。 これには、ログファイルを表示して、エラーが含まれているかどうかを確認します。 詳しくは、[この節](../../production/using/database-cleanup-workflow.md)を参照してください。

**メンテナンスプラン**

データベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 これを行うには、データベース管理者に連絡して詳細を確認してください。

* そのメンテナンススケジュール
* 以前に実行したメンテナンス計画
* スクリプトログの表示

詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

>[!IMPORTANT]
>
>ミッドソーシング設定を使用する場合は、データベースを定期的に維持することが不可欠です。 マーケティングプラットフォームで配信を分析する場合、マーケティングインスタンスはミッドソーシングインスタンスに情報を送信します。 プロセスが遅れると、マーケティングインスタンスに影響を与えます。

**作業テーブルの管理**

ワークテーブルの数とサイズを確認してください。 特定のサイズを超えると、データベースのパフォーマンスが影響を受けます。 これらのテーブルは、ワークフローと配信によって作成されます。 ワークフローと配信がアクティブな間、データベースに残ります。 ワークテーブルのサイズを制限するには、次の操作を実行します。

* 次のステータスの配信を停止または削除します：**[!UICONTROL 失敗]**、**[!UICONTROL 進行中]**、**[!UICONTROL 配信準備完了]**、または&#x200B;**[!UICONTROL 一時停止]**。
* エラーが原因で一時停止したワークフローを停止または削除します。
* **[!UICONTROL 終了]** アクティビティを含まないテストに使用されるワークフローのうち、ステータスが&#x200B;**[!UICONTROL 一時停止]**&#x200B;のままであるすべてのワークフローを停止します。

>[!IMPORTANT]
>
>操作に時間がかかり、多くのスペースが解放される場合、これは詳細なメンテナンスが必要であることを意味します（インデックスの再構築など）。 詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

**Adobe Campaign プロセスの監視**

Adobe Campaignのインストール設定に応じて、次の2つのツールを使用してプラットフォームを監視できます。

* インスタンスの実稼動ページ。 詳しくは、[手動モニタリング &#x200B;](../../production/using/monitoring-processes.md#manual-monitoring)を参照してください。
* *netreport* スクリプト。 詳しくは、[Adobe Campaign スクリプトによる自動監視](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts)を参照してください。

## 詳細 {#specifics}

問題の原因を特定するために、リアルタイムの診断を実行する必要が生じる場合があります。 まずプロセスとプラットフォームのログファイルを確認し、問題の再作成中にデータベースのアクティビティを監視します。 特に、次の点に注意してください。

* 保守の実行計画
* 実行されるSQL クエリ
* 外部プロセスが同時に実行されているかどうか（クレンジング、インポート、集計計算など）。
