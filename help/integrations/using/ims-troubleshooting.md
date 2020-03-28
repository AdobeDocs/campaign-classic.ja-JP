---
title: IMS のトラブルシューティング
seo-title: IMS のトラブルシューティング
description: IMS のトラブルシューティング
seo-description: null
page-status-flag: never-activated
uuid: 5db95afc-8cbf-4ec3-b58f-504486fe4a40
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: connecting-via-an-adobe-id
discoiquuid: e31db11a-ad8e-4fd0-bab7-0df1079231c9
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0745b9c9d72538b8573ad18ff4054ecf788905f2

---


# IMS のトラブルシューティング{#ims-troubleshooting}

以下で紹介するトラブルシューティングのヒントは、**オンプレミス版**&#x200B;のお客様が IMS 統合を使用する際によく発生する問題を解決するのに役立ちます。**ホスト版**&#x200B;のお客様は、アドビにお問い合わせください。

**外部アカウント**

以下の情報で、外部アカウントを **1 つ**&#x200B;のみ設定します。

* **内部名**：Adobe_Marketing_Cloud
* **タイプ**：Adobe Experience Cloud

同じ設定値を持つ重複した外部アカウントはすべて削除します。

**製品コンテキスト**

外部アカウントに「**製品コンテキスト**」フィールドがある場合、その値が **dma_campaign_classic** に設定されていることを確認します。

Campaign と Experience Cloud の製品コンテキストが同じ値であることを確認します。

例えば、「**製品コンテキスト**」が表示されない場合は、Campaign と Experience Cloud の両方でデフォルトの製品コンテキストを **dma_campaign** にする必要があります。「**製品コンテキスト**」が表示される場合は、Campaign と Experience Cloud の両方でデフォルトの製品コンテキストを **dma_campaign_classic** にする必要があります。

**[!UICONTROL IMS サーバー URL]**

Campaign の **Adobe Experience Cloud** 外部アカウントで、**[!UICONTROL IMS サーバー URL]** が [adobeid-na1.services.adobe.com](https://adobeid-na1.services.adobe.com/) または [ims-na1.adobelogin.com](http://ims-na1.adobelogin.com/) であることを確認します。また、ステージングと本番用のインスタンスがいずれも、同じ IMS 本番エンドポイントを指していることを確認します。

**関連付けマスク**

* ログインを試みているユーザーが、Enterprise Dashboard でオペレーターグループの一員であることを確認します。
* **[!UICONTROL 関連付けマスク]**&#x200B;が、Enterprise Dashboard でユーザーのオペレーターグループ名のプレフィックスであることを確認します。
* スペースが含まれておらず、スペルの誤りがないことを確認します。
* Campaign のオペレーターグループ名が変更されておらず、以下の構文に従っていることを確認します

```
<Association Mask> + <Operator Group Name in Campaign> = Complete name of the operator group in Enterprise Dashboard
```

**スコープ**

Campaign 外部アカウントで定義されるスコープは、IMS によりプロビジョニングされているスコープのサブセットでなければなりません。

**コールバック URL**

**コールバック URL** はホワイトリストに登録されていて、「https://」で始まる必要があります。**コールバック URL** が対応するインスタンスにリンクされていることを確認します。例えば、本番用インスタンスは本番用 URL にリダイレクトする必要があります。

**クライアント ID と秘密鍵**

クライアント ID は、Campaign 外部アカウントと IMS によりプロビジョニングされた設定との間で一致します。

入力されたクライアント秘密鍵が正しいことを確認します。

**サーバーの再起動**

Campaign 外部アカウントで上記のいずれかの設定を変更した場合は、サーバーを再起動します。

**よく発生するエラーと実行可能な解決策**

* ユーザーが adobe.com のページにリダイレクトされる。

   **[!UICONTROL コールバック URL]** に関する問題が起きています。上記の手順を参考に、**[!UICONTROL コールバック URL]** の設定を確認してください。

* 「ログインには、式に一致する権限がありません」というメッセージが表示される。

   上記の手順を参考に、**[!UICONTROL 関連付けマスク]**&#x200B;とオペレーターグループの設定を確認してください。

* ユーザーが Adobe ID ログインページにアクセスできない。

   上記の手順を参考に、スコープの設定を確認してください。

