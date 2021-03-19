---
solution: Campaign Classic
product: campaign
title: コマンドライン
description: コマンドライン
audience: installation
content-type: reference
topic-tags: appendices
translation-type: tm+mt
source-git-commit: 95d0686c4ddeb4e25eb918ca92cbd6a0b1aa1f3c
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---


# コマンドライン{#command-lines}

次のコマンドラインを使用するには、アプリケーションサーバーにアクセスする機能が必要です。 Adobeがホストする配置では、これらのコマンドはAdobeのみが実行できます。

## インスタンス{#creating-an-instance}を作成

インスタンスの作成は、次の構文を使用して、コマンドラインを使用して実行できます。

```
nlserver config -addinstance:instance/masques DNS[/lang]
```

（ここで&#x200B;**eng**&#x200B;と&#x200B;**fra**&#x200B;は、`[lang]`パラメーターに指定できる値です）。

**nlserver config -addinstance:instance1/demo*/eng**&#x200B;コマンドを使用すると、**instance1**&#x200B;という名前のインスタンスを英語で作成し、DNSマスクdemo*を使用できます。

## データベース{#declaring-a-database}を宣言

次の構文を使用して、既存のデータベースをコマンドラインからインスタンスに関連付けることができます。

```
nlserver config -setdblogin:[rbdms:]account[:database][/password]@server
```

**`[rdbms]`**&#x200B;パラメーターには次の値を指定できます。

* **postgresql**:PostgreSQLの場合、
* **oracle**:oracleのために
* **mssql**:Microsoft SQL Serverの場合、
* **DB2**:（DB2エンジン用）

次のコマンドは、**dbsrv**&#x200B;サーバーの&#x200B;**キャンペーン**&#x200B;アカウントと&#x200B;**パスワード**&#x200B;にリンクされた&#x200B;**base6**&#x200B;と呼ばれるSQLタイプのサーバーを使用して&#x200B;**demo**&#x200B;インスタンスを設定します。

```
 nlserver config -setdblogin:db:campaign:myBase/password@dbServer -instance:demo
```

