---
product: campaign
title: Campaign Tomcatの設定
description: Campaign Tomcatの設定
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a2126458-2ae5-47c6-ad13-925f0e067ecf,b4a422b4-4b8b-4883-8d74-0dccda4a5ef3
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Apache Tomcat {#configuring-tomcat}の設定

Adobe Campaignは、Apache Tomcat **と呼ばれる**&#x200B;埋め込みWebサーブレットを使用して、アプリケーションと外部インターフェイス（クライアントコンソール、追跡されるURLリンク、SOAP呼び出しなど）との間のHTTP/HTTPS要求を処理します。 外部に面するAdobe Campaignインスタンスには、通常、この前に外部Webサーバー（IISまたはApache）があります。

CampaignでのTomcatの詳細と、[このページ](../../production/using/locate-tomcat-version.md)でTomcatのバージョンを検索する方法を説明します。

>[!NOTE]
>
>この手順は、**オンプレミス**&#x200B;デプロイメントに制限されます。


## Apache Tomcat {#default-port-for-tomcat}のデフォルトポート

Tomcatサーバーの8080リスニングポートが、設定に必要な別のアプリケーションで既にビジー状態になっている場合は、8080ポートを空きポート（8090など）に置き換える必要があります。 変更するには、Adobe Campaignインストールフォルダーの&#x200B;**/tomcat-8/conf**&#x200B;ディレクトリに保存されている&#x200B;**server.xml**&#x200B;ファイルを編集します。

次に、JSPリレーページのポートを変更します。 これをおこなうには、Adobe Campaignインストールディレクトリの&#x200B;**/conf**&#x200B;ディレクトリに保存されている&#x200B;**serverConf.xml**&#x200B;ファイルを変更します。

```
<serverConf>
   ...
   <web controlPort="8005" httpPort="8090"...
   <url ... targetUrl="http://localhost:8090"...
```

## Apache Tomcat {#mapping-a-folder-in-tomcat}でのフォルダーのマッピング

顧客固有の設定を定義するには、**/tomcat-8/conf**&#x200B;フォルダーに&#x200B;**user_contexts.xml**&#x200B;ファイルを作成します。このフォルダーには、**contexts.xml**&#x200B;ファイルも格納されます。

このファイルには、次のタイプの情報が含まれます。

```
 <Context path='/foo' docBase='../customers/foo'   crossContext='true' debug='0' reloadable='true' trusted='false'/>
```

必要に応じて、この操作をサーバー側で再現できます。
