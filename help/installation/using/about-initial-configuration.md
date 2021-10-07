---
product: campaign
title: 初期設定について
description: 初期設定について
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: f77ba178-0dfb-4a2e-b33b-971765d42298
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%

---

# インスタンスの設定およびデプロイの主な手順{#about-initial-configuration}

![](../../assets/v7-only.svg)

Adobe Campaignのインストールが完了したら、制約と技術アーキテクチャで効率的に動作するように設定する必要があります。 Adobe Campaignインスタンスを設定する手順については、この章で次の順に説明します。

1. インスタンスと関連する接続を作成します。[ インスタンスの作成と ](../../installation/using/creating-an-instance-and-logging-on.md) へのログオンを参照してください。
1. データベースを作成して設定する方法については、[ データベースの作成と設定 ](../../installation/using/creating-and-configuring-the-database.md) を参照してください。
1. Adobe Campaignサーバーを設定します。[Campaign サーバーの設定 ](../../installation/using/configuring-campaign-server.md) を参照してください。
1. インスタンスをデプロイする方法については、[ インスタンスのデプロイ ](../../installation/using/deploying-an-instance.md) を参照してください。

インスタンスの設定は、プロセス（web、mta、wfserver など）を有効にすることを意味します。 をサーバー上で起動し、電子メールを送信するためのモジュールや、トラッキング用のモジュールなどを設定する 各インスタンスに対して、Adobe Campaignプロセスがサーバーでアクティブ化されます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

Adobe Campaignの操作を最適化するには、（使用するモジュール、アーキテクチャ、ニーズに応じて）各インスタンスに追加の設定が必要になる場合があります。
