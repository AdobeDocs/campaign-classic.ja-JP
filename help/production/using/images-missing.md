---
solution: Campaign Classic
product: campaign
title: 画像が見つからない
description: 画像が見つからない
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 50f95d7156e7104d90fa7a31eea30711b9c11bbf
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---


# 画像が見つからない{#images-missing}

17.9リリースでは、いくつかのファイル（特にアイコン）が移動されました。

ホストされるお客様の場合、影響はありません。 オンプレミスインストールの場合は、以下をお読みください。

**Apacheユーザー：**

Apacheユーザーは、提供された&#x200B;**apache_neolane.conf**&#x200B;を使用する場合、影響を受けません。

**IISユーザー：**

IISユーザー(Windows)の場合、ビルドの更新後、コンソールに複数のアイコンが表示されなくなります。 追加のIISの更新手順が必要です：

1. ビルドの更新後、重複がキャンペーンのインストールディレクトリにある&#x200B;**iis_neolane_setup.vbs**&#x200B;をクリックします。 デフォルトのパスはC:\Program Files (x86)\Adobe\Adobe Campaign v7\confです。
1. 前の手順で更新したIISサイトを再起動します。
