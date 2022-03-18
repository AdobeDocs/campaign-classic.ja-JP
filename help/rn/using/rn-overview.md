---
product: campaign
title: アップグレードの概要
description: Campaign Classic アップグレードの詳細
feature: Overview
role: User
level: Beginner
exl-id: 7a05fdff-8f9d-4e8d-812e-0f1509db5499
source-git-commit: 29e56d6bf2817eeb863cbe33f99233a8241f2bf5
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 53%

---

# アップグレードの概要{#rn-overview}

![](../../assets/v7-only.svg)

## リリースのステータス{#rn-statuses}

新しいビルドごとに、色分けされたステータスが表示されます。

![](assets/do-not-localize/green3.png) **一般公開** (GA) — 最新の安定したビルドで、実稼働環境で検証済みで、Adobeが推奨します。

![](assets/do-not-localize/limited3.png) **限定提供**（LA） - オンデマンドデプロイメントのみ。

![](assets/do-not-localize/blue3.png) **リリース候補**（RC） - 新機能を備えた最新バージョン。

![](assets/do-not-localize/orange3.png) **使用できなくなりました** - デプロイメントなし。バグ修正はありません。 新しいビルドへの更新をお勧めします。

![](assets/do-not-localize/red3.png) **非推奨** - デプロイメントなし。バグ修正はありません。 既存の実装はアップグレードする必要があります。

## リリースサイクル{#rn-cycle}

Adobe Campaign は定期的にアップデートされています。この定期的なアップデートは、環境の安全性を維持し、アドビの製品に対する体験を向上させ、最新かつ最大限の情報を手に入れることを目的としています。

これが重要な理由です **最新の安定版を実行する** Adobe Campaign また、最近のビルドでの問題の特定、再現、修正が通常よりも速いので、より優れたサポート体験を得ることができます。 また、発生する可能性のある多くの問題は、最新のビルドで既に修正されています。

ホステッド環境のお客様はアクションを起こすことなく、最新の安定したバージョンのアップグレードのメリットが自動的に得られます。詳しくは、[年次アップグレードの節](#yearly-upgrade)を参照してください。古いビルドから移行する場合は、まずこのバージョンにアップグレードすることをお勧めします。

## 推奨事項{#recommendations}

安定した設定を確保するために、Adobeでは、 **同じビルド** を同じクライアント構成で実行しているすべてのサーバ上に置く。

また、リリースノートで特に明記されていない限り、クライアントコンソールはにある必要があります。 **同じビルド** をサーバーインスタンスとして使用します。

実装を最新の状態に維持するため、新しいリリースのたびに、[廃止および削除された機能](../../rn/using/deprecated-features.md)と[互換性マトリックス](../../rn/using/compatibility-matrix.md)のページを必ずお読みください。

## アップグレードのプロセス{#process-upgrade}

ホスト型顧客（マネージドサービスまたはハイブリッド）は、カスタマーケアチームに連絡して、環境をアップグレードしてもらいます。

オンプレミスユーザーは、アップグレードを実行できます。これをおこなうには、 [最新の安定したビルド (GA) のダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html) お使いの環境をすべてアップグレードしてください。 [アップグレードプロセス](../../production/using/build-upgrade.md)について詳しくは、[ビルドアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md) を参照してください。

## 年次アップグレード {#yearly-upgrade}

Adobeは、アドビのソフトウェアソリューションを通じて、お客様に最高の経験と価値を提供することに取り組んでいます。 組織は、お客様がアドビのソリューションがタスクの実行に使用する関連テクノロジーの最新バージョンにアクセスできるように取り組んでいます。

Adobe Campaign Classic には、お客様に価値を提供するために、様々なテクノロジーが使用されています。このテクノロジーの組み合わせにより、常にCampaign Classicインスタンスをアップグレードし、最新バージョンを使用して優れたセキュリティ、安定性、パフォーマンスを実現する必要があります。

ホスト型ユーザーは、最新の GA ビルドを使用することで、自動的にアップグレードのメリットが得られるため、操作は必要ありません。 詳しくは、以下の FAQ を参照してください。

### このアップグレードの実施が必要な理由

ホスト版のお客様で、Campaign Classicに関連する 1 つ以上のテクノロジーをアップグレードし、現在のビルドやバージョンを更新する必要があるとアカウントで判断された場合は、Adobeから直接通知されます。

古いバージョンを実行中のオンプレミスまたはハイブリッド環境のお客様は、最新の安定したビルド(GA）に移行することをお勧めします。

これにより、アカウントの脆弱性を確実に防ぎ、更新されたパフォーマンステクノロジーを使用できるようにします。 また、このアップグレードにより、アカウントを配置し、今後、手作業や介入の必要が少ない、より簡単で定期的なアップグレードを実現します。

### このアップグレードのプロセスとタイムライン

Adobeチームが、このジャーニーを通じて組織をリードし、ガイドします。

カスタマーケア担当、製品マネージャ、エンジニア、TechOps スペシャリスト、および製品コンサルタントのチームが、お客様の経験をスムーズに活用するための支援を行います。

### 利点

<tr>
  <td>
      <img alt="セキュリティ" src="assets/do-not-localize/security.png"/>
    <div>
    <strong>セキュリティの向上</strong>
    </div>
    <ul>
    <li>Adobe Campaign Classic に使用される複数のテクノロジーは相互に連携して優れた価値を提供します。</li>
    <li>セキュリティを確保するには、すべてのインスタンスをアップデートする必要があります。</li>
    <li>常時焦点を当て、プロアクティブな保全をおこなわなければセキュリティは確保できません。</li>
    <li>セキュリティ上のリスクは存在しており、無視することはできません。Campaign Classic をアップグレードするたびに、セキュリティが向上します。</li>
    </ul>
  </td>

<td>
      <img alt="サポート" src="assets/do-not-localize/support.png" />
    <div>
    <strong>サポートの向上</strong>
    </div>
    <ul>
    <li>重大な問題のほとんどは、実際にはアップグレードで解決し、回避することができます。</li>
    <li>定期的アップグレードの実行により、直面する課題が軽減、解消されて、効率が向上します。</li>
    <li>カスタマーケアの規模が縮小され、迅速な解決が可能になり、アップグレードに関連しない問題に対するより多くの注意を払うことができます。</li>
    </ul>
  </td>
</tr>

<tr>
  <td>
      <img alt="メンテナンス" src="assets/do-not-localize/maintenance.png"/>
    <div>
    <strong>メンテナンスと安定性の強化</strong>
    </div>
    <ul>
    <li>Adobe Campaign チームは、製品の安定性とパフォーマンスを向上させる方法を特定し、既知の問題も解決します。</li>
    <li>アップグレードによって、インスタンスにはこうした改善が適用され、最新の状態に保つことができます。また、Campaign Classic インスタンスが急速に増大および複雑化している組織において、一般的な課題を解決することができます。</li>
    <li>Campaign Classicを支えるテクノロジースタック全体の改善は、組織のマーケティングチームと IT チームの両方で感じられます。</li>
    </ul>
  </td>

<td>
      <img alt="ビルドのアップグレード" src="assets/do-not-localize/upgrades.png" />
    <div>
    <strong>アップグレードが容易</strong>
    </a>
    </div>
    <ul>
    <li>Campaign Classicインスタンスのアップグレードの労力と複雑さは、2 つのバージョン (v5 —&gt; v7) の間の距離に伴って増加します。</li>
    <li>アップグレードを先送りにすればするほど、作業がより複雑になり、さらに多くの脆弱性にさらされます。</li>
    <li>定期的な更新により、アップグレードのダウンタイムが短縮され、回帰のリスクが軽減されます。</li>
    </ul>
  </td>
</tr>
</table>

## その他のリソース{#support}

* [Campaign のバージョンの確認](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)
* [ヘルプとサポート](../../support.md)
* [Campaign コントロールパネルのリリース](https://experienceleague.adobe.com/docs/control-panel/using/release-notes.html?lang=ja)
* [最新のドキュメントのアップデート](../../rn/using/documentation-updates.md)
* [非推奨および削除された機能](../../rn/using/deprecated-features.md)
* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)

新しい Experience Cloud ソリューションリリースについての情報を得るには、[Adobe Priority Product Update](https://www.adobe.com/jp/subscription/priority-product-update.html) に登録してください。
