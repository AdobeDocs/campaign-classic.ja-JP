---
product: campaign
title: プロファイルの管理
description: プロファイルの管理
feature: Profiles
audience: platform
content-type: reference
topic-tags: profile-management
exl-id: e1d0556a-6f30-4863-9025-eb9c1b8b53d3
hide: true
hidefromtoc: true
source-git-commit: d3a603bbb70dc63e72b6eed87a6503e155aff54e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 82%

---

# プロファイルの管理{#managing-profiles}



## 受信者ツリー {#recipient-tree}

高度な受信者管理機能を使用するには、Adobe Campaign ツリーを編集する必要があります。そのためには、ツールバーの「**[!UICONTROL エクスプローラー]**」ボタンをクリックします。

デフォルトでは、受信者は Adobe Campaign ツリーの「**[!UICONTROL プロファイルとターゲット]**」ノードに保存されています。同じノードから、1 つ以上のフォルダーとサブフォルダーを作成して受信者プロファイルを保存できます。

各ノードはフォルダーに一致しています。各フォルダーのデータは、相互に分離されているとみなす必要があります。したがって、複数の受信者フォルダーがある場合、コピーは慎重におこなう必要があります。

>[!NOTE]
>
> * データベース内のすべての受信者のリストを表示するには、ビューを作成する必要があります。詳しくは、[Campaign v8 （コンソール）ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/config/configuration/folders-and-views){target=_blank} を参照してください。
>
> * プロファイルの管理方法について詳しくは、[Campaign v8 （コンソール）ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/config/configuration/folders-and-views){target=_blank} を参照してください。


<!--
## Move recipients {#moving-recipients}

You can select one or more recipients, drag them from the recipient list, and drop them in the desired folder. A warning message asks you to confirm this action.

## Copy a recipient {#copying-a-recipient}

You can copy a recipient in the same folder by right-clicking the desired recipient and selecting **[!UICONTROL Copy]**.

## Delete recipients {#deleting-recipients}

To delete recipients, move them to a specific folder and then purge the content of this folder. It is **strongly recommended not to use** the **[!UICONTROL Delete]** option in this case.

To purge a folder, use the **[!UICONTROL Actions > Purge folder]** menu, accessed by right-clicking the desired folder.

![](assets/s_ncs_user_purge_folder.png)

Click **[!UICONTROL Start]** to launch the operation. The middle section of the window displays the progress status, as shown below:

![](assets/s_ncs_user_purge_folder_start.png)
-->