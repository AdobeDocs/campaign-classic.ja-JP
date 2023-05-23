---
product: campaign
title: Linux 用 web サーバーへの統合
description: Web サーバー (Linux) に Campaign を統合する方法を説明します
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: 4f8ea358-a38d-4137-9dea-f398e60c5f5d
source-git-commit: 4661688a22bd1a82eaf9c72a739b5a5ecee168b1
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 5%

---

# Linux 用 web サーバーへの統合{#integration-into-a-web-server-for-linux}



Adobe Campaignには、HTTP（および SOAP）を介してアプリケーションサーバー内のエントリポイントとして機能する Apache Tomcat が含まれています。

この統合 Tomcat サーバーを使用して、HTTP リクエストを処理できます。

この場合、次のようになります。

* デフォルトのリスニングポートは 8080 です。 変更するには、 [この節](configure-tomcat.md).
* その後、クライアントコンソールは、次のような URL を使用して接続します。

   ```
   http://<computer>:8080
   ```

ただし、セキュリティと管理上の理由から、Adobe Campaignを実行しているコンピューターがインターネットに公開され、ネットワーク外のコンソールにアクセスする場合は、専用の Web サーバーを HTTP トラフィックのメインエントリポイントとして使用することをお勧めします。

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

   次を確認します。 **エイリアス**, **authz_host** および **mime** モジュールは引き続き有効になります。 それには、次のコマンドを使用します。

   ```
   a2enmod  alias authz_host mime
   ```

1. ファイルを作成します。 **nlsrv.load** in **/etc/apache2/mods-available** 次のコンテンツを挿入します。

   Debian 8 の場合：

   ```
   LoadModule requesthandler24_module /usr/local/[INSTALL]/nl6/lib/libnlsrvmod.so
   ```

1. ファイルを作成します。 **nlsrv.conf** in **/etc/apache2/mods-available** 次のコマンドを使用します。

   ```
   ln -s /usr/local/[INSTALL]/nl6/conf/apache_neolane.conf /etc/apache2/mods-available/nlsrv.conf
   ```

1. 次のコマンドを使用して、このモジュールをアクティブにします。

   ```
    a2enmod nlsrv
   ```

   を使用している場合、 **mod_rewrite** Adobe Campaignページ用のモジュールでは、名前を変更する必要があります **nlsrv.load** および **nlsrv.conf** ファイルを **zz-nlsrv.load** および **zz-nlsrv.conf**. モジュールをアクティブにするには、次のコマンドを実行します。

   ```
   a2enmod zz-nlsrv
   ```

1. を編集します。 **/etc/apache2/envars** ファイルに次の行を追加します。

   ```
   # Added Neolane
   if [ "$LD_LIBRARY_PATH" != "" ]; then export LD_LIBRARY_PATH="/usr/local/neolane/nl6/lib:$LD_LIBRARY_PATH"; else export LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib; fi
   export USERPATH=/usr/local/neolane
   ```

   変更を保存します。

1. 次に、次のタイプのコマンドを使用して、Adobe Campaignユーザーを Apache ユーザーグループに追加し、その逆も追加します。

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

1. 内 `httpd.conf` ファイルを開き、次の Apache モジュールをアクティベートします。

   ```
   alias
   authz_host
   mime
   ```

1. 次のモジュールを非アクティブにします。

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

   非アクティブ化されたモジュールにリンクされた関数にコメントを付けます。

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

1. Adobe Campaign固有の設定ファイルを `/etc/httpd/conf.d/` フォルダー。 次に例を示します。`CampaignApache.conf`

1. の場合 **RHEL7**、次の手順をファイルに追加します。

   ```
   LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
   Include /usr/local/neolane/nl6/conf/apache_neolane.conf
   ```

1. の場合 **RHEL7**:

   を `/etc/systemd/system/httpd.service` ファイルに次の内容を含めます。

   ```
   .include /usr/lib/systemd/system/httpd.service
   
   [Service]
   Environment=USERPATH=/usr/local/neolane LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib
   ```

   systemd で使用するモジュールを更新します。

   ```
   systemctl daemon-reload
   ```

1. 次に、コマンドを実行して、Adobe Campaignオペレーターを Apache オペレーターグループに追加します。また、その逆もおこないます。

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

次に、テスト URL を送信して応答することを確認します。

これは、次のコマンドを実行することで、コマンドラインからテストできます。

```
 telnet localhost 80  
```

次の情報が必要です。

```
Trying 127.0.0.1...
Connected to localhost.localdomain.
Escape character is '^]'.
```

次に、以下を入力します。

```
GET /r/test
```

次の情報が表示されます。

```
<redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='' localHost='XXXX'/>
Connection closed by foreign host.
```

また、URL をリクエストすることもできます [`https://<computer>`](https://myserver.adobe.com/r/test) を Web ブラウザーから取得します。
