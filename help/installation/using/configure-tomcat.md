---
product: campaign
title: Campaign Tomcat の設定
description: Campaign Tomcat の設定
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=en" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a2126458-2ae5-47c6-ad13-925f0e067ecf
source-git-commit: a5762cd21a1a6d5a5f3a10f53a5d1f43542d99d4
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Apache Tomcat の設定 {#configuring-tomcat}



Adobe Campaignは **Apache Tomcat と呼ばれる埋め込み Web サーブレット** ：アプリケーションと任意の外部インターフェイス（クライアントコンソール、追跡される URL リンク、SOAP 呼び出しなど）との間の HTTP/HTTPS 要求を処理する場合。 外部に接続するAdobe Campaignインスタンスには、通常、この前に外部 Web サーバー（通常は IIS または Apache）があります。

Campaign での Tomcat の詳細と、での Tomcat バージョンの見つけ方を説明します。 [このページ](../../production/using/locate-tomcat-version.md).

>[!NOTE]
>
>この手順は次に制限されています： **オンプレミス** デプロイメント。

## Apache Tomcat のデフォルトポート {#default-port-for-tomcat}

Tomcat サーバーの 8080 リスニングポートが、設定に必要な別のアプリケーションで既にビジー状態になっている場合は、8080 ポートを空きポート（8090 など）に置き換える必要があります。 変更するには、 **server.xml** ファイルを **/tomcat-8/conf** Adobe Campaignインストールフォルダーのディレクトリ。

次に、JSP リレーページのポートを変更します。 これをおこなうには、 **serverConf.xml** ファイルを **/conf** Adobe Campaignインストールディレクトリのディレクトリ。

```
<serverConf>
   ...
   <web controlPort="8005" httpPort="8090"...
   <url ... targetUrl="http://localhost:8090"...
```

## Apache Tomcat でのフォルダーのマッピング {#mapping-a-folder-in-tomcat}

顧客固有の設定を定義するには、 **user_contexts.xml** ファイルを **/tomcat-8/conf** フォルダー ( この中にも **contexts.xml** ファイル。

このファイルには、次のタイプの情報が含まれます。

```
 <Context path='/foo' docBase='../customers/foo'   crossContext='true' debug='0' reloadable='true' trusted='false'/>
```

必要に応じて、この操作をサーバー側で再生できます。

## Tomcat エラーレポートを非表示にする {#hide-tomcat-error-report}

セキュリティ上の理由から、Tomcat エラーレポートを非表示にすることを強くお勧めします。 次に手順を示します。

1. を開きます。 **server.xml** 次の場所にあるファイル： **/tomcat-8/conf** Adobe Campaignインストールフォルダーのディレクトリ：  `/usr/local/neolane/nl6/tomcat-8/conf`
1. 既存のすべてのコンテキスト要素の後に、下部に次の要素を追加します。

   ```
   <Valve className="org.apache.catalina.valves.ErrorReportValve" showReport="false" showServerInfo="false"/>
   ```

1. nlserver および Apache Web サーバーを再起動します。
