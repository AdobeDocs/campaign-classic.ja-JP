---
solution: Campaign Classic
product: campaign
title: パーソナライズされたリンクの追跡を開始する
description: パーソナライズ可能な電子メールにリンクを記述し、Campaign Classicでの追跡をサポートする方法を説明します。
audience: delivery
content-type: reference
topic-tags: tracking-messages
exl-id: d0e00b40-e7dd-4484-b37c-fd3f3ac70fda
translation-type: ht
source-git-commit: 6854d06f8dc445b56ddfde7777f02916a60f2b63
workflow-type: ht
source-wordcount: '219'
ht-degree: 100%

---

# パーソナライズされたリンクの追跡を開始する{#tracking-personalized-links}

パーソナライゼーションを含む電子メールコンテンツ内のリンクは、特定の構文を追跡する必要があります。

電子メールコンテンツ（HTMLまたはテキスト）でJavaScriptを使用すると、動的なコンテンツを生成して受信者に送信できますが、次の2つの制限があります。

* スクリプトはデータベースに直接アクセスできません（SQL関数とAPI関数は使用できません）。
* リンクを追跡できるように、Adobe Campaign で URL を検出できる必要があります。 [詳細情報](detecting-tracking-urls.md)

特定の前処理命令を追加して、URL のスクリプトを作成し、追跡することができます。 [詳細情報](pre-processing-instructions.md)

追跡検出のために、Adobe Campaignは[Tidy](http://www.html-tidy.org/)を埋め込んでHTMLソースを解析し、パターンを検出します。 コンテンツのすべてのURLをリストして、個別に追跡できるようにします。 Adobe Campaignは再度Tidyを使用して、URL(`http://myurl.com`)をAdobe Campaignリダイレクトサーバーを指すURLに置き換えます。

例えば、初期コンテンツでは、次のようになります。`http://myurl.com/a.php?name=<%=escapeUrl(recipient.lastName)%>`は、次の特定の受信者で置き換えられます。`http://emailing.customer.com/r/?id=h617791,71ffa3,71ffa8&p1=CustomerName`

場所：

* 「h」はHTMLコンテンツを表します（テキストコンテンツの場合は「t」）。
* 617791はメッセージID / broadLog ID（16進数）です。
* 71ffa3はNmsDelivery ID（16進数）です。
* 71ffa8は、NmsTrackingUrl ID（16進数）です。
* p1、p2などは、URLで置き換えるすべてのパラメータです。
