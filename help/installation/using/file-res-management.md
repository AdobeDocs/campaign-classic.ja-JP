---
product: campaign
title: ファイルとリソースの管理
feature: Installation, Application Settings
description: Campaign でファイルとリソースの管理を設定する方法を学ぶ
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 236afdfe-fb23-4ebb-b000-76e14bf01d9e
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 2%

---

# ファイルとリソースの管理{#file-and-resmanagement}



## アップロードファイル形式を制限 {#limiting-uploadable-files}

の使用 **uploadWhiteList** Adobe Campaign サーバーでアップロードできるファイルタイプを制限する属性。

この属性は、 **dataStore** の要素 **serverConf.xml** ファイル。 で使用できるすべてのパラメーター **serverConf.xml** の一覧はこちら [セクション](../../installation/using/the-server-configuration-file.md).

この属性のデフォルト値はです。 **.+** 任意のファイルタイプをアップロードできます。

可能な形式を制限するには、属性値を有効な Java 正規表現に置き換えます。 複数の値を入力する場合は、コンマで区切ります。

例： **uploadWhiteList=&quot;.&#42;.png、&#42;.jpg&quot;** では、PNG およびJPG形式をサーバーにアップロードできます。 その他の形式は受け付けられません。

Web サーバーを設定して、重要なファイルがアップロードされないようにすることもできます。 [詳細情報](web-server-configuration.md)

>[!NOTE]
>
>この **uploadWhiteList** 属性は、Adobe Campaign サーバーでアップロードできるファイルタイプを制限します。 ただし、公開モードがの場合は、 **トラッキングサーバー** または **その他のAdobe Campaign サーバー**, **uploadWhitelist** また、これらのサーバーで属性を更新する必要があります。

## プロキシ接続設定 {#proxy-connection-configuration}

プロキシを使用して、Campaign サーバーを外部システムに接続するには、 **ファイル転送** ワークフローアクティビティ（例：）。 これを行うには、 **proxyConfig** の節 **serverConf.xml** 特定のコマンドを使用してファイルに書き込みます。 で使用できるすべてのパラメーター **serverConf.xml** の一覧はこちら [セクション](../../installation/using/the-server-configuration-file.md).

HTTP、HTTPS、FTP、SFTP などのプロキシ接続が可能です。 20.2 Campaign リリース以降、HTTP および HTTPS プロトコルパラメーターは **公開停止**. これらのパラメーターは、9032 を含む以前のビルドでも引き続き使用できるので、引き続き以下で説明します。

>[!CAUTION]
>
>基本認証モードのみがサポートされています。 NTLM 認証はサポートされていません。
>
>SOCKS プロキシはサポートされていません。
>

次のコマンドを使用できます。

```
nlserver config -setproxy:[protocol]/[serverIP]:[port]/[login][:‘https’|'http’]
```

プロトコルパラメーターは、「http」、「https」または「ftp」にすることができます。

HTTP/HTTPS トラフィックと同じポートに FTP を設定する場合は、次を使用できます。

```
nlserver config -setproxy:http/198.51.100.0:8080/user
```

「http」および「https」オプションは、プロトコルパラメーターが「ftp」の場合にのみ使用され、指定したポートでのトンネリングが HTTPS または HTTP のどちらで実行されるかを示します。

プロキシサーバーを介した FTP/SFTP および HTTP/HTTPS トラフィックに異なるポートを使用する場合は、「ftp」プロトコルパラメーターを設定する必要があります。


例：

```
nlserver config -setproxy:ftp/198.51.100.0:8080/user:’http’
```

次に、パスワードを入力します。

HTTP 接続は、proxyHTTP パラメーターで定義されます。

```
<proxyConfig enabled=“1” override=“localhost*” useSingleProxy=“0”>
<proxyHTTP address=“198.51.100.0" login=“user” password=“*******” port=“8080”/>
</proxyConfig>
```

HTTPS 接続は、proxyHTTPS パラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyHTTPS address=“198.51.100.0” login=“user” password=“******” port=“8080"/>
</proxyConfig>
```

FTP/FTPS 接続は、proxyFTP パラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyFTP address=“198.51.100.0” login=“user” password=“******” port=“5555" https=”true”/>
</proxyConfig>
```

複数の接続タイプに同じプロキシを使用する場合、useSingleProxy を「1」または「true」に設定した proxyHTTP のみが定義されます。

プロキシを経由しない内部接続がある場合は、それらをオーバーライドパラメーターに追加します。

プロキシ接続を一時的に無効にする場合は、enabled パラメーターを「false」または「0」に設定します。

プロキシ経由でiOS HTTP/2 コネクタを使用する必要がある場合、次の HTTP プロキシモードがサポートされています。

* 認証なしの HTTP
* HTTP 基本認証

プロキシモードを有効にするには、で次の変更を行う必要があります。 `serverconf.xml` ファイル：

```
<nmac useHTTPProxy="true">
```

このiOS HTTP/2 コネクタについて詳しくは、こちらを参照してください。 [ページ](../../delivery/using/about-mobile-app-channel.md).

## パブリックリソースの管理 {#managing-public-resources}

公開するには、キャンペーンにリンクされたメールや公開リソースで使用される画像が、外部からアクセス可能なサーバー上に存在している必要があります。 その後、外部の受信者やオペレーターがコンテンツフラグメントを使用できるようになります。 [詳細情報](../../installation/using/deploying-an-instance.md#managing-public-resources)。

パブリックリソースはに保存されます。 **/var/res/instance** Adobe Campaign インストールディレクトリのディレクトリ。

一致する URL は次のとおりです。 **http://server/res/instance** ここで、 **instance** は、トラッキングインスタンスの名前です。

ノードをに追加することで、別のディレクトリを指定できます。 **conf-`<instance>`.xml** ファイル：サーバーのストレージを設定します。 つまり、次の行を追加します。

```
<serverconf>
  <shared>
    <dataStore hosts="media*" lang="fra">
      <virtualDir name="images" path="/var/www/images"/>
     <virtualDir name="publicFileRes" path="$(XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)/"/>
    </dataStore>
  </shared>
</serverconf>
```

この場合、デプロイメントウィザードのウィンドウの上部に表示されるパブリックリソースの新しい URL は、このフォルダーを指している必要があります。
