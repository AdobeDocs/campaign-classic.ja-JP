---
solution: Campaign Classic
product: campaign
title: Campaign のアンインストール
description: キャンペーンのアンインストール方法
audience: installation
content-type: reference
topic-tags: appendices
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 30%

---


# Campaign のアンインストール{#uninstalling-campaign}

>[!CAUTION]
>
>これらの手順では、永久的なAdobe Campaignがアンインストールされます。 すべてのデータが失われます。

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

この[ページ](../../migration/using/migrating-in-windows-for-adobe-campaign-7.md#deleting-and-cleansing-adobe-campaign-previous-version)を参照してください。キャンペーンのインストールフォルダーを削除するのを忘れないでください。
