---
title: キャンペーンオンプレミス、ハイブリッド、およびホスト機能マトリックス
description: ホスト型デプロイメントとオンプレミスデプロイメントの主な違いを学ぶ
page-status-flag: never-activated
uuid: d1c786a1-2691-4966-9108-059004050464
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: architecture-and-hosting-models
discoiquuid: 582f7ac6-cebe-4b47-8730-bbc16fd6b1bd
translation-type: tm+mt
source-git-commit: c2e1b4cf7051b7f1b9d5f2db0d9f51a733ca2abc
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 26%

---


# ホスティングモデルごとの機能マトリックス {#capability-matrix-per-model}

Adobe Campaign Classic には一連のモジュールとオプションが付属しています。これらのモジュールの使用可否と使い方は、インストール構成のデプロイメントタイプによって異なります。この記事では、完全にホストされた(Managed Services)デプロイメントとオンプレミスデプロイメントの特定の機能の主な違いについて詳しく説明します。

このページでは、ホスト(Managed Services)デプロイメントとオンプレミスデプロイメントの主な違いを示します。 ハイブリッド展開の特殊性は、Adobeがホストし、オンプレミスでホストする要素に依存します。

この節では、異なるホスティングモデル [について説明します](../../installation/using/hosting-models.md)。

## 機能マトリックス{#capability-matrix}

| 機能 | ホスト | ハイブリッド | オンプレミス | 詳細 |
|-----------------------------------------------|------------------|-----------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| キャンペーンサーバーの設定 | オンデマンド | 使用可能 | 使用可能 | サー[バー設定ファイルは](../../installation/using/the-server-configuration-file.md)、ホストユーザーの場合に限り、Adobeが変更できます。 |
| E メールの BCC | オンデマンド | オンデマンド | 使用可能 | ホスト型およびハイブリッド型アーキテクチャの場合は、アカウント担当者に連絡して、電子メールBCCをアクティブにしてください。 オンプレミスインストールの場合は、ドキュメントのガイドラインに従います。 [詳細情報](../../installation/using/email-archiving.md) |
| Message Center実行インスタンスの管理 | オンデマンド | オンデマンド | 使用可能 | ホストされた配置では、実行インスタンス上でのユーザの作成など、特定の設定は、Adobeのみが実行できます。 [詳細情報](../../message-center/using/about-transactional-messaging.md) |
| ミッドソーシングプラットフォームの管理 | オンデマンド | オンデマンド | 使用可能 | Adobeがホストするミッドソーシングプラットフォームは、Adobeのみが設定できます。 |
| Litmusを使用したインボックスレンダリング | オンデマンド | オンデマンド | 使用可能 | Litmusアカウントが必要です。 必要な詳細を取得するか、インボックスのレンダリング設定を実行するには、Adobeに連絡する必要があります。 [詳細情報](../../delivery/using/inbox-rendering.md) |
| IMS(Adobe ID)との統合 | オンデマンド | オンデマンド | オンデマンド | IMSプロビジョニングはAdobeが実行します。 この統合は、Adobe Experience Cloud統合の前提条件です。 [詳細情報](../../integrations/using/about-adobe-id.md) |
| ファイル転送用のデータの暗号化/復号化 | オンデマンド | 使用可能 | 使用可能 | ファイルの前処理または後処理を有効にするには、必要なユーティリティをAdobe Campaignサーバーにインストールする必要があります。 ホストのお客様は、キャンペーンCampaign コントロールパネルを使用できます。 [詳細情報](../../workflow/using/importing-data.md#unzipping-or-decrypting-a-file-before-processing) |
| ファイルの圧縮/解凍 | オンデマンド利用可能 | 使用可能 | ファイルの前処理または後処理を有効にするには、必要なユーティリティをAdobe Campaignサーバーにインストールする必要があります。 ホストのお客様は、キャンペーンCampaign コントロールパネルを使用できます。 [詳細情報](../../workflow/using/importing-data.md#unzipping-or-decrypting-a-file-before-processing) |
| ドメイン名の委任 | オンデマンド | オンデマンド | 使用不可 | [詳細情報](https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html) |
| SpamAssinのインストール | オンデマンド | 使用可能 | 使用可能 | SpamAssinをインストールするには、サーバー設定ファイルを編集する必要があります。 [詳細情報](../../delivery/using/spamassassin.md) |
| 配信品質レポートへのアクセス | 使用可能 | オンデマンド | 使用可能 | 特定のハイブリッド展開では、配信品質レポートにマーケティングインスタンスからアクセスできません。 |
| LDAP認証の設定 | 利用不可 | 使用可能 | 使用可能 | LDAP設定は、オンプレミスまたはハイブリッドインストールでのみ可能です。 [詳細情報](../../installation/using/connecting-through-ldap.md) |


## Federated Data Access{#fda}

Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。[詳細情報](../../platform/using/about-fda.md)

>[!CAUTION]
>
>Accessing an external database via FDA is only possible for on-premise or hybrid installations, except with the [Snowflake connector](../../platform/using/specific-configuration-database.md#configure-access-to-snowflake).


**関連項目：**

* [互換性マトリックス](../../rn/using/compatibility-matrix.md)
* [リリースノート](../../rn/using/latest-release.md)
* [Campaign Classicのアップグレード](../../rn/using/rn-overview.md)
* [非推奨（廃止予定）および削除された機能](../../rn/using/deprecated-features.md)
* [Gold Standardリリース](../../rn/using/gold-standard.md)
* [ゴールド標準プログラム](https://helpx.adobe.com/jp/campaign/kb/gold-standard.html)。
