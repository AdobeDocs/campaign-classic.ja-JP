---
product: campaign
title: ファイルとリソースの管理
feature: Installation, Application Settings
description: Campaign でのファイルおよびリソース管理の設定方法を説明します。
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 236afdfe-fb23-4ebb-b000-76e14bf01d9e
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 3%

---

# ファイルとリソースの管理{#file-and-resmanagement}



## アップロードファイル形式の制限 {#limiting-uploadable-files}

以下を使用します。 **uploadWhiteList** 属性を使用して、Adobe Campaignサーバーでのアップロードに使用できるファイルタイプを制限します。

この属性は、 **dataStore** の要素 **serverConf.xml** ファイル。 次の **serverConf.xml** を [セクション](../../installation/using/the-server-configuration-file.md).

この属性のデフォルト値は、です。 **.+** およびを使用すると、あらゆるファイルタイプをアップロードできます。

使用可能な書式を制限するには、属性値を有効な Java 正規表現で置き換えます。 複数の値を入力する場合は、コンマで区切ります。

例： **uploadWhiteList=&quot;.&#42;.png,.&#42;.jpg&quot;** は、サーバーに PNG 形式およびJPG形式をアップロードできます。 他の形式は使用できません。

また、Web サーバーを設定して、重要なファイルがアップロードされないようにすることもできます。 [詳細情報](web-server-configuration.md)

>[!NOTE]
>
>The **uploadWhiteList** 属性によって、Adobe Campaignサーバーでのアップロードに使用できるファイルタイプが制限されます。 ただし、パブリッシュモードが **トラッキングサーバー** または **その他のAdobe Campaignサーバー**、 **uploadWhitelist** 属性も、これらのサーバーで更新する必要があります。

## プロキシ接続の設定 {#proxy-connection-configuration}

Campaign サーバーをプロキシ経由で外部システムに接続するには、 **ファイル転送** 例えば、ワークフローアクティビティを使用できます。 これをおこなうには、 **proxyConfig** のセクション **serverConf.xml** ファイルを指定します。 で使用可能なすべてのパラメーター **serverConf.xml** を [セクション](../../installation/using/the-server-configuration-file.md).

HTTP、HTTPS、FTP、SFTP のプロキシ接続が可能です。 20.2 Campaign リリース以降、HTTP および HTTPS プロトコルパラメーターは次のようになります。 **現在は使用できません**. これらのパラメーターは、9032 を含む以前のビルドで引き続き使用可能なので、以下でも説明されています。

>[!CAUTION]
>
>基本認証モードのみがサポートされます。 NTLM 認証はサポートされていません。
>
>SOCKS プロキシはサポートされていません。
>

次のコマンドを使用できます。

```
nlserver config -setproxy:[protocol]/[serverIP]:[port]/[login][:‘https’|'http’]
```

プロトコルのパラメーターは、「http」、「https」または「ftp」にすることができます。

HTTP/HTTPS トラフィックと同じポートで FTP を設定している場合は、次を使用できます。

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

複数の接続タイプで同じプロキシを使用する場合、useSingleProxy が&quot;1&quot;または&quot;true&quot;に設定された proxyHTTP のみが定義されます。

プロキシを経由する必要がある内部接続がある場合は、それらを override パラメーターに追加します。

プロキシ接続を一時的に無効にする場合は、enabled パラメーターを「false」または「0」に設定します。

プロキシを通じてiOS HTTP/2 コネクタを使用する必要がある場合、次の HTTP プロキシモードがサポートされます。

* HTTP （認証なし）
* HTTP 基本認証

プロキシモードを有効にするには、 `serverconf.xml` ファイル：

```
<nmac useHTTPProxy="true">
```

このiOS HTTP/2 コネクタについて詳しくは、次を参照してください [ページ](../../delivery/using/about-mobile-app-channel.md).

## パブリックリソースの管理 {#managing-public-resources}

キャンペーンに関連する E メールやパブリックリソースで使用される画像を公開するには、外部からアクセス可能なサーバー上に存在する必要があります。 その後、外部の受信者やオペレーターが使用できるようになります。 [詳細情報](../../installation/using/deploying-an-instance.md#managing-public-resources)

パブリックリソースは、 **/var/res/instance** Adobe Campaignインストールディレクトリのディレクトリ。

一致する URL は次のとおりです。 **http://server/res/instance** 場所 **インスタンス** は、トラッキングインスタンスの名前です。

別のディレクトリを指定するには、 **conf-`<instance>`.xml** ファイルを使用して、サーバー上のストレージを構成します。 つまり、次の行を追加します。

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

この場合、デプロイウィザードのウィンドウ上部で指定されたパブリックリソースの新しい URL が、このフォルダーを指しているはずです。
