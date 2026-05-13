---
product: campaign
title: 画像が見つからない
description: 画像が見つからない
feature: Monitoring
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 6ccda57d-f7a3-4501-b2f4-59fcb05f9013
TQID: https://experienceleague.adobe.com/GDlcjvzSGP70FlVGHmnhJHsqC3SFG5Y-kQOohR00j8c
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 5%

---

# 画像が見つからない{#images-missing}



17.9 リリースでは、いくつかのファイル（特にアイコン）が移動されました。

ホスト型のお客様の場合、影響はありません。 オンプレミスでのインストールについては、次をお読みください。

**Apache ユーザー：**

指定された&#x200B;**apache_neolane.conf**&#x200B;を使用する場合、Apache ユーザーに影響はありません。

**IIS ユーザー：**

IIS ユーザー（Windows）の場合、ビルドの更新後にコンソールに複数のアイコンが表示されなくなります。 追加のIIS更新手順が必要です。

1. ビルドの更新後、Campaign インストールディレクトリにある&#x200B;**iis_neolane_setup.vbs**&#x200B;をダブルクリックします。 デフォルトのパスはC:\Program Files （x86）\Adobe\Adobe Campaign v7\confです
1. 前の手順で更新されたIIS サイトを再起動します。
