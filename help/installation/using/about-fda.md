---
product: campaign
title: 外部データベースへのアクセス
description: 外部データベースのデータにアクセスして処理する方法を説明します。
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 9d8d1e9c-63e4-40c4-8338-b921d08ea405
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 50%

---

# Federated Data Accessの概要{#about-federated-data-access}

Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。

## 前提条件 {#operating-principle}

FDA オプションを使用すると、サードパーティのデータベースでデータモデルを拡張できます。ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。

この機能を使用するための前提条件を次に示します。

* **設定**:Snowflakeを除き、Federated Data Accessを設定するに **は、オンプレミス** のハイブリ **** ッドホスティングモデルが必要です。[詳細情報](../../installation/using/hosting-models.md)
* **外部データベースのバージョン**:Adobe Campaign FDAモジュールと互換性のある外部データベースが必要です。データベースシステムと互換性のあるバージョンのリストについて詳しくは、Campaignの[互換性マトリックス](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA)を参照してください。
* **権限**:また、ユーザーは、Adobe Campaignおよび外 [部デ](../../installation/using/remote-database-access-rights.md) ータベースに対する必要な権限も持っている必要があります。

