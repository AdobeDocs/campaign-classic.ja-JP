---
product: campaign
title: 移行に関する警告
description: 移行に関する警告
audience: migration
content-type: reference
topic-tags: migration-overview
exl-id: 46b46fc9-c7c9-4c74-b5f3-7935d5368520
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 3%

---

# 移行に関する警告{#migration-warnings}

![](../../assets/v7-only.svg)

* 移行プロセスは、エキスパートユーザー向け機能です。 少なくともAdobe Campaignのデータベースエキスパート、システム管理者およびアプリケーション開発者が支援する必要があります。
* 移行を開始する前に、使用するシステムおよびシステムコンポーネントが v7 と実際に互換性があることを確認してください。 詳しくは、 [互換性マトリックス](../../rn/using/compatibility-matrix.md).
* Adobe Campaign Cloud Messaging（以前のミッドソーシング）を使用している場合は、移行手順全体を開始する前にAdobe Campaignにお問い合わせください。
* 移行プロセスを開始する前に、次の手順を実行します。 **必須** データをバックアップします。
* 移行プロセスが完了するまでに数日かかる場合があります。
* Adobe Campaign v7 は、設定に関しては、5.11 および 6.02 のバージョンよりも厳しくなっています。 これは、主にデータの破損などの問題を回避し、データベースのデータの整合性を維持するためです。 その結果、v5.11 および v6.02 で提供されている特定の関数は v7 では動作しなくなる可能性があるので、移行後に適応が必要になる場合があります。 実稼動環境に移行する前に、すべての設定、特にAdobe Campaignの使用に必要なワークフローを体系的にテストすることをお勧めします。

>[!NOTE]
>
>また、 [移行を開始する前に](../../migration/using/before-starting-migration.md) 」セクションに入力します。
