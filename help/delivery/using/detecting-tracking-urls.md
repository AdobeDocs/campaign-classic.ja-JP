---
product: campaign
title: トラッキング URL の検出
description: URL をトラッキングするための推奨パターンについて詳しく説明します。
feature: Monitoring
role: User, Developer
exl-id: 7611d6a1-6c55-4ba3-b905-58426c944991
TQID: 'https://experienceleague.adobe.com/F63e0G1uyp-tXDiBk9cau5P-HBHttCkiFD2yw657RBw'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
    internal-label: Monitoring guidelines
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 100%
---
# トラッキング URL の検出

## 検出されない例

`<%= getURL("http://mynewsletter.com") %>` は、Webページの実際のコンテンツを電子メールで受信者に送信します。 ただし、どのリンクも追跡されません。 これは、MTAが送信前に各電子メールに対して`"<%=getURL(..."`を実行するためです。 この値は受信者ごとに異なる場合があるので、Adobe Campaignは追跡用のURLを知ることができず、タグIDを割り当てることができません。

ダウンロードするページがすべての受信者で同じである場合は、次の操作を行うことをお勧めします。

`<%@ include url="http://mynewsletter.com" %>`

この場合、分析中、トラッキング検出前にページがダウンロードされます。 Adobe Campaignは、リンクを検出し、タグIDを割り当てて追跡できます。

## 推奨パターン

`<%@`命令を処理した後、追跡するURLの構文は次のとおりです。`<a href="http://myurl.com/a.php?param1=aaa&param2=<%=escapeUrl(recipient.xxx)%>&param3=<%=escapeUrl(recipient.xxx)%>">`

>[!IMPORTANT]
>
>その他すべてのパターンはAdobeでサポートされていないので、セキュリティ上のギャップを防ぐために避ける必要があります。

## セキュリティで保護されていないパターン

コンテンツにパーソナライズされたリンクを追加する場合、潜在的なセキュリティギャップを回避するために、URL のホスト名部分にパーソナライゼーションを含めないようにしてください。 詳しくは、[このページ](../../installation/using/privacy.md#url-personalization)を参照してください。

例えば、`<a href="http://<%=myURL%>">` 構文は&#x200B;**安全ではない**&#x200B;ので、避ける必要があります。

* この構文を使用すると、Adobe Campaign で生成されたリンクに 1 つ以上のパラメーターが含まれている場合に、セキュリティ上の問題が発生する可能性があります。
* Tidyは、リンクの一部に誤ったパッチを適用する可能性があり、これはランダムに発生する可能性があります。 典型的な症状は、HTMLの一部で、電子メール配達確認には表示されますが、プレビューには表示されません。
* URLのエスケープに問題があり、URLの一部の文字が問題を引き起こす可能性があります。
* IDという名前のパラメーターをリダイレクトURLのパラメーターと競合させることはできません。
* その後、Adobe Campaignは「myURL」のすべての可能な値をまったく異なって追跡するので、追跡の関心は配信の統計に限られます。
