---
solution: Campaign Classic
product: campaign
title: パフォーマンスとスループットの問題
description: パフォーマンスとスループットの問題
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 3139a9bf5036086831e23acef21af937fcfda740
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 8%

---


# パフォーマンスとスループットの問題{#performance-and-throughput-issues}

まず、最新のビルドがインストールされていることを確認してください。 これにより、最新の機能とバグ修正を確実に行うことができます。

各リリースの内容の詳細については、[リリースノート](../../rn/using/latest-release.md)を参照してください。

## ハードウェアとインフラストラクチャ{#hardware-and-infrastructure}

オンプレミスCampaign Classicのハードウェア要件に関する一般的なガイドラインは、この[ページ](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html)で詳しく説明しています。

コンサルティングチームは、ホストするお客様に対して、データベース内の様々なタイプのテーブルで使用されている領域とSFTPサイトで使用されている領域を簡単に表示できるツールを提供できます。 また、不要なデータをクリーンアップするためのツールも提供されています。 このツールを導入する必要がある場合は、[Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。 このツールを使用して、次の点を確認してください。

* インデックスサイズがテーブルサイズより大きい場合は、真空が必要です。
* 最大膨張率を持つテーブルをチェックします。 これらのテーブルを頻繁に使用する場合は、バキュームする必要があります。
* データベースのブロックにより、電子メールの送信が停止する場合があります。

Adobe Campaignは、CPUとRAMの使用状況をチェックする[ツール](../../production/using/monitoring-processes.md#manual-monitoring)も提供します。 このツールを使用して、次のような特定のインジケーターを確認します。**メモリ**、**スワップメモリ**、**ディスク**、**アクティブプロセス**。 値が大きすぎる場合は、ワークフローの数を減らしたり、スケジュールワークフローを異なる時間に開始に変更したりできます。

## データベースチェック{#database-performances}

ほとんどの場合、パフォーマンスの問題はデータベースのメンテナンスに関連しています。 確認する主な項目は次のとおりです。

* 設定：adobe campaignプラットフォームの初期設定を確認し、完全なハードウェアチェックを実行することをお勧めします。
* Adobe Campaignプラットフォームのインストールと設定：ネットワーク設定とプラットフォームの配信品質オプションを確認します。
* データベースの保守：データベースのクリーンアップタスクが動作していること、およびデータベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 作業テーブルの数とサイズを確認します。
* リアルタイム診断：プロセスおよびプラットフォームのログファイルを確認し、問題の再作成中にデータベースのアクティビティを監視します。

>[!NOTE]
>
>詳しくは、次の節を参照してください。[データベースのパフォーマンス](../../production/using/database-performances.md)。

## アプリケーション構成{#application-configuration}

アプリケーション設定のベストプラクティスに関する記事のリストを以下に示します。

* MTAおよびMTAChildのプロセスとメモリ：**mta**&#x200B;モジュールは、**mtachild**&#x200B;子モジュールにメッセージを配布します。 各&#x200B;**mtachild**&#x200B;は、統計サーバーから認証を要求し、送信する前に、メッセージを準備します。 詳細は、この[ページ](../../installation/using/email-deliverability.md)を参照してください。
* TLS設定：スループットが低下する可能性があるので、TLSをグローバルに有効にすることはお勧めしません。 その代わりに、配信品質チームが管理するドメインごとのTLS設定は、ニーズに応じて調整する必要があります。 詳細は、この[ページ](../../installation/using/email-deliverability.md#mx-configuration)を参照してください。
* DKIM:DKIMのセキュリティレベルを確保するために、1024bは暗号化の推奨サイズであるベストプラクティスです。 これより小さいサイズの DKIM 鍵は、大多数のアクセスプロバイダーには有効とはみなされません。この[ページ](../../delivery/using/technical-recommendations.md#dkim)と[テクノテート](https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html)を参照してください。

## 配信品質の問題 {#deliverability-issues}

配信品質に関するベストプラクティスと記事のリストを以下に示します。

* IPの評価：IPの評価が十分でない場合は、パフォーマンスに影響を与えます。 **配信品質の監視**&#x200B;モジュールは、各種ツールをオファーして、プラットフォームの配信品質のパフォーマンスを追跡します。 この[ページ](../../delivery/using/monitoring-deliverability.md)を参照してください。
* IPウォームアップ：IPウォームアップは配信品質チームによって実行されます。 これには、数週間の間に、新しいIP経由での電子メールの数を徐々に増やすことが関係します。
* IPアフィニティの設定：誤ったIPアフィニティの設定により、電子メールが完全に停止する(設定に誤った演算子名やアフィニティ名が含まれる)か、スループットが低下する(アフィニティ内のIPの数が少ない)可能性があります。 この[ページ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)を参照してください。
* 電子メールのサイズ：電子メールのサイズは、スループットの重要な役割を果たします。 電子メールの最大サイズは60 KBにすることをお勧めします。 この[ページ](https://helpx.adobe.com/legal/product-descriptions/campaign.html)を参照してください。[配信スループット](../../reporting/using/global-reports.md#delivery-throughput)レポートで、1時間に転送されたバイト数を確認します。
* 無効な受信者の数が多い：無効な受信者の数が多い場合は、スループットに影響を及ぼす可能性があります。 MTAは、無効な受信者への電子メールの送信を再試行し続けます。 データベースのメンテナンスが正しいことを確認してください。
* パーソナライゼーションの量：配信が「処理中のパーソナライゼーション」にとどまる場合は、パーソナライゼーションブロックで使用するJavaScriptを確認します。

>[!NOTE]
>
>「[配信品質の重要点](../../delivery/using/deliverability-key-points.md)」も参照してください。
