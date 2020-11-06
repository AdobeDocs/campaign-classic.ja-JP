---
title: アップグレードの基本を学ぶ
description: Campaign Classic アップグレードの詳細
page-status-flag: never-activated
uuid: 269d590c-5a6d-40b9-a879-02f5033863fc
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: rns
content-type: reference
topic-tags: latest-release-notes
discoiquuid: 5df34f55-135a-4ea8-afc2-f9427ce5ae7b
translation-type: ht
source-git-commit: 877ca2275c9338377da9e435e070c9911314fe51
workflow-type: ht
source-wordcount: '428'
ht-degree: 100%

---


# アップグレードの基本を学ぶ{#rn-overview}

Adobe Campaign は定期的に更新されています。年間平均で 2～3 個のマイナーバージョンがリリースされ、新機能、改善点および修正点が追加されています。さらに、累積的な修正のみを含むビルドを定期的にリリースしています。

この定期的なアップデートは、環境の安全性を維持し、アドビの製品に対する体験を向上させ、最新かつ最大限の情報を手に入れることを目的としています。

これが、最新バージョンの Adobe Campaign を実行することが非常に重要であると考える理由です。また、最近のビルドでの問題の特定、再現、修正が通常よりも速いという点で、より優れたサポート体験を得ることができます。また、発生する可能性のある多くの問題は、最新のビルドで既に修正されています。

## リリースのステータス{#rn-statuses}

ステータスは各ビルドに関連付けられています。ステータスのリストと、その解釈について以下に示します。

![](assets/do-not-localize/green3.png) **一般提供**（GA） - 実稼働環境で検証済みで、Adobe が推奨します。

**最新の GA ビルド**&#x200B;は、Gold Standard 10 です。[ここ](../../rn/using/gold-standard.md#gs-10)をクリックしてください。

![](assets/do-not-localize/limited3.png) **限定提供**（LA） - オンデマンドデプロイメントのみ。

![](assets/do-not-localize/blue3.png) **リリース候補**（RC） - 新機能を備えた最新バージョン。

**最新の RC ビルド**&#x200B;は Campaign Classic 20.3 です。[ここ](../../rn/using/latest-release.md)をクリックしてください。

![](assets/do-not-localize/orange3.png) **現在使用不可** - 新しいビルドに更新する必要があります。

![](assets/do-not-localize/red3.png) **非推奨（廃止予定）** - 新しいビルドへの更新が必須です。

## 推奨事項{#recommendations}

安定した構成を確保するために、同じクライアント構成で実行しているすべてのサーバーに同じ安定したビルドをインストールすることをお勧めします。

実装を最新の状態に維持するには、各新リリースで、[廃止および削除された機能](../../rn/using/deprecated-features.md)および、[互換性マトリックス](../../rn/using/compatibility-matrix.md)のページを必ずお読みください。

## アップグレードのプロセス{#process-upgrade}

ホスト型顧客（マネージドサービスまたはハイブリッド）は、環境をアップグレードするには、カスタマーケアに連絡する必要があります。

オンプレミスユーザーは、アップグレードを実行できます。これをおこなうには、[最新の安定したビルドをダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)して、すべての環境をアップグレードする必要があります。[アップグレードプロセス](../../production/using/build-upgrade.md)の詳細については、[ビルドアップグレードの FAQ](../../platform/using/faq-build-upgrade.md) を参照してください。

### Gold Standard{#upgrade-for-gold-standard-users}

Gold Standard のユーザーは、[最新の GA ビルド](../../rn/using/gold-standard.md#gs-10)を使用することで、自動的に Gold Standard のアップグレードのメリットが得られるため、操作は必要ありません。[詳細情報](https://helpx.adobe.com/jp/campaign/kb/gold-standard.html)。

>[!NOTE]
>Gold Standard の互換性マトリックスは、[GA 互換性マトリックス](../../rn/using/compatibility-matrix-gs.md)に記載されています。

## サポートおよびその他の役に立つリンク{#support}

* [ヘルプとサポート](https://helpx.adobe.com/jp/campaign/kb/ac-support.html#acc-support)
* [コントロールパネルのリリース](https://docs.adobe.com/content/help/ja-JP/control-panel/using/release-notes.html)
* [最新のドキュメントのアップデート](../../rn/using/documentation-updates.md)
* [非推奨（廃止予定）および削除された機能](../../rn/using/deprecated-features.md)

新しい Experience Cloud ソリューションリリースについての情報を得るには、[Adobe Priority Product Update](https://www.adobe.com/jp/subscription/priority-product-update.html) に登録してください。
