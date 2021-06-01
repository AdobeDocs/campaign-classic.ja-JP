---
product: campaign
title: コマンドライン
description: コマンドライン
audience: installation
content-type: reference
topic-tags: appendices
exl-id: 5cd4abb0-2bd2-4b23-902c-41b08a1d2f7a
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# コマンドライン{#command-lines}

次のコマンドラインでは、アプリケーションサーバーにアクセスする機能が必要です。 Adobeがホストするデプロイメントでは、これらのコマンドはAdobeのみ実行できます。

## インスタンス{#creating-an-instance}の作成

インスタンスの作成は、次の構文を使用して、コマンドラインを使用して実行できます。

```
nlserver config -addinstance:instance/masques DNS[/lang]
```

（ここで、**eng**&#x200B;と&#x200B;**fra**&#x200B;は`[lang]`パラメーターに使用できる値です）。

コマンド&#x200B;**nlserver config -addinstance:instance1/demo*/eng**&#x200B;を使用して、DNSマスクdemo*を使用して、**instance1**&#x200B;という名前のインスタンスを英語で作成できます。

## データベース{#declaring-a-database}を宣言します。

次の構文を使用して、既存のデータベースをコマンドラインからインスタンスに関連付けることができます。

```
nlserver config -setdblogin:[rbdms:]account[:database][/password]@server
```

**`[rdbms]`**&#x200B;パラメーターには、次の値を指定できます。

* **postgresql**:（PostgreSQLの場合）
* **oracle**:oracle
* **mssql**:（Microsoft SQL Serverの場合）
* **DB2**:（DB2エンジン用）

次のコマンドは、**campaign**&#x200B;アカウントと&#x200B;**password** （**dbsrv**&#x200B;サーバー上）にリンクされたSQLタイプのサーバー&#x200B;**base6**&#x200B;を使用して&#x200B;**demo**&#x200B;インスタンスを設定します。

```
 nlserver config -setdblogin:db:campaign:myBase/password@dbServer -instance:demo
```
