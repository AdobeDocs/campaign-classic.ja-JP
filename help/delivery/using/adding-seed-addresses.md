---
product: campaign
title: シードアドレスの追加
description: シードアドレスの追加
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Seed Address
role: User
exl-id: ae6eb4b0-b419-4661-9d63-e758f0242a0f
TQID: https://experienceleague.adobe.com/pVYaTG48-HiK0RwJXgBbIMWa-o-R7jlEpauXNXvGi5E
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
feature_v2:
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2:
  - id: e95a583b-fcfa-4524-8666-46a29c828119
  - id: c8da4fdd-eb94-4751-a43c-f82733fb2d6e
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: f4da0e76-df77-451e-ad61-21afb7bd8810
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 91%

---

# シードアドレスの追加{#adding-seed-addresses}

## 配信のシードアドレス {#seed-addresses-in-a-delivery}

特定のシードアドレスを配信に追加するには、**[!UICONTROL 宛先]**&#x200B;リンクをクリックし、「**[!UICONTROL シードアドレス]**」タブを選択します。

![](assets/s_ncs_user_edit_del_addresses_tab.png)

次の 3 種類の挿入モードがあります。

1. 単一のシードアドレスを入力する。

   そのためには、「**[!UICONTROL 追加]**」ボタンをクリックし、アドレスフィールドの内容を設定します。 この操作を各アドレスに対して繰り返します。

1. アドレステンプレートをインポートし、ニーズに合わせて変更する。

   そのためには、**[!UICONTROL シードテンプレートをインポート...]** リンクをクリックし、アドレステンプレートを含んだフォルダーを選択します。 詳しくは、[この節](creating-seed-addresses.md#creating-seed-address-templates)を参照してください。

   必要な場合は、アドレスを追加した後にアドレスをダブルクリックするか、「**[!UICONTROL 詳細]**」ボタンをクリックして、各アドレスの内容を変更します。

1. 挿入する制御アドレスを動的に選択する条件を作成する。

   そのためには、**[!UICONTROL 動的条件を編集...]** リンクをクリックし、シードアドレスの選択パラメーターを入力します。 例えば、ある特定のフォルダーに格納されているすべてのシードアドレスや、組織の特定の部門に属しているシードアドレスを含めることができます。

   この例については、[ユースケース：条件に基づいたシードアドレスの選択](use-case-selecting-seed-addresses-on-criteria.md)の節を参照してください。

>[!NOTE]
>
>このオプションは、使用する受信者テーブルがデフォルトの&#x200B;**nms:recipient** テーブルではなく、Adobe Campaignの&#x200B;**[!UICONTROL 配信品質]** モジュールで提供されている受信ボックスレンダリング機能を使用している場合に使用します。
>
>詳しくは、[外部の受信者テーブルの使用](using-an-external-recipient-table.md)および[受信ボックスレンダリング](inbox-rendering.md)に関するドキュメントを参照してください。

また、配信では、アドレスを抽出ファイルに挿入する際の方法をカスタマイズすることもできます。 デフォルトでは出力ファイルの並べ替え順に従って挿入されますが、ファイルの冒頭または末尾に挿入する指定や、メインターゲットの送信者中にランダムに挿入する指定が可能です。

![](assets/s_ncs_user_edit_del_addresses_sort.png)

## キャンペーンのシードアドレス {#seed-addresses-in-a-campaign}

キャンペーンのターゲットにシードアドレスを追加するには、キャンペーンを選択し、「**[!UICONTROL 編集]**」タブをクリックします。

次のように、「**[!UICONTROL キャンペーンの詳細設定]**」リンクをクリックし、「**[!UICONTROL シードアドレス]**」タブを選択します。

![](assets/s_ncs_user_edit_op_addresses_tab.png)

キャンペーンから挿入したシードアドレスは、キャンペーンの各配信のターゲットに追加されます。
