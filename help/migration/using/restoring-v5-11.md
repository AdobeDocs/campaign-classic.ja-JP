---
title: v5.11の復元
seo-title: v5.11の復元
description: v5.11の復元
seo-description: null
page-status-flag: never-activated
uuid: 4480c97c-5845-483c-a17b-644f05783b4e
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: rollback
discoiquuid: ef778333-8e50-402b-9a69-78ac94497c67
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9482a99c3be164651b3428179388cb0a8a75783f

---


# v5.11の復元{#restoring-v}

v7からv5.11を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、復元します。
1. Neolane v5. **back** (Linuxでは&#x200B;**nl5.back** )フォルダーを回復し、名前を **Neolane v5** (**** linuxではnl5)に変更し、元の場所に戻します。
1. IIS webサイトレベルでNeolane v5の統合を再確立するために、リスンポートを再割り当てしてIISを再設定します。
1. Adobe Campaign v7サービスを停止します。
1. IISを再起動します。
1. Adobe Campaign v5サービスを再起動します。

