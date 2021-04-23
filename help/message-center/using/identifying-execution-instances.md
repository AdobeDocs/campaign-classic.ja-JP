---
solution: Campaign Classic
product: campaign
title: 実行インスタンスの識別
description: 実行インスタンスの識別
audience: message-center
content-type: reference
topic-tags: instance-configuration
exl-id: bf81a058-8715-4da2-a2d5-4362c433c549
translation-type: ht
source-git-commit: 6854d06f8dc445b56ddfde7777f02916a60f2b63
workflow-type: ht
source-wordcount: '107'
ht-degree: 100%

---

# 実行インスタンスの識別{#identifying-execution-instances}

コントロールインスタンスから各実行インスタンスの履歴を閲覧した際にそれぞれを区別できるよう、各実行インスタンスには一意の識別子を割り当てなければなりません。コントロールインスタンスと実行インスタンスが同じマシンにインストールされている場合でもこの手順は必須です。各実行インスタンスへの識別子の割り当ては、デプロイウィザードを使用して手動でおこなうか、コントロールインスタンスから「**接続を初期化**」ボタンをクリックして自動でおこなうことができます（[コントロールインスタンス](../../message-center/using/creating-a-shared-connection.md#control-instance)を参照）。

手動で識別子を割り当てるには、各実行インスタンスにてデプロイウィザードを開き、**[!UICONTROL Message Center]** ウィンドウに移動し、インスタンスに任意の識別子を指定します。

![](assets/messagecenter_id_execinstance_001.png)
