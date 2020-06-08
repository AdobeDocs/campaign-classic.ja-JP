---
title: テンプレートのパブリッシュ
seo-title: テンプレートのパブリッシュ
description: テンプレートのパブリッシュ
seo-description: null
page-status-flag: never-activated
uuid: f83dbe5f-762c-4c58-aeed-6ec289eb522f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: message-templates
discoiquuid: 43908738-a71a-49be-ac00-175f57a0555c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1486e897a125520c51661db3030c62ab380fb173
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 71%

---


# テンプレートのパブリッシュ{#template-publication}

コントロールインスタンスでメッセージテンプレートを作成したら、そのテンプレートをすべての実行インスタンスにパブリッシュすることができます。パブリケーションを使用すると、実行インスタンスに2つのメッセージテンプレートを自動的に作成し、リアルタイムメッセージとバッチイベントにリンクしたメッセージを送信できます。

>[!IMPORTANT]
>
>テンプレートに変更を加えた場合には、トランザクションメッセージ配信の際に変更内容が反映されるよう、忘れずにテンプレートをパブリッシュしてください。

>[!NOTE]
>
>トランザクションメッセージテンプレートをパブリッシュすると、タイポロジルールが実行インスタンスに自動的にパブリッシュされます。

1. コントロールインスタンス内で、ツリーの **[!UICONTROL Message Center／トランザクションメッセージテンプレート]**&#x200B;フォルダーに移動します。
1. 実行インスタンスにパブリッシュするテンプレートを選択します。
1. 「 **[!UICONTROL 公開]**」をクリックします。

   ![](assets/messagecenter_publish_model_008.png)

Once publication is complete, both message templates to be applied to batch and real-time type events are created in the tree of the production instance in the **[!UICONTROL Administration > Production > Message Center Execution> Default > Transactional message templates]** folder.

![](assets/messagecenter_deployed_model_001.png)

>[!NOTE]
>
>トランザクションメッセージテンプレートの既存のフィールド（送信者のアドレスなど）を空の値と置き換えた場合、トランザクションメッセージをもう一度パブリッシュすると、既存のインスタンス上にある対応するフィールドは更新されません。引き続き以前の値が含まれます。ただし、空でない値を追加すると、次回のパブリッシュ後に、対応するフィールドが通常どおり更新されます。
