---
product: campaign
title: 配信の送信に関するトラブルシューティング
description: 配信の監視に関する問題のトラブルシューティング方法と配信パフォーマンスについて詳しく説明します。
feature: Monitoring, Deliverability, Troubleshooting
role: User
exl-id: 37b1d7fb-7ceb-4647-9aac-c8a80495c5bf
source-git-commit: eac670cd4e7371ca386cee5f1735dc201bf5410a
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 16%

---

# 配信の送信に関するトラブルシューティング {#delivery-troubleshooting}

>[!NOTE]
>
>配信のトラブルシューティングに関する包括的なガイダンスは、Campaign v8 ドキュメントに記載されており、Campaign Classic v7 と Campaign v8 の両方のユーザーに適用できます。
>
>* 一般的な配信エラーとソリューション：[ 配信エラーについて ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"}
>* 配信遅延の診断：[Campaign UI での配信の監視 ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"}
>* 配信のベストプラクティス：[ 配信のベストプラクティス ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"}
>
>このページは、ハイブリッドデプロイメントとオンプレミスデプロイメントの **0}Campaign Classic v7 固有のトラブルシューティング } について説明します。**

## トラブルシューティング {#v7-specific}

**Campaign Classic v7 ハイブリッド/オンプレミスデプロイメント** の場合、管理するインフラストラクチャに固有の次のトラブルシューティング手順を実行します。

### MX ルールの設定

特定の ISP でスロットルの問題が発生した場合は、MX ルールの設定を確認して調整する必要がある場合があります。 MX ルールと割り当て量の詳細については、[ この節 ](../../installation/using/email-deliverability.md#about-mx-rules) を参照してください。

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
>Campaign v8 Managed Cloud Services ユーザーの場合、テクニカルワークフローとインフラストラクチャの監視はAdobeで管理されます。 [Campaign v8 ドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} を参照して、配信コンテンツとターゲティングに焦点を当てます。

## 関連トピック

* [ 配信エラーについて ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} （Campaign v8 ドキュメント）
* [ 配信のベストプラクティス ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} （Campaign v8 ドキュメント）
* [Campaign UI での配信の監視 ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"} （Campaign v8 ドキュメント）
* [ データベースメンテナンス ](../../production/using/recommendations.md) （v7 ハイブリッド/オンプレミス）
* [ メール配信品質 ](../../installation/using/email-deliverability.md) （v7 ハイブリッド/オンプレミス）
