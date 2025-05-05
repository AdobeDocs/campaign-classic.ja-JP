---
product: campaign
title: パフォーマンスとスループットの問題
description: パフォーマンスとスループットの問題
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: fe69efda-a052-4f67-9c13-665f011d0a2b
source-git-commit: 6803b6628313db9108a191fd143dac68ee799149
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 13%

---

# パフォーマンスとスループットの問題{#performance-and-throughput-issues}

まず、最新のビルドがインストールされていることを確認する必要があります。 これにより、最新の機能とバグ修正が確実に提供されます。

各リリースの内容について詳しくは、[ リリースノート ](../../rn/using/latest-release.md) を参照してください。

## ハードウェアとインフラストラクチャ {#hardware-and-infrastructure}

オンプレミスCampaign Classicのハードウェア要件の一般的なガイドラインについて詳しくは、この [ ページ ](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html) を参照してください。

コンサルティングチームは、ホスト環境のお客様に、データベース内の様々なタイプのテーブルで使用されているスペースおよび SFTP サイトで使用されているスペースを簡単に確認できるツールを提供できます。 また、不要なデータをクリーンアップできるツールも用意されています。 このツールを実装する必要がある場合は [&#128279;](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)Adobeカスタマーケアにお問い合わせください。 このツールを使用して確認すべき重要な事項を次に示します。

* インデックスサイズがテーブルサイズより大きい場合、バキュームが必要です。
* 最大の膨張を持つテーブルをチェックしてください。 これらのテーブルを頻繁に使用する場合は、掃除機をかける必要があります。
* データベースがブロックされると、メールが送信されなくなることがあります。

Adobe Campaignには、CPUと RAM の使用状況を確認する [ ツール ](../../production/using/monitoring-processes.md#manual-monitoring) もあります。 このツールを使用して、**メモリ**、**スワップメモリ**、**ディスク**、**アクティブなプロセス** などの特定の指標を確認します。 値が大きすぎる場合は、ワークフローの数を減らすか、異なる時間にワークフローを開始するようにスケジュールすることができます。

## データベースチェック {#database-performances}

ほとんどの場合、パフォーマンスの問題はデータベースのメンテナンスに関連しています。 確認する主な項目は次のとおりです。

* 設定：Adobe Campaignのプラットフォームの初期設定を確認し、完全なハードウェアチェックを実行することをお勧めします。
* Adobe Campaign プラットフォームのインストールと設定：ネットワーク設定とプラットフォームの配信品質オプションを確認します。
* データベースのメンテナンス：データベースクリーンアップタスクが操作可能で、データベースのメンテナンスが正しくスケジュールおよび実行されていることを確認します。 ワークテーブルの数とサイズを確認します。
* リアルタイム診断：プロセスおよびプラットフォームのログファイルを確認し、問題を再現する際にデータベースのアクティビティを監視します。

>[!NOTE]
>
>詳しくは、次の節を参照してください。[ データベースパフォーマンス ](../../production/using/database-performances.md)。

## アプリケーション設定 {#application-configuration}

アプリケーション設定のベストプラクティスに関連する記事のリストを以下に示します。

* MTA および MTAChild プロセスおよびメモリ：**mta** モジュールは、メッセージを **mtachild** 子モジュールに配布します。 各 **mtachild** は、統計サーバーから認証を要求して送信する前に、メッセージを準備します。 詳しくは、この [ ページ ](../../installation/using/email-deliverability.md) を参照してください。
* TLS 設定：TLS をグローバルに有効にすると、スループットが低下する可能性があるので、推奨されません。 代わりに、配信品質チームが管理するドメインごとの TLS 設定は、必要に応じて調整する必要があります。 詳しくは、この [ ページ ](../../installation/using/email-deliverability.md#mx-configuration) を参照してください。

  >[!NOTE]
  >
  >配信品質チームのエンゲージメントは契約に基づいており、配信品質エンゲージメントに関する情報については、お客様はアドビ担当者に問い合わせる必要があります。

* DKIM: DKIMのセキュリティレベルを確保するには、ベストプラクティスとして推奨される暗号化サイズは 1024 b です。 DKIMの低いキーは、多くのアクセスプロバイダーでは有効と見なされません。 [このページ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html?lang=ja#authentication)を参照してください。

## 配信品質の問題 {#deliverability-issues}

配信品質に関連するベストプラクティスと記事のリストを以下に示します。

* IP レピュテーション：IP レピュテーションが十分に適切でない場合、パフォーマンスに影響を与えます。 **配信品質の監視** モジュールは、プラットフォームの配信品質のパフォーマンスを追跡する様々なツールを提供します。 この[ページ](../../delivery/using/monitoring-deliverability.md)を参照してください。
* IP ウォームアップ：IP ウォームアップは、配信品質チームが実行します。 これには、数週間かけて新しい IP を通じてメールの数を徐々に増やす必要があります。

  >[!NOTE]
  >
  >配信品質チームのエンゲージメントは契約に基づいており、配信品質エンゲージメントに関する情報については、お客様はアドビ担当者に問い合わせる必要があります。

* IP アフィニティの設定：IP アフィニティの設定を誤ると、メールが完全に停止したり（設定でオペレーター/アフィニティ名が正しくありません）、スループットが低下したり（アフィニティに含まれる IP の数が少なくなっています）することがあります。 この[ページ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)を参照してください。
* メールサイズ：メールのサイズは、スループットで重要な役割を果たします。 推奨最大メールサイズは 60 KB です。 この [ ページ ](https://helpx.adobe.com/jp/legal/product-descriptions/campaign.html) を参照してください。 [ 配信スループット ](../../reporting/using/global-reports.md#delivery-throughput) レポートで、時間単位で転送されたバイト数を確認します。
* 無効な受信者の数が多い：無効な受信者が多数ある場合、スループットに影響する可能性があります。 MTA が無効な受信者へのメールの送信を再試行し続ける。 データベースが適切に維持されていることを確認してください。
* パーソナライゼーションの量：配信が「Personalization中」のままの場合は、パーソナライゼーションブロックで使用されているJavaScriptを確認します。

>[!NOTE]
>
>[ 配信品質 ](../../delivery/using/about-deliverability.md) の節も参照してください。 配信品質の詳細については、[アドビの配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja)を参照してください。
