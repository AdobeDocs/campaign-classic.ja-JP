---
product: campaign
title: コマンドライン
description: コマンドライン
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: appendices
exl-id: 5cd4abb0-2bd2-4b23-902c-41b08a1d2f7a
TQID: https://experienceleague.adobe.com/e85vFL0iZ586ICGGH1CP6fgqGU717W1aPDWqmj40-3s
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 144
ht-degree: 4%

---

# コマンドライン{#command-lines}



次のコマンドラインでは、アプリケーションサーバーにアクセスする機能が必要です。 Adobeでホストされているデプロイメントの場合、これらのコマンドはAdobeでのみ実行できます。

## インスタンスの作成 {#creating-an-instance}

インスタンス作成は、次の構文でコマンドラインを使用して実行できます。

```sql
nlserver config -addinstance:instance/masques DNS[/lang]
```

（**eng**&#x200B;および&#x200B;**fra**&#x200B;は、`[lang]` パラメーターで指定できる値です）

コマンド **nlserver config -addinstance:instance1/demo&#42;/eng**&#x200B;を使用すると、**instance1**&#x200B;という名前のインスタンスを英語でDNS マスクデモ &#42;と共に作成できます。

## データベースの宣言 {#declaring-a-database}

既存のデータベースをコマンドラインからインスタンスに関連付けるには、次の構文を使用します。

```sql
nlserver config -setdblogin:[rbdms:]account[:database][/password]@server
```

**`[rdbms]`** パラメーターには次の値を指定できます。

* **postgresql**: PostgreSQLの場合
* **oracle**: Oracleの場合
* **mssql**: Microsoft SQL Serverの場合、

次のコマンドは、**campaign** アカウントとその&#x200B;**password**&#x200B;にリンクされた&#x200B;**base6**&#x200B;というSQL タイプのサーバーを&#x200B;**dbsrv** サーバー上に&#x200B;**demo** インスタンスに設定します。

```sql
 nlserver config -setdblogin:db:campaign:myBase/password@dbServer -instance:demo
```
