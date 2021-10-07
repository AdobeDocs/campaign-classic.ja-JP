---
product: campaign
title: ファイルとリソースの管理
description: Campaign でのファイルおよびリソース管理の設定方法を説明します。
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 236afdfe-fb23-4ebb-b000-76e14bf01d9e
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# ファイルとリソースの管理{#file-and-resmanagement}

![](../../assets/v7-only.svg)

## アップロードファイル形式の制限 {#limiting-uploadable-files}

**uploadWhiteList** 属性を使用して、Adobe Campaignサーバーでアップロードできるファイルの種類を制限します。

この属性は、**serverConf.xml** ファイルの **dataStore** 要素内で使用できます。 **serverConf.xml** で使用できるすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に記載されています。

この属性のデフォルト値は **です。+** で、任意のファイルタイプをアップロードできます。

使用可能な書式を制限するには、属性値を有効な Java 正規表現で置き換えます。 複数の値をコンマで区切って入力できます。

例：**uploadWhiteList=&quot;.*.png,.*.jpg&quot;** を使用すると、PNG 形式とJPG形式をサーバーにアップロードできます。 他の形式は使用できません。

>[!NOTE]
>
>Internet Explorer では、完全なファイルパスを正規表現で検証する必要があります。

また、Web サーバーを設定して、重要なファイルがアップロードされないようにすることもできます。 [詳細情報](web-server-configuration.md)

## プロキシ接続の設定 {#proxy-connection-configuration}

例えば、**ファイル転送** ワークフローアクティビティを使用して、Campaign サーバーをプロキシ経由で外部システムに接続できます。 これを実現するには、特定のコマンドを使用して **serverConf.xml** ファイルの **proxyConfig** セクションを設定する必要があります。 **serverConf.xml** で使用できるすべてのパラメーターは、この [ セクション ](../../installation/using/the-server-configuration-file.md) に記載されています。

次のプロキシ接続が可能です。HTTP、HTTPS、FTP、SFTP。 20.2 Campaign リリースより、HTTP および HTTPS プロトコルパラメーターは **使用できなくなりました**。 これらのパラメーターは、9032 を含む以前のビルドで引き続き使用可能なので、以下に示します。

>[!CAUTION]
>
>基本認証モードのみがサポートされます。 NTLM 認証はサポートされていません。
>
>SOCKS プロキシはサポートされていません。

次のコマンドを使用できます。

```
nlserver config -setproxy:[protocol]/[serverIP]:[port]/[login][:‘https’|'http’]
```

プロトコルパラメーターは、「http」、「https」または「ftp」です。

HTTP/HTTPS トラフィックと同じポートに FTP を設定する場合は、次を使用できます。

```
nlserver config -setproxy:http/198.51.100.0:8080/user
```

「http」および「https」オプションは、プロトコルパラメーターが「ftp」の場合にのみ使用され、指定したポートでのトンネリングが HTTPS または HTTP のどちらで実行されるかを示します。

プロキシサーバー経由で FTP/SFTP と HTTP/HTTPS トラフィックに別のポートを使用する場合は、「ftp」プロトコルパラメーターを設定する必要があります。


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

複数の接続タイプで同じプロキシを使用する場合、useSingleProxy が「1」または「true」に設定された proxyHTTP のみが定義されます。

プロキシを経由する必要がある内部接続がある場合は、それらをオーバーライドパラメータに追加します。

プロキシ接続を一時的に無効にする場合は、enabled パラメータを「false」または「0」に設定します。

プロキシ経由でiOS HTTP/2 コネクタを使用する必要がある場合、次の HTTP プロキシモードがサポートされます。

* HTTP（認証なし）
* HTTP 基本認証

プロキシモードを有効にするには、`serverconf.xml` ファイルで次の変更を行う必要があります。

```
<nmac useHTTPProxy="true">
```

このiOS HTTP/2 コネクタについて詳しくは、この [ ページ ](../../delivery/using/about-mobile-app-channel.md) を参照してください。

## パブリックリソースの管理 {#managing-public-resources}

キャンペーンに関連する E メールやパブリックリソースで使用される画像を公開するには、外部からアクセス可能なサーバー上に存在する必要があります。 その後、外部の受信者やオペレーターが使用できるようになります。 [詳細情報](../../installation/using/deploying-an-instance.md#managing-public-resources)。

パブリックリソースは、Adobe Campaignインストールディレクトリの **/var/res/instance** ディレクトリに保存されます。

一致する URL は次のとおりです。**http://server/res/instance** ここで **instance** はトラッキングインスタンスの名前です。

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

この場合、デプロイウィザードのウィンドウの上部で指定したパブリックリソースの新しい URL が、このフォルダーを指している必要があります。
