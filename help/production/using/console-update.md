---
product: campaign
title: コンソールの更新
description: コンソールの更新
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3a127bbe-9abb-4b5b-bd7e-e1ea550929ba
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 8%

---

# コンソールの更新{#console-update}



選択した **[!UICONTROL コンソールの更新を要求しない]** 」オプションを選択し、更新リクエストを再アクティブ化する場合は、次の手順に従います。

1. を使用して、レジストリデータベースのエディターを開きます。 **regedit** Windows のコマンド **[!UICONTROL 開始/実行]** メニュー

   ![](assets/ncs_console_update_1.png)

1. ツリーに、 **[!UICONTROL HKEY_CURRENT_USERSoftwareneolaneNL_6nlclient]** ノード。
1. を削除します。 **[!UICONTROL confAdvisedUpgrade]** レジストリエディタを開き、閉じます。

   ![](assets/ncs_console_update_2.png)
