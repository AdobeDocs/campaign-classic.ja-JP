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



「**[!UICONTROL コンソール更新をリクエストしない]**」オプションを選択し、更新リクエストを再アクティブ化する場合は、次の手順を適用します。

1. Windows **[!UICONTROL 開始/実行]** メニューの&#x200B;**regedit** コマンドを使用して、レジストリ データベースのエディターを開きます。

   ![](assets/ncs_console_update_1.png)

1. ツリーに、**[!UICONTROL HKEY_CURRENT_USERSoftwareneolaneNL_6nlclient]** ノードのオプションを表示します。
1. **[!UICONTROL confAdvisedUpgrade]** エントリを削除し、レジストリエディターを閉じます。

   ![](assets/ncs_console_update_2.png)
