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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 3%

---


# 環境の複製{#duplicating-environments}

## はじめに {#introduction}

### 概要 {#overview}

>[!CAUTION]
>
>サーバーとデータベース(ホスト環境)にアクセスできない場合は、以下に説明する手順を実行できません。 Adobeにお問い合わせください。

Adobe Campaignを使用するには、1つ以上の環境をインストールして設定する必要があります。開発、テスト、実稼働前、実稼働中など

各環境にはAdobe Campaignインスタンスが含まれ、各Adobe Campaignインスタンスは1つ以上のデータベースにリンクされます。 アプリケーションサーバーは、1つ以上のプロセスを実行できます。これらのほとんどすべては、インスタンスデータベースに直接アクセスできます。

この節では、ソース環境をターゲット環境に復元するために、Adobe Campaign環境と重複に適用されるプロセスについて詳しく説明します。つまり、同じ2つの作業環境を生み出します。

それには、次の手順に従います。

1. ソース・環境内のすべてのインスタンスにデータベースのコピーを作成します。
1. ターゲット環境のすべてのインスタンスで、これらのコピーを復元し、
1. 起動する前に、 **nms:freezeInstance.js** 焼灼スクリプトをターゲット環境で実行します。

   このプロセスは、サーバーとその設定には影響しません。

   >[!NOTE]
   >
   >Adobe Campaignに関しては、 **焼灼** は、外部との対話をすべてのプロセスに止めるためのアクションを組み合わせます。ログ、トラッキング、配信、キャンペーンワークフローなど\
   >この手順は、(通常の環境から1回、複製された環境から1回)複数回のメッセージ配信を避けるために必要です。

   >[!CAUTION]
   >
   >1つの環境に複数のインスタンスを含めることができます。 各Adobe Campaignインスタンスには、ライセンス契約が適用されます。 使用許諾契約を確認して、使用できる環境数を確認します。\
   >以下の手順では、インストールした環境やインスタンスの数に影響を与えることなく、環境を転送できます。

### 開始前 {#before-you-start}

>[!CAUTION]
>
>転送プロセスを開始する前に、ソースおよびターゲット環境のすべてのインスタンスに対して、データベースの完全バックアップを実行することを強くお勧めします。 この方法で問題が発生した場合は、バックアップを復元し、初期設定に戻すことができます。

このプロセスが動作するためには、ソースとターゲットの環境が同じインスタンス数、同じ目的(マーケティングインスタンス、配信インスタンス)および同様の設定を持つ必要があります。 技術構成は、ソフトウェアの前提条件を満たす必要があります。 両方の環境に同じコンポーネントをインストールする必要があります。

## 実装 {#implementation}

### 転送手順 {#transfer-procedure}

この節では、ケーススタディを介してソース環境をターゲット環境に転送する際に必要な手順を理解するのに役立ちます。ここでは、実稼働環境(**prod** instance)を開発環境(**dev** instance)に復元し、「ライブ」プラットフォームにできる限り近いコンテキストで動作させることを目的としています。

次の手順は、慎重に実行する必要があります。ソース・環境・データベースをコピーする際に、一部のプロセスがまだ進行中である場合があります。 注意機能（以下の手順3）は、メッセージが2回送信されるのを防ぎ、データの一貫性を維持します。

>[!CAUTION]
>
>* 次の手順はPostgreSQL言語で有効です。 SQL言語が異なる場合（Oracleなど）は、SQLクエリを適合させる必要があります。
>* 以下のコマンドは、PostgreSQLの **prod** Instanceおよび **dev** Instanceのコンテキスト内に適用されます。

>



### ステップ1 — ソース環境(prod)データのバックアップを作成する {#step-1---make-a-backup-of-the-source-environment--prod--data}

データベースのコピー

すべてのソース・環境・データベースをコピーして開始します。 操作はデータベースエンジンに依存し、データベース管理者の責任を負います。

PostgreSQLでは、次のコマンドが実行されます。

```
pg_dump mydatabase > mydatabase.sql
```

### 手順2 -ターゲット環境設定（開発環境）のエクスポート {#step-2---export-the-target-environment-configuration--dev-}

ほとんどの設定要素は、環境ごとに異なります。外部アカウント(ミッドソーシング、ルーティングなど)、技術オプション（プラットフォーム名、DatabaseId、電子メールアドレス、デフォルトURLなど）

ソースデータベースをターゲットデータベースに保存する前に、ターゲット環境（開発環境）の設定を書き出す必要があります。 これを行うには、次の2つのテーブルの内容を書き出します。 **xtkoption** と **nmsextaccount**。

このエクスポートにより、開発環境の設定を維持し、開発データ(ワークフロー、テンプレート、Web アプリケーション、受信者など)のみを更新できます。

これを行うには、次の2つの要素に対してパッケージエクスポートを実行します。

* xtk:option **** テーブルを&#39;options_dev.xml&#39;ファイルに書き出します。次の内部名を持つレコードは含まれません。&#39;WdbcTimeZone&#39;、&#39;NmsServer_LastPostUpgrade&#39;、および&#39;NmsBroadcast_RegexRules&#39;です。
* 「extaccount_dev.xml」ファイルで、IDが0(@id &lt;> 0)でないすべてのレコードの **nms:extAccount** テーブルをエクスポートします。

書き出したオプション/アカウントの数が、各ファイルで書き出す行数と等しいことを確認します。

>[!NOTE]
>
>パッケージエクスポートでエクスポートする行の数は1000行です。 オプションまたは外部アカウントの数が1000を超える場合は、複数のエクスポートを実行する必要があります。
> 
>詳しくは、[この節](../../platform/using/working-with-data-packages.md#exporting-packages)を参照してください。

>[!NOTE]
>
>nmsextaccountテーブルをエクスポートすると、外部アカウントに関連するパスワード(ミッドソーシング、Message Center Execution、SMPP、IMS、その他の外部アカウント用のパスワードなど)はエクスポートされません。 外部アカウントを環境に再度インポートした後、パスワードを再入力する必要が生じる場合があるので、正しいパスワードに事前にアクセスできることを確認してください。

### 手順3 -ターゲット環境（開発環境）を停止する {#step-3---stop-the-target-environment--dev-}

すべてのターゲット環境サーバーでAdobe Campaignプロセスを停止する必要があります。 この操作は、オペレーティングシステムによって異なります。

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
>Windowsでは、 **webmdl** プロセスは、他の操作に影響を与えることなくアクティブなままです。

また、実行中のシステムプロセスがないことを確認することもできます。

それには、次の手順に従います。

* Windowsの場合： **タスクマネージャーを開き** 、 **nlserver.exe** プロセスがないことを確認します。
* Linuxの場合： **ps auxを実行する | grep nlserver** コマンドを実行し、nlserver **** プロセスが存在しないことを確認します。

### 手順4 -ターゲット環境（開発環境）でデータベースを復元する {#step-4---restore-the-databases-in-the-target-environment--dev-}

ターゲット・環境でソース・データベースをリストアするには、次のコマンドを使用します。

```
psql mydatabase < mydatabase.sql
```

### 手順5 -ターゲット環境（開発環境）の注意 {#step-5---cauterize-the-target-environment--dev-}

誤動作を防ぐために、配信送信とワークフローの実行にリンクされたプロセスを、ターゲット環境がアクティブ化されたときに自動的に実行しないようにする必要があります。

これを行うには、次のコマンドを実行します。

```
nlserver javascript nms:freezeInstance.js -instance:<dev> -arg:run
```

### 手順6 — 注意喚起を確認する {#step-6---check-cauterization}

1. IDが0に設定されている配信部品が唯一の配信部品であることを確認します。

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

### 手順7 -ターゲット環境Webプロセス（開発環境）を再起動する {#step-7---restart-the-target-environment-web-process--dev-}

ターゲット環境で、すべてのサーバーのAdobe Campaignプロセスを開始し直します。

>[!NOTE]
>
>開発 **環境のAdobe Campaignを再開する前に、追加の安全手順を適用できます** 。 **web** モジュールのみを開始します。
>  
>これを行うには、インスタンスの設定ファイル(**config-dev.xml**)を編集し、各モジュール（mta、statなど）のautoStart=&quot;true&quot;オプションの前に「_」文字を追加します。

次のコマンドを実行してWebプロセスを開始します。

```
nlserver start web
```

次のコマンドを使用して、Webプロセスのみが開始したことを確認します。

```
nlserver pdump
```

クライアントコンソール機能へのアクセス権を確認します。

### 手順8 — オプションと外部アカウントをターゲット環境（開発環境）に読み込む {#step-8---import-options-and-external-accounts-into-the-target-environment--dev-}

>[!CAUTION]
>
>この手順では、Webプロセスのみを開始する必要があります。 そうでない場合は、続行する前に、実行中の他のプロセスを停止します

特に、読み込む前に、ファイルの複数行の値を確認してください(例：optionsテーブルの&#39;NmsTracking_Pointer&#39;、および外部アカウントテーブルの配信またはミッドソーシングがアカウントする)

ターゲット環境データベース（開発環境）から設定を読み込むには：

1. データベースの管理コンソールを開き、IDが0(@id &lt;> 0)でない外部アカウント(table nms:extAccount)を削除します。
1. Adobe Campaignコンソールで、パッケージの読み込み機能を使用して、以前に作成したoptions_dev.xmlパッケージを読み込みます。

   「 **[!UICONTROL 管理」>「プラットフォーム」>「オプション]** 」ノードで、オプションが実際に更新されていることを確認します。

1. Adobe Campaignコンソールで、パッケージの読み込み機能を使用して以前に作成したextaccount_dev.xmlを読み込みます

   外部データベースが、 **[!UICONTROL 管理/プラットフォーム/外部アカウントで実際にインポートされていることを確認します]** 。

### 手順9 — すべてのプロセスを再起動し、ユーザーを変更する（開発環境） {#step-9---restart-all-processes-and-change-users--dev-}

Adobe Campaignプロセスを開始するには、次のコマンドを使用します。

* Windowsの場合：

   ```
   net start nlserver6
   ```

* Linuxの場合：

   ```
   /etc/init.d/nlserver6 start
   ```

次のコマンドを使用して、プロセスが起動しているかどうかを確認します。

```
nlserver pdump
```

ユーザーを変更して、開発プラットフォームに既に存在するユーザーを検索します。
