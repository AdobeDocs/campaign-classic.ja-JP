---
title: Linux 用 Web サーバーへの統合
seo-title: Linux 用 Web サーバーへの統合
description: Linux 用 Web サーバーへの統合
seo-description: null
page-status-flag: never-activated
uuid: 7b18d176-4458-46a8-8da4-3621f90c6b13
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
discoiquuid: 752ba848-aee9-4bb0-b2c5-490f3124f74e
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 8%

---


# Linux 用 Web サーバーへの統合{#integration-into-a-web-server-for-linux}

Adobe Campaignには、HTTP（およびSOAP）を介してアプリケーションサーバーのエントリポイントとして機能するApache Tomcatが含まれます。

この統合Tomcatサーバーを使用して、HTTP要求を処理できます。

この場合、次のようになります。

* デフォルトのリスニングポートは8080です。 変更する方法については、「Tomcatの [設定](../../installation/using/configuring-campaign-server.md#configuring-tomcat)」を参照してください。
* 次に、クライアントコンソールは次のようなURLを使用して接続します。

   ```
   http://<computer>:8080
   ```

ただし、セキュリティと管理上の理由から、Adobe Campaignを実行しているコンピュータがインターネット上に公開され、ネットワーク外のコンソールにアクセスする場合は、HTTPトラフィックのメインエントリポイントとして専用のWebサーバを使用することをお勧めします。

また、Webサーバーでは、HTTPsプロトコルを使用してデータの機密性を保証できます。

同様に、トラッキング機能を使用する場合はWebサーバを使用する必要があります。この機能は、Webサーバへの拡張モジュールとしてのみ使用できます。

>[!NOTE]
>
>トラッキング機能を使用しない場合は、ApacheまたはIISの標準インストールを実行し、キャンペーンへのリダイレクトを行うことができます。 追跡用Webサーバー拡張モジュールは不要です。

## Apache WebサーバーとDebianの設定 {#configuring-the-apache-web-server-with-debian}

このプロセスは、APTに基づく配布の下にApacheをインストールした場合に適用されます。

次の手順に従います。

1. 次のコマンドを使用して、デフォルトで読み込まれるモジュールを無効にします。

   ```
   a2dismod auth_basic authn_file authz_default authz_user autoindex cgi dir env negotiation userdir
   ```

   **alias**、 **authz_host** 、および **mime** モジュールが引き続き有効であることを確認します。 それには、次のコマンドを使用します。

   ```
   a2enmod  alias authz_host mime
   ```

1. /etc/apache2/mods-available **に** nlsrv.load **** ファイルを作成し、次のコンテンツを挿入します。

   Debian 8の場合：

   ```
   LoadModule requesthandler24_module /usr/local/[INSTALL]/nl6/lib/libnlsrvmod.so
   ```

1. 次のコマンドを使用して、/etc/apache2/mods-available **** ( **/etc/apache2/mods-available** )のファイルnlsrv.confを作成します。

   ```
   ln -s /usr/local/[INSTALL]/nl6/tomcat-7/conf/apache_neolane.conf /etc/apache2/mods-available/nlsrv.conf
   ```

1. 次のコマンドを使用して、このモジュールをアクティブにします。

   ```
    a2enmod nlsrv
   ```

   Adobe Campaignページに **mod_rewrite** モジュールを使用する場合は、 **nlsrv.load** とnlsrv.confファイルの名前を変更し、nlsrv.load **と** nlsrv.confファイルの名前を **srv-nsrv.loadlzに変更し、srv.conf-lezに変更する必要があり******&#x200B;ます。 モジュールをアクティブにするには、次のコマンドを実行します。

   ```
   a2enmod zz-nlsrv
   ```

1. /etc/apache2 **/envars** ファイルを編集し、次の行を追加します。

   ```
   # Added Neolane
   if [ "$LD_LIBRARY_PATH" != "" ]; then export LD_LIBRARY_PATH="/usr/local/neolane/nl6/lib:$LD_LIBRARY_PATH"; else export LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib; fi
   export USERPATH=/usr/local/neolane
   ```

   変更を保存します。

1. 次に、次のタイプのコマンドを使用して、Adobe CampaignユーザーをApacheユーザーグループに追加したり、その逆を行ったりします。

   ```
   usermod neolane -G www-data
   usermod www-data -G neolane
   ```

1. Apacheを再起動します。

   ```
   invoke-rc.d apache2 restart
   ```

## RHELでのApache Webサーバーの設定 {#configuring-apache-web-server-in-rhel}

この手順は、RPM（RHEL、CentOS、およびSuse）ベースのパッケージでApacheをインストールし、保護した場合に適用されます。

次の手順に従います。

1. ファイルで、次のApacheモジュールを `httpd.conf` アクティブ化します。

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

1. フォルダー内にAdobe Campaign固有の設定ファイルを作成し `/etc/httpd/conf.d/` ます。 次に例を示します。`CampaignApache.conf`

1. RHEL7 **の場合は、次の手順をファイルに追加します**。

   ```
   LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
   Include /usr/local/neolane/nl6/tomcat-7/conf/apache_neolane.conf
   ```

1. RHEL7 **の場合**:

   追加次の内容を含むファイル： `/etc/systemd/system/httpd.service`

   ```
   .include /usr/lib/systemd/system/httpd.service
   
   [Service]
   Environment=USERPATH=/usr/local/neolane LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib
   ```

   systemdで使用するモジュールを更新します。

   ```
   systemctl daemon-reload
   ```

1. 次に、次のコマンドを実行して、Adobe Campaign演算子をApache演算子グループに追加し、逆に追加します。

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

## Webサーバーの起動と設定のテスト{#launching-the-web-server-and-testing-the-configuration}

これで、Apacheを起動して設定をテストできます。 これで、Adobe Campaignモジュールのコンソールにバナーが表示されます（特定のオペレーティングシステムに2つのバナーが表示されます）。

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

次に、テストURLを送信して応答するかどうかを確認します。

コマンドラインで次のコマンドを実行して、このテストを実行できます。

```
 telnet localhost 80  
```

以下を入手する必要があります。

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

Webブラウザー [`https://<computer>`](https://machine/r/test) からURLを要求することもできます。
