---
solution: Campaign Classic
product: campaign
title: 初期設定について
description: 初期設定について
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: f77ba178-0dfb-4a2e-b33b-971765d42298
translation-type: tm+mt
source-git-commit: b0a1e0596e985998f1a1d02236f9359d0482624f
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%

---

# インスタンスの設定とデプロイの主な手順{#about-initial-configuration}

Adobe Campaignのインストールが完了したら、制約や技術的なアーキテクチャを使用して効率的に動作するように設定する必要があります。 Adobe Campaignインスタンスを設定する手順については、この章で以下の手順を説明します。

1. インスタンスと関連する接続を作成します。詳しくは、[インスタンスの作成と](../../installation/using/creating-an-instance-and-logging-on.md)へのログを参照してください。
1. データベースの作成と設定については、[データベースの作成と設定](../../installation/using/creating-and-configuring-the-database.md)を参照してください。
1. Adobe Campaignサーバーを設定します。[キャンペーンサーバーの設定](../../installation/using/configuring-campaign-server.md)を参照してください。
1. インスタンスをデプロイする方法については、[インスタンスのデプロイ](../../installation/using/deploying-an-instance.md)を参照してください。

インスタンスの設定は、プロセス（web、mta、wfserverなど）を有効にすることを意味します。 をサーバーで起動し、電子メール送信用、トラッキング用などのモジュールを設定する 各インスタンスに対して、Adobe Campaignプロセスはサーバー上でアクティブ化されます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

Adobe Campaignの動作を最適化するために、各インスタンスに追加の設定が必要になる場合があります（使用するモジュール、アーキテクチャ、ニーズに応じて異なります）。
