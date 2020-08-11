---
title: パフォーマンスとスループットの問題
seo-title: パフォーマンスとスループットの問題
description: パフォーマンスとスループットの問題
seo-description: null
page-status-flag: never-activated
uuid: 28c35453-9a15-44a3-9961-f4c604c209c2
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: ec66e3e3-b09a-44a4-914d-e3b38c7643f8
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: bc54cef4c44be4c694e062f56685dbb09d2fcf8e
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 7%

---


# パフォーマンスとスループットの問題{#performance-and-throughput-issues}

>[!NOTE]
>
>まず、最新のビルドがインストールされていることを確認してください。 これにより、最新の機能とバグ修正を確実に行うことができます。 各リリースの内容の詳細については、 [リリースノート](../../rn/using/latest-release.md) を参照してください。

## ハードウェアとインフラストラクチャ {#hardware-and-infrastructure}

オンプレミスCampaign Classicのハードウェア要件に関する一般的なガイドラインを、この [記事で詳しく説明します](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)。

コンサルティングチームは、ホストするお客様に対して、データベース内の様々なタイプのテーブルで使用されている領域とSFTPサイトで使用されている領域を簡単に表示できるツールを提供できます。 また、不要なデータをクリーンアップするためのツールも提供されています。 このツールを実装する必要がある場合は、コンサルティングチームまたはサポートチームにお問い合わせください。 このツールを使用して、次の点を確認してください。

* インデックスサイズがテーブルサイズより大きい場合は、真空が必要です。
* 最大膨張率を持つテーブルをチェックします。 これらのテーブルを頻繁に使用する場合は、バキュームする必要があります。
* データベースのブロックにより、電子メールの送信が停止する場合があります。

Adobe Campaignは、CPUとRAMの使用状況をチェックする [ツールも提供します](../../production/using/monitoring-processes.md#manual-monitoring) 。 このツールを使用して、次のような特定のインジケーターを確認します。 **メモリ**、 **スワップメモリ**、 **ディスク**、 **アクティブプロセス**。 値が大きすぎる場合は、ワークフローの数を減らしたり、スケジュールワークフローを異なる時間に開始に変更したりできます。

## データベースのパフォーマンス {#database-performances}

ほとんどの場合、パフォーマンスの問題はデータベースのメンテナンスに関連しています。 確認する主な項目は次のとおりです。

* 設定：adobe campaignプラットフォームの初期設定を確認し、完全なハードウェアチェックを実行することをお勧めします。
* Adobe Campaignプラットフォームのインストールと設定：ネットワーク設定とプラットフォームの配信品質オプションを確認します。
* データベースの保守：データベースのクリーンアップタスクが動作していること、およびデータベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 作業テーブルの数とサイズを確認します。
* リアルタイム診断：プロセスおよびプラットフォームのログファイルを確認し、問題の再作成中にデータベースのアクティビティを監視します。

>[!NOTE]
>
>For more information, refer to this section: [Database performances](../../production/using/database-performances.md).

## アプリケーション設定 {#application-configuration}

アプリケーション設定のベストプラクティスに関する記事のリストを以下に示します。

* MTAおよびMTAChildのプロセスとメモリ：mta **モジュールは、** mtachild **** 子モジュールにメッセージを配信します。 各 **mtachildは** 、統計サーバーから認証を要求し、送信する前に、メッセージを準備します。 Refer to this [page](../../installation/using/email-deliverability.md) for more information.
* TLS設定：スループットが低下する可能性があるので、TLSをグローバルに有効にすることはお勧めしません。 その代わりに、配信品質チームが管理するドメインごとのTLS設定は、ニーズに応じて調整する必要があります。 Refer to this [page](../../installation/using/email-deliverability.md#mx-configuration) for more information.
* DKIM:DKIMのセキュリティレベルを確保するために、1024bは暗号化の推奨サイズであるベストプラクティスです。 これより小さいサイズの DKIM 鍵は、大多数のアクセスプロバイダーには有効とはみなされません。この [ページ](../../delivery/using/technical-recommendations.md#dkim) と [テクノノートを参照してください](https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html)。

## 配信品質の問題 {#deliverability-issues}

配信品質に関するベストプラクティスと記事のリストを以下に示します。

* IPの評価：IPの評価が十分でない場合は、パフォーマンスに影響を与えます。 「 **配信品質の監視** 」モジュールでは、プラットフォームの配信品質パフォーマンスを追跡する様々なツールをオファーします。 この[ページ](../../delivery/using/monitoring-deliverability.md)を参照してください。
* IPウォームアップ：IPウォームアップは配信品質チームによって実行されます。 これには、数週間の間に、新しいIP経由での電子メールの数を徐々に増やすことが関係します。
* IPアフィニティの設定：誤ったIPアフィニティの設定により、電子メールが完全に停止する(設定に誤った演算子名やアフィニティ名が含まれる)か、スループットが低下する(アフィニティ内のIPの数が少ない)可能性があります。 この[ページ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)を参照してください。
* 電子メールのサイズ：電子メールのサイズは、スループットの重要な役割を果たします。 電子メールの最大サイズは60 KBにすることをお勧めします。 この[ページ](https://helpx.adobe.com/legal/product-descriptions/campaign.html)を参照してください。[ [配信スループット](../../reporting/using/global-reports.md#delivery-throughput) ]レポートで、時間別に転送されたバイト数をチェックします。
* 無効な受信者の数が多い：無効な受信者の数が多い場合は、スループットに影響を及ぼす可能性があります。 MTAは、無効な受信者への電子メールの送信を再試行し続けます。 データベースのメンテナンスが正しいことを確認してください。
* パーソナライゼーションの量：配信が「処理中のパーソナライゼーション」にとどまる場合は、パーソナライゼーションブロックで使用するJavaScriptを確認します。

>[!NOTE]
>
>「 [配信品質の主要ポイント](../../delivery/using/deliverability-key-points.md) 」も参照してください。

