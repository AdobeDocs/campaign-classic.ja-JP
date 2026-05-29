---
product: campaign
title: コンソールの更新
description: コンソールの更新
feature: Monitoring, Upgrade
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 3a127bbe-9abb-4b5b-bd7e-e1ea550929ba
TQID: https://experienceleague.adobe.com/oNVXa9DaMu-b-GpfxT-Z0jFbWEd-MnsSzu8Jdb0S0Fw
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
feature_v2: []
subfeature_v2: id: c03a11ff-bdf9-4e5b-b279-f468b4293464id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 64
ht-degree: 9%

---

# コンソールの更新{#console-update}



「**[!UICONTROL コンソール更新をリクエストしない]**」オプションを選択し、更新リクエストを再アクティブ化する場合は、次の手順を適用します。

1. Windows **[!UICONTROL 開始/実行]** メニューの&#x200B;**regedit** コマンドを使用して、レジストリ データベースのエディターを開きます。

   ![](assets/ncs_console_update_1.png)

1. ツリーに、**[!UICONTROL HKEY_CURRENT_USERSoftwareneolaneNL_6nlclient]** ノードのオプションを表示します。
1. **[!UICONTROL confAdvisedUpgrade]** エントリを削除し、レジストリエディターを閉じます。

   ![](assets/ncs_console_update_2.png)
