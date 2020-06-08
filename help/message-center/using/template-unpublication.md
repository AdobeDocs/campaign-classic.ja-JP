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
source-git-commit: 71aeeda3edafc64dbe696ce6f344b8b0ccdc43d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 10%

---


# テンプレートの非公開{#template-unpublication}

メッセージテンプレートを実行インスタンスに公開した後は、非公開にできます。

実際、公開済みのテンプレートは、引き続き呼び出すことができます。 したがって、メッセージテンプレートを使用しなくなった場合は、非公開にすることをお勧めします。 これは、不要なトランザクションメッセージを誤って送信するのを避けるためです。 例えば、クリスマスキャンペーンにのみ使用するメッセージテンプレートを公開したとします。 クリスマス期間が終わったら、公開を取り消し、来年に再度公開することができます。

また、 **[!UICONTROL 発行済みステータスのトランザクションメッセージテンプレートは削除できません]** 。 最初に公開を取り消す必要があります。

トランザクションメッセージテンプレートの公開を取り消すには、次の手順に従います。

1. コントロールインスタンス内で、ツリーの **[!UICONTROL Message Center／トランザクションメッセージテンプレート]**&#x200B;フォルダーに移動します。
1. 非公開にするテンプレートを選択します。
1. 「 **[!UICONTROL 非公開]**」をクリックします。

   <!--1. Fill in the **[!UICONTROL Log of the process]** field.-->

1. 「**[!UICONTROL 開始]**」をクリックします。

![](assets/message-center-unpublish.png)

トランザクションメッセージテンプレートのステータスが「 **[!UICONTROL 公開済み]** 」から「 **[!UICONTROL 編集中]**」に変わります。

非公開が完了したら、次の操作を行います。

* 両方のメッセージテンプレート(バッチタイプテンプレートおよびリアルタイムタイプイベントに適用)が各実行インスタンスから削除されます。 これらのプロパティは、 **[!UICONTROL 管理/実稼働/Message Centerの実行/デフォルト/トランザクションメッセージテンプレート]** フォルダーに表示されなくなりました。

* テンプレートを非公開にした後は、必要に応じて、コントロールインスタンスから削除できます。 これを行うには、リストから選択し、画面の右上にある **[!UICONTROL 削除]** ボタンをクリックします。