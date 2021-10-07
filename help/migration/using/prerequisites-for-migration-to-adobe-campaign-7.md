---
product: campaign
title: Adobe Campaign 7 への移行の前提条件
description: Adobe Campaign 7 への移行の前提条件
audience: migration
content-type: reference
topic-tags: migrating-to-adobe-campaign-7
exl-id: 747d8a2c-b13a-4852-a9b5-0d37b236a36f
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 22%

---

# Adobe Campaign 7 への移行の前提条件{#prerequisites-for-migration-to-adobe-campaign}

![](../../assets/v7-only.svg)

移行を実行する前に、[ 移行を開始する前に ](../../migration/using/before-starting-migration.md) および [ プラットフォームの設定 ](../../migration/using/configuring-your-platform.md) を参照してください。

v6.02 からAdobe Campaign v7 に移行する場合、事前に配信された一部のファイルは配信されません。

クライアントエラーが表示された場合は、新しいAdobe Campaign v7 コードでダッシュボードを更新するか、v6.02 インスタンスから v7 インスタンスに次のファイルを手動でコピーする必要があります。

```
v6.02 files and spaces:
/usr/local/neolane/nl6/datakit/xtk/eng/css/dropDownMenu.css
/usr/local/neolane/nl6/datakit/xtk/eng/js/client/dropDownMenu.js
v6.1 files and spaces:
/usr/local/neolane/nl6/deprecated/xtk/css/dropDownMenu.css
/usr/local/neolane/nl6/deprecated/xtk/js/client/dropDownMenu.js  
```
