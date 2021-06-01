---
product: campaign
title: Web トラッキングタグの作成
description: Web トラッキングタグの作成
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: 160df6e1-43e5-4eb9-ad2f-5db444e314ea
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 4%

---

# Web トラッキングタグの作成{#creating-web-tracking-tags}

追跡するサイトの各ページは、Adobe Campaignプラットフォームで参照されている必要があります。 この参照は、次の2つの方法で実行できます。

1. 追跡するURLの手動定義
1. 追跡するURLのオンザフライ作成。

## アプリケーション{#defining-the-urls-to-be-tracked-in-the-application}で追跡するURLの定義

このメソッドを使用すると、追跡するページを手動で定義し、関連するWebトラッキングタグの例を生成できます。 この操作は、クライアントコンソールの&#x200B;**[!UICONTROL キャンペーンの実行/リソース/Webトラッキングタグ]**&#x200B;ノードで定義されます。

![](assets/d_ncs_integration_webtracking_screen.png)

ページに挿入するHTMLコードを生成するには：

* タグのラベルを入力：これはトラッキングログに表示されます。
* ソースURLを指定します。このフィールドは情報提供を目的とし、追跡するページを示します（オプション）。
* 必要に応じて、有効期間を入力します。
* 「**[!UICONTROL HTMLコードを生成]**」をクリックします。

次に、生成したコードをコピーし、トラッキングするページに貼り付けます。

## 追跡するURLのオンザフライ作成{#on-the-fly-creation-of-urls-to-be-tracked}

**tagid**&#x200B;パラメーターの値に情報を追加することで、WebトラッキングURLをその場で作成できます。

* 追跡するページのタイプ：WEBの場合は「w」、TRANSACTIONの場合は「t」
* URLを作成する必要があるフォルダーの内部名。

次の2つの情報は、トラッキングされるページの識別子に文字「|」を追加して連結する必要があります。

```
tagid=<identifier>|<type>|<foldername>
```

>[!IMPORTANT]
>
>**tagid**&#x200B;パラメーターをURLパラメーターとして使用する場合は、必ず値をエンコードしてください。

**例**:トランザクションタイプのwebトラッキングURLの作成。

**http://myserver.adobe.com/r/a?tagid=home%7Ct%7CMyFolder**
