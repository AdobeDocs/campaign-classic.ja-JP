---
solution: Campaign Classic
product: campaign
title: キャンペーンTomcatの設定
description: キャンペーンTomcatの設定
audience: installation
content-type: reference
topic-tags: initial-configuration
translation-type: tm+mt
source-git-commit: 8ab0aab42accbd1253d53e8133f5af0a38c724ea
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# Apache Tomcatを設定{#configuring-tomcat}

Adobe Campaignは、Apache Tomcat **と呼ばれる**&#x200B;埋め込みWebサーブレットを使用して、アプリケーションと外部インターフェイス（クライアントコンソール、追跡されたURLリンク、SOAP呼び出しなど）との間のHTTP/HTTPS要求を処理します。 外部Webサーバー（通常はIISまたはApache）が、外部向けのAdobe Campaignインスタンス用にこのサーバーの前にあることがよくあります。

キャンペーンでのTomcatの詳細と、[このページ](../../production/using/locate-tomcat-version.md)でTomcatのバージョンを見つける方法を説明します。

>[!NOTE]
>
>この手順は、**オンプレミス**&#x200B;のデプロイメントに制限されます。


## Apache Tomcatのデフォルトポート{#default-port-for-tomcat}

Tomcatサーバの8080リスニングポートが、設定に必要な別のアプリケーションで既にビジー状態になっている場合は、8080ポートを空きポート（8090など）に置き換える必要があります。 変更するには、Adobe Campaignのインストールフォルダーの&#x200B;**/tomcat-8/conf**&#x200B;ディレクトリに保存されている&#x200B;**server.xml**&#x200B;ファイルを編集します。

次に、JSPリレーページのポートを変更します。 これを行うには、Adobe Campaignインストールディレクトリの&#x200B;**/conf**&#x200B;ディレクトリに保存されている&#x200B;**serverConf.xml**&#x200B;ファイルを変更します。

```
<serverConf>
   ...
   <web controlPort="8005" httpPort="8090"...
   <url ... targetUrl="http://localhost:8090"...
```

## Apache Tomcat {#mapping-a-folder-in-tomcat}でのフォルダのマッピング

お客様固有の設定を定義するには、**/tomcat-8/conf**&#x200B;コンテキストーに&#x200B;**user_コンテキストー.xml**&#x200B;ファイルを作成します。このフォルダーには、**フォルダー.xml**&#x200B;ファイルも含まれます。

このファイルには、次の種類の情報が含まれます。

```
 <Context path='/foo' docBase='../customers/foo'   crossContext='true' debug='0' reloadable='true' trusted='false'/>
```

必要に応じて、この操作をサーバー側で再生できます。
