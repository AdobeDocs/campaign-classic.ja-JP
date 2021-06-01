---
product: campaign
title: スキーマの再生成
description: スキーマの再生成
audience: configuration
content-type: reference
topic-tags: editing-schemas
exl-id: 6c48cfea-6d20-4462-a485-71e1575a08a7
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 6%

---

# スキーマの再生成{#regenerating-schemas}

スキーマを変更して変更を保存すると、拡張スキーマが自動的に生成されます。 ただし、変更を適用するには、スキーマを手動で再生成する必要が生じる場合があります。 手順は次のとおりです。

1. 再生成するスキーマを選択します。
1. 右クリックし、**[!UICONTROL アクション/選択したスキーマを再生成…を選択します。]**&#x200B;を参照してください。
1. 「**[!UICONTROL OK]**」をクリックして、プロセスを確定して起動します。

「プレビュー」タブと「ドキュメント」タブで、生成されたスキーマの構造を確認できます。 詳しくは、[原則](../../configuration/using/data-schemas.md#principles)の節を参照してください。

>[!NOTE]
>
>例えば、リバースリンクでの依存関係の問題を解決するために、すべてのスキーマの再生成を強制する必要がある場合は、Adobe Campaignアプリケーションサーバーから次のコマンドを起動できます。
>
>**nlserver config -postupgrade -instance:&#39;&lt;instance_name>&#39; -force**
>
>その後、Adobe Campaignアプリケーションサーバーを再起動し、クライアントコンソールから切断し、再接続する必要があります。
