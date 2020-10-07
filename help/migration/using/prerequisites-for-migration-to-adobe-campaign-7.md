---
title: Adobe Campaign 7 への移行の前提条件
seo-title: Adobe Campaign 7 への移行の前提条件
description: Adobe Campaign 7 への移行の前提条件
seo-description: null
page-status-flag: never-activated
uuid: 9f4e4cdf-5338-4597-9d9d-5a3bd13033c7
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
discoiquuid: a3bbd8cc-97c6-4b08-adbf-76ab77b97262
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Adobe Campaign 7 への移行の前提条件{#prerequisites-for-migration-to-adobe-campaign}

移行を実行する前に、「移行を開始する [前に](../../migration/using/before-starting-migration.md) 」および「プラットフォームの [設定](../../migration/using/configuring-your-platform.md) 」の節を参照してください。

v6.02からAdobe Campaignv7に移行する場合、以前に配信された一部のファイルは配信されません。

クライアントエラーが表示された場合は、ダッシュボードを新しいAdobe Campaignのv7コードで更新するか、v6.02インスタンスからv7インスタンスに手動で次のファイルをコピーする必要があります。

```
v6.02 files and spaces:
/usr/local/neolane/nl6/datakit/xtk/eng/css/dropDownMenu.css
/usr/local/neolane/nl6/datakit/xtk/eng/js/client/dropDownMenu.js
v6.1 files and spaces:
/usr/local/neolane/nl6/deprecated/xtk/css/dropDownMenu.css
/usr/local/neolane/nl6/deprecated/xtk/js/client/dropDownMenu.js  
```
