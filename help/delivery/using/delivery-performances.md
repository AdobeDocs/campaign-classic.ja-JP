---
product: campaign
title: 配信パフォーマンスのベストプラクティス
description: 配信パフォーマンスとベストプラクティスについて詳しく説明します
feature: Deliverability
role: User, Developer
exl-id: cc793d7b-0a26-4a75-97ed-d79c87d9b3b8
source-git-commit: eac670cd4e7371ca386cee5f1735dc201bf5410a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 6%

---

# 配信パフォーマンスのベストプラクティス {#delivery-performances}

>[!NOTE]
>
>配信のパフォーマンスとベストプラクティスに関する包括的なガイダンスについては、[Campaign v8 配信のベストプラクティス ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices) ページを参照してください。 このコンテンツは、Campaign Classic v7 ユーザーと Campaign v8 ユーザーの両方に適用されます。
>
>このページは、ハイブリッドデプロイメントとオンプレミスデプロイメントの **0}Campaign Classic v7 固有のパフォーマンス設定 } について説明します。**

配信パフォーマンス、プラットフォームの最適化、強制隔離管理、データベースのメンテナンス、スケジュールに関する包括的なベストプラクティスについては、[Campaign v8 配信のベストプラクティスドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} を参照してください。

## パフォーマンスチューニング {#best-practices-performance}

**Campaign Classic v7 ハイブリッド/オンプレミスデプロイメント** の場合は、次のデータベースとインフラストラクチャの最適化により、配信パフォーマンスを向上させることができます。

### データベースの最適化

**インデックスアドレス**：アプリケーションで使用される SQL クエリのパフォーマンスを最適化します。 インデックスは、データスキーマのメイン要素から宣言できます。 この最適化には、オンプレミスデプロイメントで使用できる直接データベースアクセスとスキーマのカスタマイズが必要です。

### インフラストラクチャの調整

**大規模な配信設定**:100 万人を超える受信者への配信には、送信キューの容量が必要です。 オンプレミスインストールの場合、MTA の子は、カスタムバッチサイズを処理するように設定できます。 これらの設定をインフラストラクチャの処理能力に応じて調整する場合は、システム管理者にお問い合わせください。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、インフラストラクチャの最適化と MTA 設定は、Adobeで管理されます。 デプロイメントに適用できるパフォーマンスの推奨事項については、[Campaign v8 配信のベストプラクティス ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} を参照してください。

## データベースのメンテナンス {#performance-issues}

**Campaign Classic v7 ハイブリッド/オンプレミスデプロイメント** の場合、プラットフォームとデータベースのメンテナンスは、配信の送信パフォーマンスに直接影響します。

定期的なメンテナンスタスクには、次のものが含まれます。

**データベースクリーンアップ**：データベースクリーンアップワークフローを使用して、古い配信ログ、トラッキングデータおよび一時テーブルを削除します。 データベースのメンテナンスが不十分だと、配信の準備と送信が遅くなる可能性があります。

**データベースパフォーマンスの監視**：クエリのパフォーマンス、インデックスの断片化およびテーブル統計を監視します。 詳しいガイダンスについては、[ このページ ](../../production/using/database-performances.md) を参照してください。

**テクニカルワークフロー監視**：すべてのテクニカルワークフロー（特に、クリーンアップ、トラッキング、配信品質の更新のワークフロー）がエラーなく正しく実行されていることを確認します。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、データベースのメンテナンスとテクニカルワークフローは、Adobeによって監視および管理されます。 [Campaign v8 配信の監視ドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitoring-deliverability){target="_blank"} で説明されているように、配信固有の監視に焦点を当てます。

## 関連トピック

* [ 配信のベストプラクティス ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} （Campaign v8 ドキュメント）
* [ 配信品質の監視 ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitoring-deliverability){target="_blank"} （Campaign v8 ドキュメント）
* [配信のトラブルシューティング](delivery-troubleshooting.md)
* [ データベースのパフォーマンス ](../../production/using/database-performances.md) （v7 ハイブリッド/オンプレミス）
