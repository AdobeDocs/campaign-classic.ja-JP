---
product: campaign
title: 通常のコマンド
description: 通常のコマンド
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 472ccc04-e68e-4ccb-90e9-7d626a4e794f
source-git-commit: b7dedddc080d1ea8db700fabc9ee03238b3706cc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 8%

---

# 通常のコマンド{#usual-commands}



ここでは、Adobe Campaignの通常のコマンドを示します。

コマンド **nlserver** は、Adobe Campaign アプリケーション全体に対する入力コマンドです。

このコマンドの構文は次のとおりです：**nlserver **`<command>`****`<arguments>`****

モジュールに対応するパラメーター **`<command>`**。

>[!NOTE]
>
>* いずれの場合も、**-noconsole** 引数を追加して、モジュールが起動されると表示されるコメントを削除できます。
>* 逆に、引数 **-verbose を追加して** 詳細な情報を表示できます。
>

## コマンドの監視 {#monitoring-commands-}

>[!NOTE]
>
>すべてのモジュールを一覧表示するには、**nlserver pdump** コマンドを使用する必要があります。

パラメーター **-who** を追加して、進行中の接続（データベースとアプリケーション）をリストできます。

```sql
nlserver pdump -who
HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
web@default (9984) - 50.1 Mo
watchdog (2273) - 6.6 Mo
syslogd@default (9931) - 7.0 Mo
trackinglogd@default (9985) - 45.6 Mo
mta@test (9986) - 9.6 Mo
wfserver@test (9987) - 8.8 Mo

Connections ------------------------------------------------------
Last Access IP Instance Login 
DD/MM/YYYY HH:MM:SS 127.0.0.1 default formation_fr|tracking
DD/MM/YYYY HH:MM:SS 127.0.0.1 default internal|monitoring

Connection pool --------------------------------------------------
Datasource Server Provider Login 
default xxxxx myserver myprovider test400
```

もう 1 つの便利なコマンドは **nlserver monitor** です。 監視 XML ファイル（Adobe Campaign クライアントまたは **monitor.jsp** web ページを介して取得）が一覧表示されます。

パラメーター **-missing** を追加して、存在しないモジュール（モジュールのエラー、モジュールのシャットダウンなど）を一覧表示できます。

```sql
nlserver monitor -missing
HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
inMail@test
mta@test
wfserver@test
```

これは、自動スタートアップだが起動されていないモジュールに対応します。

## モジュール起動コマンド {#module-launch-commands}

モジュールを起動するための構文は、引き続き次の形式となります。

```sql
nlserver start <module>@<INSTANCE>
```

```sql
nlserver stop <module>@<INSTANCE>
```

>[!NOTE]
>
>**`<instance>`** は、設定ファイルに入力されたインスタンスの名前、またはモノインスタンスモジュールの場合 **デフォルト** に対応します。

## サービスのシャットダウン {#shut-down-services}

Adobe Campaign サービスを停止するには、次のいずれかのコマンドを使用します。

* ルートまたは管理者のアクセス権がある場合：

   * Linux の場合

     ```sql
     /etc/init.d/nlserver6 stop
     ```

     >[!NOTE]
     >
     >20.1 以降では、次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl stop nlserver**

   * Windows の場合：

     ```sql
     net stop nlserver6
     ```

* そうでない場合は、Adobe Campaign アカウントで次のようにします。

  ```sql
  nlserver shutdown 
  ```

## サービスの再起動 {#restart-services}

同様に、Adobe Campaignを再起動するには、次のいずれかのコマンドを使用します。

* ルートまたは管理者のアクセス権がある場合：

   * Linux の場合：`/etc/init.d/nlserver6 start`

     >[!NOTE]
     >
     >20.1 以降では、次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl start nlserver**

   * Windows の場合：`net start nlserver6`

* それ以外の場合は、Adobe Campaign アカウントで **nlserver watchdog -svc -noconsole** を実行します。

## config コマンド {#the-config-command}

**config** コマンドを使用すると、データベース接続の再構成を含むサーバー構成を管理できます。

**nlserver** 実行可能ファイルの **config** コマンドを **-setdblogin** パラメーターと共に使用します。

```sql
nlserver config -setdblogin:<[dbms:]account[:database][/password]@server>
```

```sql
nlserver config -setdblogin:PostgreSQL:<accountName>:test6@dbserver
```

パスワードを入力します。

**internal** パスワードを変更するには：**nlserver config -internalpassword**

>[!IMPORTANT]
>
>**内部** 識別子でログオンするには、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

>[!NOTE]
>
>* 一般に、設定ファイルを手動で変更する代わりに、**config** コマンドを使用できます
>* パラメーターのリストを取得するには、**-?** パラメーター：**nlserver config -?**
>* oracleデータベースの場合は、アカウントを指定しないでください。 構文は次のようになります。
>
>  `nlserver config -setdblogin:Oracle:test6@dbserver`
>
