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
TQID: https://experienceleague.adobe.com/THf7A2u5ktNphqdI8K8ePzLNqCdyCmcqWN0OpYJfVh0
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c1579802-ddd4-4214-8a91-97b2066abe11id: d095671a-1355-40aa-8b5f-06c33c68080bid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 805
ht-degree: 19%

---

# パフォーマンスとスループットの問題{#performance-and-throughput-issues}

まず、最新のビルドがインストールされていることを確認する必要があります。 これにより、最新の機能とバグ修正が確実に提供されます。

各リリースの内容について詳しくは、[ リリースノート ](../../rn/using/latest-release.md)を参照してください。

## ハードウェアとインフラ {#hardware-and-infrastructure}

オンプレミス Campaign Classicのハードウェア要件に関する一般的なガイドラインについては、この[ ページ ](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)で詳しく説明しています。

コンサルティングチームは、ホストされている顧客に、データベース内の様々なタイプのテーブルで使用されているスペースと、SFTP サイトで使用されているスペースを簡単に確認できるツールを提供できます。 また、不要なデータをクリーンアップするためのツールも提供します。 このツールを実装する必要がある場合は、[Adobe カスタマーケア ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。 ここでは、このツールを使用して確認すべき重要な点をいくつか紹介します。

* インデックスサイズがテーブルサイズよりも大きい場合は、真空が必要です。
* 最大の膨張を持つテーブルを確認してください。 これらの表が頻繁に使用される場合は、真空引きする必要があります。
* データベースをブロックすると、電子メールの送信が停止する可能性があります。

Adobe Campaignには、CPUとRAMの使用状況を確認するための[ ツール ](../../production/using/monitoring-processes.md#manual-monitoring)も用意されています。 このツールを使用して、**メモリ**、**スワップ メモリ**、**ディスク**、**アクティブプロセス**&#x200B;などの特定の指標を確認します。 値が高すぎる場合は、ワークフローの数を減らすか、異なる時間に開始するようにワークフローをスケジュールできます。

## データベースチェック {#database-performances}

ほとんどの場合、パフォーマンスの問題はデータベースのメンテナンスに関連しています。 確認すべき主な項目は次のとおりです。

* 設定：最初のAdobe Campaign プラットフォーム設定を確認し、完全なハードウェアチェックを実行することをお勧めします。
* Adobe Campaign プラットフォームのインストールと設定：ネットワーク設定とプラットフォームの配信品質オプションを確認します。
* データベースのメンテナンス：データベースのクリーンアップタスクが動作しており、データベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 ワークテーブルの数とサイズを確認します。
* リアルタイム診断：プロセスとプラットフォームのログファイルを確認し、問題の再作成中にデータベースのアクティビティを監視します。

>[!NOTE]
>
>詳しくは、この節を参照してください：[ データベースのパフォーマンス ](../../production/using/database-performances.md)。

## アプリケーション設定 {#application-configuration}

アプリケーション設定のベストプラクティスに関連する記事のリストを次に示します。

* MTAおよびMTAChild プロセスとメモリ：**mta** モジュールは、メッセージを&#x200B;**mtachild**&#x200B;子モジュールに配布します。 各&#x200B;**mtachild**&#x200B;は、統計サーバーに認証を要求して送信する前に、メッセージを準備します。 詳しくは、この[ ページ ](../../installation/using/email-deliverability.md)を参照してください。
* TLS設定：スループットを減らすことができるため、TLSをグローバルに有効にすることは推奨されません。 代わりに、配信品質チームによって管理されるドメインごとのTLS設定は、ニーズに応じて調整する必要があります。 詳しくは、この[ ページ ](../../installation/using/email-deliverability.md#mx-configuration)を参照してください。

  >[!NOTE]
  >
  >配信品質チームのエンゲージメントは契約に基づいており、配信品質エンゲージメントに関する情報については、お客様はアドビ担当者に問い合わせる必要があります。

* DKIM:DKIMのセキュリティレベルを確保するために、1024bは推奨される暗号化サイズのベストプラクティスです。 DKIM キーが低い場合、ほとんどのアクセス プロバイダーでは有効とは見なされません。 [このページ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html?lang=ja#authentication)を参照してください。

## 配信品質の問題 {#deliverability-issues}

以下に、配信品質に関するベストプラクティスと記事の一覧を示します。

* IP レピュテーション：IP レピュテーションが十分でない場合、パフォーマンスに影響があります。 **配信品質モニタリング** モジュールには、プラットフォームの配信品質パフォーマンスを追跡するための様々なツールが用意されています。 詳しくは、この[ページ](../../delivery/using/about-delivery-monitoring.md#deliverability-monitoring)を参照してください。
* IP ウォームアップ：IP ウォームアップは、配信品質チームによって実行されます。 これには、数週間かけて新しいIPを通じたメール数を徐々に増やすことが含まれます。

  >[!NOTE]
  >
  >配信品質チームのエンゲージメントは契約に基づいており、配信品質エンゲージメントに関する情報については、お客様はアドビ担当者に問い合わせる必要があります。

* IP アフィニティの設定：IP アフィニティの設定が正しくないと、電子メールを完全に停止したり（設定でオペレーター名やアフィニティ名が正しくありません）、スループットを低下させたり（アフィニティ内のIPの数が少ない）する可能性があります。 詳しくは、この[ページ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)を参照してください。
* メールサイズ：メールサイズはスループットにおいて重要な役割を果たします。 推奨される最大メールサイズは60 KBです。 この[ページ](https://helpx.adobe.com/legal/product-descriptions/campaign.html)を参照してください。 [配信スループット ](../../reporting/using/global-reports.md#delivery-throughput) レポートで、転送されたバイト数を時間で確認します。
* 無効な受信者の数が多い：無効な受信者の数が多い場合、スループットに影響を与える可能性があります。 MTAは、無効な受信者に電子メールを送信し続けます。 データベースが適切に管理されていることを確認してください。
* パーソナライズの量：配信が「進行中のPersonalization」に留まる場合は、パーソナライゼーションブロックで使用されるJavaScriptを確認します。

>[!NOTE]
>
>「[配信品質](../../delivery/using/about-deliverability.md)」の節も参照してください。 配信品質の詳細については、[アドビの配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja)を参照してください。
