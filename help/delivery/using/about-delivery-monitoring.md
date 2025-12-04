---
product: campaign
title: 配信監視の基本を学ぶ
description: Campaign Classic 配信監視機能の詳細情報
feature: Monitoring, Deliverability
role: User
exl-id: 9ce11da0-e37b-459e-8ec7-d2bddf59bdf7
source-git-commit: a85d94e8ff66e8468b4fe2f071df48437393bbce
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 64%

---

# 配信監視の基本を学ぶ {#about-delivery-monitoring}

>[!IMPORTANT]
>
>このページでは、ハイブリッドデプロイメントとオンプレミスデプロイメントの **0}Campaign Classic v7 固有のモニタリング機能について説明します。**

## 機能の監視

### 配信の監視 {#monitoring-deliveries}

**Campaign Classic v7 ハイブリッド/オンプレミスデプロイメントの場合**、サーバーリソースと MTA （メール転送エージェント）設定に対してさらにモニタリングが必要です。

#### 保留中の配信のトラブルシューティング {#pending-deliveries}

配信が送信されず、そのステータスが「**保留中**」のままになっている場合は、どのような状況が考えられるでしょうか。

* 実行プロセスが、リソースが使用可能になるのを待っています。MTA が開始されていない可能性があります。MTA サーバー上で mta@instance モジュールが開始されていることを確認し、必要であれば MTA モジュールを開始します。詳しくは、[こちら](../../production/using/administration.md)を参照してください。

* 送信インスタンスに設定されていないアフィニティを配信で使用している可能性があります。ヒント：トラフィック管理の設定（IP アフィニティ）を確認します。詳しくは、送信 SMTP トラフィックの制御を参照してください。

>[!NOTE]
>
>これらの手順は、エキスパートユーザーがオンプレミスインストールでのみ実行できます。

### 配信品質の監視 {#deliverability-monitoring}

#### 配信品質パッケージのインストール {#deliverability-package}

この機能は、Adobe Campaign の専用パッケージで使用できます。使用するには、このパッケージをインストールする必要があります。インストールしたら、サーバーを再起動してパッケージを有効にします。

* ホストクライアントおよびハイブリッドクライアントの場合、**配信品質の監視**&#x200B;はアドビのテクニカルサポートおよびコンサルタントがインスタンスに設定します。詳しくは、アドビのアカウント担当者にお問い合わせください。

* オンプレミスでのインストールの場合は、**[!UICONTROL ツール]**／**[!UICONTROL 詳細設定]**／**[!UICONTROL パッケージをインポート]**&#x200B;メニューから&#x200B;**[!UICONTROL 配信品質の監視 (メールの配信品質)]** パッケージをインストールする必要があります。詳しくは、[Campaign Classic標準パッケージのインストール ](../../installation/using/installing-campaign-standard-packages.md) を参照してください。

#### 配信品質のワークフロー {#deliverability-workflow}

Adobe Campaign Classic では、**配信品質の監視**&#x200B;は&#x200B;**[!UICONTROL 配信品質の更新]**&#x200B;ワークフローが管理します。このワークフローは、デフォルトですべてのインスタンスにインストールされ、バウンスメール選定ルールのリスト、ドメインのリストおよび MX のリストを初期化できます。**[!UICONTROL 配信品質の監視 (メールの配信品質)]** パッケージをインストールすると、このワークフローが毎日夜間に実行されてルールリストを定期的に更新し、プラットフォームの配信品質の積極的管理が可能になります。

**配信品質パッケージを使用すると、次の項目にアクセスできます。**

* [受信ボックスレンダリングレポート](inbox-rendering.md)を使用すると、コンテンツや評判をスキャンするために、主要なメールクライアントにメッセージをプレビューできます。
* メッセージ品質の概要（受信ボックス、スパム）。

#### 監視ツール {#monitoring-tools}

**オンプレミスインストールの場合**、次の監視ツールを使用できます。

* **[!UICONTROL 配信スループット]**&#x200B;レポートは、一定期間にわたるプラットフォーム全体のスループットの概要を示します。詳しくは、[この節](../../reporting/using/global-reports.md#delivery-throughput)を参照してください。
* 各配信は、異なるインターネットサービスプロバイダー（ISP）に関するブロードキャスト統計情報レポートを生成します。配信品質に影響を与える可能性のあるデータ品質と評価の指標がいくつか表示されます。次の数値が含まれます。
   * **[!UICONTROL ハードバウンス]**&#x200B;はデータの質を示します。この数は 2％未満にする必要があります。
   * **[!UICONTROL ソフトバウンス]**&#x200B;は評判を示します。任意の ISP に対して、この値を 10％以下にする必要があります。

  詳しくは、[配信統計](../../reporting/using/global-reports.md#delivery-statistics)を参照してください。

#### 監視のガイドライン {#monitoring-guidelines}

**オンプレミスインストールの場合**、配信品質の監視に関するその他のガイドラインを次に示します。

* プラットフォーム全体で[配信スループット](../../reporting/using/global-reports.md#delivery-throughput)を定期的にチェックして、元のセットアップと整合性が取れているかどうかを検証します。
* 配信テンプレートで[再試行](understanding-delivery-failures.md#retries-after-a-delivery-temporary-failure)が適切に設定されていることを確認します（再試行期間が 30 分、再試行回数が 21 回以上）。
* [バウンス](understanding-delivery-failures.md#bounce-mail-management)メールボックスがアクセス可能で、アカウントの有効期限が近づいていないかを定期的に検証します。
* [配信ダッシュボード](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"}で各配信スループットをチェックして、配信コンテンツの効力（例：「フラッシュセール」の配信期間は数日ではなく数分にする必要がある）と合致していることを確認します。
* ウェーブを使用する場合、次のものがトリガーされる前に各ウェーブが完了するための十分な時間があることを検証します。
* エラーの数と新しい[強制隔離](understanding-quarantine-management.md)が他の配信と整合性が取れていることをチェックします。
* [配信ログ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-dashboard#delivery-logs-and-history){target="_blank"}の詳細を慎重に調べて、ハイライト表示されたエラーの種類をチェックします（ブロックリスト、DNS の問題、スパム対策ルールなど）。

### トラブルシューティング {#delivery-troubleshooting}

**ハイブリッド/オンプレミスデプロイメント** で配信に関する問題が発生した場合は、特定のアクションを実行できます。

* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)
* [画像の表示の問題](../../production/using/image-display-issues.md)
* [配信パフォーマンスの問題](delivery-performances.md)
* [一時ファイルの問題](../../production/using/temporary-files.md) - *オンプレミスのお客様のみ*

## 配信の監視

次のリソースは、Campaign Classic v7 での配信パフォーマンスのモニタリングとトラッキングに役立ちます。

### 配信ダッシュボードへのアクセス

配信リストにアクセスし、配信ダッシュボードを使用して送信アクティビティを監視する方法を説明します。

* [Campaign UI での配信の監視 ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"} （Campaign v8 ドキュメント - v7 と v8 の両方に適用）
* [ 配信ステータス ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-statuses){target="_blank"} （Campaign v8 ドキュメント）
* [ 詳細：配信ログのカスタマイズ ](customize-delivery-logs.md) （v7 ハイブリッド/オンプレミスのみ – スキーマ拡張）

### メッセージインタラクションのトラッキング

開封数、クリック数、配信に対する受信者のインタラクションをトラッキングします。

* [ メッセージトラッキングドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/analytics/tracking/tracking){target="_blank"} （Campaign v8 ドキュメント - v7 と v8 の両方に適用）
* [ トラッキングするリンクの設定 ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/analytics/tracking/tracked-links){target="_blank"} （Campaign v8 ドキュメント）
* [ トラッキングログへのアクセス ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/analytics/tracking/tracking-logs){target="_blank"} （Campaign v8 ドキュメント）

### 配信パフォーマンスの最適化

配信パフォーマンスの問題に関するベストプラクティスとトラブルシューティング：

* [ 配信のベストプラクティス ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} （Campaign v8 ドキュメント - v7 と v8 の両方に適用）
* [ 配信のパフォーマンスとトラブルシューティング ](delivery-performance-troubleshooting.md) （v7 ハイブリッド/オンプレミス固有の設定）

### エラーと強制隔離について

配信エラー、バウンスメール、強制隔離アドレスの管理：

* [ 配信エラーについて ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} （Campaign v8 ドキュメント - v7 と v8 の両方に関する包括的なガイド）
* [ 強制隔離管理 ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/quarantines){target="_blank"} （Campaign v8 ドキュメント - v7 と v8 の両方に関する包括的なガイド）
* [ 配信エラーと強制隔離の設定 ](delivery-failures-quarantine.md) （v7 ハイブリッド/オンプレミス固有の設定）
