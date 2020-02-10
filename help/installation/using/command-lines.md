---
title: コマンドライン
seo-title: コマンドライン
description: コマンドライン
seo-description: null
page-status-flag: never-activated
uuid: fa897d6a-0326-4922-8936-2471af2f213c
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: appendices
discoiquuid: 3621d4ec-8839-40c3-a574-486c408f79ba
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 46f5bfb41bfe9c938ac0ffa767ead3e47a32047d

---


# コマンドライン{#command-lines}

次のコマンドラインを使用するには、アプリケーションサーバーにアクセスする機能が必要です。 アドビがホストするデプロイメントの場合、これらのコマンドはアドビのみが実行できます。

## インスタンスの作成 {#creating-an-instance}

インスタンスの作成は、次の構文を使用して、コマンドラインを使用して実行できます。

```
nlserver config -addinstance:instance/masques DNS[/lang]
```

( **eng** と **fraは** 、パラメーターの値 `[lang]` です)

コマンド **nlserver config -addinstance:instance1/demo*/eng** を使用すると、DNSマスクdemo*を使用して **instance1** という名前のインスタンスを英語で作成できます。

## データベースの宣言 {#declaring-a-database}

次の構文を使用して、既存のデータベースをコマンドラインからインスタンスに関連付けることができます。

```
nlserver config -setdblogin:[rbdms:]account[:database][/password]@server
```

このパラメーターには、次の値を指定で **`[rdbms]`** きます。

* **postgresql**:PostgreSQLの場合、
* **oracle**:Oracleの場合、
* **mssql**:（Microsoft SQL serverの場合）
* **DB2**:DB2エンジン用に作成されました。

次のコマンドは、 **demo** instanceを、 **campaignアカウントにリンクされた** base6 **(** base6 **)というSQLタイプのサーバを使用して設定します。****** dbsrv server:

```
 nlserver config -setdblogin:db:campaign:myBase/password@dbServer -instance:demo
```

