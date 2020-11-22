---
solution: Campaign Classic
product: campaign
title: コマンドライン
description: コマンドライン
audience: installation
content-type: reference
topic-tags: appendices
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---


# コマンドライン{#command-lines}

次のコマンドラインを使用するには、アプリケーションサーバーにアクセスする機能が必要です。 Adobeがホストする配置では、これらのコマンドはAdobeのみが実行できます。

## インスタンスの作成 {#creating-an-instance}

インスタンスの作成は、次の構文を使用して、コマンドラインを使用して実行できます。

```
nlserver config -addinstance:instance/masques DNS[/lang]
```

( **eng** と **fra** は、 `[lang]` パラメータに指定できる値です)。

コマンド **nlserver config -addinstance:instance1/demo*/eng** を使用すると、DNSマスクdemo*を使用して、 **instance1** という名前のインスタンスを英語で作成できます。

## データベースの宣言 {#declaring-a-database}

次の構文を使用して、既存のデータベースをコマンドラインからインスタンスに関連付けることができます。

```
nlserver config -setdblogin:[rbdms:]account[:database][/password]@server
```

この **`[rdbms]`** パラメーターには次の値を指定できます。

* **postgresql**:PostgreSQLの場合、
* **oracle**:oracleは
* **mssql**:Microsoft SQL Serverの場合、
* **DB2**:（DB2エンジン用）

次のコマンドは、 **キャンペーンにリンクされたSQLタイプserver** base6 **というSQLタイプserverを使用して** demo **インスタンスを設定します。 accountはdbsrv********** srv serverに対してpasswordを設定します。

```
 nlserver config -setdblogin:db:campaign:myBase/password@dbServer -instance:demo
```

