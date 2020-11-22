---
solution: Campaign Classic
product: campaign
title: 画像が見つからない
description: 画像が見つからない
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 5%

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

