---
product: campaign
title: ファイルとリソースの管理
feature: Installation, Application Settings
description: Campaign でファイルとリソースの管理を設定する方法を学ぶ
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
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

Adobe Campaign サーバーでアップロードできるファイルタイプを制限するには、**uploadWhiteList** 属性を使用します。

この属性は、**serverConf.xml** ファイルの **dataStore** 要素内で使用できます。 **serverConf.xml** で使用可能なすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に一覧表示されます。

この属性のデフォルト値は **です。+** 任意のファイルタイプをアップロードできます。

可能な形式を制限するには、属性値を有効な Java 正規表現に置き換えます。 複数の値を入力する場合は、コンマで区切ります。

例：**uploadWhiteList=&quot;。&#42;.png、&#42;.jpg」** PNG およびJPG形式をサーバーにアップロードできます。 その他の形式は受け付けられません。

Web サーバーを設定して、重要なファイルがアップロードされないようにすることもできます。 [詳細情報](web-server-configuration.md)

>[!NOTE]
>
>**uploadWhiteList** 属性は、Adobe Campaign サーバー上でアップロードできるファイルタイプを制限します。 ただし、公開モードが **トラッキングサーバー** または **その他のAdobe Campaign サーバー** の場合、これらのサーバーの **uploadWhitelist** 属性も更新する必要があります。

## プロキシ接続設定 {#proxy-connection-configuration}

**ファイル転送** ワークフローアクティビティなどを使用して、プロキシ経由で Campaign サーバーを外部システムに接続できます。 これを行うには、特定のコマンドで **serverConf.xml** ファイルの **proxyConfig** セクションを設定する必要があります。 **serverConf.xml** で使用可能なすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に一覧表示されます。

HTTP、HTTPS、FTP、SFTP などのプロキシ接続が可能です。 20.2 Campaign リリース以降、HTTP および HTTPS プロトコルパラメーターは **使用できなくなりました**。 これらのパラメーターは、9032 を含む以前のビルドでも引き続き使用できるので、引き続き以下で説明します。

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

プロキシモードを有効にするには、`serverconf.xml` ファイルで次の変更を行う必要があります。

```
<nmac useHTTPProxy="true">
```

このiOS HTTP/2 コネクタについて詳しくは、この [ ページ ](../../delivery/using/about-mobile-app-channel.md) を参照してください。

## パブリックリソースの管理 {#managing-public-resources}

公開するには、キャンペーンにリンクされたメールや公開リソースで使用される画像が、外部からアクセス可能なサーバー上に存在している必要があります。 その後、外部の受信者やオペレーターがコンテンツフラグメントを使用できるようになります。 [詳細情報](../../installation/using/deploying-an-instance.md#managing-public-resources)。

パブリックリソースは、Adobe Campaign インストールディレクトリの **/var/res/instance** ディレクトリに格納されます。

一致する URL は **http://server/res/instance** です。ここで **instance** はトラッキングインスタンスの名前です。

別のディレクトリを指定するには、**conf-`<instance>`.xml** ファイルにノードを追加して、サーバー上のストレージを設定します。 つまり、次の行を追加します。

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
