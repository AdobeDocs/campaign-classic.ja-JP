---
product: campaign
title: 画像が見つからない
description: 画像が見つからない
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 6ccda57d-f7a3-4501-b2f4-59fcb05f9013
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---

# 画像が見つからない{#images-missing}

![](../../assets/v7-only.svg)

17.9 リリースでは、複数のファイル（特にアイコン）が移動されました。

ホスト型のお客様の場合、影響はありません。 オンプレミスインストールの場合は、以下をお読みください。

**Apache ユーザー：**

Apache ユーザーが提供された **apache_neolane.conf**.

**IIS ユーザー：**

IIS ユーザー (Windows) の場合、ビルドの更新後にコンソールにいくつかのアイコンが表示されません。 追加の IIS 更新手順が必要です。

1. ビルドの更新後、ダブルクリックします。 **iis_neolane_setup.vbs** は Campaign インストールディレクトリにあります。 デフォルトのパスはC:\Program Files (x86)\Adobe\Adobe Campaign v7\confです。
1. 前の手順で更新した IIS サイトを再起動します。
