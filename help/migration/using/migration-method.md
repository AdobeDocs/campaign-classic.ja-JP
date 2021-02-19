---
solution: Campaign Classic
product: campaign
title: 移行方法
description: 移行方法
audience: migration
content-type: reference
topic-tags: migration-overview
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 1%

---


# 移行方法{#migration-method}

## 環境の最新化{#modernizing-your-environment}

移行を実行すると、環境（データベースエンジン、オペレーティングシステム）を更新する可能性があります。 Adobe Campaignでは、実稼働環境を最新バージョンにアップグレードすることを強くお勧めします。

32ビット版のデータベースとオペレーティングシステムは引き続きv7でサポートされますが、今後のAdobe Campaign版ではサポートされなくなります。 プラットフォームを可能な限り早く64ビットにアップグレードすることを強くお勧めします。

v6.02では、「マルチタイムゾーン」モードはPostgreSQLデータベースエンジンでのみ使用可能でした。 どの種類のデータベースエンジンを使用しても提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。 詳しくは、[タイムゾーン](../../migration/using/general-configurations.md#time-zones)の節を参照してください。

>[!IMPORTANT]
>
>Adobe Campaign5.11および6.02でサポートされているソフトウェアバージョンの一部は、Adobe Campaignv7ではサポートされなくなりました。
>
>Adobe Campaignでサポートされているバージョンの詳細については、[互換表](../../rn/using/compatibility-matrix.md)を参照してください。

## キーの移行手順{#key-migration-steps}

Adobe Campaignv7への移行の一般的な手順については、[移行を開始する前](../../migration/using/before-starting-migration.md)の節に説明されています。

Adobe Campaignv7への移行の導入手順について詳しくは、[Adobe Campaign7](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md)への移行の前提条件の節を参照してください。

必要な設定は、既存の設定とプラットフォームの初期バージョンによって異なります。 これらの設定については、[一般的な設定](../../migration/using/general-configurations.md)の節で説明します。

## 特定の構成{#specific-configurations}

Adobe Campaignv7で引き起こされた変更は、以前のバージョンで開発された特定の設定を適応させる必要があることを意味する場合もあります。 したがって、移行前に、すべての設定に関する監査を実行する必要がある場合があります。Adobe Campaignにお問い合わせください。

たとえば、Web アプリケーション、SQLdataを使用するスキーマ拡張機能、またはあらかじめ用意されたスキーマのクローン作成に関する特定の設定には注意が必要です。 詳しくは、「[プラットフォーム](../../migration/using/configuring-your-platform.md)の設定」を参照してください。

同様に、Adobe Campaign内のセキュリティの高まりに対応するために、いくつかの内部メカニズムが修正されています。これらの対応する設定を適用する必要があります。
