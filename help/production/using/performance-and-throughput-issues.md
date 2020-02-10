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
source-git-commit: 34cd6e6cf5652c9e2163848c2b1ef32f53ee6ca4

---


# パフォーマンスとスループットの問題{#performance-and-throughput-issues}

>[!NOTE]
>
>まず、最新のビルドがインストールされていることを確認します。 これにより、最新の機能とバグ修正が確実に提供されます。 各リリースの内 [容の詳細については](https://docs.campaign.adobe.com/doc/AC/en/RN.html) 、「リリースノート」を参照してください。

## ハードウェアとインフラストラクチャ {#hardware-and-infrastructure}

オンプレミスCampaign Classicのハードウェア要件に関する一般的なガイドラインをこの記事で詳し [く説明します](https://helpx.adobe.com/campaign/kb/hardware-sizing-guide.html)。

コンサルティングチームは、ホストされる顧客に対して、データベース内の様々なタイプのテーブルで使用されている領域とSFTPサイトで使用されている領域を簡単に確認できるツールを提供できます。 また、不要なデータをクリーンアップするためのツールも提供されます。 このツールを実装する必要がある場合は、コンサルティングチームまたはサポートチームにお問い合わせください。 このツールを使用して確認する必要がある重要な点を次に示します。

* インデックスサイズがテーブルサイズより大きい場合は、真空が必要です。
* 最大膨張を持つテーブルを確認します。 これらのテーブルを頻繁に使用する場合は、バキューム処理が必要です。
* データベースをブロックすると、電子メールの送信が停止する場合があります。

また、Adobe Campaignには、CPUとRAMの使 [用状況を](../../production/using/monitoring-processes.md#manual-monitoring) 確認するツールも用意されています。 このツールを使用して、次のような特定のインジケータを確認します。 **Memory**, **Swap Memory**, Disk **, Active Processes****** Active Processes 値が大きすぎる場合は、ワークフローの数を減らしたり、ワークフローを異なる時間に開始するようにスケジュールしたりできます。

## データベースのパフォーマンス {#database-performances}

ほとんどの場合、パフォーマンスの問題はデータベースのメンテナンスに関連しています。 確認する主な項目を次に示します。

* 設定：最初のAdobe Campaignプラットフォーム設定を確認し、完全なハードウェアチェックを実行することをお勧めします。
* Adobe Campaignプラットフォームのインストールと設定：ネットワーク設定とプラットフォームの配信品質オプションを確認します。
* データベースの保守：データベースのクリーンアップタスクが動作し、データベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 作業用テーブルの数とサイズを確認します。
* リアルタイム診断：プロセスおよびプラットフォームのログファイルを確認し、問題の再作成中にデータベースのアクティビティを監視します。

>[!NOTE]
>
>For more information, refer to this section: [Database performances](../../production/using/database-performances.md).

## アプリケーション設定 {#application-configuration}

以下に、アプリケーション設定のベストプラクティスに関する記事の一覧を示します。

* MTAおよびMTAChildのプロセスとメモリ：mtaモジュール **は** 、メッセージをmtachild子モジュールに **配信します** 。 各mtchildは **** 、統計サーバーから認証を要求して送信する前に、メッセージを準備します。 Refer to this [page](../../installation/using/email-deliverability.md) for more information.
* TLS設定：tlsをグローバルに有効にすることは、スループットを低下させる可能性があるので、お勧めしません。 その代わり、配信品質チームが管理するドメインごとのTLS設定は、ニーズに応じて調整する必要があります。 Refer to this [page](../../installation/using/email-deliverability.md#mx-configuration) for more information.
* DKIM:dkimのセキュリティレベルを確保するために、1024bは暗号化の推奨サイズであるベストプラクティスです。 これより小さいサイズの DKIM 鍵は、大多数のアクセスプロバイダーには有効とはみなされません。このページとこ [のテクノ](../../delivery/using/technical-recommendations.md#domainkeys-identified-mail--dkim-) ートを参照し [てください](https://helpx.adobe.com/campaign/kb/domain-name-delegation.html)。

## 配信品質の問題 {#deliverability-issues}

配信品質に関するベストプラクティスと記事を以下に示します。

* IPの評判：ipの評判が十分でない場合は、パフォーマンスに影響を与えます。 配信品質監 **視モジュールは** 、プラットフォームの配信品質パフォーマンスを追跡するための様々なツールを提供します。 この[ページ](../../delivery/using/technical-monitoring.md)を参照してください。
* IPウォームアップ：ipウォームアップは配信品質チームによって実行されます。 これには、数週間にわたって新しいIPを介した電子メールの数が徐々に増えていきます。
* IP親和性の設定：ip親和性の設定が正しくないと、電子メールが完全に停止する（設定での演算子/親和性の名前が正しくない）か、スループットが低下する（親和性内のIPの数が少ない）可能性があります。 この[ページ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)を参照してください。
* 電子メールサイズ：電子メールのサイズは、スループットに重要な役割を果たします。 電子メールの最大サイズは60 KBにすることをお勧めします。 この[ページ](https://helpx.adobe.com/legal/product-descriptions/campaign.html)を参照してください。[配信スル [ープット](../../reporting/using/reports-on-deliveries.md#delivery-throughput) ]レポートで、1時間ごとに転送されたバイト数を確認します。
* 無効な受信者の数が多い：無効な受信者の数が多いと、スループットに影響を与える可能性があります。 MTAは、無効な受信者への電子メールの送信を再試行し続けます。 データベースのメンテナンスが良好であることを確認してください。
* パーソナライゼーションの量：配信が「パーソナライゼーション中」のままの場合は、パーソナライゼーションブロックで使用されるJavaScriptを確認します。

>[!NOTE]
>
>『配信品質はじめに』ガイドを参照す [るのを忘れないで](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/deliverability.html) 。

