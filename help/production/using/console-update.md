---
product: campaign
title: コンソールの更新
description: コンソールの更新
feature: Monitoring, Upgrade
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3a127bbe-9abb-4b5b-bd7e-e1ea550929ba
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 9%

---

# コンソールの更新{#console-update}



「**[!UICONTROL コンソールの更新をリクエストしない]**」オプションを選択した場合、更新リクエストを再アクティブ化するには、次の手順に従います。

1. Windows の [ スタート ]>[ 実行 ] メニューで **regedit** コマンドを使用して、レジストリ・データベースのエディタ **[!UICONTROL を開き]** す。

   ![](assets/ncs_console_update_1.png)

1. ツリーで、**[!UICONTROL HKEY_CURRENT_USERSotwareneolaneNL_6nlclient]** ノードのオプションを表示します。
1. **[!UICONTROL confAdvisedUpgrade]** エントリを削除し、レジストリエディターを閉じます。

   ![](assets/ncs_console_update_2.png)
