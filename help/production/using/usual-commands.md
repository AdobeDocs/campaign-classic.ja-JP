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
TQID: https://experienceleague.adobe.com/54ErpGUWBV076fqJIdr2ZsJlKVicuFf4xNgk-qDvvmQ
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2:
  - id: c03a11ff-bdf9-4e5b-b279-f468b4293464
  - id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 458
ht-degree: 11%

---

# 通常のコマンド{#usual-commands}



ここでは、Adobe Campaignの通常のコマンドの一覧を示します。

コマンド **nlserver**&#x200B;は、Adobe Campaign アプリケーション全体の入力コマンドです。

このコマンドの構文は次のとおりです。**nlserver &#x200B;**`<command>`**&#x200B;**`<arguments>`**&#x200B;**

パラメーター&#x200B;**`<command>`**&#x200B;はモジュールに対応しています。

>[!NOTE]
>
>* いずれにしても、**-noconsole**&#x200B;引数を追加して、モジュールの開始後に表示されるコメントを削除できます。
>* 逆に、引数&#x200B;**-verbose**&#x200B;を追加すると、より多くの情報を表示できます。
>

## 監視コマンド {#monitoring-commands-}

>[!NOTE]
>
>すべてのモジュールを一覧表示するには、**nlserver pdump** コマンドを使用する必要があります。

パラメーター&#x200B;**-who**&#x200B;を追加して、進行中の接続（データベースとアプリケーション）を一覧表示できます。

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

もう1つの便利なコマンドは、**nlserver monitor**&#x200B;です。 監視XML ファイル（**monitor.jsp** web ページまたはAdobe Campaign クライアントで取得）が一覧表示されます。

パラメーター&#x200B;**-missing**&#x200B;を追加して、存在しないモジュール（モジュールのエラー、モジュールのシャットダウンなど）を一覧表示できます

```sql
nlserver monitor -missing
HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
inMail@test
mta@test
wfserver@test
```

これは、自動起動を備えているが、起動していないモジュールに対応します。

## モジュール起動コマンド {#module-launch-commands}

モジュールを起動する構文は、引き続き次の形式になります。

```sql
nlserver start <module>@<INSTANCE>
```

```sql
nlserver stop <module>@<INSTANCE>
```

>[!NOTE]
>
>**`<instance>`**&#x200B;は、設定ファイルに入力されたインスタンスの名前に対応します。また、モノラルインスタンスモジュールの場合は&#x200B;**デフォルト**&#x200B;に対応します。

## サービスのシャットダウン {#shut-down-services}

Adobe Campaign サービスを停止するには、次のいずれかのコマンドを使用します。

* rootまたは管理者のアクセス権がある場合：

   * Linuxでは：

     ```sql
     /etc/init.d/nlserver6 stop
     ```

     >[!NOTE]
     >
     >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）: **systemctl stop nlserver**

   * Windowsでは：

     ```sql
     net stop nlserver6
     ```

* そうでない場合は、Adobe Campaign アカウントで次の操作を行います。

  ```sql
  nlserver shutdown 
  ```

## サービスの再起動 {#restart-services}

同様に、Adobe Campaignを再起動するには、次のいずれかのコマンドを使用します。

* rootまたは管理者のアクセス権がある場合：

   * Linuxの場合：`/etc/init.d/nlserver6 start`

     >[!NOTE]
     >
     >20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）: **systemctl start nlserver**

   * Windowsの場合：`net start nlserver6`

* それ以外の場合は、Adobe Campaign アカウントで&#x200B;**nlserver watchdog -svc -noconsole**

## config コマンド {#the-config-command}

**config** コマンドを使用すると、データベース接続の再設定を含むサーバー設定を管理できます。

**-setdblogin** パラメーターを使用して、**nlserver**&#x200B;実行可能ファイルの&#x200B;**config** コマンドを使用します。

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
>**Internal**&#x200B;識別子でログオンするには、事前にパスワードを定義しておく必要があります。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#internal-identifier)を参照してください。

>[!NOTE]
>
>* 通常、設定ファイルを手動で変更する代わりに、**config** コマンドを使用できます
>* パラメーターのリストを取得するには、**-?**&#x200B;を使用します パラメーター：**nlserver config -?**
>* Oracle データベースの場合は、アカウントを指定しないでください。 構文は次のようになります。
>
>  `nlserver config -setdblogin:Oracle:test6@dbserver`
>

MSSQLの例を次に示します。

```sql
nlserver config -setdblogin:mssql:<login>/"<password>"@<server> -instance:<instance_name> 
```

* ログイン（例：アカウント :user）とサーバーは、config-&lt;instance_name>.xml ファイルのdataSource ノードにあります。
* パスワードは引用符「」で囲む必要があります。

