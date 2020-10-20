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
source-git-commit: c03e90b2e2f57606749c86cda343ce5756fec122
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 44%

---


# 機能マトリックス {#capability-matrix-per-model}

Adobe Campaign Classic には一連のモジュールとオプションが付属しています。これらのモジュールの使用可否と使い方は、インストール構成のデプロイメントタイプによって異なります。この記事では、完全にホストされた(Managed Services)デプロイメントとオンプレミスデプロイメントの特定の機能の主な違いについて詳しく説明します。

このページでは、ホスト(Managed Services)デプロイメントとオンプレミスデプロイメントの主な違いを示します。 ハイブリッド展開の特殊性は、Adobeがホストし、オンプレミスでホストする要素に依存します。

この節では、異なるホスティングモデル [について説明します](../../installation/using/hosting-models.md)。

## 導入モデルごとの可用性 {#capability-matrix}

| 機能 | ホスト | ハイブリッド | オンプレミス | 詳細 |
|-----------------------------------------------|------------------|-----------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| キャンペーンサーバーの設定 | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../installation/using/the-server-configuration-file.md) |
| E メールの BCC | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../installation/using/email-archiving.md) |
| Message Center実行インスタンスの管理 | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../message-center/using/about-transactional-messaging.md) |
| ミッドソーシングプラットフォームの管理 | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../installation/using/mid-sourcing-server.md) |
| Litmusを使用したインボックスレンダリング | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../delivery/using/inbox-rendering.md) |
| IMS(Adobe ID)との統合 | オンデマンド | オンデマンド | オンデマンド | [詳細情報](../../integrations/using/about-adobe-id.md) |
| ファイル転送用のデータの暗号化/復号化 | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../workflow/using/importing-data.md#unzipping-or-decrypting-a-file-before-processing) |
| ファイルの圧縮/解凍 | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../workflow/using/importing-data.md#unzipping-or-decrypting-a-file-before-processing) |
| ドメイン名の委任 | オンデマンド | オンデマンド | 使用不可 | [詳細情報](https://helpx.adobe.com/jp/campaign/kb/domain-name-delegation.html) |
| SpamAssinのインストール | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../delivery/using/spamassassin.md) |
| 配信品質レポートへのアクセス | 使用可能 | オンデマンド | 使用可能 | [詳細情報](../../delivery/using/monitoring-deliverability.md) |
| LDAP認証の設定 | 利用不可 | 使用可能 | 使用可能 | [詳細情報](../../installation/using/connecting-through-ldap.md) |


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
* [ゴールドスタンダードプログラム](https://helpx.adobe.com/jp/campaign/kb/gold-standard.html)
