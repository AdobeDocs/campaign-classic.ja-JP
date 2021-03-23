---
solution: Campaign Classic
product: campaign
title: Adobe Campaign Classic の配信品質の監視
description: Adobe Campaign クラシックの配信品質の監視に関するツールおよびガイドラインについて説明します。
audience: delivery
content-type: reference
topic-tags: deliverability-management
translation-type: tm+mt
source-git-commit: 5d1a653a9a164c34bb70efcc86ff2d7bdf1130a2
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 88%

---


# 配信品質の監視{#monitoring-deliverability}

以下に、Adobe Campaignが提供する様々な監視ツールの詳細と、Adobe Campaignが提供する機能を活用してプラットフォームの配信品質を監視するための追加のガイドラインを示します。

## 配信品質の監視 {#configuration}

この機能は、Adobe Campaign の専用パッケージで使用できます。使用するには、このパッケージをインストールする必要があります。インストールしたら、サーバーを再起動してパッケージを有効にします。
* ホストクライアントおよびハイブリッドクライアントの場合、**配信品質の監視**&#x200B;はアドビのテクニカルサポートおよびコンサルタントがインスタンスに設定します。詳しくは、アドビのアカウント担当者にお問い合わせください。

* オンプレミスでのインストールの場合は、**[!UICONTROL ツール]**／**[!UICONTROL 詳細設定]**／**[!UICONTROL パッケージをインポート]**&#x200B;メニューから&#x200B;**[!UICONTROL 配信品質の監視 (E メールの配信品質)]** パッケージをインストールする必要があります。詳しくは、[Campaign Classic 標準パッケージのインストール](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

Adobe Campaign Classic では、**配信品質の監視**&#x200B;は&#x200B;**[!UICONTROL 配信品質の更新]**&#x200B;ワークフローが管理します。このワークフローは、デフォルトですべてのインスタンスにインストールされ、バウンスメールの検証ルールのリスト、ドメインのリストおよび MX のリストを初期化できます。**[!UICONTROL 配信品質の監視 (E メールの配信品質)]** パッケージをインストールすると、このワークフローが毎日夜間に実行されてルールリストを定期的に更新し、プラットフォームの配信品質の積極的管理が可能になります。

配信品質パッケージを使用すると以下にアクセスすることができます。

* [受信ボックスレンダリングレポート](../../delivery/using/inbox-rendering.md)を使用すると、コンテンツや評判をスキャンするために、主要な E メールクライアントにメッセージをプレビューできます。
* メッセージ品質の概要（受信ボックス、スパム）。

## 監視ツール {#monitoring-tools}

次のツールも使用できます。

* **[!UICONTROL 配信スループット]**&#x200B;レポートは、一定期間にわたるプラットフォーム全体のスループットの概要を示します。詳しくは、[この節](../../reporting/using/global-reports.md#delivery-throughput)を参照してください。
* 各配信は、異なるインターネットサービスプロバイダー（ISP）に関するブロードキャスト統計情報レポートを生成します。配信品質に影響を与える可能性のあるデータ品質と評価の指標がいくつか表示されます。次の数値が含まれます。
   * **[!UICONTROL ハードバウンス]**&#x200B;はデータの質を示します。この数は 2％未満にする必要があります。
   * **[!UICONTROL ソフトバウンス]**&#x200B;は評判を示します。任意の ISP に対して、この値を 10％以下にする必要があります。

   詳しくは、[配信統計](../../reporting/using/global-reports.md#delivery-statistics)を参照してください。
* より一般的に、[配信ダッシュボード](../../delivery/using/about-delivery-monitoring.md)は次の項目のアクセスを提供します。
   * [配信の概要](../../delivery/using/delivery-dashboard.md#delivery-summary)：送信の詳細、送信するメッセージ数、処理済みおよび送信済みの成功件数を表示します。
   * [配信ログと履歴](../../delivery/using/delivery-dashboard.md#delivery-logs-and-history)：除外されたターゲットとその理由を示します。
   * [トラッキングログ](../../delivery/using/delivery-dashboard.md#tracking-logs)：開封数およびクリック数などのトラッキング情報を示します。

## 監視のガイドライン {#monitoring-guidelines}

配信品質の監視に関する追加のガイドラインを示します。

* プラットフォーム全体で[配信スループット](../../reporting/using/global-reports.md#delivery-throughput)を定期的にチェックして、元のセットアップと整合性が取れているかどうかを検証します。
* 配信テンプレートで[再試行](../../delivery/using/understanding-delivery-failures.md#retries-after-a-delivery-temporary-failure)が適切に設定されていることを確認します（再試行期間が 30 分、再試行回数が 21 回以上）。
* [バウンス](../../delivery/using/understanding-delivery-failures.md#bounce-mail-management)メールボックスがアクセス可能で、アカウントの有効期限が近づいていないかを定期的に検証します。
* [配信ダッシュボード](../../delivery/using/delivery-dashboard.md)からアクセス可能な各配信のスループットをチェックし、配信の内容の有効性(例：「flash sales」は、日単位ではなく分単位で配信する必要があります。
* [ウェーブ](../../delivery/using/steps-sending-the-delivery.md#sending-using-multiple-waves)を使用する場合、次のものがトリガーされる前に各ウェーブが完了するための十分な時間があることを検証します。
* エラーの数と新しい[強制隔離](../../delivery/using/understanding-quarantine-management.md)が他の配信と整合性が取れていることをチェックします。
* [配信ログ](../../delivery/using/delivery-dashboard.md#delivery-logs-and-history)の詳細を慎重に調べて、ハイライト表示されたエラーの種類をチェックします（ブロックリスト、DNS の問題、スパム対策ルールなど）。

<!--### Delivery Reports - Broadcast Statistics {#broadcast-statistics}

Each delivery will generate a broadcast statistics report when you open a delivery in the “Deliveries List”, which includes some reputation metrics that may impact your deliverability.-->
