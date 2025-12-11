---
product: campaign
title: 配信のパフォーマンスとトラブルシューティング
description: Campaign Classic v7 で配信パフォーマンスを最適化し、問題をトラブルシューティングする方法について説明します
feature: Monitoring, Deliverability, Troubleshooting
role: User, Developer
exl-id: cc793d7b-0a26-4a75-97ed-d79c87d9b3b8
source-git-commit: 2ebae2b84741bf26dd44c872702dbf3b0ebfc453
workflow-type: ht
source-wordcount: '669'
ht-degree: 100%

---

# 配信のパフォーマンスとトラブルシューティング {#delivery-performance-troubleshooting}

>[!NOTE]
>
>配信のパフォーマンスとベストプラクティスに関する包括的なガイダンスについて詳しくは、[Campaign v8 配信のベストプラクティス](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/start/delivery-best-practices)ページを参照してください。このコンテンツは、Campaign Classic v7 と Campaign v8 の両方のユーザーに適用されます。
>
>このページでは、ハイブリッドおよびオンプレミスのデプロイメントでのパフォーマンスの最適化とトラブルシューティングに対する **Campaign Classic v7 固有の設定**&#x200B;について説明します。

配信パフォーマンス、プラットフォームの最適化、強制隔離管理、データベースのメンテナンス、スケジュールのレコメンデーションに関する包括的なベストプラクティスについて詳しくは、[Campaign v8 配信のベストプラクティスドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"}を参照してください。

## パフォーマンスの最適化 {#performance-optimization}

**Campaign Classic v7 ハイブリッド／オンプレミスデプロイメント**&#x200B;の場合、次のデータベースとインフラストラクチャの最適化により配信パフォーマンスを向上させることができます。

### データベースの最適化

アプリケーションで使用される SQL クエリのパフォーマンスを最適化する&#x200B;**インデックスアドレス**。インデックスは、データスキーマのメイン要素から宣言できます。この最適化には、オンプレミスデプロイメントで使用可能な直接データベースアクセスとスキーマカスタマイズが必要です。

### インフラストラクチャの調整

**大規模配信の設定**：100 万人を超える受信者への配信には、送信キューにスペースが必要です。オンプレミスインストールの場合、MTA 子はカスタムバッチサイズを処理するように設定できます。インフラストラクチャの処理能力に基づいてこれらの設定を調整するには、システム管理者にお問い合わせください。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、インフラストラクチャの最適化と MTA 設定はアドビで管理されます。デプロイメントに適用できるパフォーマンスのレコメンデーションについて詳しくは、[Campaign v8 配信のベストプラクティス](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"}を参照してください。

### データベースのメンテナンス {#database-maintenance}

**Campaign Classic v7 ハイブリッド／オンプレミスデプロイメント**&#x200B;の場合、プラットフォームとデータベースのメンテナンスは配信の送信パフォーマンスに直接影響します。

定期的なメンテナンスタスクを以下に示します。

**データベースのクリーンアップ**：データベースのクリーンアップワークフローを使用して、古い配信ログ、トラッキングデータ、一時テーブルを削除します。データベースのメンテナンスが不十分だと、配信の準備と送信が遅くなる場合があります。

**データベースパフォーマンスの監視**：クエリのパフォーマンス、インデックスの断片化、テーブル統計を監視します。ガイドについて詳しくは、[このページ](../../production/using/database-performances.md)を参照してください。

**テクニカルワークフローの監視**：すべてのテクニカルワークフロー（特にクリーンアップ、トラッキング、配信品質の更新ワークフロー）がエラーなく正しく実行されていることを確認します。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、データベースのメンテナンスとテクニカルワークフローはアドビで監視および管理されます。[Campaign v8 配信の監視ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitoring-deliverability){target="_blank"}で説明されているように、配信固有の監視に焦点を当てています。

## 配信の問題のトラブルシューティング {#troubleshooting}

>[!NOTE]
>
>配信のトラブルシューティングに関する包括的なガイダンスは、Campaign v8 ドキュメントに記載されており、Campaign Classic v7 と Campaign v8 の両方のユーザーに適用できます。
>
>* 一般的な配信エラーと解決策：[配信エラーについて](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"}
>* 配信遅延の診断：[Campaign UI での配信の監視](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"}
>* 配信のベストプラクティス：[配信のベストプラクティス](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"}
>
>この節では、ハイブリッドおよびオンプレミスのデプロイメントでの **Campaign Classic v7 固有のトラブルシューティング**&#x200B;について説明します。

**Campaign Classic v7 ハイブリッド／オンプレミスデプロイメント**&#x200B;の場合、次のトラブルシューティング手順は管理するインフラストラクチャに固有です。

### MX ルールの設定

特定の ISP でスロットルの問題が発生する場合は、MX ルールの設定を確認して調整する必要があります。MX ルールと割り当て量について詳しくは、[この節](../../installation/using/email-deliverability.md#about-mx-rules)を参照してください。

### 配信パフォーマンスのデータベースメンテナンス

ミッドソーシングデプロイメントで次のエラーが発生した場合：

```
Error during the call of method 'AppendDeliveryPart' on the mid sourcing server: 'Communication error with the server: please check this one is correctly configured. Code HTTP 408 'Service temporarily unavailable'.
```

原因は、データをミッドソーシングサーバーに送信する前に、マーケティングインスタンスでデータの作成に時間がかかりすぎているというパフォーマンスの問題に関連しています。

**オンプレミスインストールの場合**、データベースをクリーンアップしてインデックスを再作成します。データベースのメンテナンスについて詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

スケジュールされているアクティビティのすべてのワークフロー、および失敗ステータスのすべてのワークフローも再開する必要があります。[この節](../../workflow/using/scheduler.md)を参照してください。

### テクニカルワークフローの監視

オンプレミスインストールの場合、配信品質に関連するすべてのテクニカルワークフローがエラーなく実行されていることを確認します。

**配信品質の更新ワークフロー**：バウンスメール選定ルールと配信品質インジケーターを更新します。

**トラッキングワークフロー**：送信済み配信のトラッキングデータを処理します。

**データベースクリーンアップワークフロー**：パフォーマンスを維持するために、古い配信ログと一時テーブルを定期的にパージします。

**[!UICONTROL 管理]**／**[!UICONTROL 本番]**／**[!UICONTROL テクニカルワークフロー]**&#x200B;でワークフローのステータスを確認します。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、テクニカルワークフローとインフラストラクチャの監視はアドビで管理されます。[Campaign v8 ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"}で説明されているように、配信コンテンツとターゲティングに焦点を当てます。

## 関連トピック

* [配信エラーについて](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"}（Campaign v8 ドキュメント）
* [配信のベストプラクティス](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"}（Campaign v8 ドキュメント）
* [Campaign UI での配信の監視](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"}（Campaign v8 ドキュメント）
* [データベースメンテナンス](../../production/using/recommendations.md) （v7 ハイブリッド／オンプレミス）
* [メール配信品質](../../installation/using/email-deliverability.md)（v7 ハイブリッド／オンプレミス）
* [データベースパフォーマンス](../../production/using/database-performances.md)（v7 ハイブリッド／オンプレミス）

