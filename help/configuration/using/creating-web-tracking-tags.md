---
product: campaign
title: Web トラッキングタグの作成
description: Web トラッキングタグの作成方法を学ぶ
feature: Application Settings
role: Data Engineer, Developer
exl-id: 160df6e1-43e5-4eb9-ad2f-5db444e314ea
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Web トラッキングタグの作成{#creating-web-tracking-tags}

トラッキングするサイトの各ページは、Adobe Campaign プラットフォームで参照する必要があります。 この参照は、次の 2 つの方法で実行できます。

1. 追跡する URL の手動定義、
1. トラッキングする URL のオンザフライ作成。

## アプリケーションで追跡する URL の定義 {#defining-the-urls-to-be-tracked-in-the-application}

このメソッドを使用すると、追跡するページを手動で定義し、関連する web トラッキングタグの例を生成できます。 この操作は、クライアントコンソールの **[!UICONTROL キャンペーンの実行/リソース/Web トラッキングタグ]** ノードで定義されます。

![](assets/d_ncs_integration_webtracking_screen.png)

ページに挿入するHTMLコードを生成するには、次の手順を実行します。

* タグのラベルを入力します。このラベルがトラッキングログに表示されます。
* ソース URL を指定：このフィールドは情報目的で、追跡するページを指定できます（オプション）。
* 必要に応じて、有効期間を入力し、
* 「**[!UICONTROL HTMLコードを生成]**」をクリックします。

次に、生成されたコードをコピーし、追跡するページに貼り付けます。

## トラッキングする URL のオンザフライ作成 {#on-the-fly-creation-of-urls-to-be-tracked}

**tagid** パラメーターの値に情報を追加することで、その場で web トラッキング URL を作成できます。

* 追跡されるページのタイプ : WEB の場合は「w」、TRANSACTION の場合は「t」。
* URL を作成する必要があるフォルダーの内部名。

これらの 2 つの情報は、文字「|」を追加して、追跡するページの識別子と連結する必要があります。

```
tagid=<identifier>|<type>|<foldername>
```

>[!IMPORTANT]
>
>**tagid** パラメーターを URL パラメーターとして使用する場合は、その値をエンコードすることを忘れないでください。

**例**：トランザクションタイプの web トラッキング URL の作成。

**http://myserver.adobe.com/r/a?tagid=home%7Ct%7CMyFolder**
