---
product: campaign
title: Campaign オンプレミス、ハイブリッド、ホスト機能マトリックス
description: ホスト型デプロイメントとオンプレミス型デプロイメントの主な違いについて説明します。
exl-id: a2c425a8-9bde-4259-9140-5ada5397ed5f
source-git-commit: 1e11b7419388698f5de366cbeddf2be88ef12873
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 46%

---

# モデルごとの機能マトリックス{#capability-matrix-per-model}

![](../../assets/v7-only.svg)

Adobe Campaign Classic には一連のモジュールとオプションが付属しています。これらのモジュールの使用可否と使い方は、インストール構成のデプロイメントタイプによって異なります。この記事では、完全にホストされている (Managed Services) 機能とオンプレミスデプロイメントの間の特定の機能の主な違いに関する詳細を説明します。

このページでは、ホスト型 (Managed Services) デプロイメントとオンプレミスデプロイメントの主な違いについて説明します。 ハイブリッドデプロイメントの特性は、Adobeがホストし、お客様のプレミスでホストする要素によって異なります。

様々なホスティングモデルが導入されました [この節](../../installation/using/hosting-models.md).

## デプロイメントモデルごとの可用性 {#capability-matrix}

| 機能 | ホスト | ハイブリッド | オンプレミス | 詳細 |
|-----------------------------------------------|------------------|-----------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campaign サーバーの設定 | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../installation/using/the-server-configuration-file.md) |
| BCC で E メールを送信 | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../installation/using/email-archiving.md) |
| Message Center 実行インスタンスの管理 | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../message-center/using/about-transactional-messaging.md) |
| ミッドソーシングプラットフォームの管理 | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../installation/using/mid-sourcing-server.md) |
| Litmus を使用した受信ボックスレンダリング | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../delivery/using/inbox-rendering.md) |
| IMS(Adobe ID) との統合 | オンデマンド | オンデマンド | オンデマンド | [詳細情報](../../integrations/using/about-adobe-id.md) |
| ファイル転送のデータの暗号化/復号化 | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../platform/using/unzip-decrypt.md) |
| ファイルの圧縮/解凍 | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../platform/using/unzip-decrypt.md) |
| ドメイン名のデリゲーション | オンデマンド | オンデマンド | 利用不可 | [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/setting-up-new-subdomain.html?lang=ja) |
| SpamAssassin のインストール | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../delivery/using/spamassassin.md) |
| 配信品質レポートへのアクセス | 使用可能 | オンデマンド | 使用可能 | [詳細情報](../../delivery/using/monitoring-deliverability.md) |
| LDAP 認証の設定 | なし | 使用可能 | 使用可能 | [詳細情報](../../installation/using/connecting-through-ldap.md) |


## Federated Data Access{#fda}

Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。[詳細情報](../../installation/using/about-fda.md)

>[!CAUTION]
>
>互換性のある外部データベースシステムは、ホスティングモデルに応じて異なります。 詳しくは、 [Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md).

**関連項目：**

* [互換性マトリックス](../../rn/using/compatibility-matrix.md)
* [リリースノート](../../rn/using/latest-release.md)
* [Campaign Classicのアップグレード](../../rn/using/rn-overview.md)
* [非推奨（廃止予定）および削除された機能](../../rn/using/deprecated-features.md)
* [[!DNL Gold Standard] リリース](../../rn/using/gold-standard.md)
