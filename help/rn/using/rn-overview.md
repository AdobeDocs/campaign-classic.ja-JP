---
title: アップグレードの基本を学ぶ
description: アップグレードの基本を学ぶ
page-status-flag: never-activated
uuid: 269d590c-5a6d-40b9-a879-02f5033863fc
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: rns
content-type: reference
topic-tags: latest-release-notes
discoiquuid: 5df34f55-135a-4ea8-afc2-f9427ce5ae7b
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 100%

---


# アップグレードの基本を学ぶ{#rn-overview}

Adobe Campaign は定期的に更新されています。年間平均で 2～3 個のマイナーバージョンがリリースされ、新機能、改善点および修正点が追加されています。さらに、累積的な修正のみを含むビルドを定期的にリリースしています。

この定期的なアップデートは、環境の安全性を維持し、アドビの製品に対する体験を向上させ、最新かつ最大限の情報を手に入れることを目的としています。

これが、最新バージョンの Adobe Campaign を実行することが非常に重要であると考える理由です。また、最近のビルドでの問題の特定、再現、修正が通常よりも速いという点で、より優れたサポート体験を得ることができます。また、発生する可能性のある多くの問題は、最新のビルドで既に修正されています。

## リリースのステータス{#rn-statuses}

Campaign Classic 19.2 以降では、ステータスが各ビルドに関連付けられます。ステータスのリストと、その解釈について以下に示します。

![](assets/do-not-localize/green3.png)**General Availability（一般的な可用性）** - 利用可能な最新の安定したビルドです。ビルドは本番環境で検証済みです。

**最後の安定したビルド**&#x200B;は、Gold Standard 10 です。[ここ](../../rn/using/gold-standard.md#gs-10)をクリックしてください

![](assets/do-not-localize/limited3.png) **Limited Availability（制限された可用性）** - 本番環境で現在検証中のビルドです。オンデマンドでのデプロイメントのみ可能です。

![](assets/do-not-localize/blue3.png) **Release Candidate（リリース候補）** - アドビによって検証されたビルドです。本番環境での検証待ちです。

![](assets/do-not-localize/orange3.png) **No longer available（利用できなくなりました）** - バグが修正された新しいビルドを利用できます。更新が必要です。

![](assets/do-not-localize/red3.png) **Deprecated（非推奨）** - 既知の不具合を含みます。更新は必須です。

## アップグレードのプロセス{#process-upgrade}

ホスト型顧客（マネージドサービスまたはハイブリッド）は、環境をアップグレードするには、サポートに連絡する必要があります。

Gold Standard のユーザーは、安定した最新バージョンを使用することで、自動的に Gold Standard のアップグレードのメリットが得られるため、操作は必要ありません。[詳細情報](https://helpx.adobe.com/jp/campaign/kb/gold-standard.html#gs-10)

オンプレミスユーザーは、アップグレードを実行できます。これをおこなうには、[最新の安定したビルドをダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)して、すべての環境をアップグレードする必要があります。[アップグレードプロセス](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html)の詳細については、[ビルドアップグレードの FAQ](https://helpx.adobe.com/jp/campaign/kb/build-upgrade-faq.html) を参照してください。

## 推奨事項{#recommendations}

安定した構成を確保するために、同じクライアント構成で実行しているすべてのサーバーに同じ安定したビルドをインストールすることをお勧めします。

実装を最新の状態に維持するには、各新リリースで、[廃止および削除された機能](../../rn/using/deprecated-features.md)および、[互換性マトリックス](../../rn/using/compatibility-matrix.md)のページを必ずお読みください。

新しい Experience Cloud ソリューションリリースについての情報を得るには、[Adobe Priority Product Update](https://www.adobe.com/jp/subscription/priority-product-update.html) に登録します。

その他の[推奨事項](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html#Recommendations)の詳細を確認します。

## サポートおよびその他の役に立つリンク{#support}

* [ヘルプとサポート](https://helpx.adobe.com/jp/campaign/kb/ac-support.html#acc-support)
* [コントロールパネルのリリース](https://docs.adobe.com/content/help/ja-JP/control-panel/using/release-notes.html)
* [ドキュメントの更新](../../rn/using/documentation-updates.md)
* [以前のリリース](../../rn/using/release--20-1.md)
* [非推奨（廃止予定）の機能 ](../../rn/using/deprecated-features.md)
* [互換性マトリックス](../../rn/using/compatibility-matrix.md)

