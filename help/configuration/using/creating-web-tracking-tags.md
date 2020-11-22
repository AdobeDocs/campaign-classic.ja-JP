---
solution: Campaign Classic
product: campaign
title: Web トラッキングタグの作成
description: Web トラッキングタグの作成
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 4%

---


# Web トラッキングタグの作成{#creating-web-tracking-tags}

追跡するサイトの各ページは、Adobe Campaignプラットフォームで参照されている必要があります。 この参照は、次の2つの方法で実行できます。

1. 追跡するURLの手動定義、
1. 追跡するURLのオンザフライ作成。

## アプリケーションで追跡するURLの定義 {#defining-the-urls-to-be-tracked-in-the-application}

この方法を使用すると、追跡するページを手動で定義し、関連するWebトラッキングタグーの例を生成できます。 この操作は、クライアントコンソールの **[!UICONTROL キャンペーン実行/リソース/Web トラッキングタグ]** ・ノードで定義します。

![](assets/d_ncs_integration_webtracking_screen.png)

ページに挿入するHTMLコードを生成するには：

* タグのラベルを入力：それはトラッキングログに示される
* ソースURLを指定します。このフィールドは情報を提供する目的で使用され、追跡するページを指定できます（オプション）。
* 必要に応じて、有効期間を入力します。
* 「 **[!UICONTROL HTMLコードを]** 生成」をクリックします。

次に、生成されたコードをコピーして、追跡するページに貼り付けます。

## 追跡するURLのオンザフライ作成 {#on-the-fly-creation-of-urls-to-be-tracked}

WebトラッキングURLは、 **tagid** パラメーターの値に次の情報を追加することで、その場で作成できます。

* 追跡するページのタイプ：WEBの場合は&#39;w&#39;、トランザクションの場合は&#39;t&#39;、
* URLを作成する必要があるフォルダーの内部名です。

次の2つの情報は、トラッキング対象のページのIDと連結し、文字&#39;|&#39;を追加する必要があります。

```
tagid=<identifier>|<type>|<foldername>
```

>[!IMPORTANT]
>
>URLパラメーターとして使用する場合は、 **tagid** パラメーターの値をエンコードすることを忘れないでください。

**例**:トランザクションタイプのwebトラッキングURLの作成。

**http://myserver.adobe.com/r/a?tagid=home%7Ct%7CMyFolder**
