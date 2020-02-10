---
title: シードアドレスの追加
seo-title: シードアドレスの追加
description: シードアドレスの追加
seo-description: null
page-status-flag: never-activated
uuid: e94ddd46-bed6-4505-91b7-7e17abb0e9c8
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: using-seed-addresses
discoiquuid: 0b9b53bf-4dd2-416c-894e-393aded489f8
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# シードアドレスの追加{#adding-seed-addresses}

## 配信のシードアドレス {#seed-addresses-in-a-delivery}

To add specific seed addresses for a delivery, click the **[!UICONTROL To]** link, then select the **[!UICONTROL Seed addresses]** tab.

![](assets/s_ncs_user_edit_del_addresses_tab.png)

次の 3 種類の挿入モードがあります。

1. 単一のシードアドレスを入力する。

   To do this, click the **[!UICONTROL Add]** button and define the content of the address fields. この操作を各アドレスに対して繰り返します。詳しくは、[この節](../../message-center/using/managing-seed-addresses-in-transactional-messages.md#creating-a-seed-address)を参照してください。

1. アドレステンプレートをインポートし、ニーズに合わせて変更する。

   To do this, click the **[!UICONTROL Import seed templates...]** link and select the folder which contains the address templates. 詳しくは、シードアドレステンプレートの作 [成を参照してください](../../delivery/using/creating-seed-addresses.md#creating-seed-address-templates)。

   If necessary, once they are added, you can doucle-click them or click the **[!UICONTROL Detail...]** button to adapt the content of each address.

1. 挿入する制御アドレスを動的に選択する条件を作成する。

   To do this, click the **[!UICONTROL Edit the dynamic condition...]** link, then enter the seed address selection parameters. 例えば、ある特定のフォルダーに格納されているすべてのシードアドレスや、組織の特定の部門に属しているシードアドレスを含めることができます。

   この節では、次の例を示します。使 [用例：条件のシードアドレスの選択](../../delivery/using/use-case--selecting-seed-addresses-on-criteria.md)。

>[!NOTE]
>
>This option is used when the recipient table used is not the default **nms:recipient** table and you are using the Inbox Rendering functionality provided with Adobe Campaign&#39;s **[!UICONTROL Deliverability]** module.
>
>詳しくは、「外部受信者テーブルの使用 [」および「インボックスのレンダリング](../../delivery/using/using-an-external-recipient-table.md) 」のドキュメントを参照 [してください](../../delivery/using/inbox-rendering.md)。

また、配信では、アドレスを抽出ファイルに挿入する際の方法をカスタマイズすることもできます。デフォルトでは出力ファイルの並べ替え順に従って挿入されますが、ファイルの冒頭または末尾に挿入する指定や、メインターゲットの送信者中にランダムに挿入する指定が可能です。

![](assets/s_ncs_user_edit_del_addresses_sort.png)

## キャンペーンのシードアドレス {#seed-addresses-in-a-campaign}

To add seed addresses to a target for a campaign, select the operation and click the **[!UICONTROL Edit]** tab.

次に示すよ **[!UICONTROL Advanced campaign settings...]** うに、リンクをク **[!UICONTROL Seed addresses]** リックし、タブをクリックします。

![](assets/s_ncs_user_edit_op_addresses_tab.png)

キャンペーンから挿入したシードアドレスは、キャンペーンの各配信のターゲットに追加されます。
