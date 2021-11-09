---
product: campaign
title: 外部データベースへのアクセス
description: 外部データベースのデータにアクセスして処理する方法を説明します。
audience: platform
content-type: reference
topic-tags: connectors
exl-id: 9d8d1e9c-63e4-40c4-8338-b921d08ea405
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 50%

---

# Federated Data Access の概要 {#about-federated-data-access}

![](../../assets/v7-only.svg)

Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。

## 前提条件 {#operating-principle}

FDA オプションを使用すると、サードパーティのデータベースでデータモデルを拡張できます。ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。

この機能を使用するための前提条件を次に示します。

* **設定**:Snowflakeを除き、 **オンプレミス** または **ハイブリッド** ホスティングモデルを使用して Federated Data Access を設定します。 [詳細情報](../../installation/using/hosting-models.md)
* **外部データベースのバージョン**:Adobe Campaign FDA モジュールと互換性のある外部データベースが必要です。 データベースシステムと互換性のあるバージョンのリストについて詳しくは、 Campaign を参照してください。 [互換性マトリックス](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA).
* **権限**:また、 [必要な権限](../../installation/using/remote-database-access-rights.md) (Adobe Campaignおよび外部データベース )

