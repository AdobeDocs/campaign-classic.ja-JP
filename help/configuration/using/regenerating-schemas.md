---
product: campaign
title: スキーマの再生成
description: Campaign スキーマを再生成する方法を学ぶ
feature: Custom Resources
role: Data Engineer, Developer
exl-id: 6c48cfea-6d20-4462-a485-71e1575a08a7
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 2%

---

# スキーマの再生成{#regenerating-schemas}

スキーマを変更して変更を保存すると、拡張スキーマが自動的に生成されます。 ただし、変更を適用するには、スキーマを手動で再生成する必要がある場合があります。 手順は次のとおりです。

1. 再生成する必要があるスキーマを選択します。
1. 右クリックして **[!UICONTROL アクション/選択したスキーマを再生成…]** を選択します。
1. **[!UICONTROL OK]** をクリックして、プロセスを確認して開始します。

生成されたスキーマの構造を「プレビュー」タブと「ドキュメント」タブで確認できます。 詳しくは、「原則 [ の節を参照してくだ ](../../configuration/using/data-schemas.md#principles) い。

>[!NOTE]
>
>すべてのスキーマを強制的に再生成する必要がある場合（例えば、リバースリンクでの特定の依存関係の問題を解決する場合）は、Adobe Campaign アプリケーションサーバーから次のコマンドを実行できます。
>
> `nlserver config -postupgrade -instance:`&lt;instance_name>` -force`
>
>次に、Adobe Campaign アプリケーションサーバーを再起動し、クライアントコンソールを切断または再接続する必要があります。
