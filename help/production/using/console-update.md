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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 11%

---


# コンソールの更新{#console-update}

「 **[!UICONTROL Do not request console update]** （コンソールの更新を要求しない）」オプションを選択し、更新要求を再アクティブ化する場合は、次の手順を適用します。

1. Windowsの **開始/実行** メニューで、regedit **** コマンドを使用して、レジストリデータベースのエディターを開きます。

   ![](assets/ncs_console_update_1.png)

1. ツリーで、 **[!UICONTROL HKEY_CURRENT_USERSoftwarenolaneNL_6nlclient]** ノードのオプションを表示します。
1. confAdvisedUpgradeエントリを削除し **** 、レジストリエディターを閉じます。

   ![](assets/ncs_console_update_2.png)

