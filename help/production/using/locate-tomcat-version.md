---
product: campaign
title: Adobe Campaignで Tomcat バージョンを見つけます。
description: Adobe Campaignのインスタンスで使用される、埋め込み Tomcat Web サーブレットの現在のバージョンを確認する方法について説明します
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 76411b29-d300-4aaa-8d3b-d8ff74c3ce93
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# Tomcat バージョンを探します{#locate-tomcat-version}

Adobe Campaignは **Apache Tomcat と呼ばれる埋め込み web サーブレット** を使用して、アプリケーションと外部インターフェイス（クライアントコンソール、トラッキングされる URL リンク、SOAP呼び出しなど）の間の HTTP/HTTPS リクエストを処理します。 多くの場合、外部に接続するAdobe Campaign インスタンス用に、このフォルダーの前に外部 web サーバー（通常は IIS または Apache）があります。

次の手順に従って、**Campaign Classicのオンプレミスインスタンスで使用されている Tomcat の正確なバージョンを調べ** 問題のトラブルシューティングに役立てます。

## Adobe Campaignで使用される Tomcat

Tomcat は Java で実行され、JDK をインストールする必要があります。 詳しくは、「[Campaign 互換性マトリックス &#x200B;](../../rn/using/compatibility-matrix.md)」の節の Java Development Kit （JDK）を参照してください。

Adobe Campaignで使用される Tomcat は、Tomcat の一般リリースのすべての機能を使用しないカスタマイズされた埋め込みバージョンであり、フルバージョンのすべての脆弱性を被るわけではありません。 また、Tomcat は外部インターネットに公開されないようにする必要があります。公開されるAdobe Campaign インスタンスには、Tomcat の前に外部 web サーバー（IIS、Apache など）を配置して、保護します。

Tomcat の埋め込みバージョンの新しいバージョンまたはアップグレードされたバージョンは、Adobe Campaign ビルドの外部にある個別のパッチとしてではなく、Adobe Campaign自体の新しいビルドでのみリリースされます。

>[!AVAILABILITY]
>
>
>* Campaign v7.4.1 以降、Tomcat 10.1 がデフォルトのバージョンです。
>
>* Adobe Campaign Classicは、WebSocket プロトコルと HTTP2 プロトコルを使用しません。
>


## 埋め込み Tomcat のバージョンを特定する方法

Adobe Campaignのインスタンスに埋め込まれた Tomcat のバージョンを見つけるには、次の手順に従います。

>[!NOTE]
>
>確認する必要があるAdobe Campaign サーバー上のファイルにアクセスできる必要があります。 以下に説明する手順は、**オンプレミスホスティングモデル** にのみ適用されます。

1. Adobe Campaignのインストールフォルダー内の *\tomcat-11\lib* サブフォルダー（Windows の場合は *C:\Program Files\ [Installation_folder]*、Linux の場合は */usr/local/neolane/nl6* など）に移動します。

1. *catalina.jar* ファイルを外部の一時フォルダー（デスクトップなど）にコピーし、拡張子を.jar から.zip に変更します。

1. コピーしたファイルを解凍します。 これにより、多数のサブフォルダーとファイルが作成されます。

1. 解凍したファイルまたはフォルダー内で、テキストエディターを使用して、含まれているファイル *org/apache/catalina/util/ServerInfo.properties* を開くか読み取ります。 テキストエディターで開きやすくするために、.txt 拡張子を追加する必要が生じる場合があります。

1. 終了したら、サーバーマシン上にある場合は、作成した一時ファイルを削除します。

例えば、Adobe Campaignの *ServerInfo.properties* ファイルには、Tomcat v11.X を示す次の情報が含まれています。

*`server.info=Apache Tomcat/11.X`*

*`server.number=A.B.X.Y`*

*`server.built=MM DD YYY HH:MM:SS`*

特定のインスタンスで使用される Tomcat の正確なバージョンを確認したら、Tomcat 関連の問題のトラブルシューティングに役立ちます。

>[!NOTE]
>
>埋め込み Tomcat のメジャーバージョンは、Adobe Campaignのメジャーバージョンが変更された場合にのみアップグレードされます（古いバージョンは正式にサポートされなくなりますが、一部のお客様では引き続きこれらのバージョンを使用している可能性があるため、この情報は役に立つ場合があります）。
>

