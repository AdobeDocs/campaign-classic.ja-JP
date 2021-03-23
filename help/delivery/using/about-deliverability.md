---
solution: Campaign Classic
product: campaign
title: Campaign の配信品質について
description: 配信品質のベストプラクティスを説明します
audience: delivery
content-type: reference
topic-tags: deliverability-management
translation-type: tm+mt
source-git-commit: 0420de856d1506ab92d8f0e0824bf439e0ac7dc7
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 11%

---


# 配信品質とは{#about-deliverability}

配信品質を使用すると、バウンスを発生させたりスパムとしてマークされたりすることなく、受信者の受信トレイに届いたキャンペーンの成功を測定できます。 [配信品質が重要な理由を学ぶ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/deliverability-strategy-and-definition.html#why-deliverability-matters)。

より正確に言うと、電子メールの配信品質とは、メッセージが宛先に到達する能力を、個人の電子メールアドレスを介して、短時間で、コンテンツや形式に関して期待される品質を持つ特性の集まりを指します。

配信品質の概要と、主な配信品質の用語、概念、アプローチの詳細については、『[Adobe配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html)』を参照してください。

## 配信品質の向上方法{#deliverability-key-points}

配信品質の問題は、通常、インターネットサービスプロバイダーやメールサーバ管理者が実装したスパムに対する保護の対策に関連しています。

* 成功する電子メールマーケティングキャンペーンを設計する方法に関する一般的な推奨事項については、[配信品質の戦略と定義](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/deliverability-strategy-and-definition.html)を参照してください。

* Adobe Campaignの電子メールの配信品質を最適化する方法について、より具体的な推奨事項を示すために、Adobeは、この節に示すベストプラクティスを使用することをお勧めします。

>[!NOTE]
>
>ISPは、顧客をスパム業者から保護するために、新しい高度なフィルタリング技術を継続的に開発する必要があるので、電子メールの配信品質は、常に変化する基準とルールに特徴付けられています。 定期的に更新される『[Adobe配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/introduction.html)』を参照してください。

### 配信品質率

配信品質率は、受信者の受信トレイに届いたメッセージの数を、配信されたメッセージの数と比較した値です。 配信品質を向上させるために、この率を上げる作業を行う場合があります。

Adobe Campaignにより、配信品質は、特に多くの要因に左右されます。

* インスタンスの正しい設定：Adobeの担当者にお問い合わせください。
* 正当なネットワーク構成：[このセクション](../../delivery/using/optimize-delivery.md#network-config)と[ドメインの設定と方法](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html#domain-setup-and-strategy)を参照してください。
* IPアドレスの評価：[IP戦略](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html#ip-strategy)を参照してください。
* 対象となるアドレスの質：「[強制隔離管理](../../delivery/using/optimize-delivery.md#quarantine-management)」を参照してください。
* [苦情](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/metrics-for-deliverability/complaints.html)と[ハードバウンス](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/metrics-for-deliverability/bounces.html#hard-bounces)率が低い。
* メッセージの内容：[電子メールコンテンツの制御](../../delivery/using/control-message-content.md)を参照してください。
* メッセージ認証(SPF、DKIM、DMARC):[このセクション](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html#authentication)を参照してください。
* 送信者の評価：主なISPが送り手の評判を評価する方法については、[このセクション](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/internet-service-provider-specifics/overview.html)を参照してください。

## キャンペーン配信品質ツール{#deliverability-tools}

<!--Adobe Campaign provides a number of tools designed to ensure optimal deliverability.-->
Adobe Campaignには、プラットフォームの配信パフォーマンスを追跡し、改善するためのツールがいくつか用意されています。 また、キャンペーンを使用する際の配信品質を最適化するために考慮すべき主な原則についても説明します。

### 注意深くメッセージを作成する

メッセージを設定、デザイン、テストする場合は、次の節に示すベストプラクティスに従っていることを確認してください。 Adobe Campaignが提供するすべての機能を活用すると、配信品質を向上できます。

* [配信のベストプラクティス](../../delivery/using/delivery-best-practices.md)
* [E メールコンテンツの制御](../../delivery/using/control-message-content.md)
* [受信ボックスレンダリング](../../delivery/using/inbox-rendering.md)
* [配達確認の送信](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof)

### 重複のオプトイン{#double-opt-in}を通じて同意を確認

Adobeでは、無効なアドレスへのメッセージの送信を避け、不適切な通信を制限し、送信者の評判を向上させるために、重複オプトインメカニズムの実装をお勧めします。 この方法を使用すると、受信者が意図的に購読していることを確認できます。

詳しくは、[二重のオプトインを備えた購読フォームの作成](../../web/using/use-cases--web-forms.md#create-a-subscription--form-with-double-opt-in)を参照してください。

お客様からデータを収集する際のベストプラクティスについて詳しくは、『[Adobe配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/first-impressions/address-collection-and-list-growth.html#data-quality-and-hygiene)』を参照してください。

### 強制隔離管理の活用

Adobe Campaignは、一貫して発生するスパムの苦情、ハードバウンス、ソフトバウンスを収集するリストを管理します。

配信品質を保護するため、そのリスト上の住所を持つ受信者は、デフォルトでは、これらの連絡先に送信すると送信の評判が悪くなる可能性があるので、将来のすべての配信から除外されます。

一部のインターネットアクセスプロバイダーは、無効なアドレスの割合が高すぎる場合、E メールを自動的にスパムとみなします。したがって、強制隔離を使用すると、これらのプロバイダーによってブロックリストに追加されるのを回避できます。

この点について詳しくは、以下の節を参照してください。

* [配信エラーの理解](../../delivery/using/understanding-delivery-failures.md)
* [強制隔離管理の理解](../../delivery/using/understanding-quarantine-management.md)
* [強制隔離対ブロックリスト](../../delivery/using/understanding-quarantine-management.md#quarantine-vs-denylist)

### 監視ツールとレポートツールの使用

Adobe Campaignが提供する機能を使用して、配信品質を監視します。

Adobe Campaignを使用すると、組み込みのリアルタイムインジケーターとレポートを使用して、配信のパフォーマンスを確認し、配信に関するインサイトを向上できます。

この点について詳しくは、以下の節を参照してください。

* [配信品質の監視](../../delivery/using/monitoring-deliverability.md)
* [配信の監視について](../../delivery/using/about-delivery-monitoring.md)
* [Campaign の組み込みレポートについて](../../reporting/using/about-campaign-built-in-reports.md)

<!--TO REMOVE
## Background {#background}

Email deliverability presents a major challenge to marketers - whether they're sending a few thousand messages or several billion. One in five messages never reach the inbox, or their intended recipient.

Once relegated as a "technical issue" for the IT department, email deliverability continues to move higher on the marketing agenda. That's because savvy marketers recognize that although many of its elements are technical in nature, deliverability is ultimately a business issue with significant revenue implications.

Consider the email marketing funnel. Deliverability determines the number of messages received, which in turn impacts each subsequent stage of the funnel. Fewer emails received results in fewer opens, fewer clicks, and fewer conversions. **For companies with a large database, the difference between average and great deliverability could literally mean hundreds of thousands to millions of dollars in revenues.**

![](assets/deliverability_overview_1.png)

By settling for average (80%) deliverability, marketers are leaving significant conversions - and dollars - on the table.

What exactly is email deliverability? And how can marketers improve deliverability rates to widen the mouth of the funnel and squeeze more results from their email campaigns?

Email deliverability refers to the set of characteristics that determine a message's ability to reach its destination, via a personal e-mail address, within a short time, and with the expected quality in terms of content and format. These characteristics fall into four main categories: data quality, message and content, sending infrastructure, and reputation. Together, they form the foundation of a successful email deliverability program. This overview outlines the four fundamentals of email deliverability success and offers best practices for reaching the inbox and driving greater revenues from email marketing programs.

![](assets/deliverability_overview_2.png)-->
