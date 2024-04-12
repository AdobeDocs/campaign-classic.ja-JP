---
product: campaign
title: Adobe Campaignで Tomcat バージョンを見つけます。
description: Adobe Campaignのインスタンスで使用される、埋め込み Tomcat Web サーブレットの現在のバージョンを確認する方法について説明します
feature: Monitoring
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 76411b29-d300-4aaa-8d3b-d8ff74c3ce93
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 2%

---

# Tomcat バージョンを探します{#locate-tomcat-version}



Adobe Campaignはを使用します **apache Tomcat と呼ばれる埋め込み web サーブレット** アプリケーションと外部インターフェイス（クライアントコンソール、トラッキングされる URL リンク、SOAP 呼び出しなど）の間の HTTP/HTTPS 要求を処理します。 多くの場合、外部に接続するAdobe Campaign インスタンス用に、このフォルダーの前に外部 web サーバー（通常は IIS または Apache）があります。

で使用されている Tomcat の正確なバージョンを確認するには、次の手順に従います。 **Campaign Classicオンプレミスインスタンス** 問題のトラブルシューティングに役立てるため。

## Adobe Campaignで使用される Tomcat

Tomcat は Java で実行され、JDK をインストールする必要があります。 詳しくは、の Java Development Kit （JDK）を参照してください [Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md) セクション。

Adobe Campaignで使用される Tomcat は、Tomcat の一般リリースのすべての機能を使用しないカスタマイズされた埋め込みバージョンであり、フルバージョンのすべての脆弱性を被るわけではありません。 また、Tomcat は外部インターネットに公開されないようにする必要があります。公開されるAdobe Campaign インスタンスには、外部 web サーバー（IIS、Apache など）が必要です。 tomcat の前で保護します。

Tomcat の埋め込みバージョンの新しいバージョンまたはアップグレードされたバージョンは、Adobe Campaign ビルドの外部にある個別のパッチとしてではなく、Adobe Campaign自体の新しいビルドでのみリリースされます。

## 埋め込み Tomcat のバージョンを特定する方法

Adobe Campaignのインスタンスに埋め込まれた Tomcat のバージョンを見つけるには、次の手順に従います。

>[!NOTE]
>
>確認する必要があるAdobe Campaign サーバー上のファイルにアクセスできる必要があります。 以下に説明する手順は、にのみ適用されます **オンプレミスホスティングモデル**.

1. に移動します。 *\tomcat-7\lib* Adobe Campaign インストールフォルダー内のサブフォルダー（例： *C:\Program ファイル\ [Installation_folder]* Windows の場合、または */usr/local/neolane/nl6* （Linux の場合）。

1. ファイルをコピーします *catalina.jar* 外部の一時フォルダー（デスクトップなど）に移動し、拡張子を.jar から.zip に変更します。

1. コピーしたファイルを解凍します。 これにより、多数のサブフォルダーとファイルが作成されます。

1. 解凍したファイルまたはフォルダー内で、テキストエディターを使用して、以下に含まれるファイルを開くか読み取ります。 *org/apache/catalina/util/ServerInfo.properties*. テキストエディターで開きやすくするために、.txt 拡張子を追加する必要が生じる場合があります。

1. 終了したら、サーバーマシン上にある場合は、作成した一時ファイルを削除します。

例えば、 *ServerInfo.properties* Adobe Campaign用のファイルには、Tomcat v8.5.X を示す次の情報が含まれます。

*`server.info=Apache Tomcat/8.5.X`*

*`server.number=8.5.X.Y`*

*`server.built=MM DD YYY HH:MM:SS`*

特定のインスタンスで使用される Tomcat の正確なバージョンを確認したら、Tomcat 関連の問題のトラブルシューティングに役立ちます。

>[!NOTE]
>
>埋め込み Tomcat のメジャーバージョンは、Adobe Campaignのメジャーバージョンが変更された場合にのみアップグレードされます（古いバージョンは正式にサポートされなくなりますが、一部のお客様では引き続きこれらのバージョンを使用している可能性があるため、この情報は役に立つ場合があります）。
>

