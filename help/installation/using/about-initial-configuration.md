---
title: 初期設定について
seo-title: 初期設定について
description: 初期設定について
seo-description: null
page-status-flag: never-activated
uuid: d873082d-02b2-4840-ad23-fbe30b42da2c
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: initial-configuration
discoiquuid: 8565a453-a7e0-475d-9254-3f948c04d105
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 7%

---


# 初期設定について{#about-initial-configuration}

Adobe Campaignのインストールが完了したら、制約や技術的なアーキテクチャを使用して効率的に動作するように設定する必要があります。 Adobe Campaignインスタンスを設定する手順については、この章で以下の手順を説明します。

1. インスタンスと関連する接続の作成については、「インスタンスの [作成とログオン](../../installation/using/creating-an-instance-and-logging-on.md)」を参照してください。
1. データベースの作成と設定については、「データベースの [作成と設定](../../installation/using/creating-and-configuring-the-database.md)」を参照してください。
1. Adobe Campaignサーバの設定については、「 [キャンペーンサーバの設定](../../installation/using/campaign-server-configuration.md)」を参照してください。
1. インスタンスのデプロイについては、「インスタンスの [デプロイ](../../installation/using/deploying-an-instance.md)」を参照してください。

インスタンスの設定は、プロセス（web、mta、wfserverなど）を有効にすることを意味します。 をサーバーで起動し、電子メール送信用、トラッキング用などのモジュールを設定する 各インスタンスに対して、Adobe Campaignプロセスはサーバー上でアクティブ化されます。 For more on this, refer to [Enabling processes](../../installation/using/campaign-server-configuration.md#enabling-processes).

Adobe Campaignの動作を最適化するために、各インスタンスに追加の設定が必要になる場合があります（使用するモジュール、アーキテクチャ、ニーズに応じて異なります）。
