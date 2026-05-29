---
product: campaign
title: Adobe CampaignでTomcat バージョンを探す
description: Adobe Campaignのインスタンスで使用されている埋め込み型Tomcat web サーブレットの現在のバージョンを確認する方法について説明します
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 76411b29-d300-4aaa-8d3b-d8ff74c3ce93
TQID: https://experienceleague.adobe.com/cu5oSibc5iznD6CUZSoLxXf1D21g-eoJG3udHBVel7w
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
feature_v2: []
subfeature_v2: id: c03a11ff-bdf9-4e5b-b279-f468b4293464id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 539
ht-degree: 5%

---

# Tomcat バージョンの検索{#locate-tomcat-version}

Adobe Campaignは、Apache Tomcat **と呼ばれる**&#x200B;組み込みweb サーブレットを使用して、アプリケーションと任意の外部インターフェイス（クライアントコンソール、トラッキングされたURL リンク、SOAP呼び出しなど）との間でHTTP/HTTPS リクエストを処理します。 多くの場合、外部向けのAdobe Campaign インスタンスの場合、この前に外部web サーバー（通常はIISまたはApache）が存在します。

以下の手順に従って、**Campaign Classic オンプレミス インスタンス**&#x200B;で使用されているTomcatの正確なバージョンを確認し、問題のトラブルシューティングに役立ててください。

## Adobe Campaignで使用されるTomcat

TomcatはJava上で動作し、JDKをインストールする必要があります。 詳しくは、「[Campaign互換性マトリックス ](../../rn/using/compatibility-matrix.md)」セクションのJava Development Kit （JDK）を参照してください。

Adobe Campaignで使用されるTomcatは、一般的に入手可能なTomcatの完全なリリースのすべての機能を使用しないカスタマイズされた埋め込みバージョンであり、完全なバージョンのすべての脆弱性に悩まされない可能性があります。 Tomcatも外部インターネットに公開しないでください。公開されているAdobe Campaign インスタンスには、外部Web サーバー（IIS、Apacheなど）が必要です。 それを保護するためにTomcatの前に。

埋め込みバージョンのTomcatの新しいバージョンまたはアップグレードされたバージョンは、Adobe Campaign自体の新しいビルドでのみリリースされ、Adobe Campaign ビルド外の個別のパッチとしてはリリースされません。

>[!AVAILABILITY]
>
>
>* Campaign v7.4.1以降、Tomcat 10.1はデフォルトバージョンです。
>
>* Adobe Campaign Classicでは、WebSocketおよびHTTP2 プロトコルは使用されません。
>


## 埋め込まれたTomcatのバージョンを見つける方法

Adobe Campaignのインスタンスに埋め込まれたTomcatのバージョンを見つけるには、次の手順に従います。

>[!NOTE]
>
>確認する必要があるAdobe Campaign サーバー上のファイルにアクセスできる必要があります。 以下に説明する手順は、**オンプレミスホスティングモデル**&#x200B;にのみ適用されます。

1. Adobe Campaign インストールフォルダー内の&#x200B;*\tomcat-11\lib* サブフォルダーに移動します（例：Windowsの&#x200B;*C:\Program Files\ [Installation_folder]*、Linuxの&#x200B;*/usr/local/neolane/nl6*）。

1. ファイル *catalina.jar*&#x200B;を外部の一時フォルダー（デスクトップなど）にコピーし、拡張子の名前を.jarから.zipに変更します。

1. コピーしたファイルを解凍します。 その結果、多くのサブフォルダーとファイルが作成されます。

1. 解凍されたファイル/フォルダー内で、テキストエディターを使用して次の含まれるファイルを開くか、読み取ります：*org/apache/catalina/util/ServerInfo.properties*。 テキストエディターで開くために.txt拡張子を追加する必要がある場合があります。

1. 完了したら、サーバーマシン上にある場合は、作成した一時ファイルを削除します。

例えば、Adobe Campaignの&#x200B;*ServerInfo.properties* ファイルには、Tomcat v11.Xを示す次の情報が含まれています。

*`server.info=Apache Tomcat/11.X`*

*`server.number=A.B.X.Y`*

*`server.built=MM DD YYY HH:MM:SS`*

特定のインスタンスで使用されているTomcatの正確なバージョンを確立できたら、Tomcat関連の問題のトラブルシューティングに役立つ可能性があります。

>[!NOTE]
>
>組み込みTomcatのメジャーバージョンは、Adobe Campaignのメジャーバージョンが変更された場合にのみアップグレードされます（古いバージョンは正式にサポートされなくなりましたが、一部のお客様は引き続きこれらのバージョンを使用している場合があります）。
>

