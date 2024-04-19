---
product: campaign
title: メッセージのトラッキングと監視
description: メッセージのトラッキングと監視の方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Monitoring, Reporting
role: User
exl-id: a039a288-2e7b-4f35-9885-ead3ed4347af
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: ht
source-wordcount: '449'
ht-degree: 100%

---

# トラッキングと監視 {#track-and-monitor}

「**送信**」ボタンをクリックしましたか。何が起こるかを見てみましょう。配信の送信後、Adobe Campaign では、送信済みメッセージをトラッキングして、配信に対する受信者の反応を確認できます。これは、今後の送信を改善し、次のキャンペーンを最適化するのに役立ちます。

## 配信の監視 {#monitoring-deliveries}

キャンペーンを制御するには、メッセージが実際に受信者に配信されたことを確認する必要があります。

キャンペーン配信ダッシュボードから、処理済みメッセージと配信監査ログを確認できます。配信ログのメッセージのステータスも制御できます。詳しくは、[こちら](about-delivery-monitoring.md)を参照してください。

配信が送信されず、そのステータスが「**保留中**」のままになっている場合は、どのような状況が考えられるでしょうか。

* 実行プロセスが、リソースが使用可能になるのを待っています。MTA が開始されていない可能性があります。MTA サーバー上で mta@instance モジュールが開始されていることを確認し、必要であれば MTA モジュールを開始します。詳しくは、[こちら](../../production/using/administration.md)を参照してください。

* 送信インスタンスに設定されていないアフィニティを配信で使用している可能性があります。ヒント：トラフィック管理の設定（IP アフィニティ）を確認します。詳しくは、送信 SMTP トラフィックの制御を参照してください。

>[!NOTE]
>
>これらの手順はエキスパートユーザーのみ実行できます。

## 行動の追跡 {#track-behaviour}

受信者の行動を十分に把握するために、受信、開封、リンクのクリック、購読解除など、受信者が配信にどのように反応するかを追跡できます。Campaign Classic では、この情報は、配信のターゲットとなる受信者の「トラッキング」タブと配信の「トラッキング」タブに表示されます。

**ヒント**：メッセージトラッキングは、デフォルトで有効になっています。URL を設定するには、配信ウィザードの下部のセクションで「URL を表示」オプションを選択します。メッセージの URL ごとに、トラッキングを有効化するかどうかを選択できます。

詳しくは、[トラッキングの設定](how-to-configure-tracked-links.md)の節と[トラッキング指標](../../reporting/using/delivery-reports.md#tracking-indicators)の説明を参照してください。

## 配信パフォーマンス {#delivery-performances}

メッセージが配信される速度を測定するには、配信スループットを制御します。1 時間に送信されたメッセージの数とメッセージのサイズ（bps）が基準になります。詳しくは、[配信スループット](../../reporting/using/global-reports.md#delivery-throughput)を参照してください。

**ヒント**：

* 配信を失敗した状態のままインスタンス上で放置すると、一時テーブルが維持され、パフォーマンスに影響が生じるため、配信を失敗した状態のまま放置しないでください。

* アドレスの品質を維持するため、不要になった配信やアクティブでない受信者はデータベースから削除してください。

* 大規模な配信を同時にスケジュールしないようにしてください。負荷がシステム全体で均等に分散されるまでには、5～10 分かかることがあります。

## 配信のトラブルシューティング {#delivery-troubleshooting}

配信に関する問題が発生した場合は、特定のアクションを実行できます。

* [配信品質の問題](../../production/using/performance-and-throughput-issues.md#deliverability_issues)

* [画像の表示の問題](../../production/using/image-display-issues.md)

* [配信パフォーマンスの問題](delivery-performances.md)

* [一時ファイルの問題](../../production/using/temporary-files.md) - *オンプレミスのお客様のみ*
