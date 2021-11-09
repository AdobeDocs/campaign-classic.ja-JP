---
product: campaign
title: Campaign のアンインストール
description: Campaign のアンインストール方法を説明します
audience: installation
content-type: reference
topic-tags: appendices
exl-id: e2b026ba-aaf3-443d-8c36-c908288a14fd
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 30%

---

# Campaign のアンインストール{#uninstalling-campaign}

![](../../assets/v7-only.svg)

>[!CAUTION]
>
>これらの手順を実行すると、Adobe Campaignが永久にアンインストールされます。 すべてのデータが失われます。

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

この[ページ](../../migration/using/migrating-in-windows-for-adobe-campaign-7.md#deleting-and-cleansing-adobe-campaign-previous-version)を参照してください。Campaign のインストールフォルダーを忘れずに削除してください。
