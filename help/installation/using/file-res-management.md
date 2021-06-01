---
product: campaign
title: ファイルとリソースの管理
description: Campaignでのファイルおよびリソース管理の設定方法を説明します
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 236afdfe-fb23-4ebb-b000-76e14bf01d9e
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# ファイルとリソースの管理{#file-and-resmanagement}

## アップロードファイル形式{#limiting-uploadable-files}の制限

**uploadWhiteList**&#x200B;属性を使用して、Adobe Campaignサーバーでアップロードできるファイルタイプを制限します。

この属性は、**serverConf.xml**&#x200B;ファイルの&#x200B;**dataStore**&#x200B;要素内で使用できます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に記載されています。

この属性のデフォルト値は&#x200B;**です。+**&#x200B;で始まり、任意のファイルタイプをアップロードできます。

使用可能な形式を制限するには、属性値を有効なJava正規表現で置き換えます。 複数の値をコンマで区切って入力できます。

例：**uploadWhiteList=&quot;.*.png,.*.jpg&quot;**&#x200B;を使用すると、PNG形式とJPG形式をサーバーにアップロードできます。 他の形式は使用できません。

>[!NOTE]
>
>Internet Explorerでは、完全なファイルパスを正規表現で検証する必要があります。

また、Webサーバーを設定して、重要なファイルがアップロードされないようにすることもできます。 [詳細情報](web-server-configuration.md)

## プロキシ接続の設定{#proxy-connection-configuration}

例えば、**ファイル転送**&#x200B;ワークフローアクティビティを使用して、Campaignサーバーをプロキシ経由で外部システムに接続できます。 これを実現するには、特定のコマンドを使用して&#x200B;**serverConf.xml**&#x200B;ファイルの&#x200B;**proxyConfig**&#x200B;セクションを設定する必要があります。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に記載されています。

次のプロキシ接続が可能です。HTTP、HTTPS、FTP、SFTP。 20.2 Campaignリリースより、HTTPおよびHTTPSプロトコルパラメーターは&#x200B;**使用できなくなりました**。 これらのパラメーターは、9032を含む以前のビルドで引き続き使用可能なので、以下に示します。

>[!CAUTION]
>
>基本認証モードのみがサポートされます。 NTLM認証はサポートされていません。
>
>SOCKSプロキシはサポートされていません。


次のコマンドを使用できます。

```
nlserver config -setproxy:[protocol]/[serverIP]:[port]/[login][:‘https’|'http’]
```

プロトコルパラメーターは、「http」、「https」または「ftp」です。

HTTP/HTTPSトラフィックと同じポートにFTPを設定する場合は、次を使用できます。

```
nlserver config -setproxy:http/198.51.100.0:8080/user
```

「http」および「https」オプションは、プロトコルパラメーターが「ftp」の場合にのみ使用され、指定したポートでのトンネリングがHTTPS経由またはHTTP経由のどちらで実行されるかを示します。

プロキシサーバー経由でFTP/SFTPとHTTP/HTTPSトラフィックに別のポートを使用する場合は、「ftp」プロトコルパラメーターを設定する必要があります。


例：

```
nlserver config -setproxy:ftp/198.51.100.0:8080/user:’http’
```

次に、パスワードを入力します。

HTTP接続は、proxyHTTPパラメーターで定義されます。

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

複数の接続タイプで同じプロキシを使用する場合、useSingleProxyが「1」または「true」に設定されたproxyHTTPのみが定義されます。

プロキシを経由する必要がある内部接続がある場合は、それらをoverrideパラメーターに追加します。

プロキシ接続を一時的に無効にする場合は、enabledパラメーターを「false」または「0」に設定します。

## パブリックリソースの管理{#managing-public-resources}

キャンペーンに関連するEメールやパブリックリソースで使用される画像を公開するには、外部からアクセス可能なサーバー上に存在する必要があります。 その後、外部の受信者やオペレーターが使用できるようになります。 [詳細情報](../../installation/using/deploying-an-instance.md#managing-public-resources)。

パブリックリソースは、Adobe Campaignインストールディレクトリの&#x200B;**/var/res/instance**&#x200B;ディレクトリに保存されます。

一致するURLは次のとおりです。**http://server/res/instance**（**instance**&#x200B;はトラッキングインスタンスの名前）

別のディレクトリを指定するには、**conf-`<instance>`.xml**&#x200B;ファイルにノードを追加して、サーバー上のストレージを設定します。 つまり、次の行を追加します。

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

この場合、デプロイウィザードのウィンドウの上部で指定されたパブリックリソースの新しいURLが、このフォルダーを指している必要があります。
