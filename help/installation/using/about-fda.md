---
title: 外部データベースへのアクセス
description: 外部データベースのデータにアクセスして処理する方法を説明します。
page-status-flag: never-activated
uuid: b84359b9-c584-431d-80d5-71146d9b6854
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: connectors
discoiquuid: dd3d14cc-5153-428d-a98a-32b46f0fe811
translation-type: tm+mt
source-git-commit: 99d766cb6234347ea2975f3c08a6ac0496619b41
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 39%

---


# Federated Data Accessの概要 {#about-federated-data-access}

Adobe Campaign では、**Federated Data Access**（FDA）オプションを利用することができます。このオプションを使用すると、1 つ以上の外部データベースに格納されている情報を処理することが可能です。Adobe Campaign データの構造を変更しなくても、外部データにアクセスできます。

## 前提条件 {#operating-principle}

FDA オプションを使用すると、サードパーティのデータベースでデータモデルを拡張できます。ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。

この機能を使用するための前提条件は次のとおりです。

* **設定**:snowflakeを除き、Federated Data Accessを設定するには、 **オンプレミス** または **ハイブリッド** ホスティングモデルが必要です。 [詳細情報](../../installation/using/hosting-models.md)
* **外部データベースのバージョン**:adobe campaignFDAモジュールと互換性のある外部データベースが必要です。 The list of database systems and compatible versions is detailed in Campaign [Compatibility matrix](../../rn/using/compatibility-matrix.md#FederatedDataAccessFDA).
* **権限**:また、Adobe Campaignおよび外部データベースに [必要な権限](../../installation/using/remote-database-access-rights.md) も持っている必要があります。

## 制限事項{#limitations}

FDA オプションは、ワークフローにおいて外部データベースのデータをバッチモードで操作するように設計されています。パフォーマンスの問題を回避するために、次のような単一の操作のコンテキストでは、FDAモジュールを使用しないことをお勧めします。パーソナライゼーション、インタラクション、リアルタイムメッセージングなど

Adobe Campaign と外部データベースの両方を使用する必要がある操作は、できるだけおこなわないようにします。これは、次のような方法で回避できます。

* Adobe Campaign データベースを外部データベースにエクスポートし、外部データベースからのみ操作を実行して、その結果を Adobe Campaign に再インポートします。

* 外部の Adobe Campaign データベースからデータを収集し、ローカルで操作を実行します。

外部データベースのデータを使用する配信でパーソナライゼーションを実行する場合は、ワークフローで使用するデータを収集して一時テーブルに格納してから、一時テーブルのデータを使用して配信をパーソナライズします。

FDAオプションは、使用する外部データベースシステムの制限を受ける場合があります。

## 推奨事項 {#recommendations}

### 一時スキーマの作成 {#create-temporary-schemas}

Greenplum外部データベースへのアクセスは、FDAを通じて複数管理できます。 専用のオプションを使用すると、外部アカウントの設定時に作業スキーマを直接作成できます。

![](assets/fda_work_table.png)

>[!NOTE]
>
>このオプションはPostgreSQL Greenplumでのみ使用できます。

### Optimize email personalization with external data {#optimizing-email-personalization-with-external-data}

メッセージのパーソナライゼーションを専用のワークフローで事前に処理できます。 これを実行するには、配信プロパティの「 **[!UICONTROL 分析]** 」タブにある「ワークフローを使用してパーソナライズデータを準備する **** 」オプションを使用します。

配信の分析中、このオプションは、ターゲットにリンクされたすべてのデータ（外部データベースにリンクされたテーブルのデータを含む）を一時テーブルに保存するワークフローを自動的に作成し、実行します。

このオプションは、パーソナライゼーション手順を実行する際のパフォーマンスを大幅に向上させます。

### Use data from an external database in a workflow {#using-data-from-an-external-database-in-a-workflow}

複数のAdobe Campaignワークフローアクティビティでは、外部データベースに保存されたデータを使用できます。

* **外部データに対するフィルター** - [](../../workflow/using/targeting-data.md#selecting-data) クエリアクティビティを使用すると、外部データを追加して、定義済みのフィルター設定で使用できます。 詳しくは、[このページ](../../workflow/using/targeting-data.md#selecting-data)を参照してください。

* **サブセットの作成** - 「 [分割](../../workflow/using/split.md) 」アクティビティを使用すると、サブセットを作成できます。 外部データを使用して、使用するフィルタリング条件を定義できます。詳しくは、[このページ](../../workflow/using/split.md)を参照してください。

* **外部データベースのロード** — 外部データは、 [データ・ロード](../../workflow/using/data-loading--rdbms-.md) (RDBMS)アクティビティで使用できます。 Learn more in [this page](../../workflow/using/data-loading--rdbms-.md).

* **情報とリンクの追加** - [](../../workflow/using/enrichment.md) エンリッチメントアクティビティを使用すると、ワークフローのワークテーブルに追加のデータを追加したり、外部テーブルにリンクを追加したりできます。 このコンテキストでは、外部データベースのデータを使用できます。 Learn more in [this page](../../workflow/using/enrichment.md).
