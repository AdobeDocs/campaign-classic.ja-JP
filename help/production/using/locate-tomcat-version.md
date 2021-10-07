---
product: campaign
title: Adobe Campaignでの Tomcat バージョンの検索
description: Adobe Campaignのインスタンスで使用される埋め込み Tomcat Web サーブレットの現在のバージョンを確認する方法を説明します。
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 76411b29-d300-4aaa-8d3b-d8ff74c3ce93
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Tomcat バージョンの検索{#locate-tomcat-version}

![](../../assets/v7-only.svg)

Adobe Campaignは、Apache Tomcat **と呼ばれる** 埋め込み Web サーブレットを使用して、アプリケーションと外部インターフェイス（クライアントコンソール、追跡する URL リンク、SOAP 呼び出しなど）との間の HTTP/HTTPS 要求を処理します。 外部に面するAdobe Campaignインスタンスには、通常、この前に外部 Web サーバー（IIS または Apache）があります。

以下の手順に従って、問題のトラブルシューティングに役立つように、**Campaign Classicオンプレミスインスタンス** で使用される Tomcat の正確なバージョンを調べます。

## Adobe Campaignで使用される Tomcat

Tomcat は Java 上で動作し、JDK をインストールする必要があります。 詳しくは、[Campaign 互換性マトリックス ](../../rn/using/compatibility-matrix.md) の節の Java 開発キット (JDK) を参照してください。

Adobe Campaignで使用される Tomcat は、カスタマイズされた埋め込みバージョンで、Tomcat の完全な一般リリースのすべての機能を使用していないので、完全なバージョンの脆弱性がすべて損なわれることはありません。 また、Tomcat は外部のインターネットに公開されず、公開されるAdobe Campaignインスタンスには外部 Web サーバー（IIS、Apache など）が Tomcat の前で保護します。

組み込みバージョンの Tomcat の新しいバージョンまたはアップグレードバージョンは、Adobe Campaign自体の新しいビルドでのみリリースされ、Adobe Campaignビルド外の個別のパッチとしてはリリースされません。

## 埋め込み Tomcat のバージョンの検索方法

埋め込み Tomcat のバージョンをAdobe Campaignのインスタンスで検索するには、次の手順に従います。

>[!NOTE]
>
>確認する必要があるAdobe Campaignサーバー上のファイルにアクセスできる必要があります。 以下の手順は、オンプレミスでホスティングするモデル **にのみ適用されます。**

1. Adobe Campaignのインストールフォルダー内の *\tomcat-7\lib* サブフォルダーに移動します ( 例：Windows の場合は *C:\Program Files\ [Installation_folder]*、Linux の場合は */usr/local/neolane/nl6*)。

   Tomcat v6 を使用して古いバージョンのAdobe Campaignを実行している場合は、*\tomcat-6\lib* を使用します。

1. ファイル *catalina.jar* を外部の一時フォルダー（デスクトップなど）にコピーし、拡張子を.jar から.zip に変更します。

1. コピーしたファイルを解凍します。 多くのサブフォルダーとファイルが作成されます。

1. 解凍したファイル/フォルダー内で、テキストエディターを使用して次のファイルを開くか、読み取ります。*org/apache/catalina/util/ServerInfo.properties*. テキストエディターで開きやすくするために、 .txt 拡張子を追加する必要がある場合があります。

1. 完了したら、サーバーマシン上にある場合は、作成した一時ファイルを削除します。

例えば、Adobe Campaignの *ServerInfo.properties* ファイルには、Tomcat v8.5.X を示す次の情報が含まれます。

*server.info=Apache Tomcat/8.5.X*

*server.number=8.5.X.Y*

*server.built=MM DD YYY :MM:HHSS*

特定のインスタンスで使用する Tomcat の正確なバージョンを確立できたら、Tomcat に関する問題のトラブルシューティングに役立つ場合があります。

>[!NOTE]
>
>埋め込み Tomcat のメジャーバージョンは、Adobe Campaignのメジャーバージョンが変更された場合にのみアップグレードされます（旧バージョンは正式にはサポートされなくなった場合でも、一部のお客様は現在もこれらのバージョンを実行している可能性があります）。
>
>例えば、Adobe Campaign v6.02 では常に Tomcat v6.x が使用されます。
