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
source-git-commit: d7e5f68c0d2e0b94fd5cfdf2981bed29f33d9f62
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 76%
---
# トラッキング URL の検出

Adobe Campaignは、配信分析中にコンテンツ内でトラッキングするURLを検出します。

Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 URLの検出方法と使用するパターンについては、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/analytics/tracking/personalized-links#url-detection){target=_blank}を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/analytics/tracking/personalized-links#url-detection){target=_blank}

## セキュリティで保護されていないパターン

コンテンツにパーソナライズされたリンクを追加する場合、潜在的なセキュリティギャップを回避するために、URL のホスト名部分にパーソナライゼーションを含めないようにしてください。 詳しくは、[このページ](../../installation/using/privacy.md#url-personalization)を参照してください。

例えば、`<a href="http://<%=myURL%>">` 構文は&#x200B;**安全ではない**&#x200B;ので、避ける必要があります。

* この構文を使用すると、Adobe Campaign で生成されたリンクに 1 つ以上のパラメーターが含まれている場合に、セキュリティ上の問題が発生する可能性があります。
* Tidyは、リンクの一部に誤ったパッチを適用する可能性があり、これはランダムに発生する可能性があります。 典型的な症状は、HTMLの一部で、電子メール配達確認には表示されますが、プレビューには表示されません。
* URLのエスケープに問題があり、URLの一部の文字が問題を引き起こす可能性があります。
* IDという名前のパラメーターをリダイレクトURLのパラメーターと競合させることはできません。
* その後、Adobe Campaignは「myURL」のすべての可能な値をまったく異なって追跡するので、追跡の関心は配信の統計に限られます。
