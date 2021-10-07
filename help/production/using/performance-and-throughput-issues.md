---
product: campaign
title: パフォーマンスとスループットの問題
description: パフォーマンスとスループットの問題
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: fe69efda-a052-4f67-9c13-665f011d0a2b
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 11%

---

# パフォーマンスとスループットの問題{#performance-and-throughput-issues}

![](../../assets/v7-only.svg)

まず、最新のビルドがインストールされていることを確認する必要があります。 これにより、最新の機能とバグ修正を利用できます。

各リリースの内容について詳しくは、[ リリースノート ](../../rn/using/latest-release.md) を参照してください。

## ハードウェアとインフラストラクチャ {#hardware-and-infrastructure}

オンプレミスCampaign Classicのハードウェア要件に関する一般的なガイドラインについては、この [ ページ ](https://helpx.adobe.com/jp/campaign/kb/hardware-sizing-guide.html) を参照してください。

コンサルティングチームは、ホスト型のお客様に、データベース内の様々なタイプのテーブルで使用されている容量や SFTP サイトで使用されている容量を簡単に確認できるツールを提供できます。 また、不要なデータをクリーンアップするためのツールも提供されています。 このツールを実装する必要がある場合は、[Adobeカスタマーケア ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) にお問い合わせください。 このツールを使用して確認すべき重要な点を次に示します。

* インデックスサイズがテーブルサイズより大きい場合は、真空処理が必要です。
* 最大膨張率を持つテーブルを確認します。 これらのテーブルを頻繁に使用する場合は、バキュームする必要があります。
* データベースをブロックすると、E メールの送信が停止する場合があります。

Adobe Campaignは、CPU と RAM の使用状況を確認する [ ツール ](../../production/using/monitoring-processes.md#manual-monitoring) も提供しています。 このツールを使用して、次のような特定の指標を確認します。**メモリ**、**スワップメモリ**、**ディスク**、**アクティブプロセス**。 値が大きすぎる場合は、ワークフローの数を減らしたり、異なる時間に開始するようにワークフローをスケジュールしたりできます。

## データベースのチェック {#database-performances}

ほとんどの場合、パフォーマンスの問題はデータベースのメンテナンスに関連しています。 次に、確認する主な項目を示します。

* 設定：最初のAdobe Campaignプラットフォーム設定を確認し、完全なハードウェアチェックを実行することをお勧めします。
* Adobe Campaignプラットフォームのインストールと設定：ネットワーク設定とプラットフォーム配信品質オプションを確認します。
* データベースのメンテナンス：データベースのクリーンアップタスクが動作し、データベースのメンテナンスが正しくスケジュールされ、実行されていることを確認します。 作業用テーブルの数とサイズを確認します。
* リアルタイム診断：プロセスおよびプラットフォームログファイルを確認し、問題の再作成中にデータベースアクティビティを監視します。

>[!NOTE]
>
>詳しくは、この節を参照してください。[ データベースのパフォーマンス ](../../production/using/database-performances.md)。

## アプリケーションの設定 {#application-configuration}

以下に、アプリケーション設定のベストプラクティスに関する記事のリストを示します。

* MTA および MTAChild プロセスとメモリ：**mta** モジュールは、メッセージを **mtachild** 子モジュールに配信します。 各 **mtachild** は、統計サーバに認証をリクエストし、メッセージを送信する前に、メッセージを準備します。 詳しくは、この [ ページ ](../../installation/using/email-deliverability.md) を参照してください。
* TLS 設定：スループットを低下させる可能性があるので、TLS をグローバルに有効にすることはお勧めしません。 代わりに、配信品質チームが管理するドメインごとの TLS 設定は、ニーズに応じて調整する必要があります。 詳しくは、この [ ページ ](../../installation/using/email-deliverability.md#mx-configuration) を参照してください。
* DKIM:DKIM のセキュリティレベルを保証するために、1024b がベストプラクティスとして推奨される暗号化サイズです。 これより小さいサイズの DKIM 鍵は、大多数のアクセスプロバイダーには有効とはみなされません。[このページ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html?lang=ja#authentication)を参照してください。

## 配信品質の問題 {#deliverability-issues}

配信品質に関するベストプラクティスと記事のリストを次に示します。

* IP レピュテーション：IP レピュテーションが十分でない場合は、パフォーマンスに影響を与えます。 **配信品質の監視** モジュールは、プラットフォームの配信品質のパフォーマンスをトラッキングする様々なツールを提供します。 この[ページ](../../delivery/using/monitoring-deliverability.md)を参照してください。
* IP ウォームアップ：IP ウォームアップは、配信品質チームによって実行されます。 これには、数週間の間に新しい IP 経由で E メールの数を徐々に増やす必要があります。
* IP アフィニティの設定：IP アフィニティの設定が正しくない場合、e メール全体を停止したり（設定におけるオペレーター/アフィニティの名前が正しくない場合）、スループットが低下する（アフィニティ内の IP の数が少ない場合）ことがあります。 この[ページ](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)を参照してください。
* E メールのサイズ：E メールのサイズは、スループットに重要な役割を果たします。 E メールの最大サイズは 60 KB です。 この[ページ](https://helpx.adobe.com/legal/product-descriptions/campaign.html)を参照してください。[ 配信スループット ](../../reporting/using/global-reports.md#delivery-throughput) レポートで、1 時間に転送されたバイト数を確認します。
* 無効な受信者の数が多い：無効な受信者の数が多い場合は、スループットに影響を与える可能性があります。 MTA は引き続き無効な受信者への E メールの送信を再試行します。 データベースが適切にメンテナンスされていることを確認してください。
* パーソナライゼーションの量：配信が「パーソナライゼーション中」のままの場合は、パーソナライゼーションブロックで使用される JavaScript を確認します。

>[!NOTE]
>
>[ 配信品質 ](../../delivery/using/about-deliverability.md) の節も参照してください。 配信品質の詳細については、[アドビの配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja)を参照してください。
