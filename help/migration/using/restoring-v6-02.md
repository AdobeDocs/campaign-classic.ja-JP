---
title: v6.02の復元
seo-title: v6.02の復元
description: v6.02の復元
seo-description: null
page-status-flag: never-activated
uuid: df21209b-4825-42fa-a303-f383f872abb5
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: rollback
discoiquuid: 4f65ba19-e9f0-4425-b640-f27c61394859
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9482a99c3be164651b3428179388cb0a8a75783f

---


# v6.02の復元{#restoring-v}

v7からv6.02を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、復元します。
1. Neolane v6.back **(Linuxでは** nl6.back **)フォルダーを回復し、名前を** Neolane v6 **(** nl6 Linuxでは&#x200B;**** nl6)に変更し、元の場所に戻します。
1. IIS webサイトレベルでAdobe Campaign v6.02の統合を再確立するために、リスンポートを再割り当てしてIISを再設定します。
1. Adobe Campaign v6.1サービスを停止します。
1. IISを再起動します。
1. Adobe Campaign v6.02サービスを再起動します。

