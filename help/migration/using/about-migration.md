---
product: campaign
title: Campaign Classicへの移行
description: 以前のCampaign バージョンからCampaign Classicに移行する方法について説明します
feature: Upgrade
audience: migration
content-type: reference
topic-tags: migration-overview
hide: true
exl-id: 3050238d-6f77-4ffa-9aef-677ab8009388
source-git-commit: 720a5f4edf534788f7fd143a476c25e58a6f1586
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---

# 移行の基本を学ぶ{#about-migration}



このドキュメントでは、移行の前提条件、Adobe Campaign Classic v7への移行の手順について詳しく説明します。 手順とオプション設定は、設定によって異なります。

移住プロセスは慎重に実行されなければならず、その影響は事前に完全に考慮されなければならず、手順は厳格に実行されなければなりません。 これは、エキスパートユーザーのみが実行する必要があります。 移行手順を開始する前に、[Adobe カスタマーケア ](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせいただくことを強くお勧めします。

移行がスムーズに実行され、エラーが発生しないことを確認するために、事前にテスト/ステージ環境で移行をテストする必要があります。 実稼動環境の移行は、移行されたテスト環境が完全に検証された後にのみ実行する必要があります。

>[!NOTE]
>
>Adobe Campaign v7に搭載されている新機能と機能強化について詳しくは、[ リリースノート ](../../rn/using/latest-release.md)を参照してください。


## 前提条件

* 移行プロセスは、エキスパートユーザーが実行する必要があります。 少なくともAdobe Campaignのデータベースの専門家、システム管理者、アプリケーション開発者の支援を受ける必要があります。
* 移行を開始する前に、使用するシステムとシステムコンポーネントがv7と互換性があることを確認してください。 [詳細情報](../../rn/using/compatibility-matrix.md)。
* Adobe Campaign Cloud Messaging （ミッドソーシングデプロイメント）を使用している場合は、開始する前にAdobeカスタマーケアにお問い合わせください。
* 移行プロセスを開始する前に、**データを** バックアップする必要があります。
* 移行プロセスが完了するまでに数日かかる場合があります。
* Adobe Campaign v7は、以前のものよりも安全なバージョンです。これにより、データの破損などの問題を回避し、データベース内のデータの整合性を維持するための設定ガイドラインに影響します。 お客様は、ワークフローを含むあらゆる設定をテストする責任があります。

その他の前提条件は、[このページ ](../../migration/using/before-starting-migration.md)で利用できます。


## 近代化された環境 {#modernizing-your-environment}

移行を実行すると、環境（データベースエンジン、オペレーティングシステム）が更新される可能性があります。 Adobe Campaignでは、実稼動環境を最新バージョンにアップグレードすることを強くお勧めします。

>[!CAUTION]
>
>Adobe Campaign v7でサポートされているバージョンについて詳しくは、[互換性マトリックス ](../../rn/using/compatibility-matrix.md)を参照してください。

## 移行の主な手順 {#key-migration-steps}

Adobe Campaign v7への移行に関する一般的な手順については、[このページ ](../../migration/using/before-starting-migration.md)で詳しく説明しています。


## 特定の設定 {#specific-configurations}

Adobe Campaign v7による変更は、以前のバージョンで開発した特定の設定を適応させる必要があることも意味します。 そのため、移行前にすべての設定を監査する必要がある場合があります。詳しくは、Adobe Campaignにお問い合わせください。

たとえば、Web アプリケーションの特定の設定、SQLdataを使用したスキーマ拡張機能、すぐに使用できるスキーマの複製などに特に注意を払う必要があります。 詳しくは、[このページ](../../migration/using/configuring-your-platform.md)を参照してください。

同様に、Adobe Campaign内で高まるセキュリティに対応するために、一部の内部メカニズムが変更されました。それに応じて、これらの設定を調整する必要があります。

