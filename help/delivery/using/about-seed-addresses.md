---
solution: Campaign Classic
product: campaign
title: シードアドレスについて
description: シードアドレスについて
audience: delivery
content-type: reference
topic-tags: using-seed-addresses
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 100%

---


# シードアドレスについて{#about-seed-addresses}

シードアドレスは、定義されたターゲット条件に合わない受信者を配信のターゲットにする場合に使用されます。これにより、配信スコープ外の受信者が他のターゲット受信者と同様に配信を受信することができます。

これらを使用する主な理由の 1 つが、**メーリングリスト保護**&#x200B;です。メーリングリストにシードアドレスを挿入すると、メーリングリストに送信された配信をシードアドレスが受信するので、第三者によってメーリングリストが使用されているかどうかを知ることができます。

さらに、シードアドレスを使用すると、配達確認を送信することで、送信前に&#x200B;**配信のパーソナライゼーションとレンダリングをプレビューおよびテスト**&#x200B;できます（[配達確認としてのシードアドレスの使用](../../delivery/using/steps-defining-the-target-population.md#using-seed-addresses-as-proof)を参照）。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](../../delivery/using/steps-defining-the-target-population.md#seeds-and-proofs-video)

シードアドレス機能には次のメリットがあります。

* 受信者プロファイルから取得したデータを使用してランダムにフィールドを置換できます。例えば、シードアドレスセクションなどの E メールアドレスを入力するだけで、プロファイルに基づいて他のフィールドの値を自動的に設定できます（[使用例：フィールド置換の設定](../../delivery/using/use-case--configuring-the-field-substitution.md)を参照）。
* データ管理機能を利用するワークフローを使用する場合、配信で処理される追加のデータをシードアドレスのレベルで入力し、値を強制できます。これにより、ランダムな値による置換を回避します。
* シードアドレスは、**[!UICONTROL クリック数]**、**[!UICONTROL 開封数]**、**[!UICONTROL 購読解除]**&#x200B;の配信統計に関するレポートからは自動的に除外されます。

シードアドレスをインポートするか、配信またはキャンペーン上で直接作成すると、シードアドレスが配信のターゲットに追加されます。

>[!NOTE]
>
>シードアドレスは受信者テーブルに属さず、別のテーブルに作成されます。新しいデータで受信者テーブルを拡張する場合、シードアドレステーブルも同じデータで拡張する必要があります。そうしないと、拡張されたフィールドはシードアドレスでは考慮されません。
>
>シードアドレステーブルの拡張方法の例については、[使用例：条件によるシードアドレスの選択](../../delivery/using/use-case--selecting-seed-addresses-on-criteria.md)の節で説明しています。

ダイレクトメール配信の場合、シードアドレスは抽出時に追加され、出力ドキュメントに織り込まれます。

>[!IMPORTANT]
>
>ダイレクトメール配信の場合は、抽出ファイルフォーマットは次の制限事項に従っている必要があります。
>
>* 「**[!UICONTROL グループを処理（GROUP BY + HAVING）]**」オプションは使用できません。
>* 要素のコレクションが抽出される場合、「**[!UICONTROL 単一行（エキスパートユーザー）]**」オプションをオンにしない限り、それらのフィールドのシードアドレスの値は空になります。詳しくは、[この節](../../platform/using/exporting-data.md#step-7---data-formatting)を参照してください。

>


