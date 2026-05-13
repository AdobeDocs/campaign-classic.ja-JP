---
product: campaign
title: IMS のトラブルシューティング
description: IMS のトラブルシューティング
feature: Configuration
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: integrations
content-type: reference
topic-tags: connecting-via-an-adobe-id
exl-id: 1ce89c3a-1fe6-4ed6-9547-2eb9713a0ec3
TQID: https://experienceleague.adobe.com/cUoMAlp8ExhammApiilFqRyrOkyyqxk1om0AifZVxb0
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: d5ef99fa-df0c-4153-bf94-105ad0724167
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 3ebf57870a8fa7b2ad742f3978e982bc80c798d2
workflow-type: tm+mt
source-wordcount: 521
ht-degree: 86%

---

# IMS のトラブルシューティング{#ims-troubleshooting}


以下で紹介するトラブルシューティングのヒントは、**オンプレミス版**&#x200B;および&#x200B;**ハイブリッド版**&#x200B;のお客様が IMS 統合を使用する際によく発生する問題を解決するのに役立ちます。 **ホスト版**&#x200B;のお客様は、アドビにお問い合わせください。

**外部アカウント**

以下の情報で、外部アカウントを **1 つ**&#x200B;のみ設定します。

* **内部名**：Adobe_Marketing_Cloud
* **タイプ**：Adobe Experience Cloud

同じ設定値を持つ重複した外部アカウントはすべて削除します。

**製品コンテキスト**

外部アカウントに「**製品コンテキスト**」フィールドがある場合、その値が **dma_campaign_classic** に設定されていることを確認します。

Campaign と Experience Cloud の製品コンテキストが同じ値であることを確認します。

例えば、「**製品コンテキスト**」が表示されない場合は、Campaign と Experience Cloud の両方でデフォルトの製品コンテキストを **dma_campaign** にする必要があります。 「**製品コンテキスト**」が表示される場合は、Campaign と Experience Cloud の両方でデフォルトの製品コンテキストを **dma_campaign_classic** にする必要があります。

**[!UICONTROL IMS サーバー URL]**

Campaign の **Adobe Marketing Cloud** 外部アカウントで、**[!UICONTROL IMS サーバー URL]** が `adobeid-na1.services.adobe.com` または `ims-na1.adobelogin.com` であることを確認します。 また、ステージングと本番用のインスタンスがいずれも、同じ IMS 本番エンドポイントを指していることを確認します。

**関連付けマスク**

* ログインを試みているユーザーが、Enterprise Dashboard でオペレーターグループの一員であることを確認します。
* **[!UICONTROL 関連付けマスク]**&#x200B;が、Enterprise Dashboard でユーザーのオペレーターグループ名の接頭辞であることを確認します。
* スペースが含まれておらず、スペルの誤りがないことを確認します。
* Campaign のオペレーターグループ名が変更されておらず、以下の構文に従っていることを確認します

```
<Association Mask> + <Operator Group Name in Campaign> = Complete name of the operator group in Enterprise Dashboard
```

**スコープ**

Campaign 外部アカウントで定義されるスコープは、IMS によりプロビジョニングされているスコープのサブセットでなければなりません。

**コールバック URL**

**コールバック URL** は「https://」から始まり、許可リストに追加される必要があります。 **コールバック URL** が対応するインスタンスにリンクされていることを確認します。 例えば、本番用インスタンスは本番用 URL にリダイレクトする必要があります。

**クライアント ID と秘密鍵**

クライアント ID は、Campaign 外部アカウントと IMS によりプロビジョニングされた設定との間で一致します。

入力されたクライアント秘密鍵が正しいことを確認します。

**サーバーの再起動**

Campaign 外部アカウントで上記のいずれかの設定を変更した場合は、サーバーを再起動します。

**よく発生するエラーと実行可能な解決策**

* ユーザーが adobe.com のページにリダイレクトされる。

  **[!UICONTROL コールバック URL]** に関する問題が起きています。 上記の手順を参考に、**[!UICONTROL コールバック URL]** の設定を確認してください。

* 「ログインには、式に一致する権限がありません」というメッセージが表示される。

  上記の手順を参考に、**[!UICONTROL 関連付けマスク]**&#x200B;とオペレーターグループの設定を確認してください。

* ユーザーが Adobe ID ログインページにアクセスできない。

  上記の手順を参考に、スコープの設定を確認してください。

**WebView2 キャッシュの問題**

Adobe IDで&#x200B;**[!UICONTROL クライアントコンソール]**&#x200B;にログインする際に問題が発生した場合は、ローカル WebView2 キャッシュをクリアしてみてください。 多くの場合、これで問題は解決します。 次の手順に従います。

1. **[!UICONTROL クライアントコンソール]**&#x200B;を閉じ、実行中の`nlclient` プロセスをすべて停止します。

1. 次の場所からすべての`webview2`および`webview2Cache` フォルダーを削除します：

   * `C:\ProgramData\Neolane\NL_5\nlclient\`
   * `C:\Users\<username>\AppData\Roaming\Neolane\NL_5\nlclient\`

1. **[!UICONTROL クライアントコンソール]**&#x200B;を再起動し、Adobe IDでログインします。 キャッシュフォルダーは、次回の起動時に自動的に再作成されます。
