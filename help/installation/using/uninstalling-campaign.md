---
product: campaign
title: Campaign のアンインストール
description: Campaign のアンインストール方法を学ぶ
feature: Installation
audience: installation
content-type: reference
hide: true
hidefromtoc: true
topic-tags: appendices
exl-id: e2b026ba-aaf3-443d-8c36-c908288a14fd
source-git-commit: 49f6ffe4f78cbd790fb27ac6250f4bd7e3bc9e68
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

この [&#x200B; ページ &#x200B;](../../migration/using/migrating-in-windows-for-adobe-campaign-7.md#deleting-and-cleansing-adobe-campaign-previous-version) を参照してください。 必ず Campaign インストールフォルダーを削除してください。
