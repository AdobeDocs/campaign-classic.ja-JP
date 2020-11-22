---
solution: Campaign Classic
product: campaign
title: コンソールの更新
description: コンソールの更新
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 8%

---


# コンソールの更新{#console-update}

「 **[!UICONTROL Do not request console update]** （コンソールの更新を要求しない）」オプションを選択し、更新要求を再アクティブ化する場合は、次の手順を適用します。

1. Windowsの **開始/実行** メニューで、regedit **** コマンドを使用して、レジストリデータベースのエディターを開きます。

   ![](assets/ncs_console_update_1.png)

1. ツリーで、 **[!UICONTROL HKEY_CURRENT_USERSoftwarenolaneNL_6nlclient]** ノードのオプションを表示します。
1. confAdvisedUpgradeエントリを削除し **** 、レジストリエディターを閉じます。

   ![](assets/ncs_console_update_2.png)

