---
title: コンソールの更新
seo-title: コンソールの更新
description: コンソールの更新
seo-description: null
page-status-flag: never-activated
uuid: d2193d4f-b98c-47b1-88f1-7e5ccf4c453c
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: 9281808b-1c2f-4095-9051-f181f089f205
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# コンソールの更新{#console-update}

このオプションを選択し **[!UICONTROL Do not request console update]** て、更新リクエストを再アクティブ化する場合は、次の手順を適用します。

1. Windowsメニューのregeditコマンドを使用して、レジストリデ **ータベース** のエディタを開 **[!UICONTROL Start > Execute]** きます。

   ![](assets/ncs_console_update_1.png)

1. ツリーで、ノードのオプションを表示し **[!UICONTROL HKEY_CURRENT_USERSoftwareneolaneNL_6nlclient]** ます。
1. エントリを削 **[!UICONTROL confAdvisedUpgrade]** 除し、レジストリエディタを閉じます。

   ![](assets/ncs_console_update_2.png)

