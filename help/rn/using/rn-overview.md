---
product: campaign
title: アップグレードの基本を学ぶ
description: Campaign Classic アップグレードの詳細
feature: Overview
role: User
level: Beginner
exl-id: 7a05fdff-8f9d-4e8d-812e-0f1509db5499
source-git-commit: eb0e572f0bb6196a58a7dab4999df784d5c4851f
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 77%

---

# アップグレードの基本を学ぶ{#rn-overview}

![](../../assets/v7-only.svg)

Adobe Campaign は定期的に更新されています。毎年 1 つまたは 2 つのマイナーバージョンがリリースされ、新機能、改善点および修正点が追加されています。 さらに、累積的な修正のみを含むビルドを定期的にリリースしています。

この定期的なアップデートは、環境の安全性を維持し、アドビの製品に対する体験を向上させ、最新かつ最大限の情報を手に入れることを目的としています。

これが、お客様が重要であると考える理由です **最新バージョンを実行する** Adobe Campaign また、最近のビルドでの問題の特定、再現、修正が通常よりも速いという点で、より優れたサポート体験を得ることができます。また、発生する可能性のある多くの問題は、最新のビルドで既に修正されています。

## リリースのステータス{#rn-statuses}

新しいビルドごとに、色で具体化されたステータスが表示されます。

![](assets/do-not-localize/green3.png) **一般提供**（GA） - 実稼働環境で検証済みで、Adobe が推奨します。

![](assets/do-not-localize/limited3.png) **限定提供**（LA） - オンデマンドデプロイメントのみ。

![](assets/do-not-localize/blue3.png) **リリース候補**（RC） - 新機能を備えた最新バージョン。

![](assets/do-not-localize/orange3.png) **使用できなくなりました** - デプロイメントなし。バグ修正はありません。 新しいビルドへの更新をお勧めします。

![](assets/do-not-localize/red3.png) **非推奨** - デプロイメントなし。バグ修正はありません。 既存の実装はアップグレードする必要があります。

## 推奨事項{#recommendations}

安定した設定を確実におこなうには、 **同じ安定した建物** を同じクライアント構成で実行しているすべてのサーバ上に置く。

さらに、クライアントコンソールは、サーバーインスタンスと同じビルド上にある必要があります。

実装を最新の状態に維持するには、各新リリースで、[廃止および削除された機能](../../rn/using/deprecated-features.md)および、[互換性マトリックス](../../rn/using/compatibility-matrix.md)のページを必ずお読みください。

## アップグレードのプロセス{#process-upgrade}

ホスト型顧客（マネージドサービスまたはハイブリッド）は、環境をアップグレードするには、カスタマーケアに連絡する必要があります。

オンプレミスユーザーは、アップグレードを実行できます。これをおこなうには、[最新の安定したビルドをダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)して、すべての環境をアップグレードする必要があります。[アップグレードプロセス](../../production/using/build-upgrade.md)の詳細については、[ビルドアップグレードの FAQ](../../platform/using/faq-build-upgrade.md) を参照してください。

### [!DNL Gold Standard]{#upgrade-for-gold-standard-users}

ホストされている [!DNL Gold Standard] のユーザーは、自動的に [!DNL Gold Standard] のアップグレードのメリットが得られるため、アップグレードアクションを起こすことなく[最新の GA [!DNL Gold Standard]  ビルド](../../rn/using/gold-standard.md#gs-12)が利用できます。[詳細情報](../../rn/using/gs-overview.md)。

>[!NOTE]
>[!DNL Gold Standard] の互換性マトリックスは、[GA 互換性マトリックス](../../rn/using/compatibility-matrix-gs.md)に記載されています。

## サポートおよびその他の役立つリンク{#support}

* [Campaign のバージョンを確認する](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version).
* [ヘルプとサポート](../../support.md)
* [Campaign コントロールパネルのリリース](https://experienceleague.adobe.com/docs/control-panel/using/release-notes.html?lang=ja)
* [最新のドキュメントのアップデート](../../rn/using/documentation-updates.md)
* [非推奨および削除された機能](../../rn/using/deprecated-features.md)

新しい Experience Cloud ソリューションリリースについての情報を得るには、[Adobe Priority Product Update](https://www.adobe.com/jp/subscription/priority-product-update.html) を購読してください。
