---
title: プロファイルとオーディエンスに関する FAQ
seo-title: よくある質問
description: Campaign Classic に関する FAQ
page-status-flag: never-activated
uuid: 3f719ac2-cc26-4fb0-adda-84666c8c38e1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
discoiquuid: 16dbe423-018f-4666-9901-2120a8dc609a
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 100%

---


# プロファイルとオーディエンスに関する FAQ {#audiences-faq}

Adobe Campaign の中でターゲット母集団を選択し、オーディエンスを管理する方法を学習します。

## 受信者の作成方法は？ {#how-to-create-recipients-}

受信者はインポートするか、Campaign クライアントコンソールを使用して手動で作成することができます。Campaign でプロファイルを作成および管理する方法については、[この節](../../platform/using/about-profiles.md)を参照してください。

## プロファイルのインポート方法は？ {#how-to-import-profiles-}

データベースへの[プロファイルのインポート](../../platform/using/importing-data.md#generic-import-samples)をおこなう簡単な使用例を紹介しています。[このビデオ](https://docs.adobe.com/content/help/ja-JP/campaign-classic-learn/tutorials/getting-started/importing-profiles.html)もご覧ください。

## マーケティングキャンペーンのターゲット母集団はどのようにして定義できますか？ {#how-can-i-define-the-target-population-of-a-marketing-campaign-}

マーケティングキャンペーンの[ターゲット母集団を作成するワークフローを使用](../../campaign/using/marketing-campaign-deliveries.md#building-the-main-target-in-a-workflow)することができます。キャンペーンでターゲティングワークフローを作成する方法については、[このビデオ](https://docs.adobe.com/content/help/ja-JP/campaign-classic-learn/tutorials/getting-started/creating-a-workflow.html)をご覧ください。

## プロファイルのリストはどうすれば作成できますか？ {#how-can-i-create-a-list-of-profiles-}

リストとは、配信アクションのターゲットにしたり、インポート操作時またはワークフロー実行時に更新したりできる受信者の静的なセットです。例えば、クエリによってデータベースから抽出した母集団からリストを作成できます。

[詳しくはここをクリック](../../platform/using/creating-and-managing-lists.md#creating-a-profile-list-from-a-group)してください。また、手動でリストを作成する方法については[このビデオ](https://docs.adobe.com/content/help/ja-JP/campaign-classic-learn/tutorials/getting-started/creating-a-list-of-recipients.html)を、ワークフローで受信者のリストを作成して自動更新する方法については[この別のビデオ](https://docs.adobe.com/content/help/ja-JP/campaign-classic-learn/tutorials/profile-management/creating-a-list-of-recipients.html)を参照してください。

## メッセージの送信前に母集団の重複を排除するにはどうすればよいですか？ {#how-can-i-deduplicate-a-population-before-sending-a-message-}

ワークフローを使用して配信のターゲットから重複するものを除外し、受信者に同じメッセージが複数回送信されないようにすることができます。

例について[詳しくはここをクリック](../../workflow/using/deduplication.md#example--identify-the-duplicates-before-a-delivery)してください。

## ニュースレターの購読者を識別してターゲットにする方法は？ {#how-to-identify-and-target-subscribers-to-a-newsletter-}

Campaign での購読管理について理解し、[購読者にメッセージを送信する](../../delivery/using/managing-subscriptions.md)方法を確認してください。

## ターゲット母集団からプロファイルを除外するためのベストプラクティスとは？ {#what-is-the-best-practice-to-exclude-profiles-from-a-target-population-}

ターゲット母集団からプロファイルのリストを除外する方法については、[このページ](../../workflow/using/read-list.md)を参照してください。
