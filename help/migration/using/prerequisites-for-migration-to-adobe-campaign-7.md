---
solution: Campaign Classic
product: campaign
title: Adobe Campaign 7 への移行の前提条件
description: Adobe Campaign 7 への移行の前提条件
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 22%

---


# Adobe Campaign 7 への移行の前提条件{#prerequisites-for-migration-to-adobe-campaign}

移行を実行する前に、[移行を開始する前に](../../migration/using/before-starting-migration.md)および[プラットフォーム](../../migration/using/configuring-your-platform.md)の設定の節を参照してください。

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
