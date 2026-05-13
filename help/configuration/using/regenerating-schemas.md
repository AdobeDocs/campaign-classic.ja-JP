---
product: campaign
title: スキーマを再生成
description: Campaign スキーマを再生成する方法について説明します
feature: Custom Resources
role: Developer
exl-id: 6c48cfea-6d20-4462-a485-71e1575a08a7
TQID: https://experienceleague.adobe.com/gkWtbp4Vw-wY5yHsd4xJbDx04u3aPhdg-8kB5OXZu94
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2: id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 136
ht-degree: 2%

---

# スキーマを再生成{#regenerating-schemas}

スキーマを変更して変更を保存すると、拡張スキーマが自動的に生成されます。 ただし、変更を適用するには、スキーマを手動で再生成する必要がある場合があります。 手順は次のとおりです。

1. 再生成する必要のあるスキーマを選択します。
1. 右クリックして、**[!UICONTROL アクション / 選択したスキーマを再生成…]**&#x200B;を選択します。
1. 「**[!UICONTROL OK]**」をクリックして、プロセスを確認し、起動します。

次に、「プレビュー」タブと「ドキュメント」タブで、生成されたスキーマの構造を確認できます。 詳しくは、[原則](../../configuration/using/data-schemas.md#principles)の節を参照してください。

>[!NOTE]
>
>リバースリンクの特定の依存関係の問題を解決するために、すべてのスキーマを強制的に再生成する必要がある場合は、Adobe Campaign アプリケーションサーバーから次のコマンドを起動できます。
>
> `nlserver config -postupgrade -instance:`&lt;instance_name>` -force`
>
>その後、Adobe Campaign アプリケーションサーバーを再起動し、クライアントコンソールへの接続を切断または再接続する必要があります。
