---
title: メッセージの追跡と監視
seo-title: メッセージの追跡と監視
page-status-flag: never-activated
uuid: a540efc7-105d-4c7f-a2ee-ade4d22b3445
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliveries-best-practices
discoiquuid: 0cbc4e92-482f-4dac-a1fb-b738e7127938
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 5e6ecd636ee0b2199808c03b2fd898a194f0c1ea
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 61%

---


# トラッキングと監視 {#track-and-monitor}

「送信」ボタンをクリックしましたか。何が起こるかを見てみましょう。配信の送信後、Adobe Campaign では、送信済みメッセージをトラッキングして、配信に対する受信者の反応を確認できます。これは、今後の送信を改善し、次のキャンペーンを最適化するのに役立ちます。

## 配信の監視 {#monitoring-deliveries}

キャンペーンを制御するには、メッセージが実際に受信者に配信されたことを確認する必要があります。

キャンペーン配信ダッシュボードから、処理済みのメッセージと配信の監査ログを確認できます。
配信ログのメッセージのステータスも制御できます。[詳細情報](../../delivery/using/monitoring-a-delivery.md#delivery-dashboard)。

配信が送信されず、そのステータスが「**保留中**」のままになっている場合は、どのような状況が考えられるでしょうか。

* 実行プロセスが、リソースが使用可能になるのを待っています。MTA が開始されていない可能性があります。mta@instanceモジュールがMTAサーバーで起動されていることを確認し、必要に応じてMTAモジュールを開始します。 [詳細情報](../../production/using/administration.md)。

* 送信インスタンスに設定されていないアフィニティを配信で使用している可能性があります。ヒント：トラフィック管理(IPアフィニティ)の設定を確認します。 詳しくは、送信 SMTP トラフィックの制御を参照してください。

>[!NOTE]
>
>これらの手順はエキスパートユーザーのみ実行できます。

## トラッキング {#tracking-deliveries}

受信者の動作をより深く知るには、配信に対するユーザーの反応を追跡します。受信、開封、リンクのクリック、購読解除など Campaign Classicでは、この情報は、配信がターゲットとする受信者の「追跡」タブと配信の「追跡」タブに表示されます。 Campaign Standardは、配信の「トラッキングログ」タブに表示されます。

**ヒント**:メッセージ追跡はデフォルトで有効です。 URL を設定するには、配信ウィザードの下部のセクションで「URL を表示」オプションを選択します。メッセージの URL ごとに、トラッキングを有効化するかどうかを選択できます。

For more on this, refer to the [Configuring tracking](../../delivery/using/how-to-configure-tracked-links.md) section and the [Tracking indicators](../../reporting/using/delivery-reports.md#tracking-indicators) description.

## 配信パフォーマンス {#delivery-performances}

メッセージが配信される速度を測定するには、配信スループットを制御します。1 時間に送信されたメッセージの数とメッセージのサイズ（bps）が基準になります。詳しくは、[配信スループット](../../reporting/using/global-reports.md#delivery-throughput)を参照してください。

**ヒント**:

* 配信を失敗した状態のままインスタンス上で放置すると、一時テーブルが維持され、パフォーマンスに影響が生じるため、配信を失敗した状態のまま放置しないでください。

* アドレスの品質を維持するため、不要になった配信やアクティブでない受信者はデータベースから削除してください。

* 大規模な配信を同時にスケジュールしないようにしてください。負荷がシステム全体で均等に分散されるまでには、5～10 分かかることがあります。

## 配信のトラブルシューティング {#delivery-troubleshooting}

配信に関する問題が発生した場合は、特定のアクションを実行できます。

* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)

* [画像の表示の問題](../../production/using/image-display-issues.md)

* [配信のパフォーマンスの問題](../../delivery/using/monitoring-a-delivery.md#performance_issues)

* [一時ファイルの問題](../../production/using/temporary-files.md) — 社内 *のお客様のみ*
