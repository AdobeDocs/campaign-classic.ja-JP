---
product: campaign
title: プロファイルとオーディエンスに関する FAQ
description: Campaign Classic に関する FAQ
feature: Audiences, Troubleshooting
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: ba8bf610-cbac-41e9-8b6e-130deb8b97e2
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 100%

---

# プロファイルとオーディエンスに関する FAQ {#audiences-faq}



Adobe Campaign 内でターゲット母集団を定義しオーディエンスを管理する方法について説明します。

## 受信者を作成するにはどうすればよいですか？ {#how-to-create-recipients-}

受信者はインポートするか、Campaign クライアントコンソールを使用して手動で作成することができます。Campaign でプロファイルを作成および管理する方法については、[この節](../../platform/using/about-profiles.md)を参照してください。

## プロファイルをインポートするにはどうすればよいですか？ {#how-to-import-profiles-}

データベースへの[プロファイルのインポート](../../platform/using/import-operations-samples.md)をおこなう簡単な使用例を紹介しています。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/profile-management/importing-profiles.html?lang=ja)

## マーケティングキャンペーンのターゲット母集団を定義するにはどうすればよいですか？ {#how-can-i-define-the-target-population-of-a-marketing-campaign-}

マーケティングキャンペーンの[ターゲット母集団を作成するワークフローを使用](../../campaign/using/marketing-campaign-deliveries.md#building-the-main-target-in-a-workflow)することができます。


## プロファイルのリストを作成するにはどうすればよいですか？ {#how-can-i-create-a-list-of-profiles-}

リストとは、配信アクションのターゲットにしたり、インポート操作時またはワークフロー実行時に更新したりできる受信者の静的なセットです。例えば、クエリによってデータベースから抽出した母集団からリストを作成できます。

[詳しくはここをクリック](../../platform/using/creating-and-managing-lists.md#creating-a-profile-list-from-a-group)してください。

![](assets/do-not-localize/how-to-video.png) [このビデオ](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/profile-management/creating-a-list-of-recipients-with-a-workflow.html?lang=ja)と[このビデオ](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/profile-management/creating-a-list-of-recipients.html?lang=ja)でこの機能を確認する

## メッセージを送信する前に母集団の重複を排除するにはどうすればよいですか？  {#how-can-i-deduplicate-a-population-before-sending-a-message-}

ワークフローを使用して配信のターゲットから重複するものを除外し、受信者に同じメッセージが複数回送信されないようにすることができます。

例について[詳しくはここをクリック](../../workflow/using/deduplication.md#example--identify-the-duplicates-before-a-delivery)してください。

## ニュースレターの購読者を識別してターゲットにするにはどうすればよいですか？ {#how-to-identify-and-target-subscribers-to-a-newsletter-}

Campaign での購読管理と、[購読者にメッセージを送信する](../../delivery/using/managing-subscriptions.md)方法について説明します。

## ターゲット母集団からプロファイルを除外するためのベストプラクティスは何ですか？  {#what-is-the-best-practice-to-exclude-profiles-from-a-target-population-}

ターゲット母集団からプロファイルのリストを除外する方法については、[このページ](../../workflow/using/read-list.md)を参照してください。
