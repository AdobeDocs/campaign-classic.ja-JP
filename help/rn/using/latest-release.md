---
product: campaign
title: 最新リリース
description: 最新の Campaign Classic v7 リリースノート
feature: Release Notes
role: User
level: Beginner
exl-id: d65869ca-a785-4327-8e8d-791c28e4696c
source-git-commit: d31aa28da06e65664da655b6b082563767b35f7a
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 19%

---

# 最新リリース {#latest-release}

このページには、**最新の Campaign Classic v7 リリース**&#x200B;の新機能、改善点および修正点が記載されています。新しいビルドごとに、色分けされたステータスが表示されます。Campaign Classic v7 のビルドステータスについて詳しくは、[このページ](rn-overview.md)を参照してください。

## リリース 7.4.1 - ビルド 9383 {#release-7-4-1}

[!BADGE 一般公開（GA）]{type=Positive url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="一般公開（GA）"}

_2024年6月18日（PT）_

### 変更点と改善点 {#release-7-4-1-changes}

* Adobeによりサービスアカウント（JWT）資格情報が非推奨となったので、Adobeソリューションやアプリとの Campaign アウトバウンド統合は、OAuth サーバー間資格情報に依存するようになりました。 Campaign と Analytics の統合やExperience Cloudトリガーの統合など、アウトバウンド統合を実装している場合は、2025 年 1 月 27 日（PT）までに、Campaign 環境を v7.4.1 にアップグレードし、テクニカルアカウントを OAuth に移行する必要があります。 [詳細情報](../../integrations/using/oauth-technical-account.md)

* 一度身に着ければ [campaign テクニカルオペレーターを開発者コンソールに移行しました](../../technotes/using/ims-migration.md) および [エンドユーザー認証用に IMS に移行](../../technotes/using/migrate-users-to-ims.md)を有効にして、ユーザーインターフェイスと API 制限を有効にし、ネイティブ認証に固有のオプションと機能を削除できるようになりました。 [詳細情報](../../technotes/using/impact-ims-migration.md)



### 互換性のアップデート {#release-7-4-1-compat}

この [Adobe Campaignの互換表](compatibility-matrix.md) は、この新しいリリースに伴う変更で更新されました。以下に示します。

* Adobe Campaignは、と互換性を持つようになりました **Microsoft Server 2022** および **RHEL 9** オペレーティングシステムとして。

* Adobe Campaignは、と互換性を持つようになりました **Microsoft SQL Server 2022** および **Oracle23c** 関係データベース管理システムとして、また Federated Data Access （FDA）において。

* Adobe Campaignには、少なくとも Java Development Kit （JDK） 11 が必要になりました。 Windows の場合は、の説明に従って JRE を使用できる必要があります。 [この節](../../installation/using/application-server.md#jdk).

* モバイルアプリケーション用 Campaign （Neolane） SDK は非推奨（廃止予定）になりました。 ここで、Adobe Experience Platform SDK に移行する必要があります。 [詳細情報](deprecated-features.md)。

  サービスの継続性を確保するために、Campaign v7.4 には次の機能が備わっています。

   * iOS 16 および 17 と互換性のあるiOS用の新しい Campaign SDK 1.0.27、最新 [Apple iOS プライバシーリクエストの要件](https://developer.apple.com/news/?id=r1henawx){target="_blank"}.
   * android 14 用の新しい Campaign SDK。


### パッチ {#release-7-4-1-patches}

このリリースには、次の修正が含まれています。

NEO-74754、NEO-73174、NEO-72504、NEO-71534、NEO-71473、NEO-70195、NEO-69663、NEO-69651、NEO-67620、NEO-67235 66797 64680、NEO-63706、NEO-63657、NEO-62964、NEO-62575、NEO-58734、NEO-40531、NEO-36189、NEO-29592

