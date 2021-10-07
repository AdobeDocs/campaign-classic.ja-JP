---
product: campaign
title: 通常のコマンド
description: 通常のコマンド
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 472ccc04-e68e-4ccb-90e9-7d626a4e794f
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 4%

---

# 通常のコマンド{#usual-commands}

![](../../assets/v7-only.svg)

この節では、Adobe Campaignの通常のコマンドを示します。

**nlserver** コマンドは、Adobe Campaignアプリケーション全体に対する入力コマンドです。

このコマンドの構文は次のとおりです。**nlserver **`<command>`****`<arguments>`****

パラメーター **`<command>`** は、モジュールに対応します。

>[!NOTE]
>
>* いずれの場合でも、**-noconsole** 引数を追加して、モジュールの起動時に表示されるコメントを削除できます。
>* 逆に、引数 **-verbose** を追加して、詳細情報を表示できます。

>


## コマンドの監視 {#monitoring-commands-}

>[!NOTE]
>
>すべてのモジュールを一覧表示するには、**nlserver pdump** コマンドを使用する必要があります。

パラメーター **-who** を追加して、進行中の接続（データベースとアプリケーション）をリストできます。

```
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

もう 1 つの便利なコマンドは **nlserver monitor** です。 監視 XML ファイルのリストが表示されます (Adobe Campaignクライアントまたは **monitor.jsp** Web ページを介して取得 )。

パラメータ **-missing** を追加して、存在しないモジュール（モジュール、モジュールのシャットダウンなどのエラー）を一覧表示できます。

```
nlserver monitor -missing
HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
inMail@test
mta@test
wfserver@test
```

これは、自動起動のモジュールに対応しますが、まだ起動されていません。

## モジュール起動コマンド {#module-launch-commands}

起動モジュールの構文は、引き続き次の形式になります。

```
nlserver start <module>@<INSTANCE>
```

```
nlserver stop <module>@<INSTANCE>
```

>[!NOTE]
>
>**`<instance>`** は、設定ファイルに入力したインスタンスの名前、またはモノラルインスタンスモジュールの **** デフォルトに対応します。

## サービスのシャットダウン {#shut-down-services}

Adobe Campaignサービスを停止するには、次のいずれかのコマンドを使用します。

* root または管理者のアクセス権がある場合：

   * Linux の場合：

      ```
      /etc/init.d/nlserver6 stop
      ```

      >[!NOTE]
      >
      >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl stop nlserver**

   * Windows の場合：

      ```
      net stop nlserver6
      ```

* そうでない場合は、Adobe Campaignアカウントで次の手順を実行します。

   ```
   nlserver shutdown 
   ```

## サービスの再起動 {#restart-services}

同様に、Adobe Campaignを再起動するには、次のいずれかのコマンドを使用できます。

* root または管理者のアクセス権がある場合：

   * Linux の場合：/etc/init.d/nlserver6 start

      >[!NOTE]
      >
      >20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl start nlserver**

   * Windows の場合：net start nlserver6

* それ以外の場合は、Adobe Campaignアカウントで次の手順を実行します。**nlserver watchdog -svc -noconsole**

## config コマンド {#the-config-command}

**config** コマンドを使用すると、データベース接続の再設定など、サーバーの設定を管理できます。

**-setdblogin** パラメータを指定して、**nlserver** 実行可能ファイルの **config** コマンドを使用します。

```
nlserver config -setdblogin:<[dbms:]account[:database][/password]@server>
```

```
nlserver config -setdblogin:PostgreSQL:<accountName>:test6@dbserver
```

パスワードを入力します。

**内部** パスワードを変更するには：**nlserver config -internalpassword**

>[!IMPORTANT]
>
>**内部** 識別子を使用してログオンするには、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

>[!NOTE]
>
>* 一般的に、手動で設定ファイルを変更する代わりに、 **config** コマンドを使用できます
>* パラメータのリストを取得するには、**-?** パラメーター： **nlserver 設定 —?**
>* アカウントデータベースの場合は、Oracleを指定しないでください。 構文は次のようになります。
>
>  nlserver config -setdblogin:Oracle:test6@dbserver
