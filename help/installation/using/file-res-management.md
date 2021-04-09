---
solution: Campaign Classic
product: campaign
title: ファイルとリソースの管理
description: キャンペーンでのファイルとリソースの管理を構成する方法を学びます。
audience: installation
content-type: reference
topic-tags: initial-configuration
translation-type: tm+mt
source-git-commit: ae4f86f3703b9bfe7f08fd5c2580dd5da8c28cbd
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# ファイルとリソースの管理{#file-and-resmanagement}

## アップロードファイル形式の制限{#limiting-uploadable-files}

**uploadWhiteList**&#x200B;属性を使用して、Adobe Campaignサーバーでアップロードできるファイルの種類を制限します。

この属性は、**serverConf.xml**&#x200B;ファイルの&#x200B;**dataStore**&#x200B;要素内で使用できます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

この属性のデフォルト値は&#x200B;**です。+**&#x200B;を追加し、任意のファイルタイプをアップロードできます。

使用可能な形式を制限するには、有効なJava正規式で属性値を置き換えます。 複数の値をコンマで区切って入力できます。

次に例を示します。**uploadWhiteList=&quot;.*.png,.*.jpg&quot;**&#x200B;を使用すると、PNG形式とJPG形式をサーバにアップロードできます。 その他の形式は使用できません。

>[!NOTE]
>
>Internet Explorerでは、完全なファイルパスを正規式で検証する必要があります。

また、Webサーバーを設定して、重要なファイルがアップロードされないようにすることもできます。 [詳細情報](web-server-configuration.md)

## プロキシ接続の構成{#proxy-connection-configuration}

例えば、**ファイル転送**&#x200B;ワークフローアクティビティを使用して、キャンペーンサーバーをプロキシ経由で外部システムに接続できます。 これを行うには、特定のコマンドを使用して&#x200B;**serverConf.xml**&#x200B;ファイルの&#x200B;**proxyConfig**&#x200B;セクションを設定する必要があります。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

次のプロキシ接続が可能です。HTTP、HTTPS、FTP、SFTP。 20.2キャンペーンリリース以降、HTTPおよびHTTPSプロトコルのパラメーターは&#x200B;**使用できなくなりました**。 これらのパラメーターは、9032を含む以前のビルドで引き続き使用できるので、以下に説明します。

>[!CAUTION]
>
>基本認証モードのみがサポートされています。 NTLM認証はサポートされていません。
>
>SOCKSプロキシはサポートされていません。


次のコマンドを使用できます。

```
nlserver config -setproxy:[protocol]/[serverIP]:[port]/[login][:‘https’|'http’]
```

プロトコルのパラメータには、「http」、「https」、「ftp」のいずれかを使用できます。

HTTP/HTTPSトラフィックと同じポートにFTPを設定する場合は、次を使用できます。

```
nlserver config -setproxy:http/198.51.100.0:8080/user
```

「http」および「https」オプションは、プロトコルパラメータが「ftp」の場合にのみ使用され、指定したポートでのトンネリングがHTTPSまたはHTTPを使用して実行されるかどうかを示します。

プロキシサーバー経由のFTP/SFTPとHTTP/HTTPSトラフィックに異なるポートを使用する場合は、「ftp」プロトコルパラメーターを設定する必要があります。


例：

```
nlserver config -setproxy:ftp/198.51.100.0:8080/user:’http’
```

次に、パスワードを入力します。

HTTP接続は、proxyHTTPパラメーターで定義します。

```
<proxyConfig enabled=“1” override=“localhost*” useSingleProxy=“0”>
<proxyHTTP address=“198.51.100.0" login=“user” password=“*******” port=“8080”/>
</proxyConfig>
```

HTTPS接続は、proxyHTTPSパラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyHTTPS address=“198.51.100.0” login=“user” password=“******” port=“8080"/>
</proxyConfig>
```

FTP/FTPS接続は、proxyFTPパラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyFTP address=“198.51.100.0” login=“user” password=“******” port=“5555" https=”true”/>
</proxyConfig>
```

複数の接続タイプで同じプロキシを使用する場合、proxyHTTPのみがuseSingleProxyを&quot;1&quot;または&quot;true&quot;に設定して定義されます。

プロキシを経由する必要がある内部接続がある場合は、それらをoverrideパラメーターに追加します。

プロキシ接続を一時的に無効にする場合は、有効なパラメーターを「false」または「0」に設定します。

## パブリックリソースの管理{#managing-public-resources}

公開されるようにするには、キャンペーンにリンクされた電子メールやパブリックリソースで使用される画像が、外部からアクセス可能なサーバー上に存在する必要があります。 その後、外部の受信者や演算子で使用できます。 [詳細情報](../../installation/using/deploying-an-instance.md#managing-public-resources)。

パブリックリソースは、Adobe Campaignインストールディレクトリの&#x200B;**/var/res/instance**&#x200B;ディレクトリに保存されます。

一致するURLは次のとおりです。**http://server/res/instance**&#x200B;ここで&#x200B;**instance**&#x200B;は、トラッキングインスタンスの名前です。

別のディレクトリを指定するには、**conf-`<instance>`.xml**&#x200B;ファイルにノードを追加して、サーバー上のストレージを設定します。 これは、次の行を追加することを意味します。

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

この場合、デプロイメントウィザードのウィンドウ上部に表示されるパブリックリソースの新しいURLは、このフォルダーを指す必要があります。
