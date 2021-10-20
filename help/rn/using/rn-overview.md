---
product: campaign
title: アップグレードの基本を学ぶ
description: Campaign Classic アップグレードの詳細
feature: Overview
role: User
level: Beginner
exl-id: 7a05fdff-8f9d-4e8d-812e-0f1509db5499
source-git-commit: b3a3ec871bca9132f10b319ba1f93aeda80d6747
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 100%

---

# アップグレードの基本を学ぶ{#rn-overview}

![](../../assets/v7-only.svg)

Adobe Campaign は定期的に更新されています。年間平均で 2～3 個のマイナーバージョンがリリースされ、新機能、改善点および修正点が追加されています。さらに、累積的な修正のみを含むビルドを定期的にリリースしています。

この定期的なアップデートは、環境の安全性を維持し、アドビの製品に対する体験を向上させ、最新かつ最大限の情報を手に入れることを目的としています。

これが、最新バージョンの Adobe Campaign を実行することが非常に重要であると考える理由です。また、最近のビルドでの問題の特定、再現、修正が通常よりも速いという点で、より優れたサポート体験を得ることができます。また、発生する可能性のある多くの問題は、最新のビルドで既に修正されています。

## リリースのステータス{#rn-statuses}

ステータスは各ビルドに関連付けられています。ステータスのリストと、その解釈について以下に示します。

![](assets/do-not-localize/green3.png) **一般提供**（GA） - 実稼働環境で検証済みで、Adobe が推奨します。

**最新の GA ビルド**&#x200B;は、[[!DNL Gold Standard] 11 リリース](../../rn/using/gold-standard.md#gs-11)および [Campaign 21.1.4 リリース](../../rn/using/latest-release.md#release-21-1-4-build-9340)です。

![](assets/do-not-localize/limited3.png) **限定提供**（LA） - オンデマンドデプロイメントのみ。

![](assets/do-not-localize/blue3.png) **リリース候補**（RC） - 新機能を備えた最新バージョン。

![](assets/do-not-localize/orange3.png) **使用できなくなりました** - デプロイメントなし。バグ修正はありません。 新しいビルドへの更新をお勧めします。

![](assets/do-not-localize/red3.png) **非推奨** - デプロイメントなし。バグ修正はありません。 既存の実装はアップグレードする必要があります。

## 推奨事項{#recommendations}

安定した設定を確保するために、同じクライアント設定で実行しているすべてのサーバーに同じ安定したビルドをインストールすることをお勧めします。

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

* [ヘルプとサポート](../../support.md)
* [Campaign コントロールパネルのリリース](https://experienceleague.adobe.com/docs/control-panel/using/release-notes.html?lang=ja)
* [最新のドキュメントのアップデート](../../rn/using/documentation-updates.md)
* [非推奨および削除された機能](../../rn/using/deprecated-features.md)

新しい Experience Cloud ソリューションリリースについての情報を得るには、[Adobe Priority Product Update](https://www.adobe.com/jp/subscription/priority-product-update.html) を購読してください。
