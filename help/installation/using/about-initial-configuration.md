---
solution: Campaign Classic
product: campaign
title: 初期設定について
description: 初期設定について
audience: installation
content-type: reference
topic-tags: initial-configuration
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 5%

---


# 初期設定について{#about-initial-configuration}

Adobe Campaignのインストールが完了したら、制約や技術的なアーキテクチャを使用して効率的に動作するように設定する必要があります。 Adobe Campaignインスタンスを設定する手順については、この章で以下の手順を説明します。

1. インスタンスと関連する接続の作成については、[インスタンスの作成と](../../installation/using/creating-an-instance-and-logging-on.md)へのログを参照してください。
1. データベースの作成と設定については、[データベースの作成と設定](../../installation/using/creating-and-configuring-the-database.md)を参照してください。
1. Adobe Campaignサーバーの設定については、[キャンペーンサーバーの設定](../../installation/using/campaign-server-configuration.md)を参照してください。
1. インスタンスのデプロイについては、「[インスタンスのデプロイ](../../installation/using/deploying-an-instance.md)」を参照してください。

インスタンスの設定は、プロセス（web、mta、wfserverなど）を有効にすることを意味します。 をサーバーで起動し、電子メール送信用、トラッキング用などのモジュールを設定する 各インスタンスに対して、Adobe Campaignプロセスはサーバー上でアクティブ化されます。 詳しくは、[プロセスの有効化](../../installation/using/campaign-server-configuration.md#enabling-processes)を参照してください。

Adobe Campaignの動作を最適化するために、各インスタンスに追加の設定が必要になる場合があります（使用するモジュール、アーキテクチャ、ニーズに応じて異なります）。
