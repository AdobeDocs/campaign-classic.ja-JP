---
product: campaign
title: Web トラッキングタグの作成
description: Web トラッキングタグの作成方法
feature: Application Settings
role: Developer
exl-id: 160df6e1-43e5-4eb9-ad2f-5db444e314ea
TQID: https://experienceleague.adobe.com/PG8eMBoER5bR4uc9jaQfDX4mm3rhhMxfmF5Wv4brUtg
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 0%

---

# Web トラッキングタグの作成{#creating-web-tracking-tags}

トラッキングするサイトの各ページは、Adobe Campaign プラットフォームで参照する必要があります。 この参照は、次の2つの方法で実行できます。

1. トラッキングするURLの手動での定義，
1. 追跡するURLのオンザフライ作成。

## アプリケーションでトラッキングするURLの定義 {#defining-the-urls-to-be-tracked-in-the-application}

この方法では、トラッキングするページを手動で定義し、関連するweb トラッキングタグの例を生成できます。 この操作は、クライアントコンソールの&#x200B;**[!UICONTROL キャンペーン実行> リソース >Web トラッキングタグ]** ノードで定義されます。

![](assets/d_ncs_integration_webtracking_screen.png)

ページに挿入するHTML コードを生成するには、次の手順を実行します。

* タグのラベルを入力します。タグはトラッキングログに表示され、
* ソース URLを指定します。このフィールドは情報目的で、トラッキング対象ページを指定できます（オプション）。
* 必要に応じて有効期間を入力し，
* 「**[!UICONTROL Generate]** HTML コード」をクリックします。

次に、生成されたコードをコピーし、追跡するページに貼り付けます。

## 追跡するURLのオンザフライ作成 {#on-the-fly-creation-of-urls-to-be-tracked}

**tagid** パラメーターの値に情報を追加することで、Web トラッキング URLを即座に作成できます。

* 追跡されるページのタイプ：WEBの場合は「w」、トランザクションの場合は「t」
* URLを作成する必要があるフォルダーの内部名。

これら2つの情報は、文字「|」を追加して、追跡ページの識別子と連結する必要があります。

```
tagid=<identifier>|<type>|<foldername>
```

>[!IMPORTANT]
>
>**tagid** パラメーターの値は、URL パラメーターとして使用する場合は、必ずエンコードしてください。

**例**：トランザクションタイプのweb トラッキング URLの作成。

**http://myserver.adobe.com/r/a?tagid=home%7Ct%7CMyFolder**
