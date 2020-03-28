---
title: インバウンド E メール
seo-title: インバウンド E メール
description: インバウンド E メール
seo-description: null
page-status-flag: never-activated
uuid: 6bcc7952-f051-4e50-8833-95d49c7ed781
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: event-activities
discoiquuid: 4c0530b1-0292-45bc-8730-668bc5b8550b
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

---


# インバウンド E メール{#inbound-emails}

「**インバウンド E メール**」アクティビティでは、POP3 メールサーバーから E メールメッセージをダウンロードして処理できます。

![](assets/email_rec_edit_1.png)

「**インバウンド E メール**」アクティビティの最初のタブで、POP3 サーバーのパラメーターとメール受信時に実行するスクリプトを入力できます。2 番目のタブではアクティビティのスケジュールを設定でき、3 番目のタブではアクティビティの有効期限を設定できます。

1. **[!UICONTROL インバウンド E メール]**

   * **[!UICONTROL 外部アカウントを使用]**

      このオプションが有効化されている場合、ネットワーク接続のパラメーターを入力せずに外部 POP3 アカウントを選択できます。「**[!UICONTROL 外部アカウント]**」フィールドに、メールサービスの接続に使用する外部 POP3 アカウントを指定します。このオプションは、「外部アカウントを使用」オプションが有効にされている場合のみ表示されます。

      このオプションを選択しない場合は、次のパラメーターを指定する必要があります。

      ![](assets/email_rec_edit_1b.png)

      * **[!UICONTROL POP3 サーバー]**

         POP3 サーバーの名前

      * **[!UICONTROL POP3 アカウント]**

         ユーザーの名前。

      * **[!UICONTROL パスワード]**

         アカウントのパスワード

      * **[!UICONTROL ポート]**

         POP3 接続のポート番号デフォルトのポート番号は 110 です。
   * **[!UICONTROL E メールが処理されたらすぐに停止します]**

      このオプションを設定すると E メールが 1 個ずつ処理されます。このアクティビティは、トランジションを 1 回のみ有効化した後、処理を完了し、未処理の E メールをサーバー上に残します。


1. **[!UICONTROL スクリプト]**

   このスクリプトは、E メールを処理し、メールの内容に応じて様々な処理を実行します。スクリプトは E メールごとに実行されます。また、E メールに実行される処理（放置または削除）およびアウトバウンドトランジションの有効化を指定できます。

   戻りコードは、次のいずれかの値になります。

   * 1 - サーバーから E メールを削除して、アウトバウンドトランジションを有効化します。
   * 2 - サーバーに E メールを残して、アウトバウンドトランジションを有効化します。
   * 3 - サーバーから E メールを削除します。
   * 4 - サーバーに E メールを残します。
   E メールのコンテンツには、グローバル変数 **[!UICONTROL mailMessage]** からアクセスできます。

1. **[!UICONTROL スケジュール]**

   アクティビティのスケジュールを設定するには、「**[!UICONTROL スケジュール設定]**」タブをクリックして、「**[!UICONTROL プランの実行]**」を選択します。「**[!UICONTROL 変更]**」ボタンをクリックして、スケジュールを設定します。

   スケジュールの設定は、スケジュール設定アクティビティの場合と同じです。[スケジューラー](../../workflow/using/scheduler.md)を参照してください。

1. **[!UICONTROL 有効期限]**

   「**[!UICONTROL 有効期限]**」タブで、有効期限の延長を設定できます。

   ![](assets/email_rec_edit_3.png)

   有効期限の設定は、スケジュール設定アクティビティの場合と同じです。[有効期限](../../workflow/using/executing-a-workflow.md#expirations)を参照してください。

