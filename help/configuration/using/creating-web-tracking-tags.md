---
product: campaign
title: Web トラッキングタグの作成
description: Web トラッキングタグの作成
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: 160df6e1-43e5-4eb9-ad2f-5db444e314ea
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 4%

---

# Web トラッキングタグの作成{#creating-web-tracking-tags}

![](../../assets/v7-only.svg)

追跡するサイトの各ページは、Adobe Campaignプラットフォームで参照する必要があります。 この参照は、次の 2 つの方法で実行できます。

1. 追跡する URL の手動定義
1. 追跡する URL のオンザフライ作成。

## アプリケーションで追跡する URL の定義 {#defining-the-urls-to-be-tracked-in-the-application}

この方法では、トラッキングするページを手動で定義し、関連する Web トラッキングタグの例を生成できます。 この操作は、クライアントコンソールの **[!UICONTROL キャンペーンの実行/リソース/Web トラッキングタグ]** ノードで定義されます。

![](assets/d_ncs_integration_webtracking_screen.png)

ページに挿入するHTMLコードを生成するには：

* タグのラベルを入力：これはトラッキングログに表示されます。
* ソース URL を指定します。このフィールドは情報提供のためのもので、追跡するページを指定できます（オプション）。
* 必要に応じて、有効期間を入力します。
* 「**[!UICONTROL 生成]** HTMLコード」をクリックします。

次に、生成したコードをコピーし、トラッキングするページに貼り付けます。

## 追跡する URL のオンザフライ作成 {#on-the-fly-creation-of-urls-to-be-tracked}

**tagid** パラメーターの値に情報を追加することで、Web トラッキング URL をその場で作成できます。

* 追跡するページのタイプ：WEB の場合は&#39;w&#39;、TRANSACTION の場合は&#39;t&#39;
* URL を作成する必要があるフォルダーの内部名。

次の 2 つの情報は、追跡するページの識別子に文字「|」を追加して連結する必要があります。

```
tagid=<identifier>|<type>|<foldername>
```

>[!IMPORTANT]
>
>**tagid** パラメーターを URL パラメーターとして使用する場合は、必ず値をエンコードしてください。

**例**:トランザクションタイプの web トラッキング URL の作成。

**http://myserver.adobe.com/r/a?tagid=home%7Ct%7CMyFolder**
