---
solution: Campaign Classic
product: campaign
title: Adobe CampaignでTomcatバージョンを検索
description: Adobe Campaignのインスタンスで使用される埋め込みTomcat Webサーブレットの現在のバージョンを調べる方法を説明します。
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 49e49d5e35d14a31236cc4f78188cdf77353fbbf
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# Tomcatバージョンの検索{#locate-tomcat-version}

Adobe Campaignは、Apache Tomcat **と呼ばれる**&#x200B;埋め込みWebサーブレットを使用して、アプリケーションと外部インターフェイス（クライアントコンソール、追跡されたURLリンク、SOAP呼び出しなど）との間のHTTP/HTTPS要求を処理します。 外部Webサーバー（通常はIISまたはApache）が、外部向けのAdobe Campaignインスタンス用にこのサーバーの前にあることがよくあります。

問題のトラブルシューティングに役立つために、**Campaign Classicのオンプレミスインスタンス**&#x200B;で使用されているTomcatの正確なバージョンを調べるには、次の手順に従います。

## Adobe Campaignで使用されるTomcat

TomcatはJava上で実行され、JDKをインストールする必要があります。 詳しくは、「[キャンペーン互換表](../../rn/using/compatibility-matrix.md)」の節の「Java Development Kit(JDK)」を参照してください。

Adobe Campaignで使用されるTomcatはカスタマイズされた組み込みバージョンで、Tomcatの完全なGAリリースの機能の一部を使用するわけではなく、完全なバージョンの脆弱性が完全に損なわれることはありません。 また、Tomcatを外部のインターネットに公開しないでください。また、公開されるAdobe Campaignインスタンスには外部Webサーバー（IIS、Apacheなど）が必要です。 Tomcatの前で保護します。

組み込みバージョンの新しいバージョンまたはアップグレードされたバージョンのTomcatは、Adobe Campaign自体の新しいビルドでのみリリースされ、Adobe Campaignビルドの外部の個別のパッチとしてはリリースされません。

## 埋め込みTomcatのバージョンを特定する方法

埋め込みTomcatのAdobe Campaignをインスタンス内で検索するには、次の手順に従います。

>[!NOTE]
>
>確認する必要があるAdobe Campaignサーバー上のファイルにアクセスできる必要があります。 以下に説明する手順は、**オンプレミスホスティングモデル**&#x200B;にのみ適用されます。

1. Adobe Campaignーのインストールフォルダー内の&#x200B;*\tomcat-7\lib*&#x200B;サブフォルダーに移動します(例：Windowsの場合は&#x200B;*C:\Program Files\ [Installation_folder]*、Linuxの場合は&#x200B;*/usr/local/neolane/nl6*)。

   Tomcat v6を使用して古いバージョンのAdobe Campaignを実行している場合は、*\tomcat-6\lib*&#x200B;を使用します。

1. ファイル&#x200B;*catalina.jar*&#x200B;を外部の一時フォルダー（デスクトップなど）にコピーし、拡張子を.jarから.zipに変更します。

1. コピーしたファイルを解凍します。 その結果、多くのサブフォルダーとファイルが作成されます。

1. 解凍されたファイル/フォルダー内で、次のファイルを開くか、テキストエディターを使用して読みます。*org/apache/catalina/util/ServerInfo.properties*. テキストエディタで開きやすくするために、.txt拡張子を追加する必要がある場合があります。

1. 完了したら、サーバマシン上にある場合は、作成した一時ファイルを削除します。

例えば、Adobe Campaign用の&#x200B;*ServerInfo.properties*&#x200B;ファイルには、Tomcat v8.5.Xを示す次の情報が含まれます。

*server.info=Apache Tomcat/8.5.X*

*server.number=8.5.X.Y*

*server.built=MM DD YYYY HH:MM:SS*

特定のインスタンスで使用されるTomcatの正確なバージョンを確立できたら、Tomcatに関する問題のトラブルシューティングに役立つ場合があります。

>[!NOTE]
>
>組み込みTomcatのメジャーバージョンは、Adobe Campaignのメジャーバージョンが変更された場合にのみアップグレードされます（旧バージョンは正式にはサポートされなくなりますが、一部のお客様は、これらのバージョンを引き続き実行している可能性があります）。
>
>例えば、Adobe Campaignv6.02では常にTomcat v6.xが使用されます。