---
product: campaign
title: 移行方法
description: 移行方法
audience: migration
content-type: reference
topic-tags: migration-overview
exl-id: dd4d068b-f414-448f-8d9a-eedf44e7b6e6
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 1%

---

# 移行方法{#migration-method}

## 環境の最新化{#modernizing-your-environment}

移行を実行すると、環境（データベースエンジン、オペレーティングシステム）を更新する可能性があります。 Adobe Campaignでは、実稼動環境を最新バージョンにアップグレードすることを強くお勧めします。

32ビットバージョンのデータベースとオペレーティングシステムは、v7で引き続きサポートされますが、今後のバージョンのAdobe Campaignではサポートされなくなります。 できるだけ早くプラットフォームを64ビットにアップグレードすることを強くお勧めします。

v6.02では、「マルチタイムゾーン」モードはPostgreSQLデータベースエンジンでのみ使用可能でした。 どのタイプのデータベースエンジンを使用しても、提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。 詳しくは、[タイムゾーン](../../migration/using/general-configurations.md#time-zones)の節を参照してください。

>[!IMPORTANT]
>
>Adobe Campaign 5.11および6.02でサポートされている一部のソフトウェアバージョンは、Adobe Campaign v7ではサポートされなくなりました。
>
>Adobe Campaignでサポートされているバージョンについて詳しくは、[互換表](../../rn/using/compatibility-matrix.md)を参照してください。

## 主な移行手順{#key-migration-steps}

Adobe Campaign v7への移行の一般的な手順については、[移行を開始する前に](../../migration/using/before-starting-migration.md)の節で説明しています。

Adobe Campaign v7への移行の実装手順について詳しくは、 [Adobe Campaign 7への移行の前提条件の節を参照してください。](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md)

必要な設定は、既存の設定とプラットフォームの最初のバージョンによって異なります。 これらの設定については、[一般的な設定](../../migration/using/general-configurations.md)の節で説明します。

## 特定の設定{#specific-configurations}

また、Adobe Campaign v7によってもたらされた変更は、以前のバージョンで開発された特定の設定を適応させる必要があることを意味する場合もあります。 したがって、移行前に、すべての設定に対して監査を実行する必要が生じる場合があります。不明な点はAdobe Campaignにお問い合わせください。

例えば、Webアプリケーションの特定の設定、SQLdataを使用したスキーマ拡張、または標準のスキーマクローン作成に特に注意する必要があります。 詳しくは、[プラットフォームの設定](../../migration/using/configuring-your-platform.md)の節を参照してください。

同様に、Adobe Campaign内のセキュリティの高まりに対応するために、いくつかの内部メカニズムが変更されています。これらの対応する設定は、調整する必要があります。
