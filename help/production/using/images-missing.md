---
product: campaign
title: 画像が見つからない
description: 画像が見つからない
feature: Monitoring
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 6ccda57d-f7a3-4501-b2f4-59fcb05f9013
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 11%

---

# 画像が見つからない{#images-missing}



17.9 リリースでは、複数のファイル（特にアイコン）が移動されました。

ホスト型のお客様の場合、影響はありません。 オンプレミスインストールの場合は、以下をお読みください。

**Apache ユーザー：**

Apache ユーザーが提供された **apache_neolane.conf**.

**IIS ユーザー：**

IIS ユーザー (Windows) の場合、ビルドの更新後にコンソールにいくつかのアイコンが表示されません。 追加の IIS 更新手順が必要です。

1. ビルドの更新後、ダブルクリックします。 **iis_neolane_setup.vbs** は Campaign のインストールディレクトリにあります。 デフォルトのパスはC:\Program Files (x86)\Adobe\Adobe Campaign v7\conf です。
1. 前の手順で更新した IIS サイトを再起動します。
