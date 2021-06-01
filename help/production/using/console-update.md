---
product: campaign
title: コンソールの更新
description: コンソールの更新
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3a127bbe-9abb-4b5b-bd7e-e1ea550929ba
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 8%

---

# コンソールの更新{#console-update}

「**[!UICONTROL コンソールの更新を要求しない]** 」オプションを選択し、更新リクエストを再アクティブ化する場合は、次の手順に従います。

1. Windowsの&#x200B;**[!UICONTROL 開始/]**&#x200B;を実行メニューの&#x200B;**regedit**&#x200B;コマンドを使用して、レジストリデータベースのエディターを開きます。

   ![](assets/ncs_console_update_1.png)

1. ツリーで、 **[!UICONTROL HKEY_CURRENT_USERSoftwareneolaneNL_6nlclient]**&#x200B;ノードのオプションを表示します。
1. **[!UICONTROL confAdvisedUpgrade]**&#x200B;エントリを削除し、レジストリエディターを閉じます。

   ![](assets/ncs_console_update_2.png)
