---
product: campaign
title: 環境の複製
description: 環境の複製
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: data-processing
exl-id: 2c933fc5-1c0a-4c2f-9ff2-90d09a79c55a
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 5%

---

# 環境の複製{#duplicating-environments}



## はじめに {#introduction}

### 概要 {#overview}

>[!IMPORTANT]
>
>サーバーおよびデータベース（ホスト環境）へのアクセス権がない場合は、以下の手順を実行できません。 Adobeにお問い合わせください。

Adobe Campaignを使用するには、開発、テスト、プリプロダクション、プロダクションなど、1つ以上の環境をインストールして設定する必要があります。

各環境にはAdobe Campaign インスタンスが含まれ、各Adobe Campaign インスタンスは1つ以上のデータベースにリンクされています。 アプリケーションサーバーは1つ以上のプロセスを実行できます。これらのほぼすべてがインスタンスデータベースに直接アクセスできます。

この節では、Adobe Campaign環境を複製するために適用されるプロセス（ソース環境をターゲット環境に復元し、2つの同一の作業環境を作成するプロセス）について詳しく説明します。

それには、次の手順に従います。

1. ソース環境のすべてのインスタンスでデータベースのコピーを作成します。
1. ターゲット環境のすべてのインスタンスでこれらのコピーを復元します。
1. 起動前に、ターゲット環境で&#x200B;**nms:freezeInstance.js**&#x200B;焼灼化スクリプトを実行します。

   このプロセスは、サーバーとその設定には影響しません。

   >[!NOTE]
   >
   >Adobe Campaignのコンテキストでは、**焼灼化**&#x200B;は、ログ、トラッキング、配信、キャンペーンワークフローなど、外部とやり取りするすべてのプロセスを停止できるアクションを組み合わせています。\
   >この手順は、メッセージを複数回配信することを避けるために必要です（公称環境から1回、重複環境から1回）。

   >[!IMPORTANT]
   >
   >1つの環境に複数のインスタンスを含めることができます。 各Adobe Campaign インスタンスには、ライセンス契約が適用されます。 ライセンス契約を確認して、利用可能な環境の数を確認してください。\
   >以下の手順では、インストールした環境とインスタンスの数に影響を与えることなく、環境を転送できます。

### 始める前に {#before-you-start}

>[!IMPORTANT]
>
>転送プロセスを開始する前に、ソース環境とターゲット環境のすべてのインスタンスに対してデータベースの完全バックアップを実行することを強くお勧めします。 これにより、問題が発生した場合は、バックアップを復元して初期設定に戻すことができます。

このプロセスを機能させるには、ソース環境とターゲット環境に同じ数のインスタンス、同じ目的（マーケティングインスタンス、配信インスタンス）および同様の設定が必要です。 技術設定は、ソフトウェアの前提条件に準拠している必要があります。 両方の環境に同じコンポーネントをインストールする必要があります。

## 実装 {#implementation}

### 移行手続き {#transfer-procedure}

このセクションでは、ケーススタディを介してソース環境をターゲット環境に転送するために必要な手順を理解するのに役立ちます。ここでの目的は、実稼働環境（**prod** インスタンス）を開発環境（**dev** インスタンス）に復元し、「ライブ」プラットフォームにできるだけ近いコンテキストで動作させることです。

次の手順は、細心の注意を払って実行する必要があります。ソース環境データベースをコピーしても、一部のプロセスが引き続き実行される場合があります。 認証（以下のステップ 3）により、メッセージが2回送信されるのを防ぎ、データの一貫性を維持します。

>[!IMPORTANT]
>
>* 次の手順は、PostgreSQL言語で有効です。 SQL言語が異なる場合（Oracleなど）、SQL クエリを適応させる必要があります。
>* 以下のコマンドは、**prod** インスタンスと&#x200B;**dev** インスタンスのコンテキスト内でPostgreSQLの下に適用されます。
>

### 手順1 - ソース環境（prod）データのバックアップを作成する {#step-1---make-a-backup-of-the-source-environment--prod--data}

データベースのコピー

まず、すべてのソース環境データベースをコピーします。 操作はデータベースエンジンに依存し、データベース管理者の責任です。

PostgreSQLでは、コマンドは次のとおりです。

```
pg_dump mydatabase > mydatabase.sql
```

### 手順2 - ターゲット環境設定（開発）のエクスポート {#step-2---export-the-target-environment-configuration--dev-}

ほとんどの設定要素は、外部アカウント（ミッドソーシング、ルーティングなど）、技術的なオプション（プラットフォーム名、DatabaseId、メールアドレス、デフォルトのURLなど）ごとに異なります。

ソースデータベースをターゲットデータベースに保存する前に、ターゲット環境（dev）設定をエクスポートする必要があります。 これを行うには、次の2つのテーブルのコンテンツを書き出します。**xtkoption**&#x200B;と&#x200B;**nmsextaccount**。

この書き出しでは、開発設定を保持し、開発データ（ワークフロー、テンプレート、Web アプリケーション、受信者など）のみを更新できます。

これを行うには、次の2つの要素に対してパッケージの書き出しを実行します。

* **xtk:option** テーブルを、&#39;options_dev.xml&#39; ファイルに書き出します。内部名が&#39;WdbcTimeZone&#39;、&#39;NmsServer_LastPostUpgrade&#39;、&#39;NmsBroadcast_RegexRules&#39;のレコードは含まれません。
* 「extaccount_dev.xml」ファイルで、IDが0以外のすべてのレコード（@id &lt;> 0）の&#x200B;**nms:extAccount** テーブルを書き出します。

書き出されたオプション/アカウントの数が、各ファイルに書き出す行数に等しいことを確認します。

>[!NOTE]
>
>パッケージの書き出しで書き出す行数は1000行です。 オプションまたは外部アカウントの数が1000を超える場合は、いくつかの書き出しを実行する必要があります。
> 
>詳しくは、[この節](../../platform/using/working-with-data-packages.md#exporting-packages)を参照してください。

>[!NOTE]
>
>nmsextaccount テーブルをエクスポートすると、外部アカウントに関連するパスワード（ミッドソーシング、Message Center Execution、SMPP、IMS、その他の外部アカウントのパスワードなど）はエクスポートされません。 外部アカウントが環境に読み込まれた後に再入力する必要がある場合があるので、事前に正しいパスワードにアクセスできることを確認してください。

### 手順3 - ターゲット環境（開発）の停止 {#step-3---stop-the-target-environment--dev-}

すべてのターゲット環境サーバーでAdobe Campaign プロセスを停止する必要があります。 この操作は、オペレーティングシステムによって異なります。

すべてのプロセスを停止することも、データベースに書き込むプロセスのみを停止することもできます。

すべてのプロセスを停止するには、次のコマンドを使用します。

* Windowsでは：

  ```
  net stop nlserver6
  ```

* Linuxでは：

  ```
  /etc/init.d/nlserver6 stop
  ```

すべてのプロセスが停止したことを確認するには、次のコマンドを使用します。

```
nlserver pdump
```

>[!NOTE]
>
>Windowsでは、他の操作に影響を与えることなく、**webmdl** プロセスを引き続きアクティブにできます。

また、実行中のシステムプロセスがないことも確認できます。

それには、次の手順に従います。

* Windowsの場合：**タスクマネージャー**&#x200B;を開き、**nlserver.exe** プロセスがないことを確認します。
* Linuxの場合：**ps aux | grep nlserver** コマンドを実行し、**nlserver** プロセスがないことを確認します。

### 手順4 - ターゲット環境（開発）のデータベースを復元する {#step-4---restore-the-databases-in-the-target-environment--dev-}

ターゲット環境のソースデータベースを復元するには、次のコマンドを使用します。

```
psql mydatabase < mydatabase.sql
```

### 手順5 - ターゲット環境（開発）の認証 {#step-5---cauterize-the-target-environment--dev-}

誤動作を避けるために、ターゲット環境がアクティブ化されたときに、配信の送信とワークフローの実行にリンクされたプロセスを自動的に実行しないでください。

これを行うには、次のコマンドを実行します。

```
nlserver javascript nms:freezeInstance.js -instance:<dev> -arg:run
```

### 手順6 – 焼結の確認 {#step-6---check-cauterization}

1. IDが0に設定されている配信者が唯一の配信者であることを確認します。

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

### 手順7 - ターゲット環境のWeb プロセス（開発）を再起動する {#step-7---restart-the-target-environment-web-process--dev-}

ターゲット環境で、すべてのサーバーのAdobe Campaign プロセスを再起動します。

>[!NOTE]
>
>**dev**&#x200B;環境でAdobe Campaignを再起動する前に、追加の安全手順を適用できます。**web** モジュールのみを起動します。
>  
>これを行うには、インスタンスの設定ファイル （**config-dev.xml**）を編集し、各モジュールのautoStart=&quot;true&quot; オプション （mta、statなど）の前に「_」文字を追加します。

次のコマンドを実行して、Web プロセスを開始します。

```
nlserver start web
```

次のコマンドを使用して、web プロセスのみが開始されていることを確認します。

```
nlserver pdump
```

クライアントコンソール機能へのアクセスを確認してください。

### 手順8 - オプションと外部アカウントをターゲット環境（開発）にインポートする {#step-8---import-options-and-external-accounts-into-the-target-environment--dev-}

>[!IMPORTANT]
>
>この手順で開始するのは、web プロセスのみです。 そのような場合は、他の実行中のプロセスを停止してから続行してください

何よりも、インポートする前に、ファイルの複数行の値を確認します（例：オプションテーブルの「NmsTracking_Pointer」、外部アカウントテーブルの配信アカウントまたはミッドソーシングアカウント）。

ターゲット環境データベース（dev）から設定をインポートするには、次の手順を実行します。

1. データベースの管理コンソールを開き、IDが0 （@id &lt;> 0）ではない外部アカウント（テーブル nms:extAccount）をパージします。
1. Adobe Campaign コンソールで、以前にパッケージの読み込み機能を使用して作成したoptions_dev.xml パッケージを読み込みます。

   オプションが&#x200B;**[!UICONTROL 管理/ プラットフォーム / オプション]** ノードで実際に更新されていることを確認します。

1. Adobe Campaign コンソールで、以前にパッケージの読み込み機能で作成したextaccount_dev.xmlを読み込みます

   外部データベースが実際に&#x200B;**[!UICONTROL 管理/ プラットフォーム / 外部アカウント]**&#x200B;にインポートされていることを確認します。

### 手順9 – すべてのプロセスを再起動してユーザーを変更（開発） {#step-9---restart-all-processes-and-change-users--dev-}

Adobe Campaign プロセスを開始するには、次のコマンドを使用します。

* Windowsでは：

  ```
  net start nlserver6
  ```

* Linuxでは：

  ```
  /etc/init.d/nlserver6 start
  ```

次のコマンドを使用して、プロセスが開始されていることを確認します。

```
nlserver pdump
```

ユーザーを変更して、開発プラットフォームにすでに存在するユーザーを見つけます。
