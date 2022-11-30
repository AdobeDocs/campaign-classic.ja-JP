---
product: campaign
title: テクニカルノート — Adobe Campaignシステムのアップグレード
description: Adobe Campaign
hide: true
hidefromtoc: true
exl-id: 78949d94-60b3-44f1-8e5a-d61b5b723e87
source-git-commit: 7d7185e9d8c376d1390dc7e5f6a8724c3cbcfd40
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 11%

---

# Adobe Campaign 2023 環境のアップグレード {#ac-system-upgrade}

Campaign インフラストラクチャは、サードパーティ製システムを利用しており、最新のバージョンと修正を定期的に更新する必要があります。 これらの更新は、サービスの継続性を確保し、Campaign 環境をセキュリティリスクから保護するために必須です。 また、サードパーティのシステム変更との互換性を確保するには、Campaign のアップグレードが必要です。

As a **ホスト型または管理型Cloud Servicesのお客様**&#x200B;のAdobeに、必要に応じて、これらのアップグレードに関する情報が表示されます。 コンプライアンスを確保するために、推奨事項に従って環境をアップグレードする必要があります。

As a **オンプレミスまたはハイブリッドの顧客**&#x200B;の場合、Adobeでは、同じカレンダーに従ってシステムと Campaign のバージョンをアップグレードすることを強くお勧めします。

セキュリティ上の理由から、 [最新の Campaign ビルドのインストール](#ac-upgrade)を選択し、 [オペレーティングシステム](#os-upgrade) および/または [関係データベース管理システム (RDBMS)](#pg-upgrade).

>[!NOTE]
>
>これらの変更点に関するご質問については、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。関連トピック [ビルドアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md).

## Campaign ビルドのアップグレード {#ac-upgrade}

**影響の有無**

次の影響を受ける場合： [オペレーティングシステムのアップグレード](#os-upgrade) および/または [データベースシステムのアップグレード](#pg-upgrade) 以下に説明するように、Campaign 環境を [最新 7.3.2 バージョン](../../rn/using/latest-release.md#release-7-3-2)：これらのシステムと互換性があります。

**更新方法**

* ホストCloud Servicesまたは管理ユーザーのお客様は、Adobeから連絡を受け、Campaign のバージョンをアップグレードします。
* ハイブリッドのお客様の場合、Adobeは、ミッドソーシング環境で予定されているビルドアップグレード日を通知します。 また、マーケティング環境を同じバージョンにアップグレードする必要があります。
* オンプレミス版のお客様は、Campaign 環境を最新の 7.3.2 ビルドにアップグレードする必要があります。


## オペレーティングシステムのアップグレード {#os-upgrade}

**影響の有無**

Debian オペレーティングシステムで Campaign を実行している場合、最新の Debian セキュリティアップデートのメリットを活用するには、Campaign インフラストラクチャを次の場所に移動する必要があります。 **Debian 11**. Debian 9 は 2022 年 6 月 30 日に提供終了となり、セキュリティの修正はおこなわれなくなりました。 Adobeは、2023 年 6 月 30 日まで Debian 9 のセキュリティサポートを提供しています。

**更新方法**

* ホスト型または管理型Cloud Servicesのお客様は、Adobeから連絡を受け、環境をアップグレードします。
* ハイブリッドのお客様の場合、Adobeは、ミッドソーシング環境で予定されているアップグレード日を通知します。 マーケティング環境も Debian で実行している場合は、Debian 11 にもアップグレードする必要があります。
* オンプレミスのお客様は、環境を Debian 11 にアップグレードする必要があります。

## データベースシステムのアップグレード {#pg-upgrade}

**影響の有無**

Campaign のデータベースシステムが PostgreSQL の場合、最新の PostgreSQL の革新とセキュリティ更新を活用するには、 **PostgreSQL 14**. PostreSQL 11 は、2023 年 11 月 9 日に提供終了となります。

**更新方法**

* ホスト型または管理型のCloud Servicesのお客様は、Adobeから連絡を受けて、データベースシステムを PostgreSQL 11 から PostgreSQL 14 にアップグレードします。
* ハイブリッドのお客様で、マーケティングデータベースシステムが PostgreSQL の場合は、PostgreSQL 14 にアップグレードする必要があります。
* オンプレミス型のお客様は、データベースシステムを PostgreSQL 14 にアップグレードするよう求められます。


## 参考になるリンク

* [環境のアップグレード](../../production/using/build-upgrade.md)
* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [最新のCampaign Classicビルドをダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/ja/campaign.html)
* [ユーザーへの新しいクライアントコンソールの公開](../../installation/using/client-console-availability-for-windows.md)
