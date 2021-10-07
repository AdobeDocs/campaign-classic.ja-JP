---
product: campaign
title: 環境の複製
description: 環境の複製
audience: production
content-type: reference
topic-tags: data-processing
exl-id: 2c933fc5-1c0a-4c2f-9ff2-90d09a79c55a
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 3%

---

# 環境の複製{#duplicating-environments}

![](../../assets/v7-only.svg)

## はじめに {#introduction}

### 概要 {#overview}

>[!IMPORTANT]
>
>サーバーとデータベース（ホスト環境）にアクセスできない場合、以下に説明する手順を実行できません。 Adobeに連絡。

Adobe Campaignを使用するには、1 つ以上の環境をインストールして設定する必要があります。開発、テスト、プリプロダクション、実稼動など

各環境には 1 つのAdobe Campaignインスタンスが含まれ、各Adobe Campaignインスタンスは 1 つ以上のデータベースにリンクされています。 アプリケーションサーバーは、1 つ以上のプロセスを実行できます。ほとんどの場合、これらはインスタンスデータベースに直接アクセスできます。

この節では、Adobe Campaign環境の複製に適用するプロセスについて詳しく説明します。例えば、ソース環境をターゲット環境に復元する場合、2 つの同じ作業環境が作成されます。

それには、次の手順に従います。

1. ソース環境内のすべてのインスタンスにデータベースのコピーを作成します。
1. ターゲット環境のすべてのインスタンスにこれらのコピーを復元
1. 起動前に、ターゲット環境で **nms:freezeInstance.js** 焼灼スクリプトを実行します。

   このプロセスは、サーバーとその設定には影響しません。

   >[!NOTE]
   >
   >Adobe Campaignのコンテキストでは、 **焼灼** は、外部との対話をすべてのプロセスを停止するためのアクションを組み合わせます。ログ、トラッキング、配信、キャンペーンワークフローなど\
   >この手順は、（通常の環境から 1 回、複製した環境から 1 回）メッセージを複数回配信しないようにするために必要です。

   >[!IMPORTANT]
   >
   >1 つの環境に複数のインスタンスを含めることができます。 各Adobe Campaignインスタンスには、ライセンス契約が適用されます。 使用許諾契約を調べて、使用できる環境の数を確認してください。\
   >以下の手順を実行すると、インストールした環境やインスタンスの数に影響を与えることなく、環境を転送できます。

### 事前準備 {#before-you-start}

>[!IMPORTANT]
>
>転送プロセスを開始する前に、ソース環境とターゲット環境のすべてのインスタンスに対して、データベースの完全バックアップを実行することを強くお勧めします。 この方法で問題が発生した場合は、バックアップを復元し、初期設定に戻すことができます。

このプロセスが機能するには、ソース環境とターゲット環境のインスタンス数、同じ目的（マーケティングインスタンス、配信インスタンス）、同様の設定が同じである必要があります。 技術的な設定は、ソフトウェアの前提条件に従う必要があります。 両方の環境に同じコンポーネントをインストールする必要があります。

## 実装 {#implementation}

### 転送手順 {#transfer-procedure}

この節では、ケーススタディを使用して、ソース環境をターゲット環境に移行するために必要な手順を説明します。ここでの目的は、実稼動環境（**prod** インスタンス）を開発環境（**dev** インスタンス）に復元し、「ライブ」プラットフォームにできるだけ近いコンテキストで動作させることです。

次の手順は慎重に実行する必要があります。ソース環境のデータベースをコピーする際に、一部のプロセスが進行中の可能性があります。 注意点（手順 3 を参照）により、メッセージが 2 回送信されるのを防ぎ、データの一貫性を維持します。

>[!IMPORTANT]
>
>* 次の手順は、PostgreSQL 言語で有効です。 SQL 言語が異なる場合 (Oracleなど ) は、SQL クエリを適応させる必要があります。
>* 以下のコマンドは、PostgreSQL の **prod** インスタンスと **dev** インスタンスのコンテキスト内で適用されます。

>


### 手順 1 — ソース環境（実稼動）データのバックアップを作成する {#step-1---make-a-backup-of-the-source-environment--prod--data}

データベースのコピー

まず、すべてのソース環境データベースをコピーします。 操作はデータベースエンジンに依存し、データベース管理者がおこないます。

PostgreSQL では、コマンドは次のようになります。

```
pg_dump mydatabase > mydatabase.sql
```

### 手順 2 — ターゲット環境設定（開発）の書き出し {#step-2---export-the-target-environment-configuration--dev-}

ほとんどの設定要素は、環境ごとに異なります。外部アカウント（ミッドソーシング、ルーティングなど）、テクニカルオプション（プラットフォーム名、データベース ID、E メールアドレス、デフォルト URL など）

ソース・データベースをターゲット・データベースに保存する前に、ターゲット環境（開発）の設定を書き出す必要があります。 これをおこなうには、次の 2 つのテーブルの内容をエクスポートします。**xtkoption** と **nmsextaccount**

この書き出しを使用すると、開発環境の設定を保持し、開発データ（ワークフロー、テンプレート、Web アプリケーション、受信者など）のみを更新できます。

これをおこなうには、次の 2 つの要素に対してパッケージのエクスポートを実行します。

* **xtk:option** テーブルを、次の内部名を持つレコードを除いた「options_dev.xml」ファイルにエクスポートします。&#39;WdbcTimeZone&#39;、&#39;NmsServer_LastPostUpgrade&#39;および&#39;NmsBroadcast_RegexRules&#39;。
* 「extaccount_dev.xml」ファイルで、ID が 0(@id &lt;> 0) でないすべてのレコードの **nms:extAccount** テーブルをエクスポートします。

エクスポートするオプション/アカウントの数が、各ファイルにエクスポートする行数と等しいことを確認します。

>[!NOTE]
>
>パッケージのエクスポートでエクスポートする行数は 1,000 行です。 オプションまたは外部アカウントの数が 1,000 を超える場合は、複数のエクスポートを実行する必要があります。
> 
>詳しくは、[この節](../../platform/using/working-with-data-packages.md#exporting-packages)を参照してください。

>[!NOTE]
>
>nmsextaccount テーブルをエクスポートすると、外部アカウントに関連するパスワード（例えば、ミッドソーシング、Message Center の実行、SMPP、IMS および他の外部アカウントのパスワード）はエクスポートされません。 外部アカウントを環境に再度インポートした後で再入力する必要が生じる場合があるので、事前に正しいパスワードにアクセスできることを確認してください。

### 手順 3 — ターゲット環境（開発）の停止 {#step-3---stop-the-target-environment--dev-}

すべてのターゲット環境サーバーでAdobe Campaignプロセスを停止する必要があります。 この操作は、オペレーティングシステムによって異なります。

すべてのプロセスを停止するか、データベースに書き込むプロセスのみを停止できます。

すべてのプロセスを停止するには、次のコマンドを使用します。

* Windows の場合：

   ```
   net stop nlserver6
   ```

* Linux の場合：

   ```
   /etc/init.d/nlserver6 stop
   ```

次のコマンドを使用して、すべてのプロセスが停止したことを確認します。

```
nlserver pdump
```

>[!NOTE]
>
>Windows では、**webmdl** プロセスは、他の操作に影響を与えることなくアクティブなままです。

また、実行中のシステムプロセスがないことを確認することもできます。

それには、次の手順に従います。

* Windows の場合：**タスクマネージャー** を開き、**nlserver.exe** プロセスがないことを確認します。
* Linux の場合：**ps aux を実行します。 | grep nlserver** コマンドを実行し、**nlserver** プロセスがないことを確認します。

### 手順 4 — ターゲット環境（開発）でのデータベースの復元 {#step-4---restore-the-databases-in-the-target-environment--dev-}

ターゲット環境でソース・データベースをリストアするには、次のコマンドを使用します。

```
psql mydatabase < mydatabase.sql
```

### 手順 5 — ターゲット環境（開発）の焼灼 {#step-5---cauterize-the-target-environment--dev-}

誤動作を防ぐため、配信の送信とワークフローの実行にリンクされたプロセスは、ターゲット環境がアクティブ化されたときに自動的に実行されないようにする必要があります。

これをおこなうには、次のコマンドを実行します。

```
nlserver javascript nms:freezeInstance.js -instance:<dev> -arg:run
```

### 手順 6 — 注意点の確認 {#step-6---check-cauterization}

1. ID が 0 に設定されているのが配信部分のみであることを確認します。

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

### 手順 7 — ターゲット環境の Web プロセス（開発）の再起動 {#step-7---restart-the-target-environment-web-process--dev-}

ターゲット環境で、すべてのサーバーのAdobe Campaignプロセスを再起動します。

>[!NOTE]
>
>**dev** 環境でAdobe Campaignを再起動する前に、次の手順を実行して、さらに安全な手順を実行できます。**web** モジュールのみを起動します。
>  
>これをおこなうには、インスタンスの設定ファイル (**config-dev.xml**) を編集し、各モジュール（mta、stat など）の autoStart=&quot;true&quot;オプションの前に&quot;_&quot;文字を追加します。

次のコマンドを実行して、Web プロセスを開始します。

```
nlserver start web
```

次のコマンドを使用して、Web プロセスのみが開始されたことを確認します。

```
nlserver pdump
```

クライアントコンソールへのアクセス機能を確認します。

### 手順 8 — オプションと外部アカウントをターゲット環境（開発）に読み込む {#step-8---import-options-and-external-accounts-into-the-target-environment--dev-}

>[!IMPORTANT]
>
>この手順では、Web プロセスのみを開始する必要があります。 そうでない場合は、他の実行中のプロセスを停止してから続行します

特に、読み込む前に、複数行のファイルの値を確認します ( 例：オプション表の「NmsTracking_Pointer」および外部アカウント表の配信またはミッドソーシングアカウント )

ターゲット環境データベース（開発環境）から設定を読み込むには、次の手順を実行します。

1. データベースの Admin Console を開き、ID が 0(@id &lt;> 0) でない外部アカウント（テーブル nms:extAccount）をパージします。
1. Adobe Campaignコンソールで、パッケージの読み込み機能で以前に作成した options_dev.xml パッケージを読み込みます。

   **[!UICONTROL 管理/プラットフォーム/オプション]** ノードで、オプションが実際に更新されていることを確認します。

1. Adobe Campaignコンソールで、パッケージのインポート機能を使用して以前に作成した extaccount_dev.xml をインポートします。

   **[!UICONTROL 管理/プラットフォーム/外部アカウント]** で、外部データベースが実際にインポートされたことを確認します。

### 手順 9 — すべてのプロセスを再起動し、ユーザーを変更する（開発） {#step-9---restart-all-processes-and-change-users--dev-}

Adobe Campaignプロセスを開始するには、次のコマンドを使用します。

* Windows の場合：

   ```
   net start nlserver6
   ```

* Linux の場合：

   ```
   /etc/init.d/nlserver6 start
   ```

次のコマンドを使用して、プロセスが開始されていることを確認します。

```
nlserver pdump
```

ユーザーを変更して、開発プラットフォームに既に存在するユーザーを検索します。
