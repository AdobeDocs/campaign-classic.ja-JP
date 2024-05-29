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

このコマンドの構文は次のとおりです。 **nlserver **`<command>`****`<arguments>`****

パラメーター **`<command>`** は、モジュールに対応します。

>[!NOTE]
>
>* いずれの場合も、 **-noconsole** モジュールの開始後に表示されるコメントを削除するための引数。
>* 逆に、引数を追加できます **-verbose** 詳細情報を表示します。
>

## コマンドの監視 {#monitoring-commands-}

>[!NOTE]
>
>すべてのモジュールをリストするには、 **nlserver pdump** コマンド。

パラメーターを追加できます **-who** 実行中の接続（データベースおよびアプリケーション）をリストします。

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

もう 1 つの便利なコマンドは次のとおりです。 **nlserver モニター**. 監視 XML ファイル（Adobe Campaign クライアントまたは経由で取得）が一覧表示されます **monitor.jsp** web ページ）を参照してください。

パラメーターを追加できます **– 不明** 存在しないモジュールを一覧表示します（モジュールのエラー、モジュールのシャットダウンなど）。

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
>**`<instance>`** 設定ファイルに入力されたインスタンスの名前、または **default** モノインスタンスモジュールの場合。

## サービスのシャットダウン {#shut-down-services}

Adobe Campaign サービスを停止するには、次のいずれかのコマンドを使用します。

* ルートまたは管理者のアクセス権がある場合：

   * Linux の場合

     ```sql
     /etc/init.d/nlserver6 stop
     ```

     >[!NOTE]
     >
     >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl stop nlserver**

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

   * Linux の場合 `/etc/init.d/nlserver6 start`

     >[!NOTE]
     >
     >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl start nlserver**

   * Windows の場合： `net start nlserver6`

* それ以外の場合は、Adobe Campaign アカウントで次の操作を行います。 **nlserver watchdog -svc -noconsole**

## config コマンド {#the-config-command}

この **config** コマンドを使用すると、データベース接続の再構成を含む、サーバーの構成を管理できます。

の使用 **config** コマンド **nlserver** を含む実行可能ファイル **-setdblogin** パラメーター。

```sql
nlserver config -setdblogin:<[dbms:]account[:database][/password]@server>
```

```sql
nlserver config -setdblogin:PostgreSQL:<accountName>:test6@dbserver
```

パスワードを入力します。

を変更するには **内部** パスワード： **nlserver config -internalpassword**

>[!IMPORTANT]
>
>を使用してログオンするには **内部** 識別子。事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

>[!NOTE]
>
>* 通常は、設定ファイルを手動で変更する代わりに、 **config** コマンド
>* パラメーターのリストを取得するには、を使用します **-?** パラメーター： **nlserver 構成 – ?**
>* oracleデータベースの場合は、アカウントを指定しないでください。 構文は次のようになります。
>
>  `nlserver config -setdblogin:Oracle:test6@dbserver`
>
