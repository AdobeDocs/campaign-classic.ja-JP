---
solution: Campaign Classic
product: campaign
title: 追跡URLの検出
description: URLを追跡するための推奨パターンについての詳細
audience: delivery
content-type: reference
topic-tags: tracking-messages
translation-type: tm+mt
source-git-commit: 768fe62db4efd1217c22973c7e5dc31097d67bae
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 86%

---


# 追跡URLの検出

## 検出されない例

`<%= getURL("http://mynewsletter.com") %>` は、Webページの実際のコンテンツを電子メールで受信者に送信します。ただし、どのリンクも追跡されません。 これは、MTAが送信前に各電子メールに対して`"<%=getURL(..."`を実行するためです。 この値は受信者ごとに異なる場合があるので、Adobe Campaignは追跡用のURLを知ることができず、タグIDを割り当てることができません。

ダウンロードするページがすべての受信者で同じである場合は、次の操作を行うことをお勧めします。

`<%@ include url="http://mynewsletter.com" %>`

この場合、分析中、トラッキング検出前にページがダウンロードされます。 Adobe Campaignは、リンクを検出し、タグIDを割り当てて追跡できます。

## 推奨パターン

`<%@`命令を処理した後、追跡するURLの構文は次のとおりです。`<a href="http://myurl.com/a.php?param1=aaa&param2=<%=escapeUrl(recipient.xxx)%>&param3=<%=escapeUrl(recipient.xxx)%>">`

>[!IMPORTANT]
>
>その他すべてのパターンはAdobeでサポートされていないので、セキュリティ上のギャップを防ぐために避ける必要があります。

## 保護されていないパターン

コンテンツにパーソナライズされたリンクを追加する場合、潜在的なセキュリティギャップを避けるために、URL の hostname 部分はパーソナライズしないでください。詳しくは、[こちらのページ](../../installation/using/privacy.md#url-personalization)を参照してください。

例えば、`<a href="http://<%=myURL%>">`構文は&#x200B;**セキュリティで保護されていない**&#x200B;ので、避ける必要があります。

* この構文を使用すると、Adobe Campaignによって生成されたリンクに1つ以上のパラメーターが含まれている場合に、セキュリティの問題が発生する可能性があります。
* Tidyは、リンクの一部に誤ったパッチを適用する可能性があり、これはランダムに発生する可能性があります。 典型的な症状は、HTMLの一部で、電子メール配達確認には表示されますが、プレビューには表示されません。
* URLのエスケープに問題があり、URLの一部の文字が問題を引き起こす可能性があります。
* IDという名前のパラメーターをリダイレクトURLのパラメーターと競合させることはできません。
* その後、Adobe Campaignは「myURL」のすべての可能な値をまったく異なって追跡するので、追跡の関心は配信の統計に限られます。
