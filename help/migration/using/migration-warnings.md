---
product: campaign
title: 移行に関する警告
description: 移行に関する警告
audience: migration
content-type: reference
topic-tags: migration-overview
exl-id: 46b46fc9-c7c9-4c74-b5f3-7935d5368520
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 3%

---

# 移行に関する警告{#migration-warnings}

* 移行プロセスは、エキスパートユーザー向けに用意されています。 少なくともAdobe Campaignのデータベースエキスパート、システム管理者およびアプリケーション開発者の支援が必要です。
* 移行を開始する前に、使用するシステムおよびシステムコンポーネントがv7と互換性があることを確認します。 [互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。
* Adobe Campaign Cloud Messaging（以前のミッドソーシング）を使用している場合は、移行手順全体を開始する前にAdobe Campaignにお問い合わせください。
* 移行プロセスを開始する前に、データを&#x200B;**バックアップする必要があります。**
* 移行プロセスが完了するまでに数日かかる場合があります。
* Adobe Campaign v7は、設定に関しては、5.11および6.02のバージョンより厳しくなっています。 これは、主に、データの破損や、データベース内のデータの整合性を維持するなどの問題を回避するためです。 その結果、v5.11およびv6.02で提供されている特定の関数はv7では動作しなくなり、移行後に適応が必要になる場合があります。 実稼動環境に移行する前に、すべての設定(特にAdobe Campaignの使用に必要なワークフロー)を体系的にテストすることをお勧めします。

>[!NOTE]
>
>移行を開始する前に、[](../../migration/using/before-starting-migration.md)の節も参照してください。
