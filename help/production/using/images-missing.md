---
product: campaign
title: 画像が見つからない
description: 画像が見つからない
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 6ccda57d-f7a3-4501-b2f4-59fcb05f9013
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---

# 画像が見つからない{#images-missing}

17.9リリースでは、いくつかのファイル（特にアイコン）が移動されました。

ホスト型のお客様の場合、影響はありません。 オンプレミスインストールの場合は、以下をお読みください。

**Apacheユーザー：**

提供された&#x200B;**apache_neolane.conf**&#x200B;を使用しているApacheユーザーには影響はありません。

**IISユーザー：**

IISユーザー(Windows)の場合、ビルドの更新後に、コンソールにいくつかのアイコンが表示されません。 追加のIIS更新手順が必要です。

1. ビルドの更新後、Campaignのインストールディレクトリにある&#x200B;**iis_neolane_setup.vbs**&#x200B;をダブルクリックします。 デフォルトのパスはC:\Program Files (x86)\Adobe\Adobe Campaign v7\confです。
1. 前の手順で更新したIISサイトを再起動します。
