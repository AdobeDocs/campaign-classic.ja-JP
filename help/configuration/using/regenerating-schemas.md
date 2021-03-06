---
product: campaign
title: スキーマを再生成
description: Campaign スキーマの再生成方法を説明します
exl-id: 6c48cfea-6d20-4462-a485-71e1575a08a7
source-git-commit: 56459b188ee966cdb578c415fcdfa485dcbed355
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 3%

---

# スキーマを再生成{#regenerating-schemas}

![](../../assets/v7-only.svg)

スキーマを変更して変更を保存すると、拡張スキーマが自動的に生成されます。 ただし、変更を適用するには、スキーマを手動で再生成する必要が生じる場合があります。 手順は次のとおりです。

1. 再生成するスキーマを選択します。
1. 右クリックして「 」を選択します。 **[!UICONTROL アクション/選択したスキーマを再生成…]** .
1. クリック **[!UICONTROL OK]** をクリックして、プロセスを確定して起動します。

「プレビュー」タブと「ドキュメント」タブで、生成されたスキーマの構造を確認できます。 詳しくは、 [原則](../../configuration/using/data-schemas.md#principles) 」セクションに入力します。

>[!NOTE]
>
>例えば、逆リンクでの依存関係の問題を解決するために、すべてのスキーマの再生成を強制する必要がある場合は、Adobe Campaignアプリケーションサーバーから次のコマンドを起動できます。
>
> `nlserver config -postupgrade -instance:`&lt;instance_name>` -force`
>
>その後、Adobe Campaignアプリケーションサーバーを再起動し、クライアントコンソールから切断し、再接続する必要があります。
