---
product: campaign
title: Campaign Classic 2024 リリース
description: Campaign Classic 2024 リリースの詳細
feature: Release Notes
role: User
level: Beginner
exl-id: 8e20391d-3628-4d0c-b413-c34e046ae810
TQID: https://experienceleague.adobe.com/xYAjQLPvvsTN7DqzdIC8cdyODew3nA-ipPjccmY8LDY
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
subfeature_v2:
  - id: c3bf7e1e-1db5-4c72-9293-e2f0b1ab73d0
  - id: e5e477db-ebc7-4368-ab0f-4d8fc2aed405
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: c372a3d67ec413fa8cf9fdbb4530762a8f2f5177
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 100%

---

# 2024 リリース{#release-2024}

## リリース 7.4.1 - ビルド 9383 {#release-7-4-1}

[!BADGE 非推奨（廃止予定）]{type=negative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="非推奨（廃止予定）"}

_2024年6月18日（PT）_

### 変更点と改善点 {#release-7-4-1-changes}

* サービスアカウント（JWT）資格情報はアドビによって廃止され、アドビのソリューションおよびアプリとの Campaign アウトバウンド統合は OAuth サーバー間の資格情報に依存するようになりました。 Campaign と Analytics 統合や Experience Cloud トリガーの統合などのアウトバウンド統合を実装している場合は、2025年1月27日（PT）までに、Campaign 環境を v7.4.1 にアップグレードし、テクニカルアカウントを OAuth に移行する必要があります。 [詳細情報](../../integrations/using/oauth-technical-account.md)

* [Campaign テクニカルオペレーターを開発者コンソールに移行](../../technotes/using/ims-migration.md)し、[エンドユーザー認証用に IMS に移行](../../technotes/using/migrate-users-to-ims.md)すると、ユーザーインターフェイスと API 制限を有効にして、ネイティブ認証に固有のオプションと機能を削除できるようになりました。 [詳細情報](../../technotes/using/impact-ims-migration.md)


### 互換性のアップデート {#release-7-4-1-compat}

[Adobe Campaign の互換性マトリックス](compatibility-matrix.md)は、この新しいリリースに伴う変更を反映して更新されており、以下にリストされています。

* Adobe Campaign は、オペレーティングシステムとして **Microsoft Server 2022** と互換性を持つようになりました。
* Adobe Campaign は、オペレーティングシステムとして **RHEL 9** と互換性を持つようになりました。

  >[!CAUTION]
  >
  >RHEL 9 を使用しているオンプレミス環境のお客様が DKIM（Domain Keys Identified Mail）認証を使用する場合は、[この節](../../installation/using/installing-packages-with-linux.md#rhel-9-update)に記載されているようにシステム設定を更新する必要があります。


* Adobe Campaign は、関係データベース管理システムとして、また Federated Data Access （FDA）において、**Microsoft SQL Server 2022** および **Oracle 23c** と互換性を持つようになりました。

* Adobe Campaign には、Java Development Kit（JDK）11 以降が必要です。 Windows の場合は、[この節](../../installation/using/application-server.md#jdk)の説明に従って JRE を使用できる必要があります。

* モバイルアプリケーション用 Campaign（Neolane）SDK は非推奨（廃止予定）になりました。 ここで、Adobe Experience Platform SDK に移行する必要があります。 [詳細情報](deprecated-features.md)。

  サービスの継続性を確保するために、Campaign v7.4 には以下が付属しています。

   * iOS 用の新しい Campaign SDK 1.0.27（iOS 16 および 17 に対応）と、最新の [Apple iOS プライバシーリクエスト要件](https://developer.apple.com/news/?id=r1henawx){target="_blank"}。
   * Android 14 用の新しい Campaign SDK。

### その他の変更 {#release-7-4-1-other}

v7.4.1 以降、RPM Linux パッケージ用の XML ライブラリは Campaign に含まれなくなりました。 オンプレミスまたはハイブリッド環境のお客様は、管理者がこれらのライブラリをインストールする必要があります。 [詳細情報](../../installation/using/installing-packages-with-linux.md)

### パッチ {#release-7-4-1-patches}

このリリースには、次の修正が含まれています。

NEO-74754、NEO-73174、NEO-72504、NEO-71534、NEO-71473、NEO-70195、NEO-69663、NEO-69651、NEO-67620、NEO-67235、NEO-66797、NEO-64680、NEO-63706、NEO-63657、NEO-62964、NEO-62575、NEO-58734、NEO-40531、NEO-36189、NEO-29592


