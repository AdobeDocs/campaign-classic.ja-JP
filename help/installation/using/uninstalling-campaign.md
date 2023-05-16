---
product: campaign
title: Campaign のアンインストール
description: Campaign のアンインストール方法を説明します
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: installation
content-type: reference
topic-tags: appendices
exl-id: e2b026ba-aaf3-443d-8c36-c908288a14fd
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 30%

---

# Campaign のアンインストール{#uninstalling-campaign}



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
