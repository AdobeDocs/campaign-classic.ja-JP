---
product: campaign
title: 最新リリース
description: 最新の Campaign Classic v7 リリースノート
feature: Release Notes
role: User
level: Beginner
exl-id: d65869ca-a785-4327-8e8d-791c28e4696c
source-git-commit: 2296c1a7f6b818991d1620281077547d9250f16d
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 76%

---

# 最新リリース {#latest-release}

このページには、**最新の Campaign Classic v7 リリース**&#x200B;の新機能、改善点および修正点が記載されています。 新しいビルドごとに、色分けされたステータスが表示されます。 Campaign Classic v7 のビルドステータスについて詳しくは、[このページ](rn-overview.md)を参照してください。

## リリース 7.4.3 - ビルド 9394 {#release-7-4-3}

[!BADGE 一般公開（GA）]{type=Positive url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="一般公開（GA）"}

>[!CAUTION]
>
> コンソールのアップグレードは必須です。

_2026年3月31日_

### セキュリティの強化 {#security-7-4-3}

* 最適なセキュリティ、安定性、コンプライアンスを維持するために、Debian はバージョン 13 に、PostgreSQL はバージョン 17 にアップグレードされました。 [互換性マトリックス](compatibility-matrix.md)を参照してください。

### 修正点 {#fixes-7-4-3}

>[!NOTE]
>
> 以下に示す修正は、連続する7.4.3 ビルドで段階的にロールアウトされています。 **[!UICONTROL ヘルプ/会社概要…]** [&#x200B; メニュー](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)に移動して、最新の9394@28aaec9 ビルドを使用していることを確認します。 詳細については、Adobe担当者にお問い合わせください。

* バーコードコンポーネントで高さパラメーターに上限が設定されていなかった問題を修正しました。これは、セキュリティ上の脆弱性につながる可能性がありました。 （NEO-89984）
* ワークフローを介して作成されたリスト内の列挙フィールドに一時的な名前属性がなく、インターフェイスに誤ったまたは空白の列挙ラベルが表示される問題を修正しました。 （NEO-91158）
* 重複排除アクティビティを使用してワークフローで targetData フィールドを使用する際に、パーソナライゼーションエラーにより配信の準備が失敗する問題を修正しました。 （NEO-87693）
* PostgreSQL 15 で、型変換の要件により、1 文字の文字列フィールドを他の文字列と連結できない問題を修正しました。 （NEO-88028）
* 親と子の配信 ID の不一致により、分散型マーケティングの協調キャンペーンのトラッキングログがデータベースに書き込まれない問題を修正しました。 （NEO-86836）
* 配信ログで、正常に送信されたにもかかわらずメッセージがキャンセルされたことが示される問題を修正しました。特に、ウェーブスケジュールを使用した配信に影響していました。 （NEO-78933）
* データベースのクリーンアップワークフローがデータを効率的にパージできない問題を修正しました。これは、パフォーマンスに影響を及ぼす可能性がありました。 （NEO-76439）

<!-- BUILD 7.0.9394.28aaec9 -->

* 一部の配信について、配信統計が完全に再計算されない問題を修正しました。特に、成功指標に影響が生じていました。 （NEO-88106） <!-- moved from original 7.4.3 GA Fixes section -->
* 見つからないアップストリームターゲティングスキーマを参照する特定のワークフローを開くと、クライアントコンソールがクラッシュする可能性がある問題を修正しました。 （NEO-28727）
* インストールパッケージにバージョンファイルが見つからなかったため、起動失敗後にクライアントコンソールのバージョンを特定できない問題を修正しました。 （NEO-94798）

<!--
other fixes - ommitted from release notes

Internal/non-customer-facing:

* Fixed an internal DevOps build race condition when copying the `teradata_timezones.txt` file during build packaging. (NEO-66532) — internal only; the Jira description states "No impact for customers: either it builds (99.9% of the time) or it does not."
* Fixed an internal CI/CD issue where AWS CodeBuild jobs could fail randomly on EC2 Docker containers when copying files during build. (NEO-90823) — internal CI/CD infrastructure only

Customer-specific hotfixes:

* Fixed an issue where coupon assignment could fail during delivery message preparation due to a SQL syntax error when looking up coupon codes. (NEO-92857) — Verizon only
* Fixed an issue where the error count and status in the `nms:address` table were not consistently updated on the marketing server after recurring soft bounces, causing recipients to not be quarantined as expected even though they were correctly flagged on the mid-sourcing server. (NEO-94422) — Walgreens only
-->

