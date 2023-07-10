---
product: campaign
title: 環境の複製
description: 環境の複製
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html" tooltip="Applies to on-premise and hybrid deployments only"
audience: production
content-type: reference
topic-tags: data-processing
exl-id: 2c933fc5-1c0a-4c2f-9ff2-90d09a79c55a
source-git-commit: 4661688a22bd1a82eaf9c72a739b5a5ecee168b1
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 3%

---

# 環境の複製{#duplicating-environments}



## はじめに {#introduction}

### 概要 {#overview}

>[!IMPORTANT]
>
>サーバーとデータベース（ホスト環境）へのアクセス権がない場合、以下に説明する手順を実行できません。 Adobeにお問い合わせください。

Adobe Campaignを使用するには、1 つ以上の環境をインストールして設定する必要があります。開発、テスト、実稼動前、実稼動など

各環境には 1 つのAdobe Campaignインスタンスが含まれ、各Adobe Campaignインスタンスは 1 つ以上のデータベースにリンクされています。 アプリケーションサーバーは、1 つ以上のプロセスを実行できます。これらのほとんどすべては、インスタンスデータベースに直接アクセスできます。

この節では、Adobe Campaign環境の複製に適用するプロセス（ソース環境をターゲット環境に復元する場合など）について詳しく説明します。その結果、2 つの同じ作業環境が作成されます。

それには、次の手順に従います。

1. ソース環境内のすべてのインスタンス上に、データベースのコピーを作成します。
1. ターゲット環境のすべてのインスタンスに対して、これらのコピーを復元します。
1. を実行します。 **nms:freezeInstance.js** 起動前のターゲット環境の警告スクリプト。

   このプロセスは、サーバーとその設定には影響しません。

   >[!NOTE]
   >
   >Adobe Campaignの場合、 **焼灼** は、外部とやり取りするすべてのプロセスを停止できるアクションを組み合わせます。ログ、トラッキング、配信、キャンペーンワークフローなど\
   >この手順は、（1 回は呼び出し環境から、もう 1 回は複製環境から）メッセージを複数回配信しないようにするために必要です。

   >[!IMPORTANT]
   >
   >1 つの環境に複数のインスタンスを含めることができます。 各Adobe Campaignインスタンスには、ライセンス契約が適用されます。 使用許諾契約を調べて、使用できる環境の数を確認してください。\
   >以下の手順を実行すると、インストールした環境やインスタンスの数に影響を与えることなく、環境を転送できます。

### 事前準備 {#before-you-start}

>[!IMPORTANT]
>
>転送プロセスを開始する前に、ソース環境とターゲット環境のすべてのインスタンスに対して、データベースのフルバックアップを実行することを強くお勧めします。 この方法で問題が発生した場合は、バックアップを復元し、初期設定に戻すことができます。

このプロセスを機能させるには、ソース環境とターゲット環境で同じ数のインスタンス、同じ目的（マーケティングインスタンス、配信インスタンス）、類似した設定が必要です。 技術的な設定は、ソフトウェアの前提条件に従う必要があります。 両方の環境に同じコンポーネントをインストールする必要があります。

## 実装 {#implementation}

### 転送手順 {#transfer-procedure}

この節では、ケーススタディを使用して、ソース環境をターゲット環境に移行する際に必要な手順を説明します。ここでの目的は、実稼動環境の復元です (**prod** インスタンス ) を開発環境 (**dev** インスタンス ) が、「ライブ」プラットフォームにできる限り近いコンテキストで動作するようにする必要があります。

次の手順は、慎重に実行する必要があります。ソース環境データベースをコピーする際に、一部のプロセスが進行中の可能性があります。 注意機能を使用すると（次の手順 3 で説明）、メッセージが 2 回送信されるのを防ぎ、データの一貫性を維持できます。

>[!IMPORTANT]
>
>* 次の手順は PostgreSQL 言語で有効です。 SQL 言語が異なる場合 (Oracleなど ) は、SQL クエリを適応させる必要があります。
>* 以下のコマンドは、 **prod** インスタンスと **dev** PostgreSQL のインスタンス。
>

### 手順 1 — ソース環境（実稼動）データのバックアップを作成する {#step-1---make-a-backup-of-the-source-environment--prod--data}

データベースをコピーする

まず、すべてのソース環境データベースをコピーします。 操作はデータベースエンジンに依存し、データベース管理者がおこないます。

PostgreSQL では、コマンドは次のようになります。

```
pg_dump mydatabase > mydatabase.sql
```

### 手順 2 — ターゲット環境設定（開発）を書き出す {#step-2---export-the-target-environment-configuration--dev-}

ほとんどの設定要素は、環境ごとに異なります。外部アカウント（ミッドソーシング、ルーティングなど）、技術的なオプション（プラットフォーム名、データベース ID、E メールアドレス、デフォルト URL など）。

ソースデータベースをターゲットデータベースに保存する前に、ターゲット環境（開発）の設定を書き出す必要があります。 これをおこなうには、次の 2 つのテーブルのコンテンツをエクスポートします。 **xtkoption** および **nmsexaccount**.

この書き出しを使用すると、開発設定を保持し、開発データ（ワークフロー、テンプレート、Web アプリケーション、受信者など）のみを更新できます。

これをおこなうには、次の 2 つの要素に対してパッケージのエクスポートを実行します。

* を書き出す **xtk:option** 次の内部名を持つレコードを除く「options_dev.xml」ファイルにテーブルを追加します。「WdbcTimeZone」、「NmsServer_LastPostUpgrade」および「NmsBroadcast_RegexRules」。
* 「extaccount_dev.xml」ファイルで、 **nms:extAccount** ID が 0(@id &lt;> 0) でないすべてのレコードのテーブル。

エクスポートするオプション/アカウントの数が、各ファイルでエクスポートするライン数と等しいことを確認します。

>[!NOTE]
>
>パッケージエクスポートでエクスポートする行数は 1,000 行です。 オプションまたは外部アカウントの数が 1,000 を超える場合は、複数のエクスポートを実行する必要があります。
> 
>詳しくは、[この節](../../platform/using/working-with-data-packages.md#exporting-packages)を参照してください。

>[!NOTE]
>
>nmsextaccount テーブルをエクスポートする場合、外部アカウントに関連するパスワード（ミッドソーシング、Message Center の実行、SMPP、IMS およびその他の外部アカウント用のパスワードなど）はエクスポートされません。 外部アカウントを環境に再び読み込んだ後で再入力する必要が生じる場合があるので、正しいパスワードに事前にアクセスできることを確認してください。

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
>Windows の場合、 **webmdl** プロセスは、他の操作に影響を与えることなくアクティブなままです。

また、実行中のシステムプロセスがないことも確認できます。

それには、次の手順に従います。

* Windows の場合：を開きます。 **タスクマネージャー** そして、 **nlserver.exe** プロセス。
* Linux の場合：実行 **ps aux | grep nlserver** コマンドを実行して、 **nlserver** プロセス。

### 手順 4 — ターゲット環境（開発環境）でのデータベースの復元 {#step-4---restore-the-databases-in-the-target-environment--dev-}

ターゲット環境でソース・データベースをリストアするには、次のコマンドを使用します。

```
psql mydatabase < mydatabase.sql
```

### 手順 5 — ターゲット環境（開発）の注意 {#step-5---cauterize-the-target-environment--dev-}

誤作動を避けるために、配信の送信とワークフローの実行に関連するプロセスは、ターゲット環境がアクティブ化されたときに自動的に実行されないようにする必要があります。

これをおこなうには、次のコマンドを実行します。

```
nlserver javascript nms:freezeInstance.js -instance:<dev> -arg:run
```

### 手順 6 — 注意点の確認 {#step-6---check-cauterization}

1. ID が 0 に設定されているのが唯一の配信部分であることを確認します。

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

### 手順 7 — ターゲット環境の Web プロセス（開発）を再起動する {#step-7---restart-the-target-environment-web-process--dev-}

ターゲット環境で、すべてのサーバーのAdobe Campaignプロセスを再起動します。

>[!NOTE]
>
>でAdobe Campaignを再起動する前に **dev** 環境では、さらに安全な手順を適用できます。を起動します。 **web** モジュールのみ。
>  
>これをおこなうには、インスタンスの設定ファイル (**config-dev.xml**) をクリックし、各モジュール（mta、stat など）の autoStart=&quot;true&quot;オプションの前に&quot;_&quot;文字を追加します。

次のコマンドを実行して、Web プロセスを開始します。

```
nlserver start web
```

次のコマンドを使用して、Web プロセスのみが開始したことを確認します。

```
nlserver pdump
```

クライアントコンソールが機能することを確認します。

### 手順 8 — ターゲット環境（開発）へのオプションと外部アカウントの読み込み {#step-8---import-options-and-external-accounts-into-the-target-environment--dev-}

>[!IMPORTANT]
>
>この手順では、Web プロセスのみを開始する必要があります。 そうでない場合は、他の実行中のプロセスを停止してから続行します

何よりも、インポートする前に、ファイルの複数行の値を確認します ( 例：オプションテーブルおよび外部アカウントテーブルの配信またはミッドソーシングアカウントの「NmsTracking_Pointer」)

ターゲット環境データベース（開発環境）から設定を読み込むには、次の手順に従います。

1. データベースの管理コンソールを開き、ID が 0(@id &lt;> 0) でない外部アカウント（テーブル nms:extAccount）をパージします。
1. Adobe Campaignコンソールで、パッケージのインポート機能で以前に作成した options_dev.xml パッケージをインポートします。

   でオプションが実際に更新されていることを確認します。 **[!UICONTROL 管理/プラットフォーム/オプション]** ノード。

1. Adobe Campaignコンソールで、パッケージのインポート機能を使用して作成した extaccount_dev.xml をインポートします。

   外部データベースが実際に **[!UICONTROL 管理/プラットフォーム/外部アカウント]** .

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
