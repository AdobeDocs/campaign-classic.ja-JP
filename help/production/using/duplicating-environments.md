---
product: campaign
title: 環境の複製
description: 環境の複製
feature: Monitoring
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: data-processing
exl-id: 2c933fc5-1c0a-4c2f-9ff2-90d09a79c55a
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 4%

---

# 環境の複製{#duplicating-environments}



## はじめに {#introduction}

### 概要 {#overview}

>[!IMPORTANT]
>
>サーバーおよびデータベース（ホスト環境）にアクセスできない場合、以下に説明する手順を実行できません。 Adobeにお問い合わせください。

Adobe Campaignを使用するには、開発、テスト、実稼動前、実稼動など、1 つ以上の環境をインストールして設定する必要があります。

各環境には 1 つのAdobe Campaign インスタンスが含まれ、各Adobe Campaign インスタンスは 1 つ以上のデータベースにリンクされています。 アプリケーションサーバーは、1 つ以上のプロセスを実行できます。これらのほとんど全てが、インスタンスデータベースへの直接アクセス権を持ちます。

この節では、Adobe Campaign環境の複製、つまりソース環境をターゲット環境に復元して 2 つの同一の作業環境を構築する場合のプロセスについて説明します。

それには、次の手順に従います。

1. ソース環境のすべてのインスタンス上にデータベースのコピーを作成し、
1. これらのコピーをターゲット環境のすべてのインスタンスにリストアする。
1. を実行 **nms:freezeInstance.js** 起動する前にターゲット環境で使用する焼灼スクリプト。

   このプロセスは、サーバーとその設定には影響しません。

   >[!NOTE]
   >
   >Adobe Campaignのコンテキストでは、 **焼灼** では、ログ、トラッキング、配信、キャンペーンワークフローなど、外部とやり取りするすべてのプロセスを停止するアクションを組み合わせます。\
   >この手順は、メッセージが複数回（公称環境から 1 回、重複した環境から 1 回）配信されるのを避けるために必要です。

   >[!IMPORTANT]
   >
   >1 つの環境に複数のインスタンスを含めることができます。 各Adobe Campaign インスタンスには、ライセンス契約が適用されます。 使用できる環境の数については、使用許諾契約書を確認してください。\
   >以下の手順を実行すると、インストールした環境およびインスタンスの数に影響を与えることなく環境を転送できます。

### 事前準備 {#before-you-start}

>[!IMPORTANT]
>
>転送プロセスを開始する前に、ソース環境とターゲット環境のすべてのインスタンスについて、データベースの完全バックアップを実行することを強くお勧めします。 これにより、問題が発生した場合に、バックアップを復元して初期設定に戻ることができます。

このプロセスが機能するには、ソース環境とターゲット環境が同数のインスタンス、同じ目的（マーケティングインスタンス、配信インスタンス）および類似の設定を持つ必要があります。 技術的な設定は、ソフトウェアの前提条件に準拠する必要があります。 両方の環境に同じコンポーネントをインストールする必要があります。

## 実装 {#implementation}

### 転送手順 {#transfer-procedure}

この節では、導入事例を通じてソース環境をターゲット環境に移行する際に必要な手順を説明します。ここでは、実稼動環境を復元することを目的としています（**prod** インスタンス）から開発環境（**開発** インスタンス）を使用して、「ライブ」プラットフォームにできる限り近いコンテキストで作業します。

次の手順は慎重に実行する必要があります。ソース環境のデータベースをコピーする際に、一部のプロセスがまだ進行中である可能性があります。 焼灼処理（後述の手順 3）により、メッセージが 2 回送信されるのを防ぎ、データの一貫性を維持できます。

>[!IMPORTANT]
>
>* 次のプロシージャは PostgreSQL 言語で有効です。 SQL 言語が異なる場合（Oracleなど）、SQL クエリを適応させる必要があります。
>* 以下のコマンドは、 **prod** instance および **開発** postgreSQL の下のインスタンス。
>

### 手順 1 - ソース環境（実稼動）データのバックアップを作成する {#step-1---make-a-backup-of-the-source-environment--prod--data}

データベースのコピー

まず、すべてのソース環境データベースをコピーします。 操作はデータベースエンジンに依存し、データベース管理者の責任です。

PostgreSQL では、次のコマンドを使用します。

```
pg_dump mydatabase > mydatabase.sql
```

### 手順 2 - ターゲット環境設定（開発）のエクスポート {#step-2---export-the-target-environment-configuration--dev-}

ほとんどの設定要素は、環境ごとに異なります。外部アカウント（ミッドソーシング、ルーティングなど）、技術オプション（プラットフォーム名、データベース ID、メールアドレス、デフォルト URL など）。

ターゲット・データベースにソース・データベースを保存する前に、ターゲット環境（開発）構成をエクスポートする必要があります。 それには、次の 2 つのテーブルの内容を書き出します。 **xtkoption** および **nsextaccount**.

この書き出しを使用すると、開発環境を保持し、開発データ（ワークフロー、テンプレート、web アプリケーション、受信者など）のみを更新できます。

それには、次の 2 つの要素に対してパッケージのエクスポートを実行します。

* をエクスポート **xtk:option** テーブルを「options_dev.xml」ファイルに追加します。これには、「WdbcTimeZone」、「NmsServer_LastPostUpgrade」および「NmsBroadcast_RegexRules」という内部名のレコードは含まれません。
* 「extaccount_dev.xml」ファイルで、 **nms:extAccount** id が 0 以外（@id &lt;> 0）のすべてのレコードのテーブル。

書き出されたオプション/アカウントの数が、各ファイルで書き出すラインの数と等しいことを確認します。

>[!NOTE]
>
>パッケージエクスポートでエクスポートする行数は 1000 行です。 オプションまたは外部アカウントの数が 1000 を超える場合は、複数の書き出しを実行する必要があります。
> 
>詳しくは、[この節](../../platform/using/working-with-data-packages.md#exporting-packages)を参照してください。

>[!NOTE]
>
>nmsextaccount テーブルを書き出しても、外部アカウントに関連するパスワード（ミッドソーシングのパスワード、Message Center の実行、SMPP、IMS およびその他の外部アカウントなど）は書き出されません。 外部アカウントを環境にインポートした後にパスワードの再入力が必要になる場合があるので、事前に正しいパスワードにアクセスできることを確認してください。

### 手順 3 - ターゲット環境を停止（開発） {#step-3---stop-the-target-environment--dev-}

すべての Target Environment Server でAdobe Campaign プロセスを停止する必要があります。 この操作は、オペレーティングシステムによって異なります。

すべてのプロセスを停止することも、データベースに書き込むプロセスのみを停止することもできます。

すべてのプロセスを停止するには、次のコマンドを使用します。

* Windows の場合：

  ```
  net stop nlserver6
  ```

* Linux の場合

  ```
  /etc/init.d/nlserver6 stop
  ```

次のコマンドを使用して、すべてのプロセスが停止したことを確認します。

```
nlserver pdump
```

>[!NOTE]
>
>Windows では、 **webmdl** プロセスは、他のオペレーションに影響を与えずにアクティブな状態を維持できます。

また、実行中のシステムプロセスがないことを確認することもできます。

それには、次の手順に従います。

* Windows の場合： **タスクマネージャー** を使用して、が存在しないことを確認します。 **nlserver.exe** プロセス。
* Linux の場合：を実行します **ps aux | grep nlserver** コマンドを実行して、が存在しないことを確認 **nlserver** プロセス。

### 手順 4 - ターゲット環境でのデータベースの復元（開発） {#step-4---restore-the-databases-in-the-target-environment--dev-}

ターゲット環境でソース・データベースをリストアするには、次のコマンドを使用します。

```
psql mydatabase < mydatabase.sql
```

### 手順 5 - ターゲット環境の焼灼（開発） {#step-5---cauterize-the-target-environment--dev-}

誤動作を回避するために、ターゲット環境がアクティブ化されている場合は、配信の送信とワークフローの実行に関連するプロセスを自動的に実行しないでください。

これを行うには、次のコマンドを実行します。

```
nlserver javascript nms:freezeInstance.js -instance:<dev> -arg:run
```

### 手順 6 - チェック焼灼法 {#step-6---check-cauterization}

1. ID が 0 に設定されている deliverypart のみが存在することを確認します。

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

### 手順 7 - ターゲット環境の web プロセス（開発）を再起動する {#step-7---restart-the-target-environment-web-process--dev-}

ターゲット環境で、すべてのサーバーのAdobe Campaign プロセスを再起動します。

>[!NOTE]
>
>でAdobe Campaignを再起動する前に **開発** 環境、追加の安全手順を適用できます。 **web** モジュールのみ。
>  
>それには、インスタンスの設定ファイル（**config-dev.xml**）を選択してから、各モジュール（mta、stat など）の autoStart=&quot;true&quot; オプションの前に「_」文字を追加します。

次のコマンドを実行して web プロセスを開始します。

```
nlserver start web
```

次のコマンドを使用して、web プロセスのみが開始されていることを確認します。

```
nlserver pdump
```

クライアントコンソール機能へのアクセスを確認します。

### 手順 8 - オプションと外部アカウントをターゲット環境（開発）にインポート {#step-8---import-options-and-external-accounts-into-the-target-environment--dev-}

>[!IMPORTANT]
>
>この手順で開始する必要があるのは、web プロセスのみです。 そうでない場合は、続行する前に他の実行中のプロセスを停止します

特に、読み込む前にファイルの複数行の値を確認してください（例：オプションテーブルの場合は「NmsTracking_Pointer」、外部アカウントテーブルの場合は配信または中間ソーシングアカウント）

ターゲット環境データベース（dev）から設定を読み込むには：

1. データベースの Admin Console を開き、ID が 0 （@id &lt;> 0）ではない外部アカウント（テーブル nms:extAccount）をパージします。
1. Adobe Campaign コンソールで、パッケージの読み込み機能を使用して以前に作成した options_dev.xml パッケージを読み込みます。

   オプションが実際にで更新されたことを確認します。 **[!UICONTROL 管理/ プラットフォーム / オプション]** ノード。

1. Adobe Campaign コンソールで、パッケージのインポート機能を使用して以前に作成した extaccount_dev.xml をインポートします

   外部データベースが実際ににインポートされていることを確認します。 **[!UICONTROL 管理/ プラットフォーム /外部アカウント]** .

### 手順 9 – すべてのプロセスの再起動とユーザーの変更（開発） {#step-9---restart-all-processes-and-change-users--dev-}

Adobe Campaign プロセスを開始するには、次のコマンドを使用します。

* Windows の場合：

  ```
  net start nlserver6
  ```

* Linux の場合

  ```
  /etc/init.d/nlserver6 start
  ```

次のコマンドを使用して、プロセスが開始されていることを確認します。

```
nlserver pdump
```

users を変更して、開発プラットフォームに既に存在するユーザーを検索します。
