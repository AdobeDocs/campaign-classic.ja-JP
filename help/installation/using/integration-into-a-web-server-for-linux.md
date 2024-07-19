---
product: campaign
title: Linux 用 Web サーバーへの統合
description: Campaign を web サーバーに統合する方法を学ぶ（Linux）
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: 4f8ea358-a38d-4137-9dea-f398e60c5f5d
source-git-commit: 1be1528d657537786c430ea9c8bdb3aad58ba20d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 4%

---

# Linux 用 Web サーバーへの統合 {#integration-into-a-web-server-for-linux}


Adobe Campaignには、HTTP （およびSOAP）を介してアプリケーションサーバーへのエントリポイントとして機能する Apache Tomcat が含まれています。

この統合 Tomcat サーバーを使用して、HTTP リクエストを提供できます。

この場合の解決策は、次のとおりです。

* デフォルトのリスニングポートは 8080 です。 変更するには、[ この節 ](configure-tomcat.md) を参照してください。
* その後、クライアントコンソールは、次のような URL を使用して接続します。

  ```
  https://<computer>:8080
  ```

ただし、セキュリティおよび管理上の理由から、Adobe Campaignを実行しているコンピューターがインターネットに公開され、ネットワークの外部にあるコンソールにアクセスする場合は、HTTP トラフィックの主なエントリポイントとして専用の web サーバーを使用することをお勧めします。

また、web サーバーを使用すると、HTTP プロトコルでデータの機密性を保証できます。

同様に、トラッキング機能を使用する場合は、web サーバーを使用する必要があります。トラッキング機能は、web サーバーへの拡張モジュールとしてのみ使用できます。

>[!NOTE]
>
>トラッキング機能を使用しない場合は、Campaign へのリダイレクトを使用して Apache または IIS の標準インストールを実行できます。 トラッキング web サーバー拡張機能モジュールは必須ではありません。

## Debian での Apache web サーバーの設定 {#configuring-the-apache-web-server-with-debian}

このプロセスは、APT に基づいた配布の下に Apache をインストールしている場合に適用されます。

次の手順に従います。

1. 次のコマンドを使用して、デフォルトで読み込まれているモジュールを無効にします。

   ```
   a2dismod auth_basic authn_file authz_default authz_user autoindex cgi dir env negotiation userdir
   ```

   **alias**、**authz_host**、**mime** の各モジュールが引き続き有効になっていることを確認してください。 それには、次のコマンドを使用します。

   ```
   a2enmod  alias authz_host mime
   ```

1. **/etc/apache2/mods-available にファイル** nlsrv.load **を作成し** 次の内容を挿入します。

   Debian 8 では：

   ```
   LoadModule requesthandler24_module /usr/local/[INSTALL]/nl6/lib/libnlsrvmod.so
   ```

1. **/etc/apache2/mods-available のファイル** nlsrv.conf **を次のコマンドを使用し** 作成します。

   ```
   ln -s /usr/local/[INSTALL]/nl6/conf/apache_neolane.conf /etc/apache2/mods-available/nlsrv.conf
   ```

1. このモジュールを有効にするには、次のコマンドを使用します。

   ```
    a2enmod nlsrv
   ```

   Adobe Campaign ページに **mod_rewrite** モジュールを使用している場合は、**nlsrv.load** および **nlsrv.conf** ファイルの名前を **zz-nlsrv.load** および **zz-nlsrv.conf** に変更する必要があります。 モジュールをアクティベートするには、次のコマンドを実行します。

   ```
   a2enmod zz-nlsrv
   ```

1. **/etc/apache2/envars** ファイルを編集し、次の行を追加します。

   ```
   # Added Neolane
   if [ "$LD_LIBRARY_PATH" != "" ]; then export LD_LIBRARY_PATH="/usr/local/neolane/nl6/lib:$LD_LIBRARY_PATH"; else export LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib; fi
   export USERPATH=/usr/local/neolane
   ```

   変更を保存します。

1. 次に、次のコマンドを使用して、Adobe Campaign ユーザーを Apache ユーザーグループに、またその逆に追加します。

   ```
   usermod neolane -G www-data
   usermod www-data -G neolane
   ```

1. Apache を再起動します。

   ```
   invoke-rc.d apache2 restart
   ```

## RHEL での Apache web サーバーの設定 {#configuring-apache-web-server-in-rhel}

この手順は、RPM （RHEL、CentOS および Suse）ベースのパッケージの下で Apache をインストールして保護した場合に適用されます。

次の手順に従います。

1. `httpd.conf` ファイルで、次の Apache モジュールを有効にします。

   ```
   alias
   authz_host
   mime
   ```

1. 次のモジュールをディアクティベートします。

   ```
   auth_basic
   authn_file
   authz_default
   authz_user
   autoindex
   cgi
   dir
   env
   negotiation
   userdir
   ```

   非アクティブ化されたモジュールにリンクされた関数をコメント化します。

   ```
   DirectoryIndex
   IndexOptions    
   AddIconByEncoding    
   AddIconByType    
   AddIcon    
   DefaultIcon    
   ReadmeName    
   HeaderName    
   IndexIgnore    
   LanguagePriority    
   ForceLanguagePriority
   ```

1. `/etc/httpd/conf.d/` フォルダーにAdobe Campaign固有の設定ファイルを作成します。 例：`CampaignApache.conf`

1. **RHEL7** の場合は、ファイルに次の手順を追加します。

   ```
   LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
   Include /usr/local/neolane/nl6/conf/apache_neolane.conf
   ```

1. **RHEL7** の場合：

   次の内容の `/etc/systemd/system/httpd.service` ファイルを追加します。

   ```
   .include /usr/lib/systemd/system/httpd.service
   
   [Service]
   Environment=USERPATH=/usr/local/neolane LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib
   ```

   systemd で使用されるモジュールを更新します。

   ```
   systemctl daemon-reload
   ```

1. 次に、コマンドを実行して、Adobe Campaign オペレーターを Apache オペレーターグループに追加します（その逆も同様です）。

   ```
   usermod -a -G neolane apache
   usermod -a -G apache neolane
   ```

   使用するグループ名は、Apache の設定方法によって異なります。

1. Apache とAdobe Campaign サーバーを実行します。

   RHEL7 の場合：

   ```
   systemctl start httpd
   systemctl start nlserver
   ```

## Web サーバーの起動と設定のテスト{#launching-the-web-server-and-testing-the-configuration}

これで、Apache を起動して設定をテストできます。 これで、Adobe Campaign モジュールのバナーがコンソールに表示されます（特定のオペレーティングシステムでは 2 つのバナー）。

```
 /etc/init.d/apache start
```

次の情報が表示されます。

```sql
12:26:28 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:26:28 >   Web server start (pid=29698, tid=-1212463424)...
12:26:28 >   Server started
12:26:28 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:26:28 >   Web server start (pid=29698, tid=-1212463424)...
12:26:28 >   Server started
```

次に、テスト URL を送信して、応答することを確認します。

これは、コマンドラインから次のコマンドを実行してテストできます。

```
 telnet localhost 80  
```

次を取得する必要があります。

```
Trying 127.0.0.1...
Connected to localhost.localdomain.
Escape character is '^]'.
```

次のように入力します。

```
GET /r/test
```

次の情報が表示されます。

```
<redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='' localHost='XXXX'/>
Connection closed by foreign host.
```

Web ブラウザーから URL `https://myserver.adobe.com/r/test` をリクエストすることもできます。
