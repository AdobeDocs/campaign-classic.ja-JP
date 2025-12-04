---
product: campaign
title: Campaign オンプレミス、ハイブリッドおよびホスト機能のマトリックス
description: ホストデプロイメントとオンプレミスデプロイメントの主な違いについて説明します
feature: Installation, Architecture
exl-id: a2c425a8-9bde-4259-9140-5ada5397ed5f
source-git-commit: 8b38d825aa9b0595226a444e0e463362468d51b3
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 32%

---

# モデルごとの機能マトリックス{#capability-matrix-per-model}



Adobe Campaign Classic には一連のモジュールとオプションが付属しています。これらのモジュールの使用可否と使い方は、インストール構成のデプロイメントタイプによって異なります。この記事では、完全にホストされる（Managed Services）デプロイメントとオンプレミスデプロイメントの間の特定の機能の主な違いについて詳しく説明します。

ここでは、ホスト（Managed Services）デプロイメントとオンプレミスデプロイメントの主な違いについて説明します。 ハイブリッドデプロイメントの特異性は、Adobeがホストし、オンプレミスでホストする要素によって異なります。

様々なホスティングモデルについて [ この節 ](../../installation/using/hosting-models.md) で説明します。

## デプロイメントモデルごとの可用性 {#capability-matrix}

| 機能 | ホスト | ハイブリッド | オンプレミス | 詳細 |
|-----------------------------------------------|------------------|-----------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campaign サーバーの設定 | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../installation/using/the-server-configuration-file.md) |
| BCC でメールを送信 | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../installation/using/email-archiving.md) |
| Message Center 実行インスタンスの管理 | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../message-center/using/about-transactional-messaging.md) |
| ミッドソーシングプラットフォームの管理 | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../installation/using/mid-sourcing-server.md) |
| Litmus による受信ボックスレンダリング | オンデマンド | オンデマンド | 使用可能 | [詳細情報](../../delivery/using/inbox-rendering.md) |
| IMS との統合（Adobe ID） | オンデマンド | オンデマンド | オンデマンド | [詳細情報](../../integrations/using/about-adobe-id.md) |
| ファイル転送のためのデータの暗号化/復号化 | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../platform/using/unzip-decrypt.md) |
| ファイルの圧縮/解凍 | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../platform/using/unzip-decrypt.md) |
| ドメイン名の委任 | オンデマンド | オンデマンド | 利用できません | [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/setting-up-new-subdomain.html?lang=ja) |
| SpamAssassin のインストール | オンデマンド | 使用可能 | 使用可能 | [詳細情報](../../delivery/using/spamassassin.md) |
| 配信品質レポートへのアクセス | 使用可能 | オンデマンド | 使用可能 | [詳細情報](../../delivery/using/about-delivery-monitoring.md#deliverability-monitoring) |
| LDAP 認証の設定 | なし | 使用可能 | 使用可能 | [詳細情報](../../installation/using/connecting-through-ldap.md) |


## Federated Data Access{#fda}

Adobe Campaignには、1 つ以上の外部データベースに保存された情報を処理するための **Federated Data Access** （FDA）オプションが用意されています。Adobe Campaign データの構造を変更せずに外部データにアクセスできます。 [詳細情報](../../installation/using/about-fda.md)

>[!CAUTION]
>
>互換性のある外部データベースシステムは、ホスティングモデルに応じて異なります。 詳しくは、[Campaign 互換性マトリックス ](../../rn/using/compatibility-matrix.md) を参照してください。
>

**関連項目**

* [互換性マトリックス](../../rn/using/compatibility-matrix.md)
* [リリースノート](../../rn/using/latest-release.md)
* [Campaign Classic アップグレード](../../rn/using/rn-overview.md)
* [廃止予定の機能と削除された機能](../../rn/using/deprecated-features.md)
* [[!DNL Gold Standard] リリース](../../rn/using/gold-standard.md)
