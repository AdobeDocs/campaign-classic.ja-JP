---
product: campaign
title: Campaignのアンインストール
description: Campaignのアンインストール方法について説明します
feature: Installation
audience: installation
content-type: reference
hide: true
topic-tags: appendices
exl-id: e2b026ba-aaf3-443d-8c36-c908288a14fd
source-git-commit: 76f483dcda9f8a5ed93355d68bb1d1a589d55722
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 2%

---

# Campaignのアンインストール{#uninstalling-campaign}



>[!CAUTION]
>
>これらの手順は、Adobe Campaignを完全にアンインストールします。 すべてのデータが失われます。

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

この[ ページ ](../../migration/using/migrating-in-windows-for-adobe-campaign-7.md#deleting-and-cleansing-adobe-campaign-previous-version)を参照してください。 Campaign インストールフォルダーを削除することを忘れないでください。
