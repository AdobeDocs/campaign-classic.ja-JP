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



を選択した場合 **[!UICONTROL コンソールの更新を要求しない]** 「」オプションを選択して更新リクエストを再アクティブ化する場合、次の手順に従います。

1. を使用して、レジストリデータベースのエディターを開きます。 **regedit** Windows でのコマンド **[!UICONTROL 開始/実行]** メニュー。

   ![](assets/ncs_console_update_1.png)

1. ツリーで、のオプションを表示します **[!UICONTROL HKEY_CURRENT_USERSoftwareneolaneNL_6nlclient]** ノード。
1. を削除 **[!UICONTROL confAdvisedUpgrade]** レジストリエディターを入力して閉じます。

   ![](assets/ncs_console_update_2.png)
