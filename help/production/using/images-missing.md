---
title: 画像が見つかりません
seo-title: 画像が見つかりません
description: 画像が見つかりません
seo-description: null
page-status-flag: never-activated
uuid: 0dc73ea0-70bc-476d-bdff-2e62d6929f21
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: e001db7a-7c53-477e-a534-ce4d83d68559
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# 画像が見つかりません{#images-missing}

17.9リリースでは、いくつかのファイル（特にアイコン）が移動されました。

ホストされるお客様は、影響を受けません。 オンプレミスインストールの場合は、以下をお読みください。

**Apacheユーザー：**

Apacheユーザーが提供された **apache_neolane.conf**

**IISユーザー：**

IISユーザー(Windows)の場合、ビルドの更新後、コンソールに複数のアイコンが表示されません。 追加のIISの更新手順が必要です：

1. ビルドの更新後、Campaignのインストールディレクトリにある **iis_neolane_setup.vbs** をダブルクリックします。 デフォルトのパスは、C:Program Files (x86)AdobeAdobe Campaign v7tomcat-7confです。
1. 前の手順で更新したIISサイトを再起動します。

