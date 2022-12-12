---
product: campaign
title: テクニカルノート - Adobe Campaign システムのアップグレード
description: Adobe Campaign システムのアップグレード
hide: true
hidefromtoc: true
exl-id: 78949d94-60b3-44f1-8e5a-d61b5b723e87
source-git-commit: bffad77458ab0b4d40490a52c64c99a0fe882d22
workflow-type: ht
source-wordcount: '499'
ht-degree: 100%

---

# Adobe Campaign 2023 環境のアップグレード {#ac-system-upgrade}

Campaign インフラストラクチャは、最新のバージョンと修正で定期的に更新する必要があるサードパーティ製システムに依存しています。これらの更新は、サービスの継続性を確保し、Campaign 環境をセキュリティリスクから保護するために必須です。また、サードパーティシステムの変更との互換性を確保するには、Campaign のアップグレードが必要です。

**ホステッド環境または Managed Cloud Services のお客様**&#x200B;には、これらのアップグレードが必要なときに、アドビからお知らせします。コンプライアンスを確保するために、推奨事項に従って環境をアップグレードする必要があります。

**オンプレミス環境またはハイブリッド環境のお客様**&#x200B;は、同じカレンダーに従ってシステムと Campaign のバージョンをアップグレードすることを強くお勧めします。

セキュリティ上の理由から、[最新の Campaign ビルドをインストール](#ac-upgrade)してから、[オペレーティングシステム](#os-upgrade)や[関係データベース管理システム（RDBMS）](#pg-upgrade)をアップグレードする必要があります。

>[!NOTE]
>
>これらの変更点に関するご質問については、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。[ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md) も参照してください。

## Campaign ビルドのアップグレード {#ac-upgrade}

**影響の有無**

以下で詳しく説明する[オペレーティングシステムのアップグレード](#os-upgrade)や[データベースシステムのアップグレード](#pg-upgrade)の影響を受ける場合は、Campaign 環境をこれらのシステムと互換性のある[最新の 7.3.2 バージョン](../../rn/using/latest-release.md#release-7-3-2)にアップグレードする必要があります。

**更新方法**

* ホステッド環境または Managed Cloud Services のお客様には、アドビから連絡があり、お使いの Campaign のバージョンがアップグレードされます。
* ハイブリッド環境のお客様には、お使いのミッドソーシング環境のビルドアップグレード予定日をアドビからお知らせします。また、マーケティング環境を同じバージョンにアップグレードする必要もあります。
* オンプレミス環境のお客様は、Campaign 環境を最新の 7.3.2 ビルドにアップグレードするように求められます。


## オペレーティングシステムのアップグレード {#os-upgrade}

**影響の有無**

Debian オペレーティングシステムで Campaign を実行している場合、最新の Debian セキュリティアップデートを活用するには、Campaign インフラストラクチャを **Debian 11** に移行する必要があります。Debian 9 のセキュリティサポートは、2023年6月30日（PT）まで利用可能です。

**更新方法**

* ホステッド環境または Managed Cloud Services のお客様には、アドビから連絡があり、お使いの環境がアップグレードされます。
* ハイブリッド環境のお客様には、お使いのミッドソーシング環境のアップグレード予定日をアドビからお知らせします。 マーケティング環境も Debian で実行している場合は、マーケティング環境も Debian 11 にアップグレードする必要があります。
* オンプレミス環境のお客様は、環境を Debian 11 にアップグレードするように求められます。

## データベースシステムのアップグレード {#pg-upgrade}

**影響の有無**

Campaign のデータベースシステムが PostgreSQL である場合、PostgreSQL の最新のイノベーションとセキュリティアップデートを活用するには、**PostgreSQL 14** にアップグレードする必要があります。なお、PostgreSQL 11 は、2023年11月9日（PT）に提供終了となります。

**更新方法**

* ホステッド環境または Managed Cloud Services のお客様には、アドビから連絡があり、お使いのデータベースシステムが PostgreSQL 11 から PostgreSQL 14 にアップグレードされます。
* ハイブリッド環境のお客様は、マーケティングデータベースシステムが PostgreSQL の場合、PostgreSQL 14 にアップグレードする必要があります。
* オンプレミス環境のお客様は、お使いのデータベースシステムを PostgreSQL 14 にアップグレードするように求められます。


## 参考になるリンク

* [環境のアップグレード](../../production/using/build-upgrade.md)
* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [最新の Campaign Classic ビルドのダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/ja/campaign.html)
* [ユーザーへの新しいクライアントコンソールの公開](../../installation/using/client-console-availability-for-windows.md)
