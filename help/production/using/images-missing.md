---
title: 画像が見つからない
seo-title: 画像が見つからない
description: 画像が見つからない
seo-description: null
page-status-flag: never-activated
uuid: 0dc73ea0-70bc-476d-bdff-2e62d6929f21
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: e001db7a-7c53-477e-a534-ce4d83d68559
translation-type: tm+mt
source-git-commit: d509dc584cd4ae17c6dda85c09fceee8c6162dba
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 7%

---


# 画像が見つからない{#images-missing}

17.9リリースでは、いくつかのファイル（特にアイコン）が移動されました。

ホストされるお客様の場合、影響はありません。 オンプレミスインストールの場合は、以下をお読みください。

**Apacheユーザー：**

Apacheユーザーが提供された **apache_neolane.confを使用する場合、Apacheユーザーには影響しません**

**IISユーザー：**

IISユーザー(Windows)の場合、ビルドの更新後、コンソールに複数のアイコンが表示されなくなります。 追加のIISの更新手順が必要です：

1. ビルドの更新後、重複が **iis_neolane_setup.vbs** (キャンペーンインストールディレクトリ内)をクリックします。 デフォルトのパスはC:\Program Files (x86)\Adobe\Adobe Campaign v7\confです。
1. 前の手順で更新したIISサイトを再起動します。

