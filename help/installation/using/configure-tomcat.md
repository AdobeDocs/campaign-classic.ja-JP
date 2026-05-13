---
product: campaign
title: Campaign Tomcat設定
description: Campaign Tomcat設定
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a2126458-2ae5-47c6-ad13-925f0e067ecf
TQID: https://experienceleague.adobe.com/LaGsFkomGXlahM-Do7Vwfc4OMH0UAXRiiSRq5Q-9Wto
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 352
ht-degree: 9%

---

# Apache Tomcatの設定 {#configuring-tomcat}

Adobe Campaignは、Apache Tomcat **と呼ばれる**&#x200B;組み込みweb サーブレットを使用して、アプリケーションと任意の外部インターフェイス（クライアントコンソール、トラッキングされたURL リンク、SOAP呼び出しなど）との間でHTTP/HTTPS リクエストを処理します。 多くの場合、外部向けのAdobe Campaign インスタンスの場合、この前に外部web サーバー（通常はIISまたはApache）が存在します。

CampaignのTomcatの詳細と、Tomcat バージョンを検索する方法については、[このページ &#x200B;](../../production/using/locate-tomcat-version.md)を参照してください。

>[!AVAILABILITY]
>
>
>* Campaign v7.4.1以降、Tomcat 10.1はデフォルトバージョンです。
>
>* Adobe Campaign Classicでは、WebSocketおよびHTTP2 プロトコルは使用されません。
>



## Apache Tomcatのデフォルトポート {#default-port-for-tomcat}


>[!NOTE]
>
>この手順は、**オンプレミス**&#x200B;のデプロイメントに制限されています。
>

Tomcat サーバーの8080 リスニングポートが、設定に必要な別のアプリケーションで既にビジー状態になっている場合は、8080 ポートを無料のポート（たとえば8090）に置き換える必要があります。 これを変更するには、Adobe Campaign インストールフォルダーの&#x200B;**/tomcat-X/conf** ディレクトリに保存されている&#x200B;**server.xml** ファイルを編集します。

次に、JSP リレーページのポートを変更します。 これを行うには、Adobe Campaign インストールディレクトリの&#x200B;**/conf** ディレクトリに保存されている&#x200B;**serverConf.xml** ファイルを変更します。

```xml
<serverConf>
   ...
   <web controlPort="8005" httpPort="8090"...
   <url ... targetUrl="http://localhost:8090"...
```

## Apache Tomcatでのフォルダーのマッピング {#mapping-a-folder-in-tomcat}


>[!NOTE]
>
>この手順は、**オンプレミス**&#x200B;のデプロイメントに制限されています。
>

顧客固有の設定を定義するには、**/tomcat-X/conf** フォルダーに&#x200B;**user_contexts.xml** ファイルを作成します。このフォルダーには、**contexts.xml** ファイルも含まれます。

このファイルには、次のタイプの情報が含まれます。

```xml
 <Context path='/foo' docBase='../customers/foo'   crossContext='true' debug='0' reloadable='true' trusted='false'/>
```

必要に応じて、この操作をサーバーサイドで再現できます。

## Tomcat エラーレポートを非表示にする {#hide-tomcat-error-report}


>[!NOTE]
>
>この手順は、**オンプレミス**&#x200B;のデプロイメントに制限されています。
>
>Campaign v7.4.1以降では、この変更は不要になりました。
>

セキュリティ上の理由から、Tomcat エラーレポートを非表示にすることを強くお勧めします。 次の手順に従います。

1. Adobe Campaign インストールフォルダー`/usr/local/neolane/nl6/tomcat-X/conf`の&#x200B;**/tomcat-X/conf** ディレクトリにある&#x200B;**server.xml** ファイルを開きます
1. 既存のすべてのコンテキスト要素の後ろに、次の要素を追加します。

   ```xml
   <Valve className="org.apache.catalina.valves.ErrorReportValve" showReport="false" showServerInfo="false"/>
   ```

1. nlserverとApache web サーバーを再起動します。
