---
product: campaign
title: Linux 用 web サーバーへの統合
description: Campaign を Web サーバーに統合する方法を説明します (Linux)。
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: 4f8ea358-a38d-4137-9dea-f398e60c5f5d
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 5%

---

# Linux 用 web サーバーへの統合{#integration-into-a-web-server-for-linux}

![](../../assets/v7-only.svg)

Adobe Campaignには、HTTP（および SOAP）を介してアプリケーションサーバーのエントリポイントとして機能する Apache Tomcat が含まれています。

この統合 Tomcat サーバーを使用して、HTTP リクエストを処理できます。

この場合：

* デフォルトのリスニングポートは 8080 です。 変更するには、[ この節 ](configure-tomcat.md) を参照してください。
* その後、クライアントコンソールは、次のような URL を使用して接続します。

   ```
   http://<computer>:8080
   ```

ただし、セキュリティと管理上の理由から、Adobe Campaignを実行しているコンピューターがインターネット上で公開され、ネットワーク外のコンソールにアクセスする場合は、専用の Web サーバーを HTTP トラフィックのメインエントリポイントとして使用することをお勧めします。

また、Web サーバーを使用すると、HTTPs プロトコルでデータの機密性を保証できます。

同様に、Web サーバーは、Web サーバーへの拡張モジュールとしてのみ使用できるトラッキング機能を使用する場合に使用する必要があります。

>[!NOTE]
>
>トラッキング機能を使用しない場合は、Apache または IIS の標準インストールを実行し、Campaign にリダイレクトできます。 トラッキング Web サーバー拡張モジュールは不要です。

## Debian での Apache Web サーバーの設定 {#configuring-the-apache-web-server-with-debian}

このプロセスは、APT に基づくディストリビューションの下に Apache をインストールした場合に適用されます。

次の手順に従います。

1. 次のコマンドを使用して、デフォルトで読み込まれるモジュールを無効にします。

   ```
   a2dismod auth_basic authn_file authz_default authz_user autoindex cgi dir env negotiation userdir
   ```

   **alias**、**authz_host** および **mime** モジュールが引き続き有効になっていることを確認します。 それには、次のコマンドを使用します。

   ```
   a2enmod  alias authz_host mime
   ```

1. **nlsrv.load** ファイルを **/etc/apache2/mods-available** に作成し、次の内容を挿入します。

   Debian 8 の場合：

   ```
   LoadModule requesthandler24_module /usr/local/[INSTALL]/nl6/lib/libnlsrvmod.so
   ```

1. 次のコマンドを使用して、**nlsrv.conf** を **/etc/apache2/mods-available** に作成します。

   ```
   ln -s /usr/local/[INSTALL]/nl6/conf/apache_neolane.conf /etc/apache2/mods-available/nlsrv.conf
   ```

1. 次のコマンドを使用して、このモジュールをアクティブにします。

   ```
    a2enmod nlsrv
   ```

   Adobe Campaignのページに **mod_rewrite** モジュールを使用する場合は、**nlsrv.load** および **nlsrv.conf** ファイルの名前を **zz-nlsrv.load** および **zz-nlsrv.conf&lt;a/> に変更する必要があります。**&#x200B;モジュールをアクティブにするには、次のコマンドを実行します。

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

1. 次に、次のタイプのコマンドを使用して、Adobe Campaignユーザーを Apache ユーザーグループに追加し、その逆もおこないます。

   ```
   usermod neolane -G www-data
   usermod www-data -G neolane
   ```

1. Apache を再起動します。

   ```
   invoke-rc.d apache2 restart
   ```

## RHEL での Apache Web サーバーの設定 {#configuring-apache-web-server-in-rhel}

この手順は、RPM（RHEL、CentOS および Suse）ベースのパッケージの下に Apache をインストールし、保護している場合に適用されます。

次の手順に従います。

1. `httpd.conf` ファイルで、次の Apache モジュールをアクティベートします。

   ```
   alias
   authz_host
   mime
   ```

1. 次のモジュールを非アクティブ化します。

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

   非アクティブ化されたモジュールに関連する関数にコメントを付けます。

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

1. `/etc/httpd/conf.d/` フォルダーにAdobe Campaign固有の設定ファイルを作成します。 次に例を示します。`CampaignApache.conf`

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

   systemd で使用するモジュールを更新します。

   ```
   systemctl daemon-reload
   ```

1. 次に、コマンドを実行して、Adobe Campaignオペレーターを Apache オペレーターグループに追加します。また、その逆も行います。

   ```
   usermod -a -G neolane apache
   usermod -a -G apache neolane
   ```

   使用するグループ名は、Apache の設定方法によって異なります。

1. Apache とAdobe Campaignサーバーを実行します。

   RHEL7 の場合：

   ```
   systemctl start httpd
   systemctl start nlserver
   ```

## Web サーバーの起動と設定のテスト{#launching-the-web-server-and-testing-the-configuration}

これで、Apache を起動して設定をテストできます。 Adobe Campaignモジュールのコンソールにバナーが表示されます（特定のオペレーティングシステムでは 2 つのバナー）。

```
 /etc/init.d/apache start
```

次の情報が表示されます。

```
12:26:28 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:26:28 >   Web server start (pid=29698, tid=-1212463424)...
12:26:28 >   Server started
12:26:28 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
12:26:28 >   Web server start (pid=29698, tid=-1212463424)...
12:26:28 >   Server started
```

次に、テスト URL を送信して応答するかどうかを確認します。

次のコマンドを実行して、コマンドラインからこれをテストできます。

```
 telnet localhost 80  
```

次の情報を入手する必要があります。

```
Trying 127.0.0.1...
Connected to localhost.localdomain.
Escape character is '^]'.
```

次に、を入力します。

```
GET /r/test
```

次の情報が表示されます。

```
<redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='' localHost='XXXX'/>
Connection closed by foreign host.
```

Web ブラウザーから URL [`https://<computer>`](https://myserver.adobe.com/r/test) を要求することもできます。
