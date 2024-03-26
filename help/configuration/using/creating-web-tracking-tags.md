---
product: campaign
title: Web トラッキングタグの作成
description: Web トラッキングタグの作成方法を説明します
feature: Application Settings
role: Data Engineer, Developer
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
exl-id: 160df6e1-43e5-4eb9-ad2f-5db444e314ea
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# Web トラッキングタグの作成{#creating-web-tracking-tags}

追跡するサイトの各ページは、Adobe Campaignプラットフォームで参照されている必要があります。 この参照は、次の 2 つの方法で実行できます。

1. トラッキングする URL の手動定義
1. トラッキングする URL のオンザフライ作成。

## アプリケーションで追跡する URL の定義 {#defining-the-urls-to-be-tracked-in-the-application}

このメソッドを使用すると、追跡するページを手動で定義し、関連する Web トラッキングタグの例を生成できます。 この操作は、 **[!UICONTROL キャンペーンの実行/リソース/Web トラッキングタグ]** クライアントコンソールのノード。

![](assets/d_ncs_integration_webtracking_screen.png)

ページに挿入するHTMLコードを生成するには：

* タグのラベルを入力します。このラベルはトラッキングログに表示されます。
* ソース URL を指定：このフィールドは情報提供のためのもので、トラッキングするページを指定できます（オプション）。
* 必要に応じて、有効期間を入力します。
* クリック **[!UICONTROL 生成]** HTMLコード。

次に、生成されたコードをコピーし、トラッキングするページに貼り付けます。

## トラッキングする URL のオンザフライ作成 {#on-the-fly-creation-of-urls-to-be-tracked}

即座に Web トラッキング URL を作成するには、 **tagid** パラメーター：

* 追跡されるページのタイプ： WEB の場合は「w」、トランザクションの場合は「t」
* URL を作成する必要があるフォルダーの内部名。

次の 2 つの情報は、文字&#39;|&#39;を追加することで、トラッキング対象のページの識別子で連結する必要があります。

```
tagid=<identifier>|<type>|<foldername>
```

>[!IMPORTANT]
>
>必ず **tagid** パラメーターとして使用される場合は、URL パラメーターとして使用されます。

**例**：トランザクションタイプの Web トラッキング URL の作成。

**http://myserver.adobe.com/r/a?tagid=home%7Ct%7CMyFolder**
