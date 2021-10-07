---
product: campaign
title: コンソールの更新
description: コンソールの更新
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3a127bbe-9abb-4b5b-bd7e-e1ea550929ba
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 8%

---

# コンソールの更新{#console-update}

![](../../assets/v7-only.svg)

「**[!UICONTROL コンソールの更新を要求しない]**」オプションを選択し、更新リクエストを再アクティブ化する場合は、次の手順に従います。

1. Windows の **[!UICONTROL 開始/]** 実行メニューの **regedit** コマンドを使用して、レジストリデータベースのエディターを開きます。

   ![](assets/ncs_console_update_1.png)

1. ツリーで、 **[!UICONTROL HKEY_CURRENT_USERSoftwareneolaneNL_6nlclient]** ノードのオプションを表示します。
1. **[!UICONTROL confAdvisedUpgrade]** エントリを削除し、レジストリエディタを閉じます。

   ![](assets/ncs_console_update_2.png)
