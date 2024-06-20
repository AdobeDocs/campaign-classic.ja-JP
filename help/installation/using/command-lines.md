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

（ここで、 **eng** および **fra** には、次の値を指定できます。 `[lang]` パラメーター）

コマンド **nlserver config -addinstance:instance1/demo&#42;/eng** という名前のインスタンスを作成できます **instance1** 英語（DNS マスクデモあり）&#42;.

## データベースの宣言 {#declaring-a-database}

コマンドラインから次の構文を使用して、既存のデータベースをインスタンスに関連付けることができます。

```sql
nlserver config -setdblogin:[rbdms:]account[:database][/password]@server
```

には次の値を使用できます **`[rdbms]`** パラメーター：

* **postgresql**:PostgreSQL の場合、
* **oracle**:Oracle用
* **mssql**:Microsoft SQL Server の場合、

次のコマンドは、 **デモ** という SQL タイプサーバーを持つインスタンス **base6**、にリンクされています **campaign** アカウントと **password** 日 **dbsrv** サーバー：

```sql
 nlserver config -setdblogin:db:campaign:myBase/password@dbServer -instance:demo
```
