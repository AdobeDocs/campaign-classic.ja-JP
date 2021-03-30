---
solution: Campaign Classic
product: campaign
title: シードアドレスについて
description: シードアドレスについて
audience: delivery
content-type: reference
topic-tags: using-seed-addresses
translation-type: tm+mt
source-git-commit: 9237e11edec4114b2bd0932e6128775f36aad27c
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 76%

---


# シードアドレスについて{#about-seed-addresses}

シードアドレスは、定義されたターゲット条件に合わない受信者を配信のターゲットにする場合に使用されます。これにより、配信スコープ外の受信者が他のターゲット受信者と同様に配信を受信することができます。

これらを使用する主な理由の 1 つが、**メーリングリスト保護**&#x200B;です。メーリングリストにシードアドレスを挿入すると、メーリングリストに送信された配信をシードアドレスが受信するので、第三者によってメーリングリストが使用されているかどうかを知ることができます。

また、シードアドレスは、配信を送信することで、**プレビューを実行し、送信前に**&#x200B;配達確認のパーソナライズとレンダリングをテストできます([シードアドレスを配達確認として使用](../../delivery/using/steps-defining-the-target-population.md#using-seed-addresses-as-proof)を参照)。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](../../delivery/using/steps-defining-the-target-population.md#seeds-and-proofs-video)

シードアドレス機能には次のメリットがあります。

* フィールドを受信者プロファイルから取得したデータにランダムに置き換える：これにより、例えば「シードアドレス」セクションに電子メールアドレスのみを入力し、キャンペーンがプロファイルから他のフィールドに自動的に入力できるようになります(使用例：フィールドの置き換え](../../delivery/using/use-case--configuring-the-field-substitution.md)を設定します)。[
* データ管理機能を利用するワークフローを使用する場合、配信で処理される追加のデータをシードアドレスのレベルで入力し、値を強制できます。これにより、ランダムな値による置換を回避します。
* シードアドレスは、**[!UICONTROL クリック数]**、**[!UICONTROL 開封数]**、**[!UICONTROL 購読解除]**&#x200B;の配信統計に関するレポートからは自動的に除外されます。

シードアドレスをインポートするか、配信またはキャンペーン上で直接作成すると、シードアドレスが配信のターゲットに追加されます。

>[!NOTE]
>
>シードアドレスは受信者テーブルに属さず、別のテーブルに作成されます。新しいデータで受信者テーブルを拡張する場合、シードアドレステーブルも同じデータで拡張する必要があります。そうしないと、拡張されたフィールドはシードアドレスでは考慮されません。
>
>シードアドレステーブルの拡張方法の例をこの節に示します。[使用例：条件](../../delivery/using/use-case--selecting-seed-addresses-on-criteria.md)のシードアドレスを選択

ダイレクトメール配信の場合、シードアドレスは抽出時に追加され、出力ドキュメントに織り込まれます。

>[!IMPORTANT]
>
>ダイレクトメール配信の場合は、抽出ファイルフォーマットは次の制限事項に従っている必要があります。
>
>* 「**[!UICONTROL グループを処理（GROUP BY + HAVING）]**」オプションは使用できません。
>* 要素のコレクションが抽出される場合、「**[!UICONTROL 単一行（エキスパートユーザー）]**」オプションをオンにしない限り、それらのフィールドのシードアドレスの値は空になります。詳しくは、[この節](../../platform/using/executing-export-jobs.md#step-7---data-formatting)を参照してください。

>


