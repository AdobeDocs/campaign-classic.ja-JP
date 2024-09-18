---
product: campaign
title: Campaign Tomcat の設定
description: Campaign Tomcat の設定
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: initial-configuration
exl-id: a2126458-2ae5-47c6-ad13-925f0e067ecf
source-git-commit: fd4a815bca23b94590012c4883cfaa9c29b6f118
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 4%

---

# Apache Tomcat の設定 {#configuring-tomcat}

Adobe Campaignは **Apache Tomcat と呼ばれる埋め込み web サーブレット** を使用して、アプリケーションと外部インターフェイス（クライアントコンソール、トラッキングされる URL リンク、SOAP呼び出しなど）の間の HTTP/HTTPS リクエストを処理します。 多くの場合、外部に接続するAdobe Campaign インスタンス用に、このフォルダーの前に外部 web サーバー（通常は IIS または Apache）があります。

Campaign での Tomcat の詳細と、Tomcat のバージョンを確認する方法については、[ このページ ](../../production/using/locate-tomcat-version.md) を参照してください。

>[!AVAILABILITY]
>
>
>* Campaign v7.4.1 以降、Tomcat 10.1 がデフォルトのバージョンです。
>
>* Adobe Campaign Classicは、WebSocket プロトコルと HTTP2 プロトコルを使用しません。
>



## Apache Tomcat のデフォルトポート {#default-port-for-tomcat}


>[!NOTE]
>
>この手順は、**オンプレミス** デプロイメントに制限されています。
>

Tomcat サーバーの 8080 リスニングポートが、設定に必要な別のアプリケーションで既にビジー状態の場合、8080 ポートを空きのポート（例：8090）に置き換える必要があります。 変更するには、Adobe Campaign インストールフォルダーの **/tomcat-X/conf** ディレクトリに保存されている **server.xml** ファイルを編集します。

次に、JSP リレーページのポートを変更します。 これを行うには、Adobe Campaign インストールディレクトリの **/conf** ディレクトリに保存されている **serverConf.xml** ファイルを変更します。

```xml
<serverConf>
   ...
   <web controlPort="8005" httpPort="8090"...
   <url ... targetUrl="http://localhost:8090"...
```

## Apache Tomcat でのフォルダーのマッピング {#mapping-a-folder-in-tomcat}


>[!NOTE]
>
>この手順は、**オンプレミス** デプロイメントに制限されています。
>

顧客固有の設定を定義するには、**/tomcat-X/conf** フォルダーに **user_contexts.xml** ファイルを作成します。このフォルダーには **contexts.xml** ファイルも含まれています。

このファイルには、次のタイプの情報が含まれます。

```xml
 <Context path='/foo' docBase='../customers/foo'   crossContext='true' debug='0' reloadable='true' trusted='false'/>
```

必要に応じて、サーバー側でこの操作を再現できます。

## Tomcat エラーレポートを非表示 {#hide-tomcat-error-report}


>[!NOTE]
>
>この手順は、**オンプレミス** デプロイメントに制限されています。
>
>この変更は、Campaign v7.4.1 以降、必要なくなりました。
>

セキュリティ上の理由から、Tomcat エラーレポートは非表示にすることを強くお勧めします。 次の手順に従います。

1. Adobe Campaign インストールフォルダーの **/tomcat-X/conf** ディレクトリにある **server.xml** ファイルを開きます。`/usr/local/neolane/nl6/tomcat-X/conf`
1. 既存のすべてのコンテキスト要素の後の下部に、次の要素を追加します。

   ```xml
   <Valve className="org.apache.catalina.valves.ErrorReportValve" showReport="false" showServerInfo="false"/>
   ```

1. nlserver と Apache web サーバーを再起動します。
