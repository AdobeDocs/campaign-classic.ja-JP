---
product: campaign
title: Federated Data Access の概要
description: 外部データベースのデータにアクセスして処理する方法を説明します。
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
feature: Federated Data Access
exl-id: 9d8d1e9c-63e4-40c4-8338-b921d08ea405
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 47%

---

# Federated Data Access の概要 {#about-federated-data-access}



Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。

## 前提条件 {#operating-principle}

FDA オプションを使用すると、サードパーティのデータベースでデータモデルを拡張できます。ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。

この機能を使用するための前提条件を次に示します。

* **設定**:互換性のある外部データベースのリストは、 [ホスティングモデル](../../installation/using/hosting-models.md).
* **外部データベースのバージョン**:Adobe Campaign FDA モジュールと互換性のある外部データベースが必要です。

  ホスティングモデルごとのデータベースシステムと互換性のあるバージョンのリストについて詳しくは、 Campaign を参照してください。 [互換性マトリックス](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA).

* **権限**:また、 [必要な権限](../../installation/using/remote-database-access-rights.md) (Adobe Campaignおよび外部データベース )

