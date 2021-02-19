---
solution: Campaign Classic
product: campaign
title: 通常のコマンド
description: 通常のコマンド
audience: production
content-type: reference
topic-tags: production-procedures
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 4%

---


# 通常のコマンド{#usual-commands}

この節では、Adobe Campaignの通常のコマンドをリストします。

**nlserver**&#x200B;コマンドは、Adobe Campaignアプリケーション全体の入力コマンドです。

このコマンドの構文は次のとおりです。**nlserver **`<command>`****`<arguments>`****

パラメータ&#x200B;**`<command>`**&#x200B;はモジュールに対応します。

>[!NOTE]
>
>* どのような場合でも、**-noconsole**&#x200B;引数を追加して、モジュールの起動後に表示されるコメントを削除できます。
>* 逆に、引数&#x200B;**-verbose**&#x200B;を追加すると、詳細情報を表示できます。

>



## 監視コマンド{#monitoring-commands-}

>[!NOTE]
>
>すべてのモジュールをリストするには、**nlserver pdump**&#x200B;コマンドを使用する必要があります。

パラメーター&#x200B;**-who**&#x200B;を追加して、進行中の接続（データベースとアプリケーション）をリストできます。

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

**nlserver monitor**&#x200B;もう1つの便利なコマンドです。 監視XMLファイルをリストします(Adobe Campaignクライアントで取得するか、**monitor.jsp** Webページを介して取得)。

パラメーター&#x200B;**-missing**&#x200B;を追加して、存在しないモジュールをリストできます（モジュール、モジュールのシャットダウンなどでのエラー）。

```
nlserver monitor -missing
HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
inMail@test
mta@test
wfserver@test
```

これは、自動起動のモジュールに対応しますが、まだ起動されていません。

## モジュール起動コマンド{#module-launch-commands}

モジュールを起動する構文は、次の形式を維持します。

```
nlserver start <module>@<INSTANCE>
```

```
nlserver stop <module>@<INSTANCE>
```

>[!NOTE]
>
>**`<instance>`** は、設定ファイルで入力したインスタンスの名前に対応します。または、モノラルインスタンスモジュールの **** デフォルトに対応します。

## サービスのシャットダウン {#shut-down-services}

Adobe Campaignサービスを停止するには、次のいずれかのコマンドを使用します。

* rootまたは管理者アクセス権を持っている場合：

   * Linuxの場合：

      ```
      /etc/init.d/nlserver6 stop
      ```

      >[!NOTE]
      >
      >20.1からは、（Linuxの場合は）次のコマンドを使用することをお勧めします。**systemctl stop nlserver**

   * Windowsの場合：

      ```
      net stop nlserver6
      ```

* そうでない場合は、Adobe Campaignアカウントで次の操作を行います。

   ```
   nlserver shutdown 
   ```

## サービスの再起動 {#restart-services}

同様に、Adobe Campaignを再起動するには、次のいずれかのコマンドを使用します。

* rootまたは管理者アクセス権を持っている場合：

   * Linuxの場合：/etc/init.d/nlserver6開始

      >[!NOTE]
      >
      >20.1からは、（Linuxの場合は）次のコマンドを使用することをお勧めします。**systemctl開始nlserver**

   * Windowsの場合：net開始nlserver6

* それ以外の場合は、Adobe Campaignアカウントで次の操作を行います。**nlserver watchdog -svc -noconsole**

## configコマンド{#the-config-command}

**config**&#x200B;コマンドを使用すると、データベース接続の再構成など、サーバーの設定を管理できます。

**-setdblogin**&#x200B;パラメータを指定して、**nlserver**&#x200B;実行ファイルの&#x200B;**config**&#x200B;コマンドを使用します。

```
nlserver config -setdblogin:<[dbms:]account[:database][/password]@server>
```

```
nlserver config -setdblogin:PostgreSQL:<accountName>:test6@dbserver
```

パスワードを入力します。

**内部**&#x200B;パスワードを変更するには：**nlserver config -internalpassword**

>[!IMPORTANT]
>
>**内部**&#x200B;識別子を使用してログオンするには、事前にパスワードを定義しておく必要があります。 詳しくは、[こちらの節](../../installation/using/campaign-server-configuration.md#internal-identifier)を参照してください。

>[!NOTE]
>
>* 一般に、設定ファイルを手動で変更する代わりに、**config**&#x200B;コマンドを使用できます
>* パラメーターのリストを取得するには、**-?** パラメーター： **nlserver config - ?**
>* oracleデータベースの場合は、アカウントを指定しないでください。 構文は次のとおりです。

>
>  
nlserver config -setdblogin:Oracle:test6@dbserver

