---
title: Linux用のWebサーバーへの統合
seo-title: Linux用のWebサーバーへの統合
description: Linux用のWebサーバーへの統合
seo-description: null
page-status-flag: never-activated
uuid: 7b18d176-4458-46a8-8da4-3621f90c6b13
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-linux-
discoiquuid: 752ba848-aee9-4bb0-b2c5-490f3124f74e
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: abddb3cdfcee9e41cab2e7e662d5bfd5d53d6f7e

---


# Linux用のWebサーバーへの統合{#integration-into-a-web-server-for-linux}

Adobe Campaignには、HTTP（およびSOAP）を介してアプリケーションサーバーのエントリポイントとして機能するApache tomcatが含まれています。

この統合Tomcatサーバーを使用して、HTTP要求を処理できます。

この場合：

* デフォルトのリスニングポートは8080です。 変更するには、「Tomcatの設定」を参 [照してください](../../installation/using/configuring-campaign-server.md#configuring-tomcat)。
* 次に、クライアントコンソールは次のようなURLを使用して接続します。

   ```
   http://<computer>:8080
   ```

ただし、セキュリティと管理上の理由から、Adobe Campaignを実行しているコンピューターがインターネット上で公開され、ネットワーク外のコンソールにアクセスする場合は、HTTPトラフィックのメインエントリポイントとして専用のWebサーバーを使用することをお勧めします。

また、Webサーバーを使用すると、HTTPsプロトコルでのデータの機密性を保証できます。

同様に、トラッキング機能を使用する場合はWebサーバを使用する必要があります。この機能は、Webサーバへの拡張モジュールとしてのみ使用できます。

>[!NOTE]
>
>トラッキング機能を使用しない場合は、ApacheまたはIISの標準インストールを実行し、Campaignへのリダイレクトを行うことができます。 追跡用Webサーバー拡張モジュールは不要です。

## DebianでのApache webサーバーの設定 {#configuring-the-apache-web-server-with-debian}

このプロセスは、APTに基づく配布物の下にApacheをインストールした場合に適用されます。

次の手順に従います。

1. 次のコマンドを使用して、デフォルトで読み込まれるモジュールを無効にします。

   ```
   a2dismod auth_basic authn_file authz_default authz_user autoindex cgi dir env negotiation userdir
   ```

   alias、 **authz_host**、および **mimeモジュールが有効であ****** ることを確認します。 それには、次のコマンドを使用します。

   ```
   a2enmod  alias authz_host mime
   ```

1. /etc/apache2/mods-available **内にnlsrv.load****ファイルを作成し、次のコンテンツを挿入します** 。

   Debian 7の場合：

   ```
   LoadModule requesthandler22_module /usr/local/[INSTALL]/nl6/lib/libnlsrvmod.so
   ```

   Debian 8の場合：

   ```
   LoadModule requesthandler24_module /usr/local/[INSTALL]/nl6/lib/libnlsrvmod.so
   ```

1. 次のコマンド **を使用して、** /etc/apache2/mods-availableにファイルnlsrv.conf **** を作成します。

   ```
   ln -s /usr/local/[INSTALL]/nl6/tomcat-7/conf/apache_neolane.conf /etc/apache2/mods-available/nlsrv.conf
   ```

1. 次のコマンドを使用して、このモジュールをアクティブにします。

   ```
    a2enmod nlsrv
   ```

   Adobe Campaignページ用の **mod_rewrite** モジュールを使用する場合は、 **nlsrv.load** とnlsrv.conf **ファイルの名前を、** srv.load.conf ******** srvとlosrv.conf srvに変更する必要があります。 モジュールをアクティブにするには、次のコマンドを実行します。

   ```
   a2enmod zz-nlsrv
   ```

1. /etc/apache2 **/envarsファイルを編集し** 、次の行を追加します。

   ```
   # Added Neolane
   if [ "$LD_LIBRARY_PATH" != "" ]; then export LD_LIBRARY_PATH="/usr/local/neolane/nl6/lib:$LD_LIBRARY_PATH"; else export LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib; fi
   export USERPATH=/usr/local/neolane
   ```

   変更を保存します。

1. 次に、次のタイプのコマンドを使用して、Adobe CampaignユーザーをApacheユーザーグループに追加し、その逆も同様です。

   ```
   usermod neolane -G www-data
   usermod www-data -G neolane
   ```

1. Apacheを再起動します。

   ```
   invoke-rc.d apache2 restart
   ```

## RHELでのApache webサーバーの設定 {#configuring-apache-web-server-in-rhel}

この手順は、RPM（RHEL、CentOSおよびSuse）ベースのパッケージでApacheをインストールし、保護した場合に適用されます。

次の手順に従います。

1. ファイルで、 `httpd.conf` 次のApacheモジュールをアクティブにします。

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

非アクティブ化されたモジュールにリンクされた関数をコメント化します。

    &quot;
    
    
    
    
    
    
    
    
    
    
    DirectoryIndexIndexOptionsAddIconByEncodingAddIconByTypeAddIconDefaultIconReadmeNameNameIndexIgnoreLanguagePriorityForcePriority
    &quot;

1. フォルダーにAdobe Campaign固有の設定ファイルを作成し `/etc/httpd/conf.d/` ます。

For example `CampaignApache.conf`.

1. RHEL6 **の場合**、次の手順をファイルに追加します。

   ```
   LoadModule requesthandler22_module /usr/local/neolane/nl6/lib/libnlsrvmod.so
   Include /usr/local/neolane/nl6/tomcat-7/conf/apache_neolane.conf
   ```

RHEL7 **の場合**、次の手順をファイルに追加します。

LoadModule requesthandler24_module /usr/local/neolane/nl6/lib/libnlsrvmod.soInclude /usr/local/neolane/nl6/tomcat-7/conf/apache_neolane.conf

1. **RHEL6の場合**:

ファイルに次の手順を追加し `/etc/sysconfig/httpd` ます。

    &quot;
    #Neolane/Adobe Campaign
    Configurationif [ &quot;$LD_LIBRARY_PATH&quot; != &quot;&quot; ];次に、LD_LIBRARY_PATH=&quot;/usr/local/neolane/nl6/lib:$LD_LIBRARY_PATH&quot;；をエクスポートします。else export LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib;
    fiexport USERPATH=/usr/local/neolane
    &quot;

**RHEL7の場合**:

次の内容を `/etc/systemd/system/httpd.service` 含むファイルを追加します。

    &quot;
    .include /usr/lib/systemd/system/httpd.service
    
    [Service]
    Environment=USERPATH=/usr/local/neolane LD_LIBRARY_PATH=/usr/local/neolane/nl6/lib
    &quot;

systemdが使用するモジュールを更新します。

    &quot;
    systemctl daemon-reload
    &quot;

1. 次に、次のコマンドを実行して、Adobe Campaign演算子をApache演算子グループに追加します。また、その逆も同様です。

   ```
   usermod -a -G neolane apache
   usermod -a -G apache neolane
   ```
使用するグループ名は、Apacheの設定方法によって異なります。

1. ApacheとAdobe Campaignサーバーを実行します。

RHEL6の場合：

    &quot;
    /etc/init.d/httpd start
    /etc/init.d/nlserver start
    &quot;

RHEL7の場合：

    &quot;
    systemctl start
    httpdsystemctl start nlserver
    &quot;

## Webサーバーの起動と設定のテスト{#launching-the-web-server-and-testing-the-configuration}

Apacheを起動して設定をテストできるようになりました。 Adobe Campaignモジュールでは、コンソールにバナーが表示されるようになりました（特定のオペレーティングシステムには2つのバナーが表示されます）。

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

コマンドラインから次のコマンドを実行して、このテストを実行できます。

```
 telnet localhost 80  
```

以下を入手する必要があります。

```
Trying 127.0.0.1...
Connected to localhost.localdomain.
Escape character is '^]'.
````

次のように入力します。

```
GET /r/test
````

次の情報が表示されます。

```
<redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='' localHost='XXXX'/>
Connection closed by foreign host.
````

WebブラウザーからURLをリクエストす [`http://<computer>`](http://machine/r/test) ることもできます。