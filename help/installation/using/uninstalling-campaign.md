---
product: campaign
title: Campaign のアンインストール
description: Campaign のアンインストール方法を学ぶ
feature: Installation
audience: installation
content-type: reference
topic-tags: appendices
exl-id: e2b026ba-aaf3-443d-8c36-c908288a14fd
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 2%

---

# Campaign のアンインストール{#uninstalling-campaign}



>[!CAUTION]
>
>これらの手順により、Adobe Campaignが完全にアンインストールされます。 すべてのデータが失われます。

**RHEL:**

```
rpm -e nlserver6-v7
userdel -r neolane
groupdel neolane
rm -rf /user/local/neolane
```

**Debian:**

```
apt purge nlserver6-v7
userdel -r neolane
groupdel neolane
rm -rf /user/local/neolane
```

**Windows の場合：**

こちらを参照してください [ページ](../../migration/using/migrating-in-windows-for-adobe-campaign-7.md#deleting-and-cleansing-adobe-campaign-previous-version). 必ず Campaign インストールフォルダーを削除してください。
