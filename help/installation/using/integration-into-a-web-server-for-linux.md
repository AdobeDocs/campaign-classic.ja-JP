---
product: campaign
title: Linux 用 web サーバーへの統合
description: CampaignをWebサーバーに統合する方法を説明します(Linux)。
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: 4f8ea358-a38d-4137-9dea-f398e60c5f5d
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 5%

---

# Linux 用 web サーバーへの統合{#integration-into-a-web-server-for-linux}

Adobe Campaignには、HTTP（およびSOAP）を介してアプリケーションサーバーのエントリポイントとして機能するApache Tomcatが含まれています。

この統合Tomcatサーバーを使用して、HTTPリクエストを処理できます。

この場合、次のようになります。

* デフォルトのリスニングポートは8080です。 これを変更するには、[この節](configure-tomcat.md)を参照してください。
* その後、クライアントコンソールは、次のようなURLを使用して接続します。

   ```
   http://<computer>:8080
   ```

ただし、セキュリティと管理上の理由から、Adobe Campaignを実行しているコンピューターがインターネット上で公開され、ネットワーク外のコンソールにアクセスする場合は、専用のWebサーバーをHTTPトラフィックのメインエントリポイントとして使用することをお勧めします。

また、Webサーバーを使用すると、HTTPプロトコルによるデータの機密性を保証できます。

同様に、トラッキング機能を使用する場合は、Webサーバーを使用する必要があります。この機能は、Webサーバーへの拡張モジュールとしてのみ使用できます。

>[!NOTE]
>
>トラッキング機能を使用しない場合は、ApacheまたはIISの標準インストールを実行し、Campaignにリダイレクトできます。 トラッキングWebサーバー拡張モジュールは不要です。

## DebianでのApache Webサーバーの設定{#configuring-the-apache-web-server-with-debian}

このプロセスは、APTに基づくディストリビューションの下にApacheをインストールした場合に適用されます。

次の手順に従います。

1. 次のコマンドを使用して、デフォルトで読み込まれるモジュールを無効にします。

   ```
   a2dismod auth_basic authn_file authz_default authz_user autoindex cgi dir env negotiation userdir
   ```

   **alias**、**authz_host**&#x200B;および&#x200B;**mime**&#x200B;モジュールが引き続き有効になっていることを確認します。 それには、次のコマンドを使用します。

   ```
   a2enmod  alias authz_host mime
   ```

1. **nlsrv.load**&#x200B;ファイルを&#x200B;**/etc/apache2/mods-available**&#x200B;に作成し、次のコンテンツを挿入します。

   Debian 8の場合：

   ```
   LoadModule requesthandler24_module /usr/local/[INSTALL]/nl6/lib/libnlsrvmod.so
   ```

1. 次のコマンドを使用して、**nlsrv.conf**&#x200B;ファイルを&#x200B;**/etc/apache2/mods-available**&#x200B;に作成します。

   ```
   ln -s /usr/local/[INSTALL]/nl6/conf/apache_neolane.conf /etc/apache2/mods-available/nlsrv.conf
   ```

1. 次のコマンドを使用して、このモジュールを有効にします。

   ```
    a2enmod nlsrv
   ```

   Adobe Campaignページ用に&#x200B;**mod_rewrite**&#x200B;モジュールを使用する場合、**nlsrv.load**&#x200B;および&#x200B;**nlsrv.conf**&#x200B;ファイルの名前を&#x200B;**zz-nlsrv.load**&#x200B;および&#x200B;**zz-nlsrv.conf**&#x200B;に変更する必要があります。 モジュールをアクティブにするには、次のコマンドを実行します。

   ```
   a2enmod zz-nlsrv
   ```

1. **/etc/apache2/envars**&#x200B;ファイルを編集し、次の行を追加します。

   ```
   # Added Neolane
   if [ "$LD_LIBRARY_PATH" != "" ]; then export LD_LIBRARY_PATH="/usr/local/neolane/nl6/lib:$LD_LIBRARY_PATH"; else export LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib; fi
   export USERPATH=/usr/local/neolane
   ```

   変更を保存します。

1. 次に、次のタイプのコマンドを使用して、Adobe CampaignユーザーをApacheユーザーグループに追加し、その逆を実行します。

   ```
   usermod neolane -G www-data
   usermod www-data -G neolane
   ```

1. Apacheを再起動します。

   ```
   invoke-rc.d apache2 restart
   ```

## RHELでのApache Webサーバーの設定{#configuring-apache-web-server-in-rhel}

この手順は、RPM（RHEL、CentOSおよびSuse）ベースのパッケージでApacheをインストールし、保護している場合に適用されます。

次の手順に従います。

1. `httpd.conf`ファイルで、次のApacheモジュールをアクティブにします。

   ```
   alias
   authz_host
   mime
   ```

1. 次のモジュールのアクティベートを解除します。

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

1. `/etc/httpd/conf.d/`フォルダーにAdobe Campaign固有の設定ファイルを作成します。 次に例を示します。`CampaignApache.conf`

1. **RHEL7**&#x200B;の場合は、次の手順をファイルに追加します。

   ```
   LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
   Include /usr/local/neolane/nl6/conf/apache_neolane.conf
   ```

1. **RHEL7**&#x200B;の場合：

   次の内容の`/etc/systemd/system/httpd.service`ファイルを追加します。

   ```
   .include /usr/lib/systemd/system/httpd.service
   
   [Service]
   Environment=USERPATH=/usr/local/neolane LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib
   ```

   systemdで使用するモジュールを更新します。

   ```
   systemctl daemon-reload
   ```

1. 次に、コマンドを実行して、Adobe CampaignオペレーターをApacheオペレーターグループに追加し、その逆も実行します。

   ```
   usermod -a -G neolane apache
   usermod -a -G apache neolane
   ```

   使用するグループ名は、Apacheの設定方法によって異なります。

1. ApacheとAdobe Campaignサーバーを実行します。

   RHEL7の場合：

   ```
   systemctl start httpd
   systemctl start nlserver
   ```

## Webサーバーを起動し、設定をテストします。{#launching-the-web-server-and-testing-the-configuration}

これで、Apacheを起動して設定をテストできます。 Adobe Campaignモジュールのコンソールにバナーが表示されます（特定のオペレーティングシステムでは2つのバナー）。

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

次に、テストURLを送信して応答することを確認します。

これは、次のコマンドを実行して、コマンドラインからテストできます。

```
 telnet localhost 80  
```

次の情報を取得する必要があります。

```
Trying 127.0.0.1...
Connected to localhost.localdomain.
Escape character is '^]'.
```

次に、次を入力します。

```
GET /r/test
```

次の情報が表示されます。

```
<redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='' localHost='XXXX'/>
Connection closed by foreign host.
```

WebブラウザーからURL [`https://<computer>`](https://myserver.adobe.com/r/test)を要求することもできます。
