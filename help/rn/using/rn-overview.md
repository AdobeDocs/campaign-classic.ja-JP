---
product: campaign
title: アップグレードの概要
description: Campaign Classic アップグレードの詳細
feature: Release Notes
role: User
level: Beginner
exl-id: 7a05fdff-8f9d-4e8d-812e-0f1509db5499
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 97%

---

# リリースの更新{#rn-overview}



Adobe Campaign Classic は、新機能、バグ修正、パフォーマンス、セキュリティ、操作性の向上をもたらす製品アップデートを定期的にリリースしています。 これらのアップデートは、**製品ビルド**&#x200B;としてリリースされます。新しい各ビルドに関する詳細は、[リリースノート](latest-release.md)を参照してください。

## リリースのステータス{#rn-statuses}

[リリースノート](latest-release.md)では、新しいビルドのステータスが色分けされて表示されます。 


| ステータス | 説明 |
|---|---|
| [!BADGE 一般公開]{type=Positive} | 実稼動環境で検証済され、アドビが推奨する、最新の安定したビルド。 |
| [!BADGE 限定提供（LA）]{type=Neutral} | オンデマンドデプロイメントのみ。 |
| [!BADGE リリース候補]{type=Informative} | 新機能を備えた最新ビルド。 |
| [!BADGE 公開停止]{type=Caution} | デプロイメントなし。バグ修正はありません。 新しいビルドへの更新をお勧めします。 |
| [!BADGE 非推奨]{type=negative} | デプロイメントなし。バグ修正はありません。 既存の実装はアップグレードする必要があります。 |

<!--
![](assets/do-not-localize/green3.png) **General Availability** (GA) - Latest stable build, validated in production, and recommended by Adobe. 

![](assets/do-not-localize/limited3.png) **Limited Availability** (LA) - On-demand deployment only.

![](assets/do-not-localize/blue3.png) **Release Candidate** (RC) - Latest build with new capabilities.

![](assets/do-not-localize/orange3.png) **No longer available** - No deployment. No bug fix. Update to a newer build is recommended.

![](assets/do-not-localize/red3.png) **Deprecated** - No deployment. No bug fix. Existing implementations must be upgraded.
-->

## リリースサイクル{#rn-cycle}

Adobe Campaign は定期的にアップデートされています。この定期的なアップデートは、環境の安全性を維持し、アドビの製品に対する体験を向上させ、最新かつ最大限の情報を手に入れることを目的としています。

Adobe Campaign の&#x200B;**最新の安定したビルドを実行**&#x200B;することが重要なのはこのためです。また、最近のビルドでは通常、問題の特定、再現、修正が迅速に行われるため、より優れたサポート体験を得ることができます。また、発生する可能性のある多くの問題は、最新のビルドでは修正済みとなっています。

ホステッド環境のお客様はアクションを起こすことなく、最新の安定したビルドのアップグレードのメリットが自動的に得られます。詳しくは、[年次アップグレードの節](#yearly-upgrade)を参照してください。古いビルドから移行する場合は、まずこのビルドにアップグレードすることをお勧めします。

## レコメンデーション{#recommendations}

安定した設定を確保するために、同じクライアント設定で実行しているすべてのサーバーに&#x200B;**同じビルド**&#x200B;をインストールすることをお勧めします。

また、[リリースノート](latest-release.md)で特に明記されていない限り、クライアントコンソールはサーバーインスタンスと&#x200B;**同じビルド**&#x200B;上にある必要があります。

実装を最新の状態に維持するため、新しいリリースのたびに、[廃止および削除された機能](../../rn/using/deprecated-features.md)と[互換性マトリックス](../../rn/using/compatibility-matrix.md)のページを必ずお読みください。

## アップグレードのプロセス{#process-upgrade}

ホステッド環境のマネージドサービスまたはハイブリッドのお客様は、環境をアップグレードするには、アドビカスタマーケアに連絡してください。

オンプレミスのお客様は、アップグレードを実行できます。これを行うには、[最新の安定したビルド（GA）をダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)して、すべての環境をアップグレードします。

[アップグレードプロセス](../../production/using/build-upgrade.md)について詳しくは、[ビルドアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md) を参照してください。

## 年次アップグレード {#yearly-upgrade}

アドビは、ソフトウェアソリューションを通じて最高のエクスペリエンスと価値を提供することを目指しています。アドビでは、アドビのソリューションがタスク実行のために使用する関連テクノロジーの最新バージョンにお客様がアクセスできるよう、取り組みを進めています。

Adobe Campaign Classic では、お客様に価値を提供するために、様々なテクノロジーを使用しています。こうしたテクノロジーによる優れたセキュリティ、安定性、パフォーマンスを実現するには、Campaign Classic インスタンスを定期的にアップグレードして、常に最新版を使用する必要があります。

ホステッド環境のお客様は、アップグレード操作を実行しなくても最新の GA ビルドのアップグレードのメリットを自動的に受けられます。詳しくは、以下の FAQ を参照してください。

### このアップグレードが必要な理由

ホステッド環境のお客様は、ご利用のアカウントで Campaign Classic に関連する 1 つ以上のテクノロジーのアップグレードや、インフラストラクチャを現在のビルド（v7.2.1 から v7.3.3 など）またはバージョン（v7 から v8 など）にアップグレードする必要があると判断されると、アドビから直接通知されます。

古いビルドを実行中のオンプレミスまたはハイブリッド環境のお客様は、最新の安定したビルド（GA）に移行することをお勧めします。

これにより、アカウントの脆弱性を確実に保護し、アップデートされたパフォーマンステクノロジーを利用できるようになります。また、このアップグレードにより、ご利用のアカウントで、今後は、手動での操作や介入が少なくて済む、容易な定期アップグレードを実行できるようになります。

### このアップグレードのプロセスとタイムライン

アドビのチームが、このジャーニーを通じてお客様の組織を導き、サポートします。

専任のカスタマーケア担当者、製品マネージャー、エンジニア、テクニカルオペレーションスペシャリストおよび製品コンサルタントから成るチームが、スムーズかつシームレスなエクスペリエンスになるように支援します。

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
    <li>カスタマーケアの件数や作業量が減ることで、より迅速な解決が可能となり、アップグレード以外の問題にもより注目できるようになります。</li>
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
    <li>Campaign Classic を支えるテクノロジースタック全体を改善することで、マーケティングチームと IT チーム双方が効果を実感できます。</li>
    </ul>
  </td>

<td>
      <img alt="ビルドのアップグレード" src="assets/do-not-localize/upgrades.png" />
    <div>
    <strong>アップグレードが容易</strong>
    </a>
    </div>
    <ul>
    <li>Campaign Classic インスタンスのアップグレードに要する作業量やその複雑さは、2 つのバージョンの間隔が開くほど増大します。</li>
    <li>アップグレードを先送りにすればするほど、作業がより複雑になり、さらに多くの脆弱性にさらされます。</li>
    <li>定期的アップグレードの実行により、アップグレードにかかるダウンタイムとリグレッションのリスクが軽減されます。</li>
    </ul>
  </td>
</tr>
</table>

## その他のリソース{#support}

* [Campaign のバージョンの確認](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)
* [ヘルプとサポート](../../support.md)
* [コントロールパネルのリリース](https://experienceleague.adobe.com/docs/control-panel/using/release-notes.html?lang=ja)
* [最新のドキュメントのアップデート](../../rn/using/documentation-updates.md)
* [非推奨および削除された機能](../../rn/using/deprecated-features.md)
* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)

新しい Experience Cloud ソリューションリリースについての情報を得るには、[Adobe Priority Product Update](https://www.adobe.com/jp/subscription/priority-product-update.html) に登録してください。
