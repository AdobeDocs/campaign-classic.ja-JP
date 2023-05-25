---
product: campaign
title: トラッキングするリンクの設定方法
description: トラッキングするリンクの設定方法
badge-v7: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7"
badge-v8: label="v8" type="Positive" tooltip="Also applies to Campaign v8"
feature: Monitoring
exl-id: ed88e1d6-c0d5-4a85-9f3e-be670f4bcc10
source-git-commit: 6dc6aeb5adeb82d527b39a05ee70a9926205ea0b
workflow-type: ht
source-wordcount: '603'
ht-degree: 100%

---

# トラッキングするリンクの設定方法{#how-to-configure-tracked-links}



配信ごとに、メッセージの受信と、メッセージコンテンツに挿入されたリンクの有効化をトラッキングできます。これによって、ターゲットとした配信アクションに続く受信者の行動をトラッキングできます。

トラッキングはメッセージに適用されますが、Web トラッキングを使用すると、受信者がどのように Web サイトを閲覧しているか（訪問したページ、購入など）を監視できます。web トラッキングの設定については、[この節](../../configuration/using/about-web-tracking.md)で説明しています。

>[!NOTE]
>
>パーソナライゼーションを含む電子メールコンテンツ内のリンクは、特定の構文を追跡する必要があります。 パーソナライズ可能な電子メールにリンクを追加する方法、および追跡をサポートする電子メールについて詳しくは、[このセクション](tracking-personalized-links.md)を参照してください。

トラッキング式を適用する前に、「**[!UICONTROL テキストコンテンツ]**」タブで URL を区切り文字で囲むことを強くお勧めします。 このタブに入力する URL 区切り文字は、Adobe Campaign で文字列内の URL を識別するために使用されます。 次の区切り文字のペアを使用できます。
* 括弧 ( )
* 角括弧 [ ]
* 中括弧 { }

この例では、URL https://www.adobe.com の後にセミコロンが続きます。 セミコロンは、受信者の E メールクライアントで、URL の一部として解釈される場合があります。 その結果、リンク切れになる場合があります。 この問題を回避するには、次のいずれかの方法で URL を区切り文字で囲みます。
* (https://www.adobe.com/jp);
* [https://www.adobe.com/jp];
* {https://www.adobe.com/jp};

メッセージトラッキングは、デフォルトで有効になっています。URL のトラッキング方法をパーソナライズするには、以下の手順に従います。

1. 配信ウィザードの下部のセクションで、メッセージコンテンツの下にある「**[!UICONTROL URL を表示]**」オプションを選択します。

   ![](assets/s_ncs_user_email_del_display_urls.png)

   トラッキングされる URL のリストから URL を選択すると、ミラーページ内のリンクとデフォルトで提供される購読解除リンクを除いて、配信コンテンツ内でその URL が強調表示されます。

   ![](assets/s_ncs_user_email_del_show_urls.png)

1. メッセージの URL ごとに、トラッキングを有効化するかどうかを選択します。

   >[!IMPORTANT]
   >
   >リンクの URL がラベルとして使用されている場合は、トラッキングを無効にしてフィッシングが原因で却下されるリスクを回避することをお勧めします。
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
   * **[!UICONTROL トラッキングしない]** : この URL のトラッキングを無効にします。
   * **[!UICONTROL 常に有効]**：この URL のトラッキングを常に有効化します。この情報は保存されるので、次回この URL が将来のメッセージコンテンツに再び表示された場合にそのトラッキングが自動的に有効化されます。
   * **[!UICONTROL 一度もトラッキングされてない]**：この URL のトラッキングを有効化しません。この情報は保存されるので、次回この URL が将来のメッセージに再び表示された場合にそのトラッキングが自動的に無効化されます。
   * **[!UICONTROL オプトアウト]**：この URL をオプトアウトまたは購読解除 URL とみなします。
   * **[!UICONTROL ミラーページ]**：この URL をミラーページの URL とみなします。

1. 加えて、**[!UICONTROL カテゴリ]**&#x200B;列のドロップダウンリストで、トラッキングする URL のそれぞれに対してカテゴリを選択できます。これらのカテゴリは、「**[!UICONTROL URL とクリックストリーム]**」の例に示すように、レポートに表示できます（[この節](../../reporting/using/reports-on-deliveries.md#urls-and-click-streams)を参照）。カテゴリは特定の列挙 **[!UICONTROL urlCategory]** で定義されます（[列挙の管理](../../platform/using/managing-enumerations.md)を参照）。
