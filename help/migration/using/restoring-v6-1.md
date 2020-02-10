---
title: v6.1の復元
seo-title: v6.1の復元
description: v6.1の復元
seo-description: null
page-status-flag: never-activated
uuid: 3fb71b6f-4d70-4814-a885-4d414a542eca
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: rollback
discoiquuid: e510482c-a56d-4254-90f8-19bd5c545e30
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9482a99c3be164651b3428179388cb0a8a75783f

---


# v6.1の復元{#restoring-v}

v7からv6.1を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、復元します。
1. **Adobe Campaign v6.back** (Linuxの場合は&#x200B;**nl6.back** )フォルダーを回復し、名前を **Adobe Campaign v6** (**** nl6 Linuxの場合はlinux)に変更して元の場所に戻します。
1. IIS webサイトレベルでAdobe Campaign v6.1の統合を再確立するために、リスンポートを再割り当てしてIISを再設定します。
1. Adobe Campaign v7サービスを停止します。
1. IISを再起動します。
1. Adobe Campaign v6.1サービスを再起動します。

