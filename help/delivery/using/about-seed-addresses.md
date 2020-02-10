---
title: シードアドレスについて
seo-title: シードアドレスについて
description: シードアドレスについて
seo-description: null
page-status-flag: never-activated
uuid: 80ab5abc-3ae0-484d-88c0-be039aac360d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: using-seed-addresses
discoiquuid: b49acfd0-b601-4694-88e3-cc0a169cb866
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0ce6e5277c32bc18c20dca62e5b276f654d1ace5

---


# シードアドレスについて{#about-seed-addresses}

シードアドレスは、定義されたターゲット条件に合わない受信者を配信のターゲットにする場合に使用されます。これにより、配信スコープ外の受信者が他のターゲット受信者と同様に配信を受信することができます。

これらを使用する主な理由の 1 つが、**メーリングリスト保護**&#x200B;です。メーリングリストにシードアドレスを挿入すると、メーリングリストに送信された配信をシードアドレスが受信するので、第三者によってメーリングリストが使用されているかどうかを知ることができます。

Moreover, seed addresses let you **preview and test the deliveries personalization and rendering** before their sending, by sending them proofs (see [Using seed addresses as proof](../../delivery/using/steps-validating-the-delivery.md#using-seed-addresses-as-proof)).

シードアドレス機能には次のメリットがあります。

* Random substitution of fields with data taken from recipient profiles: this lets you enter only the email address, for instance in the seed address section, and let Campaign automatically fill in the other fields form the profile (see [Use case: configuring the field substitution](../../delivery/using/use-case--configuring-the-field-substitution.md)).
* データ管理機能を利用するワークフローを使用する場合、配信で処理される追加のデータをシードアドレスのレベルで入力し、値を強制できます。これにより、ランダムな値による置換を回避します。
* Seed addresses are automatically excluded from reports on the following delivery statistics: **[!UICONTROL Clicks]**, **[!UICONTROL Opens]**, **[!UICONTROL Unsubscriptions]**.

シードアドレスをインポートするか、配信またはキャンペーン上で直接作成すると、シードアドレスが配信のターゲットに追加されます。

>[!NOTE]
>
>シードアドレスは受信者テーブルに属さず、別のテーブルに作成されます。新しいデータで受信者テーブルを拡張する場合、シードアドレステーブルも同じデータで拡張する必要があります。そうしないと、拡張されたフィールドはシードアドレスでは考慮されません。
>
>シードアドレステーブルの拡張方法の例を次に示します。使 [用例：条件に基づくシードアドレスの選択](../../delivery/using/use-case--selecting-seed-addresses-on-criteria.md)

ダイレクトメール配信の場合、シードアドレスは抽出時に追加され、出力ドキュメントに織り込まれます。

>[!CAUTION]
>
>ダイレクトメール配信の場合は、抽出ファイルフォーマットは次の制限事項に従っている必要があります。
>
>* このオプションは使用できませ **[!UICONTROL Handle groupings (GROUP BY+HAVING)]**&#x200B;ん。
>* If element collections are extracted, these fields will have an empty value for the seed addresses, unless the **[!UICONTROL Single row (expert user)]** option is selected. 詳しくは、[この節](../../platform/using/exporting-data.md#step-7---data-formatting)を参照してください。
>


