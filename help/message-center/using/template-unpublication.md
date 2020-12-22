---
solution: Campaign Classic
product: campaign
title: テンプレートのパブリッシュ
description: テンプレートのパブリッシュ
audience: message-center
content-type: reference
topic-tags: message-templates
translation-type: tm+mt
source-git-commit: 02dee9c4cc03784ccc20f147f816798248bd10f2
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 64%

---


# テンプレートの非公開{#template-unpublication}

メッセージテンプレートは、実行インスタンスで公開した後に非公開にできます。テンプレートの公開プロセスについて詳しくは、[このセクション](../../message-center/using/template-publication.md)を参照してください。

* 実際、対応するイベントがトリガーされた場合、公開済みのテンプレートは引き続き呼び出すことができます。メッセージテンプレートを使用しなくなった場合は、非公開にすることをお勧めします。 これは、不要なトランザクションメッセージを誤って送信するのを避けるためです。

   例えば、クリスマスキャンペーンにのみ使用するメッセージテンプレートを公開したとします。クリスマス期間が終わったらテンプレートを非公開にして、来年の同時期に再度パブリッシュすることができます。

* また、ステータスが「**[!UICONTROL パブリッシュ済み]**」のトランザクションメッセージテンプレートは削除できません。最初にテンプレートを非公開にする必要があります。

>[!NOTE]
>
>この機能は、Campaign 20.2 リリース以降で利用できます。

トランザクションメッセージテンプレートを非公開にするには、次の手順に従います。

1. コントロールインスタンスで、ツリーの&#x200B;**[!UICONTROL Message Center/]**&#x200B;トランザクションメッセージテンプレートフォルダーに移動します。
1. 非公開にするテンプレートを選択します。
1. 「**[!UICONTROL 非公開にする]**」をクリックします。

   <!--1. Fill in the **[!UICONTROL Log of the process]** field.-->

1. 「**[!UICONTROL 開始]**」をクリックします。

![](assets/message-center-unpublish.png)

トランザクションメッセージテンプレートのステータスが「**[!UICONTROL パブリッシュ済み]**」から「**[!UICONTROL 編集中]**」に変わります。

非公開にした後は、以下のようになります。

* 両方のメッセージテンプレート（バッチイベントおよびリアルタイムイベントに適用）が各実行インスタンスから削除されます。

   これらは、**[!UICONTROL 管理/実稼働/Message Centerの実行/デフォルト/トランザクションメッセージテンプレート]**&#x200B;フォルダーに表示されなくなりました（[このセクション](../../message-center/using/template-publication.md)を参照）。

* テンプレートを非公開にした後は、コントロールインスタンスから削除できます。

   これをおこなうには、リストからテンプレートを選択し、画面の右上にある「**[!UICONTROL 削除]**」ボタンをクリックします。