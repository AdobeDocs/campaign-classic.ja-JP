---
keywords: Campaign Classic;ホーム;人気のトピック
product: campaign
title: Adobe Campaign Classic v7 製品ドキュメント
exl-id: 6b3f1689-80de-49fd-b7ee-7a2a1931d157
TQID: 'https://experienceleague.adobe.com/Q6Oc24mo-1qDAxCWu2lGT4UvRLXB78Tr5X4sb2kHFw8'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
    internal-label: Campaigns
  - id: a4671286-a59f-47e3-b97b-90627a1977d5
    internal-label: Communication channels
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
    internal-label: APIs
subfeature_v2:
  - id: d3b34fea-a110-482f-adb2-aae8d686bac8
    internal-label: Transactional messaging
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: 186021e65b592522f3c491fb518594b5bac5d003
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 42%
---
# Campaign Classic v7 ドキュメント {#campaign-classic-documentation}

このドキュメントでは、**オンプレミスおよびハイブリッド**&#x200B;のデプロイメント（インストール、設定、アップグレード、操作、v7に固有の機能）に関するCampaign Classic v7について説明します。 インスタンスがAdobe（Managed Cloud Services）によってホストされている場合は、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/campaign-home){target="_blank"}を参照してください。 Campaign v8のドキュメントが同じ方法で作成したコンテンツは、ここでは複製されなくなりました。[v7からv8](#from-v7-to-v8)を参照してください。

<!--![](platform/using/assets/do-not-localize/banner_acc_doc.jpg) -->

## 新機能

Adobe Campaign Classic v7 製品およびドキュメントの最新の機能強化の概要を説明します。 機能、改善点、修正の包括的なリストについては、詳細な[リリースノート](rn/using/latest-release.md)を参照してください。

>[!BEGINTABS]


>[!TAB 2026年10月リリースが公開されています！]

Campaign Classic v7.4.5 - 26年10月ビルド （ビルド 9420）では、Analytics外部アカウントの修正、パーソナライゼーションの保留状態に留まる配信、サーバーCPUの使用状況、断続的なデータモデルの更新エラー、配信の作成におけるスパムチェックエラー、繰り返し発生するソフトバウンスの強制隔離が行われます。

[![画像](assets/do-not-localize/learn-more-button.svg)](rn/using/latest-release.md)

>[!TAB Adobe IMS への移行]

セキュリティと認証プロセスを強化するために、Adobe Campaign では、エンドユーザーの認証モードをログインおよびパスワードによるネイティブ認証から Adobe ID 管理システム（IMS）に移行することを強くお勧めしています。

[![画像](assets/do-not-localize/learn-more-button.svg)](technotes/using/ac-ims.md)


>[!ENDTABS]

## 基本を学ぶ

<table style="table-layout:fixed">
  <tr style="border: 0;">
    <td>
    <a href="platform/using/launching-adobe-campaign.md"><img src="assets/do-not-localize/start-launch.png"></a></a>
    <div><strong>Adobe Campaign を起動</strong><br/>Campaign クライアントコンソールを起動し、Campaign アプリケーションサーバーに接続する方法を説明します。</div>
    </td>
    <td>
    <a href="platform/using/about-profiles.md"><img src="assets/do-not-localize/start-profiles.png"></a>
    <div><strong>プロファイルの追加と管理</strong><br/>Adobe Campaign v7 データベースで簡単にプロファイル管理を調べます。 手動またはインポートによるプロファイルの追加、顧客データの絞り込み、キャンペーンのカスタマイズを簡単に行うことができます。</div>
    </td>
    <td>
    <a href="https://experienceleague.adobe.com/en/docs/campaign/automation/workflows/introduction/about-workflows" target="_blank"><img src="assets/do-not-localize/start-workflows.jpeg"></a>
    <div><strong>ワークフローを使用した自動化</strong><br/>ワークフローを活用して、セグメント化、キャンペーンの実行、ファイル処理、人間の関与などのプロセスをデザインする方法について説明します。
    </div></td>
    <td>
    <a href="delivery/using/communication-channels.md"><img src="assets/do-not-localize/start-deliveries.jpeg"></a>
    <div><strong>配信の作成</strong><br/>メール、SMS、プッシュ通知など、様々なチャネルでメッセージを送信する方法について説明します。</div>
    </td>
  </tr>
  <tr style="border: 0;">
    <td align="center"><a href="platform/using/launching-adobe-campaign.md"><img src="assets/do-not-localize/learn-more-button.svg"></a></td>
    <td align="center"><a href="platform/using/about-profiles.md"><img src="assets/do-not-localize/learn-more-button.svg"></a></td>
    <td align="center"><a href="https://experienceleague.adobe.com/en/docs/campaign/automation/workflows/introduction/about-workflows" target="_blank"><img src="assets/do-not-localize/learn-more-button.svg"></a></td>
    <td align="center"><a href="delivery/using/communication-channels.md"><img src="assets/do-not-localize/learn-more-button.svg"></a></td>
    </tr>
</table>

## ドキュメントの参照

<table style="table-layout:auto">
  <tr style="border: 0;">
    <td>
      <img src="assets/do-not-localize/icon-configure.svg" width="35px">
      <br/>
      <strong>管理者</strong><br/><a href="production/using/general-architecture.md"> アーキテクチャの原則</a> - <a href="production/using/configuration.md">Campaignの設定</a> - <a href="platform/using/launching-adobe-campaign.md">Campaignへの接続</a> - <a href="installation/using/external-accounts.md">外部システムへの接続</a> - <a href="platform/using/access-management.md">権限</a> - <a href="platform/using/privacy-management.md"> プライバシーと同意</a> - <a href="production/using/build-upgrade.md"> ビルド アップグレードの実行</a> - <a href="delivery/using/about-deliverability.md">配信品質</a>
    </td>
    <td>
      <img src="assets/do-not-localize/icon-send.svg" width="35px">
      <br/>
      <strong> マーケター</strong><br/><a href="https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui" target="_blank"> ユーザーインターフェイス </a> （Campaign v8 ドキュメント） - <a href="https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/data/import" target="_blank"> データのインポートとエクスポート </a> （Campaign v8 ドキュメント） - <a href="https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/audience/create-audiences/create-audiences" target="_blank"> リストの作成</a> （Campaign v8 ドキュメント） - <a href="delivery/using/about-services-and-subscriptions.md"> サービスとサブスクリプション </a> - <a href="delivery/using/communication-channels.md"> コミュニケーションチャネル </a> - <a href="delivery/using/about-personalization.md">Personalization</a> - <a href="https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/create-message" target="_blank"> プルーフの送信</a> （Campaign v8 ドキュメント） - <a href="delivery/using/get-started-a-b-testing.md">A/B テスト - <a href="message-center/using/about-transactional-messaging.md"> トランザクションメッセージ </a> - <a href="interaction/using/interaction-and-offer-management.md"> インタラクションとオファー管理</a> - <a href="https://experienceleague.adobe.com/en/docs/campaign/automation/workflows/introduction/about-workflows" target="_blank"> ワークフローを使用した自動化</a> （Campaign v8 ドキュメント） - <a href="https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/set-up-campaigns.html?lang=ja" target="_blank"> マーケティングキャンペーン </a> - <a href="https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/tracking/tracking" target="_blank"> メッセージトラッキング </a> （Campaign v8 ドキュメント） - <a href="https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/reports/gs-reporting" target="_blank"> レポート </a> （Campaign v8 ドキュメント）</a>
    </td>
    <td>
      <img src="assets/do-not-localize/icon-dev.svg" width="35px">
      <br/>
      <strong>開発者</strong><br/><a href="https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/datamodel" target="_blank"> データモデルの説明</a> （Campaign v8 ドキュメント） - <a href="configuration/using/about-schema-reference.md"> スキーマ構造</a> - <a href="configuration/using/editing-forms.md">入力フォーム </a> - <a href="configuration/using/about-web-services.md">API</a> - <a href="https://experienceleague.adobe.com/ja/tools/campaign-api" target="_blank">JSAPI参照ドキュメント </a> - <a href="configuration/using/about-custom-recipient-table.md"> カスタム受信者テーブル </a>
    </td>
  </tr>
</table>

## v7からv8へ {#from-v7-to-v8}

Campaign v8 ドキュメントに記載されているコンテンツは、v7 ドキュメントから削除されました。 この表を使って探してください。

| お探しの場合… | Campaign v8 ドキュメントを参照する |
| --- | --- |
| ユーザーインターフェイス | [ ユーザーインターフェイスの確認](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui){target="_blank"} |
| プロファイル、リスト、読み込みと書き出し | [ プロファイルとデータの読み込み](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/data/import){target="_blank"} |
| ワークフロー | [ ワークフローについて](https://experienceleague.adobe.com/en/docs/campaign/automation/workflows/introduction/about-workflows){target="_blank"} |
| マーケティングキャンペーン | [ マーケティングキャンペーンの基本を学ぶ](https://experienceleague.adobe.com/en/docs/campaign/automation/campaign-orchestration/set-up-campaigns){target="_blank"} |
| 配信の作成と送信 | [ メッセージの作成](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/create-message){target="_blank"} |
| ビルトインレポート | [ レポートの概要](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/reports/gs-reporting){target="_blank"} |
| 権限 | [権限の基本を学ぶ](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/permissions/gs-permissions){target="_blank"} |
| 入力フォーム | [入力フォームの基本を学ぶ](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/developer/schemas-forms/forms){target="_blank"} |

## その他のリソース

[Adobe Campaign 製品説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-campaign-managed-cloud-services.html){target="_blank"} - [互換性マトリックス](rn/using/compatibility-matrix.md) - [チュートリアル](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja){target="_blank"} - [Campaign のコントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/key-features.html?lang=ja){target="_blank"} - [メールトラッキングピクセルと CNIL ガイダンス](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/cnil-pixel-tracking){target="_blank"}
