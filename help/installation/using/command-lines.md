---
product: campaign
title: コマンドライン
description: コマンドライン
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: appendices
exl-id: 5cd4abb0-2bd2-4b23-902c-41b08a1d2f7a
source-git-commit: f032ed3bdc0b402c8281bc34e6cb29f3c575aaf9
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# コマンドライン{#command-lines}



次のコマンドラインでは、アプリケーションサーバーにアクセスできる必要があります。 Adobeがホストするデプロイメントの場合、これらのコマンドはAdobeのみが実行できます。

## インスタンスの作成 {#creating-an-instance}

インスタンスの作成は、コマンドラインを使用して次の構文で実行できます。

```sql
nlserver config -addinstance:instance/masques DNS[/lang]
```

（ここで **eng** および **fra** は、`[lang]` パラメーターの使用可能な値です）

**nlserver config -addinstance:instance1/demo&#42;/eng** コマンドを使用すると、DNS マスク demo&#42; を使用して英語で **instance1** というインスタンスを作成できます。

## データベースの宣言 {#declaring-a-database}

コマンドラインから次の構文を使用して、既存のデータベースをインスタンスに関連付けることができます。

```sql
nlserver config -setdblogin:[rbdms:]account[:database][/password]@server
```

**`[rdbms]`** パラメーターには、次の値を使用できます。

* **postgresql**:PostgreSQL の場合、
* **oracle**:Oracleの
* **mssql**:Microsoft SQL Server の場合、

次のコマンドは、**dbsrv** サーバー上の **campaign** アカウントとその **password** にリンクされた **base6** という SQL タイプサーバーを持つ **demo** インスタンスを設定します。

```sql
 nlserver config -setdblogin:db:campaign:myBase/password@dbServer -instance:demo
```
