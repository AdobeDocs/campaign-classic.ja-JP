---
title: 環境の複製
seo-title: 環境の複製
description: 環境の複製
seo-description: null
page-status-flag: never-activated
uuid: b8fb8083-e3ec-4b1c-9449-73ac03508d89
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: data-processing
discoiquuid: 9f7118f4-aef0-469c-bbe1-b62bed674faa
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 779d9162b7296339a796512838612ede1186ddcc

---


# 環境の複製{#duplicating-environments}

## はじめに {#introduction}

### 概要 {#overview}

>[!CAUTION]
>
>サーバーとデータベース（ホスト環境）にアクセスできない場合は、以下に説明する手順を実行できません。 アドビにお問い合わせください。

Adobe Campaignを使用するには、1つ以上の環境をインストールして設定する必要があります。開発、テスト、実稼働前、実稼働など

各環境にはAdobe Campaignインスタンスが含まれ、各Adobe Campaignインスタンスは1つ以上のデータベースにリンクされています。 アプリケーションサーバーは、1つ以上のプロセスを実行できます。これらのほとんどは、インスタンスデータベースに直接アクセスできます。

この節では、Adobe Campaign環境の複製（ソース環境をターゲット環境に復元する場合など）に適用されるプロセスについて詳しく説明します。その結果、2つの同じ作業環境が作成されます。

それには、次の手順に従います。

1. ソース環境のすべてのインスタンスにデータベースのコピーを作成し、
1. ターゲット環境のすべてのインスタンスに対してこれらのコピーを復元し、
1. 起動する **前に、ターゲット環境でnms:freezeInstance.js** cauterizationスクリプトを実行します。

   このプロセスは、サーバーとその設定には影響しません。

   >[!NOTE]
   >
   >Adobe Campaignのコンテキストでは、焼灼は **** 、外部との対話をすべてのプロセスに停止させるアクションを組み合わせます。ログ、追跡、配信、キャンペーンワークフローなど\
   >この手順は、メッセージを複数回（通常の環境から1回、複製された環境から1回）配信しないようにするために必要です。

   >[!CAUTION]
   >
   >1つの環境に複数のインスタンスを含めることができます。 各Adobe Campaignインスタンスにはライセンス契約が適用されます。 使用許諾契約書を確認して、使用できる環境の数を確認します。\
   >以下の手順では、インストールした環境とインスタンスの数に影響を与えることなく、環境を転送できます。

### 始める前に {#before-you-start}

>[!CAUTION]
>
>転送プロセスを開始する前に、ソース環境とターゲット環境のすべてのインスタンスに対して、データベースの完全バックアップを実行することを強くお勧めします。 この方法で問題が発生した場合は、バックアップを復元して初期設定に戻すことができます。

このプロセスが機能するには、ソース環境とターゲット環境のインスタンス数、同じ目的（マーケティングインスタンス、配信インスタンス）および同様の設定が必要です。 技術構成は、ソフトウェアの前提条件を満たす必要があります。 両方の環境に同じコンポーネントをインストールする必要があります。

## 実装 {#implementation}

### 移送手順 {#transfer-procedure}

この節では、ケーススタディを使用してソース環境をターゲット環境に移行する際に必要な手順を説明します。ここでの目的は、実稼働環境(**prod** instance)を開発環境(**dev** instance)に復元し、「実稼働」プラットフォームにできるだけ近いコンテキストで動作させることです。

次の手順は慎重に実行する必要があります。ソース環境のデータベースをコピーする際に、一部のプロセスが進行中である場合があります。 焼灼（下の手順3）は、メッセージが2回送信されるのを防ぎ、データの一貫性を維持します。

>[!CAUTION]
>
>* 以下のプロシージャはPostgreSQL言語で有効です。 SQL言語が異なる場合（Oracleなど）、SQLクエリーを適合させる必要があります。
>* 以下のコマンドは、PostgreSQLの下のprodインスタンスと **dev** インスタンスのコンテキ **スト内に適用されます** 。
>



### 手順1 — ソース環境（実稼動環境）のデータのバックアップを作成する {#step-1---make-a-backup-of-the-source-environment--prod--data}

データベースのコピー

まず、すべてのソース環境データベースをコピーします。 操作はデータベースエンジンに依存し、データベース管理者の責任を負います。

PostgreSQLでは、次のコマンドが実行されます。

```
pg_dump mydatabase > mydatabase.sql
```

### 手順2 — ターゲット環境設定（開発）のエクスポート {#step-2---export-the-target-environment-configuration--dev-}

ほとんどの設定要素は、環境ごとに異なります。外部アカウント（ミッドソーシング、ルーティングなど）、技術オプション（プラットフォーム名、DatabaseId、電子メールアドレス、デフォルトURLなど）。

ソース・データベースをターゲット・データベースに保存する前に、ターゲット環境（開発環境）の設定をエクスポートする必要があります。 これを行うには、次の2つのテーブルのコンテンツをエクスポートします。xtkoption **と** nmsextaccount ****。

この書き出しにより、開発環境の設定を維持し、開発データ（ワークフロー、テンプレート、Webアプリケーション、受信者など）のみを更新できます。

これを行うには、次の2つの要素に対してパッケージのエクスポートを実行します。

* xtk:option **テーブルを** &#39;options_dev.xml&#39;ファイルに書き出します。次の内部名を持つレコードは含めません。&#39;WdbcTimeZone&#39;、&#39;NmsServer_LastPostUpgrade&#39;、および&#39;NmsBroadcast_RegexRules&#39;。
* 「extaccount_dev.xml」ファイルで、 **** nms:extAccountテーブルを書き出し、IDが0(@id &lt;> 0)でないすべてのレコードを取得します。

書き出したオプション/アカウントの数が、各ファイルで書き出す行数と等しいことを確認します。

>[!NOTE]
>
>パッケージエクスポートでエクスポートする行の数は1,000行です。 オプションまたは外部アカウントの数が1,000を超える場合は、複数のエクスポートを実行する必要があります。
> 
>詳しくは、[この節](../../platform/using/working-with-data-packages.md#exporting-packages)を参照してください。

### 手順3 — ターゲット環境（開発）を停止する {#step-3---stop-the-target-environment--dev-}

Adobe Campaignのプロセスは、すべてのターゲット環境サーバーで停止する必要があります。 この操作は、オペレーティングシステムによって異なります。

すべてのプロセスを停止することも、データベースに書き込むプロセスのみを停止することもできます。

すべてのプロセスを停止するには、次のコマンドを使用します。

* Windowsの場合：

   ```
   net stop nlserver6
   ```

* Linuxの場合：

   ```
   /etc/init.d/nlserver6 stop
   ```

次のコマンドを使用して、すべてのプロセスが停止していることを確認します。

```
nlserver pdump
```

>[!NOTE]
>
>Windowsでは、他の操作に影響を与え **ることなく** 、Webmdlプロセスをアクティブにすることができます。

また、実行中のシステムプロセスがないことを確認することもできます。

それには、次の手順に従います。

* Windowsの場合：タスクマネ **ージャーを開き** 、nlserver.exeプロセスがないこ **とを確認します** 。
* Linuxの場合：パスオーを **実行する| grep nlserver** コマンドを実行し、nlserverプロセスが存在しないこ **とを確認** 。

### 手順4 — ターゲット環境（開発環境）でデータベースを復元する {#step-4---restore-the-databases-in-the-target-environment--dev-}

ターゲット環境でソース・データベースをリストアするには、次のコマンドを使用します。

```
psql mydatabase < mydatabase.sql
```

### 手順5 — ターゲット環境（開発）を焼灼する {#step-5---cauterize-the-target-environment--dev-}

誤動作を防ぐために、配信送信とワークフローの実行にリンクされたプロセスを、対象の環境がアクティブ化されたときに自動的に実行しないようにする必要があります。

これを行うには、次のコマンドを実行します。

```
nlserver javascript nms:freezeInstance.js -instance:<dev> -arg:run
```

### ステップ6 — 注意を確認する {#step-6---check-cauterization}

1. IDが0に設定されている配信パーツが唯一の配信パーツであることを確認します。

   ```
   SELECT * FROM neolane.nmsdeliverypart;
   ```

1. 配信ステータスが正しく更新されていることを確認します。

   ```
   SELECT iState, count(*) FROM neolane.nmsdelivery GROUP BY iState;
   ```

1. ワークフローのステータスが正しく更新されていることを確認します。

   ```
   SELECT iState, count(*) FROM neolane.xtkworkflow GROUP BY iState;
   SELECT iStatus, count(*) FROM neolane.xtkworkflow GROUP BY iStatus;
   ```

### 手順7 — ターゲット環境のWebプロセス（開発環境）を再起動する {#step-7---restart-the-target-environment-web-process--dev-}

ターゲット環境で、すべてのサーバーのAdobe Campaignプロセスを再起動します。

>[!NOTE]
>
>開発環境でAdobe Campaignを再起動する前に **** 、次の追加の安全手順を適用できます。webモジュール **のみを起動し** ます。
>  
>これを行うには、インスタンスの設定ファイル(**config-dev.xml**)を編集し、各モジュール（mta、statなど）のautoStart=&quot;true&quot;オプションの前に「_」文字を追加します。

次のコマンドを実行して、Webプロセスを開始します。

```
nlserver start web
```

次のコマンドを使用して、Webプロセスのみが開始されていることを確認します。

```
nlserver pdump
```

クライアントコンソールへのアクセス機能を確認します。

### 手順8 — ターゲット環境（開発環境）へのオプションと外部アカウントのインポート {#step-8---import-options-and-external-accounts-into-the-target-environment--dev-}

>[!CAUTION]
>
>この手順では、Webプロセスのみを開始する必要があります。 そうでない場合は、他の実行中のプロセスを停止してから続行してください

特に、読み込む前に、ファイルの複数行の値を確認します(例：オプション表の&#39;NmsTracking_Pointer&#39;と、外部アカウント表の配信または中間ソーシングアカウント)

ターゲット環境データベース（開発環境）から設定を読み込むには：

1. データベースの管理コンソールを開き、IDが0(@id &lt;> 0)でない外部アカウント（テーブルnms:extAccount）を削除します。
1. Adobe Campaignコンソールで、パッケージのインポート機能を使用して以前に作成したoptions_dev.xmlパッケージをインポートします。

   ノード内のオプションが実際に更新されていることを確認 **[!UICONTROL Administration > Platform > Options]** します。

1. Adobe Campaignコンソールで、パッケージのインポート機能を使用して以前に作成したextaccount_dev.xmlをインポートします

   に外部データベースがインポートされていることを確認しま **[!UICONTROL Administration > Platform > External accounts]** す。

### 手順9 — すべてのプロセスを再起動し、ユーザーを変更する（開発） {#step-9---restart-all-processes-and-change-users--dev-}

Adobe Campaignプロセスを開始するには、次のコマンドを使用します。

* Windowsの場合：

   ```
   net start nlserver6
   ```

* Linuxの場合：

   ```
   /etc/init.d/nlserver6 start
   ```

次のコマンドを使用して、プロセスが起動していることを確認します。

```
nlserver pdump
```

ユーザーを変更して、開発プラットフォームに既に存在するユーザーを検索します。
