---
product: campaign
title: Campaign Classicへの移行
description: 以前のバージョンの Campaign からCampaign Classicに移行する方法を説明します
audience: migration
content-type: reference
topic-tags: migration-overview
hide: true
hidefromtoc: true
exl-id: 3050238d-6f77-4ffa-9aef-677ab8009388
source-git-commit: 80cf56e330731237d5e7b394381b737f30f8b350
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 3%

---

# 移行の概要{#about-migration}

![](../../assets/v7-only.svg)

このドキュメントでは、Adobe Campaign Classic v7 への移行の前提条件、および移行の手順について詳しく説明します。 手順とオプションの設定は、設定によって異なります。

移行プロセスは慎重に実行する必要があり、その影響を事前に十分に考慮し、手順は厳密に実行する必要があります。 エキスパートユーザーのみが実行する必要があります。 連絡を取ることを強くお勧めします [Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) 移行手順を開始する前に、次の手順を実行します。

移行は、事前にテスト/ステージング環境でテストし、スムーズに実行でき、エラーが発生しないようにする必要があります。 実稼動環境の移行は、移行されたテスト環境が完全に検証された後にのみ実行する必要があります。

>[!NOTE]
>
>Adobe Campaign v7 に加わる新機能と改善点について詳しくは、 [リリースノート](../../rn/using/latest-release.md).


## 前提条件

* 移行プロセスは、エキスパートユーザーが実行する必要があります。 少なくともAdobe Campaignのデータベースエキスパート、システム管理者およびアプリケーション開発者が支援する必要があります。
* 移行を開始する前に、使用するシステムおよびシステムコンポーネントが v7 と互換性があることを確認してください。 [詳細情報](../../rn/using/compatibility-matrix.md)
* Adobe Campaign Cloud Messaging（ミッドソーシングデプロイメント）を使用する場合は、開始する前にAdobeカスタマーケアにお問い合わせください。
* 移行プロセスを開始する前に、次の手順を実行します。 **必須** データをバックアップします。
* 移行プロセスが完了するまでに数日かかる場合があります。
* Adobe Campaign v7 は、以前のバージョンよりも安全です。これは、データの破損などの問題を回避し、データベースのデータの整合性を維持するための設定ガイドラインに影響します。 お客様は、ワークフローを含むすべての設定をテストする必要があります。

その他の前提条件は、 [このページ](../../migration/using/before-starting-migration.md).


## 最新環境 {#modernizing-your-environment}

移行を実行すると、環境（データベースエンジン、オペレーティングシステム）を更新する機会が生じます。 Adobe Campaignでは、実稼動環境を最新バージョンにアップグレードすることを強くお勧めします。

>[!CAUTION]
>
>Adobe Campaign v7 でサポートされているバージョンについて詳しくは、 [互換性マトリックス](../../rn/using/compatibility-matrix.md).

## 主要な移行手順 {#key-migration-steps}

Adobe Campaign v7 への移行の一般的な手順について詳しくは、 [このページ](../../migration/using/before-starting-migration.md).


## 特定の設定 {#specific-configurations}

また、Adobe Campaign v7 で発生した変更は、以前のバージョンで開発された特定の設定に適応する必要があることを意味する場合もあります。 したがって、移行前に、すべての設定で監査を実行する必要が生じる場合があります。サポートが必要な場合は、Adobe Campaignにお問い合わせください。

例えば、Web アプリケーション、SQLdata を使用したスキーマ拡張、標準のスキーマクローン作成に関する特定の設定に特に注意する必要があります。 詳しくは、[このページ](../../migration/using/configuring-your-platform.md)を参照してください。

同様に、Adobe Campaign内のセキュリティの高まりに対応するために、いくつかの内部メカニズムが修正されています。これらの設定は、それに応じて適応させる必要があります。

