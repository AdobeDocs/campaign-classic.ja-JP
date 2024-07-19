---
product: campaign
title: Federated Data Access の基本を学ぶ
description: 外部データベースのデータにアクセスして処理する方法を説明します。
feature: Installation, Federated Data Access
exl-id: 9d8d1e9c-63e4-40c4-8338-b921d08ea405
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 47%

---

# Federated Data Access の基本を学ぶ {#about-federated-data-access}



Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。

## 前提条件 {#operating-principle}

FDA オプションを使用すると、サードパーティのデータベースでデータモデルを拡張できます。ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。

この機能を使用するために、前提条件を以下に示します。

* **設定**：互換性のある外部データベースのリストは、[ ホスティングモデル ](../../installation/using/hosting-models.md) によって異なります。
* **外部データベースバージョン**:Adobe Campaign FDA モジュールと互換性のある外部データベースが必要です。

  ホスティングモデルごとのデータベースシステムと互換性のあるバージョンのリストについては、Campaign[ 互換性マトリックス ](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA) を参照してください。

* **権限**：ユーザーは、Adobe Campaignおよび外部データベースで [ 必要な権限 ](../../installation/using/remote-database-access-rights.md) を持っている必要もあります。

