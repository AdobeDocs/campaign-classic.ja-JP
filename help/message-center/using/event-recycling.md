---
title: イベントの再利用
seo-title: イベントの再利用
description: イベントの再利用
seo-description: null
page-status-flag: never-activated
uuid: 55624a41-65a1-4759-8087-6e5d2c5c5b62
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: event-processing
discoiquuid: 568a9dec-5818-4666-b858-aa41fe827b92
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# イベントの再利用{#event-recycling}

特定のチャネルでのメッセージ配信に失敗した場合、Adobe Campaign は別のチャネルでメッセージを再送信することができます。例えば、SMS チャネルでの配信に失敗した場合、E メールチャネルを利用してメッセージを再送信します。

これには、ステータスが **Delivery error** であるすべてのイベントを再度作成し、異なるチャネルを割り当てるワークフローを設定する必要があります。

>[!CAUTION]
>
>この手順の実行は、ワークフローを使用する必要があるので、エキスパートユーザー向けの操作となります。詳しくは、アドビのアカウント担当者にお問い合わせください。

