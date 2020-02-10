---
title: プロファイルの編集
seo-title: プロファイルの編集
description: プロファイルの編集
seo-description: null
page-status-flag: never-activated
uuid: ad3cd54e-b22f-4fae-8d2a-3e0d3e45fffb
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: profile-management
discoiquuid: 93dd29e8-cf0a-4010-a3cc-f68c52c0d9ef
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 51e4d72abf3a1f48700ca38566dbf06dd24594b8

---


# プロファイルの編集{#editing-a-profile}

プロファイルに関連する情報を表示するには、プロファイルリストでプロファイルの名前をクリックします。

プロファイルの詳細が新しいタブで表示されます。

![](assets/s_user_recipient_edit.png)

プロファイルに関するデータはタブにグループ化されています。

タブとその内容は、設定およびインストールされているパッケージに応じて異なります。

>[!CAUTION]
>
>The XML schema and the form that concerns the fields in the profiles table are accessed via the **[!UICONTROL Administration > Configuration > Data schemas]** node of the Adobe Campaign tree. これらのスキーマを変更できるのは、エキスパートユーザーのみです。
>
>詳しくは、[このページ](../../configuration/using/about-schema-edition.md)を参照してください。

## 「一般」タブ{#general-tab}

この画面には、選択したプロファイルに関するすべての一般データが表示されます。特に、姓、名、E メールアドレス、E メール受信フォーマットなどが含まれています。次のような画面です。

![](assets/s_ncs_user_profile_general_tab.png)

>[!NOTE]
>
>When the **[!UICONTROL No longer contact (by any channel)]** option is selected, this means that the profile is blacklisted, i.e. the profile has expressed a wish not to be contacted (for example, by clicking an unsubscription link in a newsletter). このようなプロファイルは、どのチャネルの配信（E メール、ダイレクトメールなど）のターゲットにもなりません。詳しくは、[このページ](../../delivery/using/understanding-quarantine-management.md)を参照してください。

## 「連絡先情報」タブ{#contact-information-tab}

この画面には、選択したプロファイルのダイレクトメールの住所が表示されます。次のような画面です。

![](assets/s_ncs_user_profile_details_tab.png)

この画面には、住所の品質指標および住所に含まれるエラーの数が表示されます。この情報は、以前の配達時に見つかったエラーの数に基づいて郵便配達員が直接使用するもので、手動による変更はできません。

## 「その他」タブ{#other-tab}

この画面には、要件に基づいてパーソナライズできるユーザー定義のフィールドが表示されます。You can also change the names of the fields and define their format, via **[!UICONTROL Field properties...]**, as shown below:

![](assets/s_ncs_user_profile_others_tab.png)

>[!NOTE]
>
>フィールドプロパティおよびフィールドの追加について詳しくは、[このページ](../../configuration/using/new-field-wizard.md)を参照してください。

## 「リスト」タブ{#lists-tab}

この画面には、選択したプロファイルが属しているグループが表示されます。Click **[!UICONTROL Add]** to subscribe the profile to a list. Click **[!UICONTROL Detail]** to display the description and the list of profiles in the selected list.

![](assets/s_ncs_user_profile_groups_tab_details.png)

詳細については、「リストの作成と管 [理」を参照してください](../../platform/using/creating-and-managing-lists.md)。

## 「購読」タブ{#subscriptions-tab}

この画面には、プロファイルが購読登録した情報サービスが表示されます。

![](assets/s_ncs_user_profile_subscript_tab_details.png)

The **[!UICONTROL Detail]** button displays the properties of the selected subscription. The **[!UICONTROL Add]** button is used to add a new subscription manually.

詳しくは、[このページ](../../delivery/using/managing-subscriptions.md)を参照してください。

## 「配信」タブ{#deliveries-tab}

この画面には、選択したプロファイルの配信ログが表示されます。すべてのチャネルにおけるプロファイル宛ての配信アクションのラベル、日付およびステータスを表示することもできます。

![](assets/s_ncs_user_profile_delivery_tab.png)

## 「トラッキング」タブ{#tracking-tab}

この画面では、選択したプロファイルのトラッキングログを表示できます。この情報は、配信後のプロファイルの行動をトラッキングする場合に使用します。

![](assets/s_ncs_user_profile_tracking_tab.png)

このタブには、配信でトラッキングされたすべての URL の累積合計が表示されます。

このリストは設定可能で、通常は、クリックされた URL、クリックの日時および URL が含まれていたドキュメントが表示されます。

>[!NOTE]
>
>トラッキング機能について詳しくは、[このページ](../../delivery/using/monitoring-a-delivery.md)を参照してください。

