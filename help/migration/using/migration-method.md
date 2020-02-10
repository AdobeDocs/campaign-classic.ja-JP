---
title: 移行方法
seo-title: 移行方法
description: 移行方法
seo-description: null
page-status-flag: never-activated
uuid: 6b954d5b-cfa3-43c6-ac3d-da9185e9e9d1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: migration-overview
discoiquuid: 3ac779a7-1f91-4c1c-a439-10d01697326a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 4437d2ea4e4044245a2b9a5a870267cd1f1c0bc9

---


# 移行方法{#migration-method}

## 環境の最新化 {#modernizing-your-environment}

移行を実行すると、環境（データベースエンジン、オペレーティングシステム）を更新する可能性があります。 Adobe Campaignでは、実稼働環境を最新バージョンにアップグレードすることを強くお勧めします。

32ビット版のデータベースとオペレーティングシステムは、v7でも引き続きサポートされますが、今後のバージョンのAdobe Campaignではサポートされなくなります。 プラットフォームをできるだけ早く64ビットにアップグレードすることを強くお勧めします。

v6.02では、「マルチタイムゾーン」モードはPostgreSQLデータベースエンジンでのみ使用可能でした。 どのタイプのデータベースエンジンが使用されても提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。 詳しくは、タイムゾーンの節を参照し [てください](../../migration/using/general-configurations.md#time-zones) 。

>[!CAUTION]
>
>Adobe Campaign 5.11および6.02でサポートされているソフトウェアバージョンの一部は、Adobe Campaign v7ではサポートされなくなりました。
>
>Adobe Campaignでサポートされているバージョンの詳細については、互換表を参照 [してください](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html)。

## 主な移行手順 {#key-migration-steps}

Adobe Campaign v7への移行の一般的な手順については、「移行を開始する前に [」の節で説明します](../../migration/using/before-starting-migration.md) 。

Adobe Campaign v7への移行の導入手順について詳しくは、「Adobe Campaign 7への移行 [の前提条件」の節を参照してくだ](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) さい。

必要な設定は、既存の設定とプラットフォームの初期バージョンによって異なります。 これらの設定については、「一般設定」 [の節で説明し](../../migration/using/general-configurations.md) ます。

## 特定の設定 {#specific-configurations}

また、Adobe Campaign v7で発生した変更は、以前のバージョンで開発された特定の設定を適応させる必要があることを意味する場合もあります。 したがって、移行前に、すべての設定に関する監査を実行する必要がある場合があります。不明な点はAdobe Campaignにお問い合わせください。

例えば、Webアプリケーション、SQLdataを使用するスキーマ拡張、または標準搭載のスキーマ・クローン作成に関する特定の設定には特に注意が必要です。 詳しくは、「プラットフォームの設定」 [の節を参照してください](../../migration/using/configuring-your-platform.md) 。

同様に、Adobe Campaign内の高められたセキュリティに対応するために、いくつかの内部メカニズムが変更されました。これらの対応する設定を適合させる必要があります。
