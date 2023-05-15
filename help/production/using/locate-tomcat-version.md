---
product: campaign
title: Adobe Campaignで Tomcat バージョンを探します
description: Adobe Campaignのインスタンスで使用される埋め込み Tomcat Web サーブレットの現在のバージョンを調べる方法を説明します
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=en" tooltip="Applies to on-premise and hybrid deployments only"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 76411b29-d300-4aaa-8d3b-d8ff74c3ce93
source-git-commit: a5762cd21a1a6d5a5f3a10f53a5d1f43542d99d4
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Tomcat バージョンを検索{#locate-tomcat-version}



Adobe Campaignは **Apache Tomcat と呼ばれる埋め込み Web サーブレット** ：アプリケーションと任意の外部インターフェイス（クライアントコンソール、追跡される URL リンク、SOAP 呼び出しなど）との間の HTTP/HTTPS 要求を処理する場合。 外部に接続するAdobe Campaignインスタンスには、通常、この前に外部 Web サーバー（通常は IIS または Apache）があります。

以下の手順に従って、 **Campaign Classicオンプレミスインスタンス** 問題のトラブルシューティングに役立つように。

## Adobe Campaignで使用される Tomcat

Tomcat は Java 上で実行され、JDK をインストールする必要があります。 詳しくは、 [Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md) 」セクションに入力します。

Adobe Campaignで使用される Tomcat は、カスタマイズされた埋め込みバージョンで、Tomcat の完全な一般リリースのすべての機能を使用するわけではなく、完全なバージョンのすべての脆弱性に影響を受けない場合があります。 Tomcat は外部のインターネットに公開されず、公開されるAdobe Campaignインスタンスには外部 Web サーバー（IIS、Apache など）が必要です。 Tomcat の前で保護します。

組み込みバージョンの Tomcat の新しいバージョンまたはアップグレードバージョンは、Adobe Campaign自体の新しいビルドでのみリリースされ、Adobe Campaignビルド以外の別のパッチとしてはリリースされません。

## 埋め込み Tomcat のバージョンの検索方法

Adobe Campaignのインスタンス内で埋め込み Tomcat のバージョンを見つけるには、次の手順に従います。

>[!NOTE]
>
>確認する必要があるAdobe Campaignサーバー上のファイルにアクセスできる必要があります。 以下に説明する手順は、次の場合にのみ適用されます。 **オンプレミスホスティングモデル**.

1. 次に移動： *\tomcat-7\lib* Adobe Campaignインストールフォルダー内のサブフォルダー ( 例： *C:\Program Files\ [Installation_folder]* Windows の場合、または */usr/local/neolane/nl6* （Linux の場合）。

   Tomcat v6 を使用して古いバージョンのAdobe Campaignを実行している場合は、 *\tomcat-6\lib*.

1. ファイルをコピーします。 *catalina.jar* を外部の一時フォルダー（デスクトップなど）に追加し、拡張子を.jar から.zip に変更します。

1. コピーしたファイルを解凍します。 その結果、多くのサブフォルダーとファイルが作成されます。

1. 解凍したファイル/フォルダー内で、テキストエディターを使用して、次のファイルを開くか、読み取ります。 *org/apache/catalina/util/ServerInfo.properties*. テキストエディターで開きやすくするために、 .txt 拡張子を追加する必要がある場合があります。

1. 完了したら、サーバーマシン上にある場合は、作成した一時ファイルを削除します。

例えば、 *ServerInfo.properties* Adobe Campaign用のファイルには、Tomcat v8.5.X を示す次の情報が含まれます。

*server.info=Apache Tomcat/8.5.X*

*server.number=8.5.X.Y*

*server.build=MM DD YYY HH:MM:SS*

特定のインスタンスで使用する Tomcat の正確なバージョンを確立できたら、Tomcat に関する問題のトラブルシューティングに役立つ場合があります。

>[!NOTE]
>
>埋め込み Tomcat のメジャーバージョンは、Adobe Campaignのメジャーバージョンが変更された場合にのみアップグレードされます（旧バージョンは正式にはサポートされなくなっていますが、一部のお客様は引き続きこれらのバージョンを実行している可能性があります）。
>
>例えば、Adobe Campaign v6.02 では常に Tomcat v6.x が使用されます。
