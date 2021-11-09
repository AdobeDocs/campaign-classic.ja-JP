---
product: campaign
title: 移行方法
description: 移行方法
audience: migration
content-type: reference
topic-tags: migration-overview
exl-id: dd4d068b-f414-448f-8d9a-eedf44e7b6e6
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 1%

---

# 移行方法{#migration-method}

![](../../assets/v7-only.svg)

## 環境の最新化 {#modernizing-your-environment}

移行を実行すると、環境（データベースエンジン、オペレーティングシステム）を更新する機会が生じます。 Adobe Campaignでは、実稼動環境を最新バージョンにアップグレードすることを強くお勧めします。

32 ビットバージョンのデータベースとオペレーティングシステムは、v7 で引き続きサポートされますが、今後のバージョンのAdobe Campaignではサポートされなくなります。 できるだけ早く、プラットフォームを 64 ビットにアップグレードすることを強くお勧めします。

v6.02 では、「マルチタイムゾーン」モードは PostgreSQL データベースエンジンでのみ使用可能でした。 どのタイプのデータベースエンジンを使用しても、提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。 詳しくは、 [タイムゾーン](../../migration/using/general-configurations.md#time-zones) 」セクションに入力します。

>[!IMPORTANT]
>
>Adobe Campaign 5.11 および 6.02 でサポートされている一部のソフトウェアバージョンは、Adobe Campaign v7 ではサポートされなくなりました。
>
>Adobe Campaignでサポートされているバージョンについて詳しくは、 [互換性マトリックス](../../rn/using/compatibility-matrix.md).

## 主要な移行手順 {#key-migration-steps}

Adobe Campaign v7 への移行の一般的な手順について詳しくは、 [移行を開始する前に](../../migration/using/before-starting-migration.md) 」セクションに入力します。

Adobe Campaign v7 への移行の実装手順について詳しくは、 [Adobe Campaign 7 への移行の前提条件](../../migration/using/prerequisites-for-migration-to-adobe-campaign-7.md) 」セクションに入力します。

必要な設定は、既存の設定とプラットフォームの最初のバージョンによって異なります。 これらの概要については、 [一般設定](../../migration/using/general-configurations.md) 」セクションに入力します。

## 特定の設定 {#specific-configurations}

また、Adobe Campaign v7 で発生した変更は、以前のバージョンで開発された特定の設定に適応する必要があることを意味する場合もあります。 したがって、移行前に、すべての設定で監査を実行する必要が生じる場合があります。サポートが必要な場合は、Adobe Campaignにお問い合わせください。

例えば、Web アプリケーション、SQLdata を使用したスキーマ拡張、標準のスキーマクローン作成に関する特定の設定に特に注意する必要があります。 詳しくは、 [プラットフォームの設定](../../migration/using/configuring-your-platform.md) 」セクションに入力します。

同様に、Adobe Campaign内のセキュリティの高まりに対応するために、いくつかの内部メカニズムが修正されています。これらの対応する設定を適応させる必要があります。
