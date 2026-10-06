---
product: campaign
title: Federated Data Accessの概要
description: 外部データベースのデータにアクセスして処理する方法を説明します。
feature: Installation, Federated Data Access
exl-id: 9d8d1e9c-63e4-40c4-8338-b921d08ea405
TQID: 'https://experienceleague.adobe.com/X-VyiKlGatskoXtPoLYhb8HrAgCRLLHxTbwXDFmg8jI'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
subfeature_v2:
  - id: e656c701-3899-4db3-989c-de0980ddfffa
    internal-label: Installation
  - id: ee3dfd63-9a21-4961-9f24-ea3385284a21
    internal-label: Federated Data Access
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 47%
---
# Federated Data Accessの概要 {#about-federated-data-access}



Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。

## 前提条件 {#operating-principle}

FDA オプションを使用すると、サードパーティのデータベースでデータモデルを拡張できます。 ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。

この機能を使用するには、次の前提条件が必要です。

* **設定**：互換性のある外部データベースのリストは、[ ホスティングモデル ](../../installation/using/hosting-models.md)によって異なります。
* **外部データベース バージョン**: Adobe Campaign FDA モジュールと互換性のある外部データベースが必要です。

  ホスティングモデルごとのデータベースシステムと互換性のあるバージョンのリストについては、Campaign [互換性マトリックス ](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA)で詳しく説明しています。

* **権限**: Adobe Campaignおよび外部データベースの[必要な権限](../../installation/using/remote-database-access-rights.md)も持っている必要があります。

