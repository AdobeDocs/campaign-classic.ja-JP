---
title: Adobe Campaign Classic の配信品質の監視
description: Adobe Campaign クラシックの配信品質の監視に関するツールおよびガイドラインについて説明します。
page-status-flag: never-activated
uuid: 0b5c5dbd-f532-4d8a-a255-9e6d88357d8d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliverability-management
discoiquuid: 0baef937-f00b-4fc4-8608-a870997be684
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 91%

---


# 配信品質の監視{#monitoring-deliverability}

以下に、Adobe Campaign が提供する様々な監視ツールの詳細と、配信品質の監視に関するその他のガイドラインを示します。

## 監視ツール {#monitoring-tools}

Adobe Campaign が提供する機能を使用して、プラットフォームの配信品質を監視します。

配信品質パッケージを使用すると以下にアクセスすることができます。

* 毎日の配信品質のパフォーマンスに関する技術的なトラッキングレポート（技術的な監視）。このレポートはオンデマンドで利用でき、日次レポートを指定したアドレスに E メールで受信できます。詳しくは、アドビカスタマーケアチームにお問い合わせください。
* [受信ボックスレンダリングレポート](../../delivery/using/inbox-rendering.md)を使用すると、コンテンツや評判をスキャンするために、主要な E メールクライアントにメッセージをプレビューできます。
* メッセージ品質の概要（受信ボックス、スパム）。

次のツールも使用できます。

* **[!UICONTROL 配信スループット]**&#x200B;レポートは、一定期間にわたるプラットフォーム全体のスループットの概要を示します。詳しくは、[この節](../../reporting/using/global-reports.md#delivery-throughput)を参照してください。
* **[!UICONTROL 配信品質の技術的監視]**&#x200B;レポートには、お使いのプラットフォーム向けに配信品質の指標が多く含まれています。詳しくは、[この節](#technical-deliverability-monitoring)を参照してください。
* 各配信は、異なるインターネットサービスプロバイダー（ISP）に関するブロードキャスト統計情報レポートを生成します。配信品質に影響を与える可能性のあるデータ品質と評価の指標がいくつか表示されます。次の数値が含まれます。
   * **[!UICONTROL ハードバウンス]**&#x200B;はデータの質を示します。この数は 2％未満にする必要があります。
   * **[!UICONTROL ソフトバウンス]**&#x200B;は評判を示します。任意の ISP に対して、この値を 10％以下にする必要があります。

   詳しくは、[配信統計](../../reporting/using/global-reports.md#delivery-statistics)を参照してください。
* より一般的に、[配信ダッシュボード](../../delivery/using/monitoring-a-delivery.md#delivery-dashboard)は次の項目のアクセスを提供します。
   * [配信の概要](../../delivery/using/monitoring-a-delivery.md#delivery-summary)：送信の詳細、[送信するメッセージ数](../../delivery/using/monitoring-a-delivery.md#number-of-messages-sent)、処理済みおよび送信済みの成功件数を表示します。
   * [配信ログと履歴](../../delivery/using/monitoring-a-delivery.md#delivery-logs-and-history)：除外されたターゲットとその理由を示します。
   * [トラッキングログ](../../delivery/using/monitoring-a-delivery.md#tracking-logs)：開封数およびクリック数などのトラッキング情報を示します。

## 監視のガイドライン {#monitoring-guidelines}

配信品質の監視に関する追加のガイドラインを示します。

* プラットフォーム全体で[配信スループット](../../reporting/using/global-reports.md#delivery-throughput)を定期的にチェックして、元のセットアップと整合性が取れているかどうかを検証します。
* 配信テンプレートで[再試行](../../delivery/using/understanding-delivery-failures.md#retries-after-a-delivery-temporary-failure)が適切に設定されていることを確認します（再試行期間が 30 分、再試行回数が 21 回以上）。
* [バウンス](../../delivery/using/understanding-delivery-failures.md#bounce-mail-management)メールボックスがアクセス可能で、アカウントの有効期限が近づいていないかを定期的に検証します。
* 各配信スループットをチェックして、配信コンテンツの有効期限と整合性が取れていることを確認します（例：「フラッシュセール」は数日ではなく、数分で配信される必要があります）。
* [ウェーブ](../../delivery/using/steps-sending-the-delivery.md#sending-using-multiple-waves)を使用する場合、次のものがトリガーされる前に各ウェーブが完了するための十分な時間があることを検証します。
* エラーの数と新しい[強制隔離](../../delivery/using/understanding-quarantine-management.md)が他の配信と整合性が取れていることをチェックします。
* Carefully consult the [delivery logs](../../delivery/using/monitoring-a-delivery.md#delivery-logs-and-history) in detail to check the kind of errors that are highlighted (block lists, DNS issues, anti-spam rules, etc.).

## Signal Spam {#signal-spam}

Signal Spam は、フランスのサービスで、フランスの ISP（Orange、SFR）用の匿名化されたフィードバックループレポートを提供します。

* このサービスを使用すると、フランスの ISP のレピュテーションをフォローし、顧客のアクティビティの進化をトラッキングできます。

* また、Signal Spam は、専用インターフェンスを通じてエンドユーザーが記録した直接の苦情数を提供します。これらの苦情数は、E メールアドレスデータベースから強制隔離されます。

## 250ok {#deliverability-250ok}

[250ok](https://250ok.com/) は、IPおよびドメインブロックリスト、評価指標を提供するAdobe配信品質内部ツールの補完的な監視ソリューションです。

提供される情報はリアルタイムで、これにより先を見越した支援が可能です。

## 配信品質の技術的監視レポート {#technical-deliverability-monitoring}

配信品質の技術的監視レポートは毎日更新され、Adobe Campaign の「**[!UICONTROL ホーム]**」タブから&#x200B;**[!UICONTROL 監視]**／**[!UICONTROL 概要]**／**[!UICONTROL 技術的監視]**&#x200B;リンクをクリックすることで使用できます。このレポートには、プラットフォームに関する多数の配信品質指標が含まれます。

これらの指標は毎日午前 9 時に更新されます。

>[!NOTE]
>
>さらに、指定したアドレスで、毎日のレポートを E メールで受け取ることができます。E メールまたは Adobe Campaign エクストラネットで、リクエストする E メールアドレスをお知らせください。

![](assets/s_tn_del_monitoring.png)

次の指標がレポートで使用されます。

* **[!UICONTROL リバース DNS]**：Adobe Campaign は、IP アドレスにリバース DNS が指定されているかどうか、およびこれが IP を正しく指しているかどうかを確認します。

* **[!UICONTROL SPF]**（Sender Policy Framework）：E メール送信者が送信ドメインで承認されているかどうかを ISP およびメールボックスプロバイダーが確認できる認証メカニズムです。

* **[!UICONTROL DomainKeys]**：Yahoo が開発したサービスで、E メール送信者の ID を認証するためのものです。

* **[!UICONTROL IPおよびRBLドメイン]** (リアルタイムブラックホールリスト):ブロックリスト組織が悪い送信評価のためにフラグを付けたIPアドレスとドメインのリスト。 リストは、SpamHaus、SpamCop、SURBL/URIBL などの専門組織によって管理されます。現在、Adobe Campaign は、配信品質に大きな影響を与える RBL に対するチェックを処理します。これらの RBL は送信レピュテーションを反映し、E メールの受信が許可される前に ISP によって参照される可能性があります。

* **[!UICONTROL SNDS]**（Smart Network Data Services）：[Windows Live Hotmail のスパム対策サービス](https://sendersupport.olc.protection.outlook.com/snds/FAQ.aspx)。このタイプの情報を提供する ISP は Hotmail のみです。ベンチマークスコアは、緑色のフィルター結果、0.1％未満の苦情率、ゼロスパムトラップです。

<!--### Delivery Reports - Broadcast Statistics {#broadcast-statistics}

Each delivery will generate a broadcast statistics report when you open a delivery in the “Deliveries List”, which includes some reputation metrics that may impact your deliverability.-->
