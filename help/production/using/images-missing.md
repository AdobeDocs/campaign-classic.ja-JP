---
product: campaign
title: 画像が見つからない
description: 画像が見つからない
feature: Monitoring
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 6ccda57d-f7a3-4501-b2f4-59fcb05f9013
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 5%

---

# 画像が見つからない{#images-missing}



17.9 リリースでは、複数のファイル（特にアイコン）が移動されています。

ホスト環境のお客様の場合は、影響はありません。 オンプレミスインストールの場合は、次をお読みください。

**Apache ユーザー：**

提供されたを Apache ユーザーが使用しても、影響はありません **apache_neolane.conf**.

**IIS ユーザー：**

（Windows の） IIS ユーザーの場合、ビルドの更新後、コンソールに複数のアイコンが表示されません。 追加の IIS 更新手順が必要です。

1. ビルドの更新後、 **iis_neolane_setup.vbs** campaign インストールディレクトリの中にあります。 デフォルトのパスはC:\Program Files （x86）\Adobe\Adobe Campaign v7\conf です
1. 前の手順で更新した IIS サイトを再起動します。
