---
product: campaign
title: Campaign での配信品質の概要
description: 配信品質のベストプラクティスを説明します
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Deliverability
role: User
exl-id: f301b34c-244c-4279-b23f-8224ea8eedbe
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: ht
source-wordcount: '736'
ht-degree: 100%

---

# 配信品質とは{#about-deliverability}

配信品質は、バウンスしたりスパムと見なされることなく受信者のインボックスに到達するキャンペーンの成否を測定する手法です。[配信品質が重要な理由について説明します](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/deliverability-strategy-and-definition.html?lang=ja#why-deliverability-matters)。

より正確には、電子メールの配信品質とは、個人のメールアドレスを介して、メッセージが短時間で、コンテンツや形式の面で期待される品質で宛先に届くかどうかを決定する一連の特性を意味します。

配信品質とは何か、配信品質の主要な用語、概念およびアプローチの詳細については、[アドビの配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja)を参照してください

## 配信品質を向上させる方法 {#deliverability-key-points}

配信品質の問題は、通常、インターネットサービスプロバイダーおよびメールサーバー管理者が実行するスパム対策の指標に関係しています。

* 成功する E メールマーケティングキャンペーンを設計する方法に関する一般的な推奨事項については、[配信品質の戦略と定義](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/deliverability-strategy-and-definition.html?lang=ja)を参照してください。

* Adobe Campaign の E メールの配信品質を最適化する方法に関する具体的な推奨事項については、この節に示すベストプラクティスに従うことをお勧めします。

>[!NOTE]
>
>ISP は顧客をスパム業者から保護するために、新しい高度なフィルタリング技術を継続的に開発する必要があるので、E メールの配信品質は常に変化する基準とルールを特徴としています。必ず、[アドビの配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html?lang=ja)を参照してください。これは定期的に更新されます。

### 配信品質率

配信品質率は、受信者のインボックスに届いたメッセージの数と配信されたメッセージの数との比率です。この比率を高めることにより、配信品質を向上させることができます。

Adobe Campaign では、配信品質は多くの要因に左右されます。特に次のような要因があげられます。

* インスタンスの正しい設定：詳しくはアドビ担当者にお問い合わせください。
* 適切なネットワーク構成：[この節](optimize-delivery.md#network-config)と[ドメインの設定と戦略](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html?lang=ja#transition-process)を参照してください。
* IP アドレスの評価：[IP 戦略](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html?lang=ja#ip-strategy)を参照してください。
* アドレスの品質の目標：[強制隔離管理](optimize-delivery.md#quarantine-management)を参照してください。
* 低い[苦情](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/metrics-for-deliverability/complaints.html?lang=ja)率と[ハードバウンス](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/metrics-for-deliverability/bounces.html?lang=ja#hard-bounces)率。
* メッセージコンテンツ：[メールコンテンツの制御](control-message-content.md)を参照してください。
* メッセージ認証（SPF、DKIM、DMARC）：[この節](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html?lang=ja#authentication)を参照してください。
* 送信者の評判：主要 ISP が送信者の評判を評価する方法については、[この節](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/internet-service-provider-specifics/overview.html?lang=ja)を参照してください。

## Campaign の配信品質ツール {#deliverability-tools}

<!--Adobe Campaign provides a number of tools designed to ensure optimal deliverability.-->
Adobe Campaign には、プラットフォームの配信品質パフォーマンスを追跡し改善するためのツールがいくつか用意されています。 また、Campaign を使用する際に配信品質を最適化するために考慮すべき主な原則についても説明します。

### メッセージの慎重な作成

メッセージを設定、デザイン、テストする場合は、次の節に示すベストプラクティスに従うようにしてください。 Adobe Campaign で提供されるすべての機能を活用すると、配信品質の向上に役立ちます。

* [配信のベストプラクティス](delivery-best-practices.md)
* [メールコンテンツの制御](control-message-content.md)
* [受信ボックスのレンダリング](inbox-rendering.md)
* [配達確認の送信](steps-validating-the-delivery.md#sending-a-proof)

### ダブルオプトインによる同意確認 {#double-opt-in}

無効なアドレスへのメッセージ送信を回避し、不適切な通信を制限し、送信者の評判を向上させるには、ダブルオプトインのメカニズムの実装をお勧めします。この方法を使用すると、購読が受信者の意図によるものであることを確認できます。

詳しくは、[ダブルオプトインを備えた購読フォームの作成](../../web/using/use-cases--web-forms.md#create-a-subscription--form-with-double-opt-in)を参照してください。

顧客からデータを収集する際のベストプラクティスについて詳しくは、[アドビの配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/first-impressions/address-collection-and-list-growth.html?lang=ja#data-quality-and-hygiene)を参照してください。

### 強制隔離管理の活用

Adobe Campaign は、絶えず発生するスパムの苦情、ハードバウンス、ソフトバウンスを収集したリストを管理します。

配信品質を保護するため、アドレスがこのリストにある受信者は、デフォルトでは今後のすべての配信から除外されます。これらの連絡先に送信すると、送信の評判が低下する可能性があるからです。

一部のインターネットアクセスプロバイダーは、無効なアドレスの割合が高すぎる場合、E メールを自動的にスパムと見なします。したがって、強制隔離を使用すると、これらのプロバイダーによってブロックリストに追加されるのを回避できます。

詳しくは、以下の節を参照してください。

* [配信の失敗について](understanding-delivery-failures.md)
* [強制隔離管理について](understanding-quarantine-management.md)
* [強制隔離とブロックリストの比較](understanding-quarantine-management.md#quarantine-vs-denylist)

### 監視ツールとレポートツールの使用

Adobe Campaign が提供する機能を使用して、配信品質を監視します。

Adobe Campaign では、一連のビルトインのリアルタイムインジケーターとレポートを使用して配信のパフォーマンスを確認し、配信に関するインサイトを強化できます。

詳しくは、以下の節を参照してください。

* [配信品質の監視](monitoring-deliverability.md)
* [配信監視の基本を学ぶ](about-delivery-monitoring.md)
* [Campaign ビルトインレポートの概要](../../reporting/using/about-campaign-built-in-reports.md)
