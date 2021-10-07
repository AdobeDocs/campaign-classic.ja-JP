---
product: campaign
title: Campaign Tomcat の設定
description: Campaign Tomcat の設定
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a2126458-2ae5-47c6-ad13-925f0e067ecf
source-git-commit: ed9e76495efb0cb49e248a7d38417642c5094a11
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Apache Tomcat の設定 {#configuring-tomcat}

![](../../assets/v7-only.svg)

Adobe Campaignは、Apache Tomcat **と呼ばれる** 埋め込み Web サーブレットを使用して、アプリケーションと外部インターフェイス（クライアントコンソール、追跡する URL リンク、SOAP 呼び出しなど）との間の HTTP/HTTPS 要求を処理します。 外部に面するAdobe Campaignインスタンスには、通常、この前に外部 Web サーバー（IIS または Apache）があります。

Campaign での Tomcat の詳細と、[ このページ ](../../production/using/locate-tomcat-version.md) で Tomcat のバージョンを検索する方法を説明します。

>[!NOTE]
>
>この手順は、**オンプレミス** のデプロイメントに制限されます。

## Apache Tomcat のデフォルトポート {#default-port-for-tomcat}

Tomcat サーバーの 8080 リスニングポートが、設定に必要な別のアプリケーションで既にビジー状態になっている場合は、8080 ポートを空きポート（8090 など）に置き換える必要があります。 変更するには、Adobe Campaignインストールフォルダーの **/tomcat-8/conf** ディレクトリに保存されている **server.xml** ファイルを編集します。

次に、JSP リレーページのポートを変更します。 これをおこなうには、Adobe Campaignインストールディレクトリの **/conf** ディレクトリに保存されている **serverConf.xml** ファイルを変更します。

```
<serverConf>
   ...
   <web controlPort="8005" httpPort="8090"...
   <url ... targetUrl="http://localhost:8090"...
```

## Apache Tomcat でのフォルダーのマッピング {#mapping-a-folder-in-tomcat}

顧客固有の設定を定義するには、**/tomcat-8/conf** フォルダーに **user_contexts.xml** ファイルを作成します。このフォルダーには、**contexts.xml** ファイルも含まれます。

このファイルには、次のタイプの情報が含まれます。

```
 <Context path='/foo' docBase='../customers/foo'   crossContext='true' debug='0' reloadable='true' trusted='false'/>
```

必要に応じて、この操作をサーバー側で再現できます。
