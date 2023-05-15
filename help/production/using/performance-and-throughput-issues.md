---
product: campaign
title: パフォーマンスとスループットの問題
description: パフォーマンスとスループットの問題
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=en" tooltip="Applies to on-premise and hybrid deployments only"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: fe69efda-a052-4f67-9c13-665f011d0a2b
source-git-commit: a5762cd21a1a6d5a5f3a10f53a5d1f43542d99d4
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 11%

---

# パフォーマンスとスループットの問題{#performance-and-throughput-issues}



まず、最新のビルドがインストールされていることを確認する必要があります。 これにより、最新の機能とバグ修正を確実に利用できます。

詳しくは、 [リリースノート](../../rn/using/latest-release.md) を参照してください。

## ハードウェアとインフラストラクチャ {#hardware-and-infrastructure}

オンプレミスCampaign Classicのハードウェア要件に関する一般的なガイドラインについては、このドキュメントを参照してください [ページ](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html).

コンサルティングチームは、ホスト型のお客様に、データベース内の様々なタイプのテーブルでどのくらいの容量が使用されているか、および SFTP サイトで使用されている容量を簡単に表示できるツールを提供できます。 また、不要なデータをクリーンアップするためのツールも提供されています。 連絡先 [Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) このツールを実装する必要がある場合。 このツールを使用して確認すべき重要な点を次に示します。

* インデックスサイズがテーブルサイズより大きい場合は、空白が必要です。
* 最大膨張率を持つテーブルを確認します。 これらのテーブルを頻繁に使用する場合は、バキュームを行う必要があります。
* データベースをブロックすると、E メールの送信が停止する場合があります。

Adobe Campaignには [ツール](../../production/using/monitoring-processes.md#manual-monitoring) をクリックして、CPU と RAM の使用量を確認します。 このツールを使用して、次のような特定の指標を確認します。 **メモリ**, **スワップメモリ**, **ディスク**, **アクティブなプロセス**. 値が大きすぎる場合は、ワークフローの数を減らしたり、別の時間に開始するようにワークフローをスケジュールしたりできます。

## データベースチェック {#database-performances}

ほとんどの場合、パフォーマンスの問題はデータベースのメンテナンスに関係しています。 次に、確認する主な項目を示します。

* 設定：最初のAdobe Campaignプラットフォーム設定を確認し、完全なハードウェアチェックを実行することをお勧めします。
* Adobe Campaignプラットフォームのインストールと設定：ネットワーク設定とプラットフォーム配信品質オプションを確認します。
* データベースのメンテナンス：データベースのクリーンアップタスクが動作していること、およびデータベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 作業用テーブルの数とサイズを確認します。
* リアルタイム診断：プロセスとプラットフォームのログファイルを確認し、問題の再作成中にデータベースアクティビティを監視します。

>[!NOTE]
>
>詳しくは、この節を参照してください。 [データベースのパフォーマンス](../../production/using/database-performances.md).

## アプリケーション設定 {#application-configuration}

以下に、アプリケーション設定のベストプラクティスに関する記事のリストを示します。

* MTA と MTAChild のプロセスとメモリ：の **mta** モジュールは、メッセージを **mtachild** 子モジュール。 各 **mtachild** 統計サーバーからの認証をリクエストして送信する前に、メッセージを準備します。 詳しくは、 [ページ](../../installation/using/email-deliverability.md) を参照してください。
* TLS 設定：スループットを低下させる可能性があるので、TLS をグローバルに有効にすることはお勧めしません。 代わりに、配信品質チームが管理するドメインごとの TLS 設定は、ニーズに応じて調整する必要があります。 詳しくは、 [ページ](../../installation/using/email-deliverability.md#mx-configuration) を参照してください。
* DKIM:DKIM のセキュリティレベルを確保するために、1024b がベストプラクティスとして推奨される暗号化サイズです。 これより小さいサイズの DKIM 鍵は、大多数のアクセスプロバイダーには有効とはみなされません。[このページ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html?lang=ja#authentication)を参照してください。

## 配信品質の問題 {#deliverability-issues}

配信品質に関するベストプラクティスと記事のリストを次に示します。

* IP レピュテーション：IP レピュテーションが十分でない場合は、パフォーマンスに影響を与えます。 この **配信品質の監視** モジュールは、プラットフォームの配信品質のパフォーマンスをトラッキングする様々なツールを提供します。 この[ページ](../../delivery/using/monitoring-deliverability.md)を参照してください。
* IP ウォームアップ：IP ウォームアップは、配信品質チームが実行します。 これには、数週間にわたって新しい IP を通じて E メールの数を徐々に増やす必要があります。
* IP アフィニティの設定：IP アフィニティが正しく設定されていない場合、e メール全体を停止したり（設定におけるオペレーター/アフィニティの名前が正しくない場合）、スループットが低下したり（アフィニティ内の IP の数が少ない場合）、 この[ページ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)を参照してください。
* E メールのサイズ：スループットでは、E メールのサイズが重要な役割を果たします。 E メールの推奨最大サイズは 60 KB です。 この[ページ](https://helpx.adobe.com/legal/product-descriptions/campaign.html)を参照してください。内 [配信スループット](../../reporting/using/global-reports.md#delivery-throughput) レポートでは、1 時間に転送されたバイト数を確認します。
* 無効な受信者の数が多い：無効な受信者の数が多い場合は、スループットに影響を与える可能性があります。 MTA は無効な受信者への E メールの送信を再試行し続けます。 データベースが適切にメンテナンスされていることを確認してください。
* パーソナライゼーションの量：配信が「パーソナライゼーション中」のままの場合は、パーソナライゼーションブロックで使用される JavaScript を確認します。

>[!NOTE]
>
>関連トピック [配信品質](../../delivery/using/about-deliverability.md) 」セクションに入力します。 配信品質の詳細については、[アドビの配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja)を参照してください。
