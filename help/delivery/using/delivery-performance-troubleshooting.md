---
product: campaign
title: 配信のパフォーマンスとトラブルシューティング
description: Campaign Classic v7 で配信パフォーマンスを最適化し、問題をトラブルシューティングする方法について説明します
feature: Monitoring, Deliverability, Troubleshooting
role: User, Developer
exl-id: cc793d7b-0a26-4a75-97ed-d79c87d9b3b8
source-git-commit: 2ebae2b84741bf26dd44c872702dbf3b0ebfc453
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 5%

---

# 配信のパフォーマンスとトラブルシューティング {#delivery-performance-troubleshooting}

>[!NOTE]
>
>配信のパフォーマンスとベストプラクティスに関する包括的なガイダンスについては、[Campaign v8 配信のベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices) ページを参照してください。 このコンテンツは、Campaign Classic v7 ユーザーと Campaign v8 ユーザーの両方に適用されます。
>
>このページは、ハイブリッドデプロイメントとオンプレミスデプロイメントのパフォーマンスの最適化とトラブルシューティングのための **0&rbrace;Campaign Classic v7 固有の設定 &rbrace; をドキュメント化します。**

配信パフォーマンス、プラットフォームの最適化、強制隔離管理、データベースのメンテナンス、スケジュールに関する包括的なベストプラクティスについては、[Campaign v8 配信のベストプラクティスドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} を参照してください。

## パフォーマンスの最適化 {#performance-optimization}

**Campaign Classic v7 ハイブリッド/オンプレミスデプロイメント** の場合は、次のデータベースとインフラストラクチャの最適化により、配信パフォーマンスを向上させることができます。

### データベースの最適化

**インデックスアドレス**：アプリケーションで使用される SQL クエリのパフォーマンスを最適化します。 インデックスは、データスキーマのメイン要素から宣言できます。 この最適化には、オンプレミスデプロイメントで使用できる直接データベースアクセスとスキーマのカスタマイズが必要です。

### インフラストラクチャの調整

**大規模な配信設定**:100 万人を超える受信者への配信には、送信キューの容量が必要です。 オンプレミスインストールの場合、MTA の子は、カスタムバッチサイズを処理するように設定できます。 これらの設定をインフラストラクチャの処理能力に応じて調整する場合は、システム管理者にお問い合わせください。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、インフラストラクチャの最適化と MTA 設定は、Adobeで管理されます。 デプロイメントに適用できるパフォーマンスの推奨事項については、[Campaign v8 配信のベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} を参照してください。

### データベースのメンテナンス {#database-maintenance}

**Campaign Classic v7 ハイブリッド/オンプレミスデプロイメント** の場合、プラットフォームとデータベースのメンテナンスは、配信の送信パフォーマンスに直接影響します。

定期的なメンテナンスタスクには、次のものが含まれます。

**データベースクリーンアップ**：データベースクリーンアップワークフローを使用して、古い配信ログ、トラッキングデータおよび一時テーブルを削除します。 データベースのメンテナンスが不十分だと、配信の準備と送信が遅くなる可能性があります。

**データベースパフォーマンスの監視**：クエリのパフォーマンス、インデックスの断片化およびテーブル統計を監視します。 詳しいガイダンスについては、[&#x200B; このページ &#x200B;](../../production/using/database-performances.md) を参照してください。

**テクニカルワークフロー監視**：すべてのテクニカルワークフロー（特に、クリーンアップ、トラッキング、配信品質の更新のワークフロー）がエラーなく正しく実行されていることを確認します。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、データベースのメンテナンスとテクニカルワークフローは、Adobeによって監視および管理されます。 [Campaign v8 配信の監視ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitoring-deliverability){target="_blank"} で説明されているように、配信固有の監視に焦点を当てます。

## 配信の問題のトラブルシューティング {#troubleshooting}

>[!NOTE]
>
>配信のトラブルシューティングに関する包括的なガイダンスは、Campaign v8 ドキュメントに記載されており、Campaign Classic v7 と Campaign v8 の両方のユーザーに適用できます。
>
>* 一般的な配信エラーとソリューション：[&#x200B; 配信エラーについて &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"}
>* 配信遅延の診断：[Campaign UI での配信の監視 &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"}
>* 配信のベストプラクティス：[&#x200B; 配信のベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"}
>
>この節では、ハイブリッドデプロイメントとオンプレミスデプロイメントの **Campaign Classic v7 固有のトラブルシューティング** について説明します。

**Campaign Classic v7 ハイブリッド/オンプレミスデプロイメント** の場合、次のトラブルシューティング手順は、管理するインフラストラクチャに固有です。

### MX ルールの設定

特定の ISP でスロットルの問題が発生した場合は、MX ルールの設定を確認して調整する必要がある場合があります。 MX ルールと割り当て量の詳細については、[&#x200B; この節 &#x200B;](../../installation/using/email-deliverability.md#about-mx-rules) を参照してください。

### 配信パフォーマンスのためのデータベースメンテナンス

ミッドソーシングデプロイメントで次のエラーが発生した場合：

```
Error during the call of method 'AppendDeliveryPart' on the mid sourcing server: 'Communication error with the server: please check this one is correctly configured. Code HTTP 408 'Service temporarily unavailable'.
```

この原因は、マーケティングインスタンスがデータをミッドソーシングサーバーに送信する前にデータの作成に多くの時間を費やす、パフォーマンスの問題に関係しています。

**オンプレミスインストールの場合**、バキュームを実行し、データベースで再インデックス化します。 データベースのメンテナンスについて詳しくは、[この節](../../production/using/recommendations.md)を参照してください。

スケジュールされているアクティビティのすべてのワークフロー、および失敗ステータスのすべてのワークフローも再開する必要があります。[この節](../../workflow/using/scheduler.md)を参照してください。

### テクニカルワークフローの監視

オンプレミスインストールの場合は、配信品質に関連するすべてのテクニカルワークフローがエラーなく実行されていることを確認します。

**配信品質の更新ワークフロー**：バウンスメールの選定ルールと配信品質指標を更新します。

**トラッキングワークフロー**：送信済み配信のトラッキングデータを処理します。

**データベースクリーンアップワークフロー**：パフォーマンスを維持するために、古い配信ログと一時テーブルを定期的にパージします。

**[!UICONTROL 管理]**/**[!UICONTROL プロダクション]**/**[!UICONTROL テクニカルワークフロー]** でワークフローステータスを確認します。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、テクニカルワークフローとインフラストラクチャの監視はAdobeで管理されます。 [Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} を参照して、配信コンテンツとターゲティングに焦点を当てます。

## 関連トピック

* [&#x200B; 配信エラーについて &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} （Campaign v8 ドキュメント）
* [&#x200B; 配信のベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} （Campaign v8 ドキュメント）
* [Campaign UI での配信の監視 &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"} （Campaign v8 ドキュメント）
* [&#x200B; データベースメンテナンス &#x200B;](../../production/using/recommendations.md) （v7 ハイブリッド/オンプレミス）
* [&#x200B; メール配信品質 &#x200B;](../../installation/using/email-deliverability.md) （v7 ハイブリッド/オンプレミス）
* [&#x200B; データベースのパフォーマンス &#x200B;](../../production/using/database-performances.md) （v7 ハイブリッド/オンプレミス）

