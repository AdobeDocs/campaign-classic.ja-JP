---
title: スキーマの再生成
seo-title: スキーマの再生成
description: スキーマの再生成
seo-description: null
page-status-flag: never-activated
uuid: 455c37f1-cbaf-4503-b2e9-5eec7fad6e97
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: 0f7c835e-b429-422b-87ae-1234c7dd8fe6
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 7%

---


# スキーマの再生成{#regenerating-schemas}

スキーマを変更して変更を保存すると、拡張スキーマが自動的に生成されます。 ただし、変更を適用するには、手動でスキーマを再生成する必要がある場合があります。 手順は次のとおりです。

1. 再生成する必要があるスキーマを選択します。
1. 右クリックし、「 **[!UICONTROL アクション」>「選択したスキーマを再生成…」を選択します。]** .
1. 「 **[!UICONTROL OK]** 」をクリックして、プロセスを確定して起動します。

その後、「プレビュー」タブと「ドキュメント」タブで、生成されたスキーマの構造を確認できます。 For more on this, refer to the [Principles](../../configuration/using/data-schemas.md#principles) section.

>[!NOTE]
>
>例えば、逆リンクの特定の依存関係の問題を解決するために、すべてのスキーマを強制的に再生成する必要がある場合は、Adobe Campaignアプリケーションサーバーから次のコマンドを起動できます。
>
>**nlserver config -postupgrade -instance:`&lt;インスタンス名>&#39; -force**
>
>その後、Adobe Campaignアプリケーションサーバーを再起動し、クライアントコンソールに接続を解除/再接続する必要があります。
