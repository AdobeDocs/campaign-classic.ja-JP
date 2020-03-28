---
title: トラッキングするリンクの設定方法
seo-title: トラッキングするリンクの設定方法
description: トラッキングするリンクの設定方法
seo-description: null
page-status-flag: never-activated
uuid: 0fb41a43-8a84-4a61-bf93-97e1d448a5ec
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: tracking-messages
discoiquuid: 9cae3861-88eb-447a-aa23-9d1de0710eec
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# トラッキングするリンクの設定方法{#how-to-configure-tracked-links}

配信ごとに、メッセージの受信と、メッセージコンテンツに挿入されたリンクの有効化をトラッキングできます。これによって、ターゲットとした配信アクションに続く受信者の行動をトラッキングできます。

>[!NOTE]
>
>トラッキングはメッセージに適用されますが、Web トラッキングを使用すると、受信者がどのように Web サイトを閲覧しているか（訪問したページ、購入など）を監視できます。
>
>Web トラッキングの設定については、[この節](../../configuration/using/about-web-tracking.md)で説明しています。

メッセージトラッキングは、デフォルトで有効になっています。URL のトラッキング方法をパーソナライズするには、以下の手順に従います。

1. 配信ウィザードの下部のセクションで、メッセージコンテンツの下にある「**[!UICONTROL URL を表示]**」オプションを選択します。

   ![](assets/s_ncs_user_email_del_display_urls.png)

   トラッキングされる URL のリストから URL を選択すると、ミラーページ内のリンクとデフォルトで提供される購読解除リンクを除いて、配信コンテンツ内でその URL が強調表示されます。

   ![](assets/s_ncs_user_email_del_show_urls.png)

1. メッセージの URL ごとに、トラッキングを有効化するかどうかを選択します。

   >[!CAUTION]
   >
   >リンクの URL がラベルとして使用されている場合は、トラッキングを無効化してフィッシングによる拒否のリスクを回避することをお勧めします。
   >
   >例えば、www.adobe.com URL がメッセージに挿入され、トラッキングが有効化されている場合、ハイパーテキストリンクのコンテンツは https://nlt.adobe.net/r/?id=xxxxxx に変更されます。これは、この URL が受信者のメッセージクライアントによって不正とみなされる可能性があることを意味します。

1. 必要に応じて、トラッキングラベルを変更します。それには、ラベルをダブルクリックして、新しいラベルを入力します。

   >[!NOTE]
   >
   >トラッキングされる URL のラベルとラベルを変更して、配信のトラッキング時に情報を見やすくすることができます。クリック数の計算時には、同じ名前を持つ 2 つの URL または 2 つのラベルがまとめられます。

1. 必要に応じて、トラッキングモードを変更します。それには、次のように、ターゲットとするリンクに対応する&#x200B;**[!UICONTROL トラッキング]**&#x200B;列で新しいモードを選択します。

   ![](assets/s_ncs_user_select_tracking_mode.png)

   URL ごとに、トラッキングモードを次のいずれかの値に設定できます。

   * **[!UICONTROL 有効]**：この URL のトラッキングを有効化します。
   * **[!UICONTROL トラッキングしない]**：この URL のトラッキングを無効化します。
   * **[!UICONTROL 常に有効]**：この URL のトラッキングを常に有効化します。この情報は保存されるので、次回この URL が将来のメッセージコンテンツに再び表示された場合にそのトラッキングが自動的に有効化されます。
   * **[!UICONTROL 一度もトラッキングされてない]**：この URL のトラッキングを有効化しません。この情報は保存されるので、次回この URL が将来のメッセージに再び表示された場合にそのトラッキングが自動的に無効化されます。
   * **[!UICONTROL オプトアウト]**：この URL をオプトアウトまたは購読解除 URL とみなします。
   * **[!UICONTROL ミラーページ]**：この URL をミラーページの URL とみなします。

1. 加えて、**[!UICONTROL カテゴリ]**&#x200B;列のドロップダウンリストで、トラッキングする URL のそれぞれに対してカテゴリを選択できます。これらのカテゴリは、「**[!UICONTROL URL とクリックストリーム]**」の例に示すように、レポートに表示できます（[この節](../../reporting/using/reports-on-deliveries.md#urls-and-click-streams)を参照）。カテゴリは特定の列挙 **[!UICONTROL urlCategory]** で定義されます（[列挙の管理](../../platform/using/managing-enumerations.md)を参照）。
