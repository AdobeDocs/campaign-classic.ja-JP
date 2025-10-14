---
product: campaign
title: Campaign Classicへの移行
description: 以前のバージョンの Campaign からCampaign Classicに移行する方法を説明します
feature: Upgrade
audience: migration
content-type: reference
topic-tags: migration-overview
hide: true
hidefromtoc: true
exl-id: 3050238d-6f77-4ffa-9aef-677ab8009388
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---

# 移行の基本を学ぶ{#about-migration}



このドキュメントでは、移行の前提条件と、Adobe Campaign Classic v7 に移行する手順を詳しく説明します。 手順とオプションの設定は、設定によって異なります。

移行プロセスは慎重に実行する必要があり、その影響は事前に十分に考慮されなければならず、手順は厳密に実行される必要があります。 エキスパートユーザーのみが実行する必要があります。 移行手順を開始する前に、[Adobeカスタマーケア &#x200B;](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) に連絡することを強くお勧めします。

移行は、テスト/ステージング環境で事前にテストして、スムーズにエラーなく実行されていることを確認する必要があります。 実稼動環境の移行は、移行したテスト環境が完全に検証された後にのみ実行する必要があります。

>[!NOTE]
>
>Adobe Campaign v7 に含まれている新機能および機能強化について詳しくは、[&#x200B; リリースノート &#x200B;](../../rn/using/latest-release.md) を参照してください。


## 前提条件

* 移行プロセスは、エキスパートユーザーが実行する必要があります。 少なくとも、データベースの専門家、システム管理者、Adobe Campaignのアプリケーション開発者の支援を受ける必要があります。
* 移行を開始する前に、使用するシステムおよびシステムコンポーネントが v7 と互換性があることを確認します。 [詳細情報](../../rn/using/compatibility-matrix.md)。
* Adobe Campaign Cloud Messaging （ミッドソーシングデプロイメント）を使用する場合は、開始する前にAdobeカスタマーケアにお問い合わせください。
* 移行プロセスを開始する前に、データをバックアップします **必ず**。
* 移行プロセスが完了するまでに数日かかる場合があります。
* Adobe Campaign v7 は、以前のバージョンよりも安全なバージョンです。これは、データ破損などの問題を回避し、データベースのデータ整合性を維持するための設定ガイドラインに影響します。 お客様は、ワークフローを含むすべての設定をテストする責任があります。

その他の前提条件については、[&#x200B; このページ &#x200B;](../../migration/using/before-starting-migration.md) を参照してください。


## 最新化された環境 {#modernizing-your-environment}

移行を実行すると、環境（データベースエンジン、オペレーティングシステム）を更新できる可能性があります。 Adobe Campaignでは、実稼動環境を最新バージョンにアップグレードすることを強くお勧めします。

>[!CAUTION]
>
>Adobe Campaign v7 でサポートされているバージョンについて詳しくは、[&#x200B; 互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md) を参照してください。

## 主な移行手順 {#key-migration-steps}

Adobe Campaign v7 への一般的な移行手順について詳しくは、[&#x200B; このページ &#x200B;](../../migration/using/before-starting-migration.md) を参照してください。


## 特定の設定 {#specific-configurations}

Adobe Campaign v7 による変化は、以前のバージョンで開発された特定の設定を適応させる必要があることも意味する場合があります。 そのため、移行前にすべての設定を監査する必要が生じる場合があります。サポートが必要な場合は、Adobe Campaignにお問い合わせください。

例えば、web アプリケーションの特定の設定、SQLdata を使用したスキーマ拡張、標準のスキーマクローン作成などに、特に注意が必要です。 詳しくは、[このページ](../../migration/using/configuring-your-platform.md)を参照してください。

同様に、Adobe Campaign内のセキュリティの高まりに対応するために、内部メカニズムが変更されています。つまり、これらの設定を適切に調整する必要があります。

