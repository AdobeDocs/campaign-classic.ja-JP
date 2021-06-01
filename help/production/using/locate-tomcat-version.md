---
product: campaign
title: Adobe CampaignでのTomcatバージョンの検索
description: Adobe Campaignのインスタンスで使用される埋め込みTomcat Webサーブレットの現在のバージョンを確認する方法を説明します。
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 76411b29-d300-4aaa-8d3b-d8ff74c3ce93
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Tomcatのバージョン{#locate-tomcat-version}を探します。

Adobe Campaignは、Apache Tomcat **と呼ばれる**&#x200B;埋め込みWebサーブレットを使用して、アプリケーションと外部インターフェイス（クライアントコンソール、追跡されるURLリンク、SOAP呼び出しなど）との間のHTTP/HTTPS要求を処理します。 外部に面するAdobe Campaignインスタンスには、通常、この前に外部Webサーバー（IISまたはApache）があります。

以下の手順に従って、問題のトラブルシューティングに役立つように、**Campaign Classicオンプレミスインスタンス**&#x200B;で使用されるTomcatの正確なバージョンを確認します。

## Adobe Campaignで使用されるTomcat

TomcatはJava上で動作し、JDKをインストールする必要があります。 詳しくは、[Campaign互換性マトリックス](../../rn/using/compatibility-matrix.md)の節のJava開発キット(JDK)を参照してください。

Adobe Campaignで使用されるTomcatは、一般に利用可能なTomcatの完全リリースの機能をすべて使用しないカスタマイズされた埋め込みバージョンで、完全バージョンの脆弱性の一部が影響を受けることはありません。 また、Tomcatは外部のインターネットに公開されず、公開されるAdobe Campaignインスタンスには外部Webサーバー（IIS、Apacheなど）が必要です。 Tomcatの前で保護します。

組み込みバージョンのTomcatの新しいバージョンまたはアップグレードバージョンは、Adobe Campaign自体の新しいビルドでのみリリースされ、Adobe Campaignビルド外の個別のパッチとしてはリリースされません。

## 埋め込みTomcatのバージョンの見つけ方

Adobe Campaignのインスタンス内で埋め込みTomcatのバージョンを検索するには、次の手順に従います。

>[!NOTE]
>
>確認する必要があるAdobe Campaignサーバー上のファイルにアクセスできる必要があります。 以下の手順は、オンプレミスでホスティングするモデル&#x200B;**にのみ適用されます。**

1. Adobe Campaignインストールフォルダー内の&#x200B;*\tomcat-7\lib*&#x200B;サブフォルダーに移動します(例：Windowsの場合は&#x200B;*C:\Program Files\ [Installation_folder]*、Linuxの場合は&#x200B;*/usr/local/neolane/nl6*)。

   Tomcat v6を使用して古いバージョンのAdobe Campaignを実行している場合は、*\tomcat-6\lib*&#x200B;を使用します。

1. ファイル&#x200B;*catalina.jar*&#x200B;を外部の一時フォルダー（デスクトップなど）にコピーし、拡張子を.jarから.zipに変更します。

1. コピーしたファイルを解凍します。 多くのサブフォルダーやファイルが作成されます。

1. 解凍したファイル/フォルダー内で、テキストエディターを使用して次のファイルを開くか読み取ります。*org/apache/catalina/util/ServerInfo.properties*. テキストエディターで開きやすくするために、 .txt拡張子を追加する必要がある場合があります。

1. 完了したら、サーバーマシン上にある場合は、作成した一時ファイルを削除します。

例えば、Adobe Campaignの&#x200B;*ServerInfo.properties*&#x200B;ファイルには、Tomcat v8.5.Xを示す次の情報が含まれます。

*server.info=Apache Tomcat/8.5.X*

*server.number=8.5.X.Y*

*server.built=MM DD YYY HH:MM:SS*

特定のインスタンスで使用するTomcatの正確なバージョンを確立できたら、Tomcatに関連する問題のトラブルシューティングに役立つ場合があります。

>[!NOTE]
>
>埋め込みTomcatのメジャーバージョンは、Adobe Campaignのメジャーバージョンの変更時にのみアップグレードされます（旧バージョンは正式にはサポートされなくなった可能性がありますが、一部のお客様は引き続きこれらのバージョンを実行している可能性があります）。
>
>例えば、Adobe Campaign v6.02では常にTomcat v6.xが使用されます。
