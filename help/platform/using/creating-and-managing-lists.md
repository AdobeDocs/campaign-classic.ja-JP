---
title: リストの作成および管理
seo-title: リストの作成および管理
description: リストの作成および管理
seo-description: null
page-status-flag: never-activated
uuid: 17d1a7d0-a728-490e-a820-19f469fddbcd
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: profile-management
discoiquuid: 9fc243b2-7b7b-4083-83f6-04c12336492d
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# リストの作成および管理{#creating-and-managing-lists}

## Adobe Campaign でのリストについて {#about-lists-in-adobe-campaign}

リストは、配信アクションのターゲットにしたり、インポート操作時やワークフロー実行時に更新したりできるプロファイルの静的なセットです。例えば、クエリによってデータベースから抽出した母集団からリストを作成できます。

これらのリストを対象とした配信（E メール、SMS、またはその他のチャネルによる）を、許可型マーケティングの方針に従って設定できます。

リストの作成と管理は、「**[!UICONTROL プロファイルとターゲット]**」タブの&#x200B;**[!UICONTROL リスト]**&#x200B;リンクを使用して実行します。

![](assets/s_ncs_user_interface_group_link.png)

Adobe Campaign では、2 つのリストタイプを使用できます。

* **[!UICONTROL グループ]**&#x200B;タイプ：**[!UICONTROL グループ]**&#x200B;タイプのリストは、特定の基準に基づいて選択された個人の&#x200B;**静的な**&#x200B;リストに属しています。リストは、一連のプロファイルのスナップショットのようなものです。データベースにプロファイルが追加されても、リストが自動的に更新されることはありませんので、ご注意ください。

   **[!UICONTROL グループ]**&#x200B;タイプリストの作成方法について詳しくは、この[ページ](#creating-a-profile-list-from-a-group)を参照してください。

* **[!UICONTROL リスト]**&#x200B;タイプ：**[!UICONTROL リスト]**&#x200B;タイプのリストは、ワークフローを使用して作成および管理できます。これはデータのインポートの結果として生成される特定のリストであり、専用の&#x200B;**[!UICONTROL リスト更新]**&#x200B;ワークフローアクティビティで更新できます。

   **[!UICONTROL グループ]**&#x200B;タイプリストと異なり、このタイプのリストは&#x200B;**[!UICONTROL スケジューラー]**&#x200B;アクティビティで自動的に更新されます。**[!UICONTROL リスト]**&#x200B;タイプリストの作成方法の例については、[このページ](../../workflow/using/list-update.md)を参照してください。

## グループからのプロファイルリストの作成 {#creating-a-profile-list-from-a-group}

**[!UICONTROL プロファイルとターゲット]**&#x200B;リンクを使用して作成した&#x200B;**[!UICONTROL グループ]**&#x200B;タイプリストは、デフォルトの Adobe Campaign プロファイルテーブル（nms:recipient）に基づいている必要があります。

>[!NOTE]
>
>他のタイプのデータを含むリストを作成するには、ワークフローを実行する必要があります。例えば、訪問者テーブルでクエリを使用してからリストを更新することによって、訪問者リストを作成できます。ワークフローについて詳しくは、[この節](../../workflow/using/about-workflows.md)を参照してください。

新しい&#x200B;**[!UICONTROL グループ]**&#x200B;タイプリストを作成するには、次の手順を適用します。

1. 「**[!UICONTROL 作成]**」ボタンをクリックし、「**[!UICONTROL 新しいリスト]**」を選択します。

   ![](assets/s_ncs_user_new_group.png)

1. リスト作成ウィンドウの「**[!UICONTROL 編集]**」タブで情報を入力します。

   * 「**[!UICONTROL ラベル]**」フィールドにリスト名を入力し、必要に応じて内部名を変更します。
   * このリストの説明を入力します。
   * 有効期限を指定できます。この日付に達すると、リストはパージされ自動的に削除されます。

      ![](assets/list_expiration_date.png)

1. 「**[!UICONTROL コンテンツ]**」タブで「**[!UICONTROL 追加]**」をクリックし、リストに属するプロファイルを選択します。

   ![](assets/s_ncs_user_add_group.png)

1. 「**[!UICONTROL 保存]**」をクリックしてリストを保存します。リストの概要にリストが追加されます。

「**[!UICONTROL 作成]**」をクリックして、プロファイル追加ウィンドウから新しいプロファイルを直接作成できます。プロファイルはデータベースに追加されます。

![](assets/s_ncs_user_new_recipient_from_group.png)

プロファイルリストは、他のリストと同様に設定できます。詳しくは、[リストの設定](../../platform/using/adobe-campaign-workspace.md#configuring-lists)を参照してください。

## リストへのデータのリンク {#linking-data-to-a-list}

>[!NOTE]
>
>リストへのデータのリンクは、**[!UICONTROL グループ]**&#x200B;タイプリストでのみ可能です。

一連のプロファイルをフィルターしてリストにリンクすることができます。配信アクションをこのリスト、つまりターゲットプロファイルに送信できます。プロファイルをグループ化するには、以下の手順に従います。

1. プロファイルを選択して、右クリックします。
1. **[!UICONTROL アクション／リストに選択項目を関連付け...]** を選択します。

   ![](assets/s_ncs_user_add_selection_to_group.png)

1. 目的のリストを選択するか、**[!UICONTROL 作成]**&#x200B;ボタンを使用して新しいリストを作成し、「**[!UICONTROL 次へ]**」をクリックします。

   ![](assets/s_ncs_user_add_selection_to_group_2.png)

1. 「**[!UICONTROL 開始]**」ボタンをクリックします。

   ![](assets/s_ncs_user_add_selection_to_group_3.png)

「**[!UICONTROL リストを再作成]**」オプションでは、以前のコンテンツがリストから削除されます。プロファイルが既にリストにリンクされているかどうかを検証するためのクエリが不要なので、このモードは最適化されています。

「**[!UICONTROL データベースにこのジョブのトレースを保存しない]**」オプションをオフにした場合、このプロセスにリンクされた情報を保存する実行フォルダーを選択（または作成）できます。

ウィンドウの上部セクションで実行を監視できます。「**[!UICONTROL 停止]**」ボタンを使用してプロセスを停止できます。既に処理された連絡先がリストにリンクされます。

この操作の対象となるプロファイルで「**[!UICONTROL リスト]**」タブを使用して、プロセスを監視できます。

![](assets/s_ncs_user_add_selection_to_group_4.png)

Adobe Campaign ホームページからリストを編集することもできます。**[!UICONTROL プロファイルとターゲット／リスト]**&#x200B;メニューをクリックして、該当するリストを選択します。「**[!UICONTROL コンテンツ]**」タブには、このリストにリンクされているプロファイルが表示されます。

![](assets/s_ncs_user_add_selection_to_group_5.png)

## リストからのプロファイルの削除 {#removing-a-profile-from-a-list}

次の操作で、リストからプロファイルを削除することができます。

* リストを編集し、「**[!UICONTROL コンテンツ]**」タブでプロファイルを選択して、「**[!UICONTROL 削除]**」アイコンをクリックします。

   ![](assets/list_remove_a_recipient.png)

* プロファイルを編集し、「**[!UICONTROL リスト]**」タブをクリックして、「**[!UICONTROL 削除]**」アイコンをクリックします。

   ![](assets/recipient_remove_a_list.png)

## プロファイルリストの削除 {#deleting-a-list-of-profiles}

Adobe Campaign ツリーのグループリストから 1 つ以上のリストを削除できます。そのためには、Adobe Campaign ホームページで&#x200B;**[!UICONTROL 詳細設定／エクスプローラー]**&#x200B;リンクを選択し、ツリーを編集します。該当するグループを選択して右クリックします。「**[!UICONTROL 削除]**」を選択します。削除を確定するよう求める警告メッセージが表示されます。

>[!NOTE]
>
>リストを削除した場合、リストのプロファイルは影響を受けませんが、プロファイルのデータは更新されます。

