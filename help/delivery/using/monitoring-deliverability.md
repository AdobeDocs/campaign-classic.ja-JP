---
solution: Campaign Classic
product: campaign
title: Adobe Campaign Classic の配信品質の監視
description: Adobe Campaign クラシックの配信品質の監視に関するツールおよびガイドラインについて説明します。
audience: delivery
content-type: reference
topic-tags: deliverability-management
translation-type: ht
source-git-commit: fa5679d91808edb8e3916d5f0e0f54c73198e934
workflow-type: ht
source-wordcount: '485'
ht-degree: 100%

---


# 配信品質の監視{#monitoring-deliverability}

以下に、Adobe Campaign が提供する様々な監視ツールの詳細と、配信品質の監視に関するその他のガイドラインを示します。

## 監視ツール {#monitoring-tools}

Adobe Campaign が提供する機能を使用して、プラットフォームの配信品質を監視します。

配信品質パッケージを使用すると以下にアクセスすることができます。

* [受信ボックスレンダリングレポート](../../delivery/using/inbox-rendering.md)を使用すると、コンテンツや評判をスキャンするために、主要な E メールクライアントにメッセージをプレビューできます。
* メッセージ品質の概要（受信ボックス、スパム）。

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
* 各配信スループットをチェックして、配信コンテンツの有効期限と整合性が取れていることを確認します（例：「フラッシュセール」は数日ではなく、数分で配信される必要があります）。
* [ウェーブ](../../delivery/using/steps-sending-the-delivery.md#sending-using-multiple-waves)を使用する場合、次のものがトリガーされる前に各ウェーブが完了するための十分な時間があることを検証します。
* エラーの数と新しい[強制隔離](../../delivery/using/understanding-quarantine-management.md)が他の配信と整合性が取れていることをチェックします。
* [配信ログ](../../delivery/using/delivery-dashboard.md#delivery-logs-and-history)の詳細を慎重に調べて、ハイライト表示されたエラーの種類をチェックします（ブロックリスト、DNS の問題、スパム対策ルールなど）。

## Signal Spam {#signal-spam}

Signal Spam は、フランスのサービスで、フランスの ISP（Orange、SFR）用の匿名化されたフィードバックループレポートを提供します。

* このサービスを使用すると、フランスの ISP のレピュテーションをフォローし、顧客のアクティビティの進化をトラッキングできます。

* また、Signal Spam は、専用インターフェンスを通じてエンドユーザーが記録した直接の苦情数を提供します。これらの苦情数は、E メールアドレスデータベースから強制隔離されます。

## 250ok {#deliverability-250ok}

[250ok](https://250ok.com/) は、IP、ドメインブロックリストおよび評判の指標を提供する、アドビの配信品質内部ツールの補完的な監視ソリューションです。

提供される情報はリアルタイムで、これにより先を見越した支援が可能です。

<!--### Delivery Reports - Broadcast Statistics {#broadcast-statistics}

Each delivery will generate a broadcast statistics report when you open a delivery in the “Deliveries List”, which includes some reputation metrics that may impact your deliverability.-->
