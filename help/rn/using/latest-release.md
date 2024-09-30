---
product: campaign
title: 最新リリース
description: 最新の Campaign Classic v7 リリースノート
feature: Release Notes
role: User
level: Beginner
exl-id: d65869ca-a785-4327-8e8d-791c28e4696c
source-git-commit: 9526d466dc4613410905d9d7265c6471cd1df599
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 96%

---

# 最新リリース {#latest-release}

このページには、**最新の Campaign Classic v7 リリース**&#x200B;の新機能、改善点および修正点が記載されています。新しいビルドごとに、色分けされたステータスが表示されます。Campaign Classic v7 のビルドステータスについて詳しくは、[このページ](rn-overview.md)を参照してください。

## リリース 7.4.1 - ビルド 9383 {#release-7-4-1}

[!BADGE 一般公開（GA）]{type=Positive url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="一般公開（GA）"}

_2024年6月18日（PT）_

### 変更点と改善点 {#release-7-4-1-changes}

* サービスアカウント（JWT）資格情報はアドビによって廃止され、アドビのソリューションおよびアプリとの Campaign アウトバウンド統合は OAuth サーバー間の資格情報に依存するようになりました。Campaign と Analytics 統合や Experience Cloud トリガーの統合などのアウトバウンド統合を実装している場合は、2025年1月27日（PT）までに、Campaign 環境を v7.4.1 にアップグレードし、テクニカルアカウントを OAuth に移行する必要があります。[詳細情報](../../integrations/using/oauth-technical-account.md)

* [Campaign テクニカルオペレーターを開発者コンソールに移行](../../technotes/using/ims-migration.md)し、[エンドユーザー認証用に IMS に移行](../../technotes/using/migrate-users-to-ims.md)すると、ユーザーインターフェイスと API 制限を有効にして、ネイティブ認証に固有のオプションと機能を削除できるようになりました。[詳細情報](../../technotes/using/impact-ims-migration.md)


### 互換性のアップデート {#release-7-4-1-compat}

[Adobe Campaign の互換性マトリックス](compatibility-matrix.md)は、この新しいリリースに伴う変更を反映して更新されており、以下にリストされています。

* Adobe Campaign は、オペレーティングシステムとして **Microsoft Server 2022** および **RHEL 9** と互換性を持つようになりました。

* Adobe Campaign は、関係データベース管理システムとして、また Federated Data Access （FDA）において、**Microsoft SQL Server 2022** および **Oracle 23c** と互換性を持つようになりました。

* Adobe Campaign には、Java Development Kit（JDK）11 以降が必要です。Windows の場合は、[この節](../../installation/using/application-server.md#jdk)の説明に従って JRE を使用できる必要があります。

* モバイルアプリケーション用 Campaign（Neolane）SDK は非推奨（廃止予定）になりました。ここで、Adobe Experience Platform SDK に移行する必要があります。[詳細情報](deprecated-features.md)。

  サービスの継続性を確保するために、Campaign v7.4 には以下が付属しています。

   * iOS 用の新しい Campaign SDK 1.0.27 は、iOS 16 および 17 と、最新の [Apple iOS プライバシーリクエスト要件](https://developer.apple.com/news/?id=r1henawx){target="_blank"}と互換性があります。
   * Android 14 用の新しい Campaign SDK。

### その他の変更 {#release-7-4-1-other}

v7.4.1 以降、RPM Linux パッケージ用の XML ライブラリは Campaign に含まれなくなりました。オンプレミスまたはハイブリッド環境のお客様は、管理者がこれらのライブラリをインストールする必要があります。 [詳細情報](../../installation/using/installing-packages-with-linux.md)

### パッチ {#release-7-4-1-patches}

このリリースには、次の修正が含まれています。

NEO-74754、NEO-73174、NEO-72504、NEO-71534、NEO-71473、NEO-70195、NEO-69663、NEO-69651、NEO-67620、NEO-67235、NEO-66797、NEO-64680、NEO-63706、NEO-63657、NEO-62964、NEO-62575、NEO-58734、NEO-40531、NEO-36189、NEO-29592

