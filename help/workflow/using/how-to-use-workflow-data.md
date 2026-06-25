---
product: campaign
title: ワークフローデータの使用方法
description: ワークフローデータの使用方法を説明します
feature: Workflows, Data Management
hide: true
exl-id: 5354d608-2fea-45f9-a0aa-11c7e965ab04
TQID: https://experienceleague.adobe.com/xasYSu6WyHC0T6CpKn51bZ5K7WlspJAbB0R45AeXb8M
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
feature_v2: []
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
  - id: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 417
ht-degree: 100%

---

# ワークフローデータの使用方法{#how-to-use-workflow-data}



## データベースの更新 {#updating-the-database}

収集したすべてのデータは、データベースを更新するために、または配信内で使用できます。 例えば、メッセージのコンテンツのパーソナライゼーションを充実させること（メッセージ内に契約件数を含める、過去年間の買い物かごの平均購入額を指定するなど）や、母集団のターゲティングを詳細に行うこと（契約の共有者にメッセージを送る、オンラインサービスの高額契約者上位 1,000 人をターゲットに設定するなど）ができます。このデータは、リストにエクスポートまたはアーカイブできます。

### リスト更新とダイレクト更新 {#lists-and-direct-updates}

Adobe Campaign データベースのデータおよび既存のリストは、2 つの専用アクティビティを使用して更新できます。

* 「**[!UICONTROL リスト更新]**」アクティビティを使用して、データリスト内にワークテーブルを保存できます。

  既存のリストを選択するか、新規リストを作成することができます。 ここでは、名前が自動生成されます（場合によってはレコードフォルダーも）。

  ![](assets/s_user_create_list.png)

  [リストの更新](list-update.md)を参照してください。

* **[!UICONTROL データを更新]**&#x200B;アクティビティでは、データベースのフィールドを一括で更新します。

  詳しくは、[データを更新](update-data.md)を参照してください。

### 購読／購読解除の管理 {#subscription-unsubscription-management}

ワークフローを介した受信者の情報サービスへの購読登録と情報サービスからの購読登録解除については、[購読サービス](subscription-services.md)を参照してください。

## ワークフローを介した送信 {#sending-via-a-workflow}

### 配信アクティビティ {#delivery-activity}

配信アクティビティについて詳しくは、[配信](delivery.md)を参照してください。

### 配信のエンリッチメントとターゲティング {#enriching-and-targeting-deliveries}

コンテンツまたはターゲット母集団の選択のフレームワークをカスタマイズするために、配信はワークフロー内のデータを処理できます。

例えば、ダイレクトメール配信のフレームワーク内では、ワークフロー内で実行されるデータ操作から取り出した追加データを、抽出ファイルに含めることができます。

![](assets/s_advuser_add_data_postal_mail.png)

通常のパーソナライゼーションフィールドに加えて、ワークフローステージからのパーソナライゼーションフィールドを、配信コンテンツに追加できます。 以下の例に示すように、ダイレクトメール配信のフレームワーク内で出力ファイル名を定義するために、ワークフローアクティビティ内で定義された追加データを、配信アシスタント内に保持してアクセスすることができます。

![](assets/s_advuser_using_additional_data.png)

ワークフローテーブル内に含まれるデータは、名前で識別されます。名前は常に、「**targetData**」リンクから構成されます。 詳しくは、[ターゲットデータ](data-life-cycle.md#target-data)を参照してください。

さらに、メール配信のフレームワークでは、パーソナライゼーションフィールドで、ターゲティングワークフローステージで実行されるターゲット式のデータを使用できます。以下に例を示します。

![](assets/s_advuser_add_data_email.png)

セグメントコードがターゲティングアクティビティ内に指定されている場合、それらのコードはワークフローテーブルの特定の列に追加され、パーソナライゼーションフィールドと共に提供されます。 すべてのパーソナライゼーションフィールドを表示するには、パーソナライゼーションボタン経由でアクセス可能な&#x200B;**[!UICONTROL ターゲット式／その他...]**&#x200B;リンクをクリックします。

![](assets/s_advuser_segment_code_select.png)
