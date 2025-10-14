---
product: campaign
title: データベースパフォーマンス
description: データベースパフォーマンス
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 33dcfd4b-51fd-44f4-98e0-23eafb79d7da
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 8%

---

# データベースのパフォーマンス{#database-performances}



パフォーマンスに関する問題のほとんどは、データベースのメンテナンスに関係しています。 パフォーマンスが低下する原因を特定する際に役立つ、主なリードを 4 つ示します。

* 設定
* Adobe Campaign プラットフォームのインストールと設定
* データベースのメンテナンス
* リアルタイム診断

## 設定 {#configuration}

最初のAdobe Campaign プラットフォーム設定が引き続き有効であることを確認し、必要に応じて、配信品質やデータベースサイズの点から顧客のニーズを再評価します。 また、完全なハードウェアチェック（CPU、RAM、IO システム）を実行することをお勧めします。

>[!NOTE]
>
>インサイトについては、[Adobe Campaign ハードウェアのサイズ設定ガイド &#x200B;](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html) を参照してください。

## プラットフォーム設定 {#platform-configuration}

不適切な設定は、プラットフォームのパフォーマンスに影響を与える場合があります。 **serverConf.xml** ファイルで、ネットワーク設定、プラットフォーム配信品質オプションおよび MTA 設定を確認することをお勧めします。

## データベースのメンテナンス {#database-maintenance}

**データベースクリーンアップタスク**

データベース クリーンアップ タスクが動作していることを確認してください。 それには、ログファイルを表示して、エラーが含まれているかどうかを確認します。 詳しくは、[この節](../../production/using/database-cleanup-workflow.md)を参照してください。

**整備計画**

データベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 詳細については、データベース管理者にお問い合わせください。

* メンテナンススケジュール
* 過去に実行したメンテナンス計画
* スクリプトログの表示

詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

>[!IMPORTANT]
>
>ミッドソーシング設定を使用する場合、データベースを定期的にメンテナンスする必要があります。 マーケティングプラットフォームで配信を分析する際、マーケティングインスタンスはミッドソーシングインスタンスに情報を送信します。 プロセスの速度が低下すると、マーケティングインスタンスが影響を受けます。

**作業用テーブルの管理**

ワークテーブルの数とサイズを確認してください。 サイズが特定のサイズを超えると、データベースのパフォーマンスに影響します。 これらのテーブルは、ワークフローと配信で作成されます。 ワークフローと配信がアクティブな間、これらはデータベースに残ります。 作業用テーブルのサイズを制限するには、次の操作を実行します。

* ステータス **[!UICONTROL 失敗]**、**[!UICONTROL 処理中]**、**[!UICONTROL 配信準備完了]**、**[!UICONTROL 一時停止]** の配信を停止または削除します。
* エラーが原因で一時停止されているワークフローを停止または削除します。
* **[!UICONTROL 終了]** アクティビティを含まないテストに使用されていて、ステータスが **[!UICONTROL 一時停止]** のままになっているすべてのワークフローを停止します。

>[!IMPORTANT]
>
>操作に時間がかかり、多くのスペースを解放する場合、これは詳細なメンテナンス（インデックスの再構築など）が必要であることを意味します。 詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

**Adobe Campaign プロセスの監視**

Adobe Campaignのインストール設定に応じて、次の 2 つのツールを使用してプラットフォームを監視できます。

* インスタンスの実稼動ページ。 詳しくは、[&#x200B; 手動の監視 &#x200B;](../../production/using/monitoring-processes.md#manual-monitoring) を参照してください。
* *netreport* スクリプト。 詳しくは、[Adobe Campaign スクリプトを使用した自動モニタリング &#x200B;](../../production/using/monitoring-processes.md#automatic-monitoring-via-adobe-campaign-scripts) を参照してください。

## 詳細 {#specifics}

問題の原因を特定するために、リアルタイムの診断を実行する必要が生じる場合があります。 まず、プロセスおよび platform のログファイルを確認し、問題を再作成する際に、データベースのアクティビティを監視します。 次の点に特に注意してください。

* メンテナンス実行計画
* 実行中の SQL クエリ
* 外部プロセスが同時に実行されているかどうか（クレンジング、インポート、集計計算など）。
