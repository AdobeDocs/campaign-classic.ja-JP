---
solution: Campaign Classic
product: campaign
title: 外部データベースへのアクセス
description: 外部データベースのデータにアクセスして処理する方法を説明します。
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 9d8d1e9c-63e4-40c4-8338-b921d08ea405
translation-type: tm+mt
source-git-commit: 37802e52f1d1d38d9c3d59c439f23114a594bfef
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 50%

---

# Federated Data Accessを使用する前に{#about-federated-data-access}

Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。

## 前提条件 {#operating-principle}

FDA オプションを使用すると、サードパーティのデータベースでデータモデルを拡張できます。ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。

この機能を使用するための前提条件は次のとおりです。

* **設定**:Snowflakeを除き、Federated Data Accessを設定するには、 **On-** Premiserまたは **** ハイブリッドホストモデルが必要です。[詳細情報](../../installation/using/hosting-models.md)
* **外部データベースのバージョン**:Adobe CampaignFDAモジュールと互換性のある外部データベースが必要です。データベースシステムと互換性のあるバージョンのリストについては、キャンペーン[互換性マトリックス](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA)で詳しく説明しています。
* **権限**:また、Adobe Campaignおよび外部データベースに [必要な](../../installation/using/remote-database-access-rights.md) 権限も持っている必要があります。

