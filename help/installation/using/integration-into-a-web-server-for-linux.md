---
product: campaign
title: Linux向けWeb サーバーへの統合
description: CampaignをWeb サーバー（Linux）に統合する方法について説明します
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
exl-id: 4f8ea358-a38d-4137-9dea-f398e60c5f5d
source-git-commit: 1be1528d657537786c430ea9c8bdb3aad58ba20d
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 8%

---

# Linux向けWeb サーバーへの統合 {#integration-into-a-web-server-for-linux}


Adobe Campaignには、HTTP （およびSOAP）を介してアプリケーションサーバーのエントリポイントとして機能するApache Tomcatが含まれています。

この統合されたTomcat サーバーを使用して、HTTP リクエストを処理できます。

この場合：

* デフォルトのリスニングポートは8080です。 変更する場合は、[このセクション &#x200B;](configure-tomcat.md)を参照してください。
* クライアントコンソールは、次のようなURLを使用して接続します。

  ```
  https://<computer>:8080
  ```

ただし、セキュリティと管理上の理由から、Adobe Campaignを実行しているコンピューターがインターネット上に公開され、ネットワーク外でコンソールへのアクセスを開く場合は、HTTP トラフィックのメインエントリポイントとして専用Web サーバーを使用することをお勧めします。

Web サーバーでは、HTTPs プロトコルによるデータの機密性を保証することもできます。

同様に、Web サーバーの拡張モジュールとしてのみ使用できるトラッキング機能を使用する場合は、Web サーバーを使用する必要があります。

>[!NOTE]
>
>トラッキング機能を使用しない場合は、Campaignへのリダイレクトを使用してApacheまたはIISの標準インストールを実行できます。 トラッキング Web サーバー拡張モジュールは必要ありません。

## DebianでのApache Web サーバーの設定 {#configuring-the-apache-web-server-with-debian}

このプロセスは、APTに基づくディストリビューションにApacheをインストールした場合に適用されます。

次の手順に従います。

1. 次のコマンドを使用して、デフォルトで読み込まれたモジュールを無効にします。

   ```
   a2dismod auth_basic authn_file authz_default authz_user autoindex cgi dir env negotiation userdir
   ```

   **エイリアス**、**authz_host**&#x200B;および&#x200B;**mime** モジュールが引き続き有効であることを確認します。 それには、次のコマンドを使用します。

   ```
   a2enmod  alias authz_host mime
   ```

1. ファイル **nlsrv.load**&#x200B;を&#x200B;**/etc/apache2/mods-available**&#x200B;に作成し、次のコンテンツを挿入します。

   Debian 8の場合：

   ```
   LoadModule requesthandler24_module /usr/local/[INSTALL]/nl6/lib/libnlsrvmod.so
   ```

1. 次のコマンドを使用して、ファイル **nlsrv.conf**&#x200B;を&#x200B;**/etc/apache2/mods-available**&#x200B;に作成します。

   ```
   ln -s /usr/local/[INSTALL]/nl6/conf/apache_neolane.conf /etc/apache2/mods-available/nlsrv.conf
   ```

1. 次のコマンドでこのモジュールをアクティブ化します。

   ```
    a2enmod nlsrv
   ```

   Adobe Campaign ページに&#x200B;**mod_rewrite** モジュールを使用している場合は、**nlsrv.load**&#x200B;および&#x200B;**nlsrv.conf** ファイルの名前を&#x200B;**zz-nlsrv.load**&#x200B;および&#x200B;**zz-nlsrv.conf**&#x200B;に変更する必要があります。 モジュールをアクティベートするには、次のコマンドを実行します。

   ```
   a2enmod zz-nlsrv
   ```

1. **/etc/apache2/envvars** ファイルを編集し、次の行を追加します。

   ```
   # Added Neolane
   if [ "$LD_LIBRARY_PATH" != "" ]; then export LD_LIBRARY_PATH="/usr/local/neolane/nl6/lib:$LD_LIBRARY_PATH"; else export LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib; fi
   export USERPATH=/usr/local/neolane
   ```

   変更を保存します。

1. 次に、次のタイプのコマンドを使用して、Adobe Campaign ユーザーをApache ユーザーグループに追加します。その逆も同様です。

   ```
   usermod neolane -G www-data
   usermod www-data -G neolane
   ```

1. Apacheを再起動します。

   ```
   invoke-rc.d apache2 restart
   ```

## RHELでのApache web サーバーの設定 {#configuring-apache-web-server-in-rhel}

この手順は、RPM （RHEL、CentOS、Suse）ベースのパッケージでApacheをインストールして保護した場合に適用されます。

次の手順に従います。

1. `httpd.conf` ファイルで、次のApache モジュールをアクティブ化します。

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

   非アクティブ化されたモジュールにリンクされている関数にコメントを付けます。

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

1. Adobe Campaign固有の設定ファイルを`/etc/httpd/conf.d/` フォルダーに作成します。 例：`CampaignApache.conf`

1. **RHEL7**&#x200B;の場合、ファイルに次の手順を追加します。

   ```
   LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
   Include /usr/local/neolane/nl6/conf/apache_neolane.conf
   ```

1. **RHEL7**&#x200B;の場合：

   次の内容を含む`/etc/systemd/system/httpd.service` ファイルを追加します。

   ```
   .include /usr/lib/systemd/system/httpd.service
   
   [Service]
   Environment=USERPATH=/usr/local/neolane LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib
   ```

   systemdで使用されるモジュールを更新します。

   ```
   systemctl daemon-reload
   ```

1. 次に、次のコマンドを実行して、Adobe Campaign演算子をApache演算子グループに追加します。その逆も同様です。

   ```
   usermod -a -G neolane apache
   usermod -a -G apache neolane
   ```

   使用するグループ名は、Apacheの設定方法によって異なります。

1. ApacheとAdobe Campaign サーバーを実行します。

   RHEL7の場合：

   ```
   systemctl start httpd
   systemctl start nlserver
   ```

## Web サーバーの起動と設定のテスト{#launching-the-web-server-and-testing-the-configuration}

Apacheを起動して設定をテストできるようになりました。 これで、Adobe Campaign モジュールがコンソールにバナーを表示するようになりました（特定のオペレーティングシステムでは2つのバナー）。

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

次に、テスト URLを送信して応答することを確認します。

コマンドラインから次を実行してテストできます。

```
 telnet localhost 80  
```

次の項目を取得する必要があります。

```
Trying 127.0.0.1...
Connected to localhost.localdomain.
Escape character is '^]'.
```

次に入力します。

```
GET /r/test
```

次の情報が表示されます。

```
<redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='' localHost='XXXX'/>
Connection closed by foreign host.
```

Web ブラウザーからURL `https://myserver.adobe.com/r/test`をリクエストすることもできます。
