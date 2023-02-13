---
product: campaign
title: コマンドライン
description: コマンドライン
audience: installation
content-type: reference
topic-tags: appendices
exl-id: 5cd4abb0-2bd2-4b23-902c-41b08a1d2f7a
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# コマンドライン{#command-lines}

![](../../assets/v7-only.svg)

次のコマンドラインでは、アプリケーションサーバーにアクセスする機能が必要です。 Adobeがホストするデプロイメントの場合、これらのコマンドはAdobeのみ実行できます。

## インスタンスの作成 {#creating-an-instance}

インスタンスの作成は、次の構文を使用して、コマンドラインを使用して実行できます。

```
nlserver config -addinstance:instance/masques DNS[/lang]
```

( **eng** および **fra** は、 `[lang]` パラメータ )

コマンド **nlserver config -addinstance:instance1/demo&#42;/eng** を使用すると、 **instance1** 英語（DNS マスクデモを使用）&#42;.

## データベースを宣言 {#declaring-a-database}

次の構文を使用して、既存のデータベースをコマンドラインからインスタンスに関連付けることができます。

```
nlserver config -setdblogin:[rbdms:]account[:database][/password]@server
```

以下の値が **`[rdbms]`** パラメーター：

* **postgresql**:（PostgreSQL の場合）
* **oracle**:oracle
* **mssql**:Microsoft SQL Server の場合、
* **DB2**:DB2 エンジン用。

次のコマンドは、 **デモ** 次の SQL タイプのサーバーを持つインスタンス： **base6**、 **campaign** アカウントとその **パスワード** の **dbsrv** サーバ：

```
 nlserver config -setdblogin:db:campaign:myBase/password@dbServer -instance:demo
```
