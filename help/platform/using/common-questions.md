---
title: よくある質問
description: Adobe Campaign Classic FAQ
page-status-flag: never-activated
uuid: 3f719ac2-cc26-4fb0-adda-84666c8c38e1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
discoiquuid: 16dbe423-018f-4666-9901-2120a8dc609a
translation-type: tm+mt
source-git-commit: 99d766cb6234347ea2975f3c08a6ac0496619b41
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 100%

---


# よくある質問{#common-questions}

Campaign Classic の操作について疑問がある場合は、以下に示すよくある 10 件の質問や、該当するページにあるその他の一般的な質問を参照してください。また、次のこともできます。

* [チュートリアル動画を見る](https://docs.adobe.com/content/help/ja-JP/campaign-classic-learn/tutorials/overview.html)
* [セルフヘルプオプションを参照する](../../platform/using/tutorials.md#how-to-videos)
* [「はじめに」と「使用例」の節を読む](../../platform/using/tutorials.md#step-by-step-guides)
* 答えが見つからない場合は、[エキスパートに質問する](https://experienceleaguecommunities.adobe.com/t5/adobe-campaign-classic/ct-p/adobe-campaign-classic-community)
* サポートが必要な場合は、[Campaign のヘルプとサポートのオプションを参照する](https://helpx.adobe.com/jp/campaign/kb/ac-support.html#acc-support)

## 1. Campaign を最新版にアップグレードするにはどうすればよいですか？{#how-can-i-upgrade-campaign-to-the-latest-version-}

Adobe Campaign Classic は、お客様に最高のエクスペリエンスと価値を提供するために、様々なテクノロジーを活用しています。こうしたテクノロジーによる優れたセキュリティ、安定性、パフォーマンスを実現するには、Campaign Classic インスタンスを定期的にアップグレードして、常に最新版を使用する必要があります。

Adobe Managed Services を使用している場合は、Campaign Gold Standard のアップグレードサービスを利用できます。詳しくは、[この記事](https://helpx.adobe.com/jp/campaign/kb/gold-standard.html)を参照してください。

環境の更新方法について詳しくは、[この節](../../production/using/build-upgrade.md)を参照してください。また、このトピックに関する[よくある質問](../../platform/using/faq-build-upgrade.md)も参照してください。

## 2. データベースクリーンアップワークフローとは何ですか？{#what-is-the-database-cleanup-workflow-}

データベースクリーンアップワークフローは、データベースの急激な拡大を避けるために古いデータを削除します。ビルトインテクニカルワークフローは、ユーザーの操作なしで自動的にトリガーされます。このワークフローには、Campaign エクスプローラーの&#x200B;**[!UICONTROL 管理／プロダクション／テクニカルワークフロー]**&#x200B;ノードでアクセスできます。

データベースクリーンアップワークフローについて[詳しくは、ここをクリック](../../production/using/database-cleanup-workflow.md)してください。

## 3. どうすればセキュリティゾーンを設定できますか？{#how-can-i-configure-security-zones-}

セキュリティゾーンのセルフサービスインターフェイスを使用すると、Adobe Campaign Classic デプロイメントの VPN セキュリティゾーン設定にあるエントリを管理できます。Campaign のセキュリティゾーンについては、[この節](../../installation/using/configuring-campaign-server.md#defining-security-zones)を参照してください。

セキュリティゾーンセルフサービス UI について[詳しくはここをクリック](https://helpx.adobe.com/jp/campaign/kb/configuring-security-zones-self-service.html)してください。

## 4. 配信をエラーなく確実に送信するにはどうすればよいですか？{#how-can-i-make-sure-my-delivery-is-sent-without-errors-}

Adobe Campaign には、E メール配信を監視するための一連のダッシュボードおよびツールが用意されています。

メッセージが送信されていることの確認、実行の監視、エラーが発生した場合の対処の方法について[詳しくは、ここをクリック](../../delivery/using/monitoring-a-delivery.md)してください。

## 5. ワークフローの実行を監視できますか？{#can-i-monitor-workflow-execution}

Campaign ワークフローの実行を監視する方法については、[このページ](../../workflow/using/starting-a-workflow.md)を参照してください。

## 6. どうすれば Campaign Classic に接続できますか？{#how-can-i-connect-to-campaign-classic-}

Adobe Campaign Classic に接続するには、Adobe Campaign クライアントコンソールを起動して、インスタンスに対するログイン名とパスワードを入力する必要があります。

[詳しくはここをクリック](../../platform/using/launching-adobe-campaign.md)してください。

## 7. Campaign Classic と互換性のあるシステムやコンポーネントはどれですか？{#which-systems-and-components-campaign-classic-is-compatible-with-}

Campaign の最新ビルドでサポートされているすべてのシステムおよびコンポーネントのリストは、「[Adobe Campaign Classic 互換性マトリックス](../../rn/using/compatibility-matrix.md)」で入手できます。

## 8. Campaign Classic のリリースノートはどこにありますか？{#where-are-campaign-classic-release-notes-}

最新の Campaign Classic リリースノートは[このページ](../../rn/using/latest-release.md)で参照できます。

## 9. ドメインの設定はどのような手順でおこないますか？{#what-is-the-procedure-for-domain-delegation-}

サブドメインとは、ブランドや様々なタイプのトラフィック（トランザクションメッセージ、マーケティング情報など）を分離するために使用できるドメインの区分です。アドビは E メール配信用にドメインネームシステム（DNS）を考慮しています。これにより、クライアントがドメイン名と共に DNS エイリアスを使用することでブランドイメージを維持したり、E メール処理中の配信品質を最適化できるすべての技術的なベストプラクティスをアドビが自主的に実践したりできます。

[詳しくはここをクリック](https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html)してください。

