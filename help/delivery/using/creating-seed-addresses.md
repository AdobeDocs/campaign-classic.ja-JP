---
product: campaign
title: シードアドレスの作成
description: シードアドレスの作成方法と使用方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Seed Address
role: User, Developer
exl-id: f7dc97f0-3423-4b6f-88e2-08180f9adf8a
TQID: https://experienceleague.adobe.com/ya4m8nG7m3DUj-buOZMnd2Nzfx1J6lmIiOuo1VcHjwU
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: a658c786-869b-4194-a780-2594d663addaid: b631758a-142d-425f-b9aa-f756d85cb979id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2: id: e95a583b-fcfa-4524-8666-46a29c828119id: c8da4fdd-eb94-4751-a43c-f82733fb2d6eid: d5bbe3da-ba85-4242-817e-54f7c4b943e0id: f4da0e76-df77-451e-ad61-21afb7bd8810
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 452
ht-degree: 100%

---

# シードアドレスの作成{#creating-seed-addresses}

シードアドレスの管理には、標準的なプロファイルやターゲットではなく、Adobe Campaign 階層構造の&#x200B;**[!UICONTROL リソース／キャンペーン管理／シードアドレス]**&#x200B;でアクセスできる専用ノードを使用します。

このノードには、シードアドレスを整理するためのサブフォルダーを作成できます。 そのためには、**[!UICONTROL シードアドレス]**&#x200B;ノードを右クリックし、「**[!UICONTROL 新しい「シードアドレス」フォルダーを作成]**」を選択します。 サブフォルダーに名前を付け、**[!UICONTROL Enter]** キーを押して確定します。 これで、作成したサブフォルダー内にシードアドレスを作成したり、別の場所からシードアドレスをコピーしたりできるようになります。 詳しくは、[アドレスの定義](#defining-addresses)を参照してください。

Adobe Campaign では、シードアドレスのテンプレートも作成可能です。配信やキャンペーンにシードアドレスのテンプレートをインポートし、その配信やキャンペーンの具体的なニーズに応じて変更を加えることができます。 [シードアドレステンプレートの作成](#creating-seed-address-templates)を参照してください。

## アドレスの定義 {#defining-addresses}

シードアドレスを作成するには、以下の手順に従います。

1. シードアドレスのリストの上にある「**[!UICONTROL 新規]**」ボタンをクリックします。
1. そのアドレスに関連するデータを、「**[!UICONTROL 受信者]**」タブの該当するフィールドに入力します。 使用可能なフィールドは、姓、名、メールなど、配信受信者のプロファイル（nms:recipient テーブル）の標準的なフィールドに対応します。

   >[!NOTE]
   >
   >アドレスのラベルには、定義した姓と名が自動的に入力されます。
   >
   >シードアドレスを作成する際、各タブのすべてのフィールドに情報を入力する必要はありません。 入力されていないパーソナライゼーション要素は、配信分析時にランダムに入力されます。

   ![](assets/s_ncs_user_seedlist_new_address.png)

1. 「**[!UICONTROL アドレスフィールド]**」タブには、分析フェーズで配信ログ（**[!UICONTROL nms:broadLog]** テーブル）に挿入される値を入力します。

1. 「**[!UICONTROL 追加データ]**」タブでは、データ管理ワークフローで作成される配信のためのパーソナライゼーションデータや、特定の値を設定しておく必要があるパーソナライゼーションデータを入力します。

   >[!NOTE]
   >
   >追加のターゲットデータが、「**[!UICONTROL エンリッチメント]**」アクティビティで「@」で始まるエイリアスで定義されていることを確認してください。 そうでない場合、配信アクティビティのシードアドレスで正しく使用できなくなります。

## シードアドレステンプレートの作成 {#creating-seed-address-templates}

インポートされ、配信ごとに変更可能なアドレステンプレートを作成するためのプロセスは、新しいシードアドレスを定義する場合のプロセスと同様です。 唯一の違いは、シードアドレステンプレートのアドレスを「テンプレート」タイプのフォルダーに格納する必要があることです。

テンプレートフォルダーを定義するには、次の手順に従います。

1. 新しい&#x200B;**[!UICONTROL シードアドレス]**&#x200B;タイプのフォルダーを作成します。そのフォルダーを右クリックし、「**[!UICONTROL プロパティ...]**」を選択します。

   ![](assets/s_ncs_user_seedlist_template_folder.png)

1. 「**[!UICONTROL 制限]**」タブをクリックし、フィルター条件 **@isModel = true** を追加します。

   ![](assets/s_ncs_user_seedlist_folder_is_model.png)

   これにより、このフォルダーに格納したアドレスをアドレステンプレートとして使用できるようになります。 これらを配信またはキャンペーンにインポートし、該当する配信およびキャンペーンに特有のニーズに基づいて変更することができます（[シードアドレスの追加](adding-seed-addresses.md)を参照）。
