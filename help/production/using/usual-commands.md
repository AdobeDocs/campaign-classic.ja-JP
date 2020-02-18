---
title: 通常のコマンド
seo-title: 通常のコマンド
description: 通常のコマンド
seo-description: null
page-status-flag: never-activated
uuid: f06df8c0-d4ec-4d6b-84d5-f46d852388a3
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: 90718075-87a7-4e9a-935b-571010908e79
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: de04b5d3ceb883a571ee665f630be931a68a5a3e

---


# 通常のコマンド{#usual-commands}

ここでは、Adobe Campaignの通常のコマンドを示します。

nlserverコマンド **は** 、Adobe Campaignアプリケーション全体に対する入力コマンドです。

このコマンドの構文は次のとおりです。 **nlserver **`<command>`****`<arguments>`****

このパラメーター **`<command>`** はモジュールに対応します。

>[!NOTE]
>
>* いずれの場合も、モジュールの起動後に表示さ **れるコメントを削除するために** 、-noconsole引数を追加できます。
>* 逆に、引数 **-verboseを追加して** 、より多くの情報を表示できます。
>



## 監視コマンド {#monitoring-commands-}

>[!NOTE]
>
>すべてのモジュールを表示するには、 **nlserver pdumpコマンドを使用する必要があります** 。

「 **-who** 」パラメーターを追加して、進行中の接続（データベースおよびアプリケーション）をリストできます。

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

もう1つの便利なコマン **ドはnlserver monitorです**。 監視XMLファイル(Adobe Campaignクライアントで取得されるか、 **monitor.jsp** webページ経由で取得される)を示します。

このパラメーターを追 **加して** 、存在しないモジュール（モジュール、モジュールのシャットダウンなどのエラー）をリストします。

```
nlserver monitor -missing
HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
inMail@test
mta@test
wfserver@test
```

これは、自動起動のモジュールに対応していますが、まだ起動されていません。

## モジュール起動コマンド {#module-launch-commands}

モジュールを起動する構文は、次の形式を維持します。

```
nlserver start <module>@<INSTANCE>
```

```
nlserver stop <module>@<INSTANCE>
```

>[!NOTE]
>
>**`<instance>`** は、設定ファイルに入力されたインスタンスの名前、またはモノラルインスタンスモジ **ュールの** デフォルトに対応します。

## サービスのシャットダウン {#shut-down-services}

Adobe Campaignサービスを停止するには、次のいずれかのコマンドを使用します。

* rootまたは管理者アクセス権を持っている場合：

   * Linuxの場合：

      ```
      /etc/init.d/nlserver6 stop
      ```

      >[!NOTE]
      >
      >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）。systemctl **stop nlserver**

   * Windowsの場合：

      ```
      net stop nlserver6
      ```

* そうでない場合は、Adobe Campaignアカウントで次の操作を行います。

   ```
   nlserver shutdown 
   ```

## サービスの再起動 {#restart-services}

同様に、Adobe Campaignを再起動するには、次のいずれかのコマンドを使用できます。

* rootまたは管理者アクセス権を持っている場合：

   * Linuxの場合：/etc/init.d/nlserver6 start

      >[!NOTE]
      >
      >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）。 **systemctl start nlserver**

   * Windowsの場合：net start nlserver6

* それ以外の場合は、Adobe Campaignアカウントで次の操作を行います。 **nlserver watchdog -svc -noconsole**

## configコマンド {#the-config-command}

configコ **マンドを使用すると** 、データベース接続の再設定など、サーバー設定を管理できます。

**-setdbloginパラメータを指定して、** nlserver **実行可能ファイル** のconfigコマンドを使用します **** 。

```
nlserver config -setdblogin:<[dbms:]account[:database][/password]@server>
```

```
nlserver config -setdblogin:PostgreSQL:<accountName>:test6@dbserver
```

パスワードを入力します。

内部パスワードを変 **更するに** : **nlserver config -internalpassword**

>[!CAUTION]
>
>内部識別子を使用してログオ **ンするには** 、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/campaign-server-configuration.md#internal-identifier)を参照してください。

>[!NOTE]
>
>* 一般に、設定ファイルを手動で変更する代わりに、 **config** コマンドを使用できます
>* パラメーターのリストを取得するには、 **-?** パラメーター： **nlserver config -?**
>* Oracleデータベースの場合は、アカウントを指定しないでください。 構文は次のとおりです。
>
>  
nlserver config -setdblogin:Oracle:test6@dbserver


