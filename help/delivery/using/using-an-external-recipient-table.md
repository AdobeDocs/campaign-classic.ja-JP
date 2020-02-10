---
title: 外部の送信者テーブルの使用
seo-title: 外部の送信者テーブルの使用
description: 外部の送信者テーブルの使用
seo-description: null
page-status-flag: never-activated
uuid: a6147425-14f0-41e8-a47f-3e7072deafa7
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: using-seed-addresses
discoiquuid: 92c32b2d-d8bf-41ab-9349-ef4a15f10521
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# 外部の送信者テーブルの使用{#using-an-external-recipient-table}

配信テーブルが外部のテーブルの場合は、追加設定が必要です。The **[!UICONTROL nms:seedmember]** schema must be extended. 次のように、適切なフィールドを定義するためのタブがシードアドレスに追加されます。

![](assets/s_ncs_user_seedlist_new_tab.png)

この場合、配信にシードアドレスを追加するには、適切なタブで各種の適切なフィールドを入力するか、アドレステンプレートをインポートします。

![](assets/s_ncs_user_seedlist_add_new_tab.png)

**nms:seedMember** スキーマ拡張については、[この節](../../configuration/using/seed-addresses.md)で説明しています。
