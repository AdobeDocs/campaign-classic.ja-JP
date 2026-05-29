---
product: campaign
title: ファイルとリソースの管理
feature: Installation, Application Settings
description: Campaignでファイルとリソース管理を設定する方法について説明します
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: 236afdfe-fb23-4ebb-b000-76e14bf01d9e
TQID: https://experienceleague.adobe.com/GyNWNrT81f8tWIQizlu3KcVgKvepCjqd6G40DKeOlGo
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 675
ht-degree: 5%

---

# ファイルとリソースの管理{#file-and-resmanagement}



## アップロードファイル形式の制限 {#limiting-uploadable-files}

**uploadWhiteList**&#x200B;属性を使用して、Adobe Campaign サーバーでアップロードできるファイルタイプを制限します。

この属性は、**serverConf.xml** ファイルの&#x200B;**dataStore**&#x200B;要素内で使用できます。 **serverConf.xml**&#x200B;で使用可能なすべてのパラメーターは、この[&#x200B; セクション &#x200B;](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

この属性のデフォルト値は&#x200B;**.+**&#x200B;で、任意のファイルタイプをアップロードできます。

可能な形式を制限するには、属性値を有効なJava正規表現に置き換えます。 複数の値をコンマで区切って入力できます。

例：**uploadWhiteList=&quot;.&#42;.png,.&#42;.jpg&quot;**&#x200B;を使用すると、PNG形式とJPG形式をサーバーにアップロードできます。 他の形式は受け付けません。

また、Web サーバーを設定することで、重要なファイルがアップロードされないようにすることもできます。 [詳細情報](web-server-configuration.md)

>[!NOTE]
>
>**uploadWhiteList**&#x200B;属性は、Adobe Campaign サーバーでのアップロードに使用できるファイルタイプを制限します。 ただし、公開モードが&#x200B;**トラッキングサーバー**&#x200B;または&#x200B;**その他のAdobe Campaign サーバー**&#x200B;の場合、**uploadWhitelist**&#x200B;属性もそれらのサーバーで更新する必要があります。

## プロキシ接続設定 {#proxy-connection-configuration}

例えば、**ファイル転送** ワークフローアクティビティを使用して、Campaign サーバーをプロキシを介して外部システムに接続できます。 これを実現するには、特定のコマンドを使用して、**serverConf.xml** ファイルの&#x200B;**proxyConfig** セクションを設定する必要があります。 **serverConf.xml**&#x200B;で使用可能なすべてのパラメーターは、この[&#x200B; セクション &#x200B;](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

HTTP、HTTPS、FTP、SFTPのプロキシ接続が可能です。 20.2 Campaign リリース以降、HTTPおよびHTTPS プロトコルパラメーターは&#x200B;**使用できなくなります**。 これらのパラメーターは、以前のビルド（9032を含む）で引き続き使用できるため、以下に示します。

>[!CAUTION]
>
>基本認証モードのみがサポートされます。 NTLM認証はサポートされていません。
>
>SOCKS プロキシはサポートされていません。
>

次のコマンドを使用できます。

```
nlserver config -setproxy:[protocol]/[serverIP]:[port]/[login][:‘https’|'http’]
```

プロトコルパラメーターには、「http」、「https」または「ftp」を指定できます。

HTTP/HTTPS トラフィックと同じポートでFTPを設定する場合は、次を使用できます。

```
nlserver config -setproxy:http/198.51.100.0:8080/user
```

「http」および「https」オプションは、プロトコルパラメーターが「ftp」で、指定されたポートでのトンネリングがHTTPS経由またはHTTP経由で実行されるかどうかを示す場合にのみ使用されます。

プロキシサーバー経由でFTP/SFTPおよびHTTP/HTTPS トラフィックに異なるポートを使用する場合は、「ftp」プロトコルパラメーターを設定する必要があります。


例：

```
nlserver config -setproxy:ftp/198.51.100.0:8080/user:’http’
```

次に、パスワードを入力します。

HTTP接続は、proxyHTTP パラメーターで定義されます。

```
<proxyConfig enabled=“1” override=“localhost*” useSingleProxy=“0”>
<proxyHTTP address=“198.51.100.0" login=“user” password=“*******” port=“8080”/>
</proxyConfig>
```

HTTPS接続は、proxyHTTPS パラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyHTTPS address=“198.51.100.0” login=“user” password=“******” port=“8080"/>
</proxyConfig>
```

FTP/FTPS接続は、proxyFTP パラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyFTP address=“198.51.100.0” login=“user” password=“******” port=“5555" https=”true”/>
</proxyConfig>
```

複数の接続タイプに同じプロキシを使用する場合、useSingleProxyを「1」または「true」に設定してproxyHTTPのみが定義されます。

プロキシを経由しない内部接続がある場合は、上書きパラメーターにそれらを追加します。

プロキシ接続を一時的に無効にする場合は、有効なパラメーターを「false」または「0」に設定します。

IOS HTTP/2 コネクタをプロキシ経由で使用する必要がある場合は、次のHTTP プロキシモードがサポートされています。

* 認証なしのHTTP
* HTTP基本認証

プロキシモードを有効にするには、`serverconf.xml` ファイルで次の変更を行う必要があります。

```
<nmac useHTTPProxy="true">
```

このiOS HTTP/2 コネクタについて詳しくは、この[page](../../delivery/using/about-mobile-app-channel.md)を参照してください。

## 公開リソースの管理 {#managing-public-resources}

公開するには、キャンペーンにリンクされた電子メールや公開リソースで使用される画像が、外部からアクセスできるサーバーに存在している必要があります。 その後、外部の受信者またはオペレーターが使用できます。 [詳細情報](../../installation/using/deploying-an-instance.md#managing-public-resources)。

パブリックリソースは、Adobe Campaign インストールディレクトリの&#x200B;**/var/res/instance** ディレクトリに保存されます。

一致するURLは&#x200B;**http://server/res/instance**&#x200B;です。**instance**&#x200B;はトラッキングインスタンスの名前です。

ノードを&#x200B;**conf-`<instance>`.xml** ファイルに追加して、サーバー上のストレージを設定することで、別のディレクトリを指定できます。 つまり、次の行を追加します。

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

この場合、デプロイメントウィザードのウィンドウ上部に表示されるパブリックリソースの新しいURLは、このフォルダーを指している必要があります。
