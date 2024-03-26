---
product: campaign
title: Campaign のアンインストール
description: Campaign のアンインストール方法を説明します
feature: Installation
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: installation
content-type: reference
topic-tags: appendices
exl-id: e2b026ba-aaf3-443d-8c36-c908288a14fd
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 18%

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

これを参照してください。 [ページ](../../migration/using/migrating-in-windows-for-adobe-campaign-7.md#deleting-and-cleansing-adobe-campaign-previous-version). Campaign のインストールフォルダーを忘れずに削除してください。
