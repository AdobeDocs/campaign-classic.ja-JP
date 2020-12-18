---
solution: Campaign Classic
product: campaign
title: スキーマの再生成
description: スキーマの再生成
audience: configuration
content-type: reference
topic-tags: editing-schemas
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 6%

---


# スキーマの再生成{#regenerating-schemas}

スキーマを変更して変更を保存すると、拡張スキーマが自動的に生成されます。 ただし、変更を適用するには、手動でスキーマを再生成する必要がある場合があります。 手順は次のとおりです。

1. 再生成する必要があるスキーマを選択します。
1. 右クリックし、**[!UICONTROL Actions/Regenerate selectedスキーマ...を選択します。]**.
1. 「**[!UICONTROL OK]**」をクリックして、プロセスを確定して起動します。

その後、「プレビュー」タブと「ドキュメント」タブで、生成されたスキーマの構造を確認できます。 詳しくは、[原則](../../configuration/using/data-schemas.md#principles)の節を参照してください。

>[!NOTE]
>
>例えば、逆リンクの特定の依存関係の問題を解決するために、すべてのスキーマを強制的に再生成する必要がある場合は、Adobe Campaignアプリケーションサーバーから次のコマンドを起動できます。
>
>**nlserver config -postupgrade -instance:`&lt;instance_name>&#39; -force**
>
>その後、Adobe Campaignアプリケーションサーバーを再起動し、クライアントコンソールに接続を解除/再接続する必要があります。
