---
product: campaign
title: オペレーターグループの作成と管理
description: オペレーターグループにアクセス権を付与する方法を説明します。
badge: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: Access Management, Permissions
role: User, Admin
level: Beginner
exl-id: d5833d3d-e8ef-4f2b-8084-4ba825c79525
TQID: https://experienceleague.adobe.com/FZhH7zDL3g3tG8Ar40XJQWE-2O9Rs5-KD-NliQ6wH3M
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
  - id: afa4204e-6d08-4e29-bc35-26aafb656d48
subfeature_v2:
  - id: f529d0bd-1401-4c88-9833-43228cc1d40f
  - id: d6330382-c886-4f7a-a4f7-74e3f36c0d9c
  - id: f5293531-9312-4099-bfa3-9e67df6a8750
  - id: efa38731-2723-4334-8d8b-a778af834835
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 620
ht-degree: 100%

---

# オペレーターグループの作成と管理 {#operator-groups}

>[!NOTE]
>
>これらの手順は、**従来のネイティブ認証**&#x200B;を使用して Campaign に接続するオペレーターにのみ適用されます。 Campaign Classic v7.3.1 以降、すべてのオペレーターは、[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}を使用して Campaign に接続する必要があります。 [詳細情報](../../technotes/using/migrate-users-to-ims.md)
>
>Adobe ID を使用して Campaign に接続する場合は、次のセクションは適用されなくなります。 Adobe IMS を使用して権限を設定する方法については、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/admin/permissions/gs-permissions.html?lang=ja){target="_blank"}を参照してください。

オペレーターグループは、ツリーの&#x200B;**[!UICONTROL 管理／アクセス管理／オペレーターグループ]**&#x200B;ノードを使用して作成します。

## 新しいオペレーターグループの作成 {#creating-a-new-operator-group}

新しいオペレーターグループを作成するには、以下の手順を実行します。

1. グループリストの右側にある「**[!UICONTROL 新規]**」ボタンをクリックするか、リストを右クリックして「**[!UICONTROL 新規]**」を選択します。
1. セクション下部のウィンドウにある「**[!UICONTROL 一般]**」タブで、このグループの名前と説明を、該当するフィールドにそれぞれ入力します。

   ![](assets/s_ncs_user_create_operator_gp.png)

1. 「**[!UICONTROL コンテンツ]**」タブをクリックし、このグループの権限を定義します。
1. **[!UICONTROL 追加]**&#x200B;ボタンをクリックし、グループに付与する権限または関連付けるオペレーターを選択します。
1. 「**[!UICONTROL フォルダー]**」フィールドのドロップダウンリストまたは右側にあるフォルダーをクリックし、このグループに付与する権限または関連付けるオペレーターを指定します。
1. 追加するアクセス権またはオペレーターを選択し、「**[!UICONTROL OK]**」をクリックして確定します。

   ![](assets/s_ncs_user_create_operator_gp03.png)

   他のアクセス権やオペレーターを追加するには、この操作を繰り返します。

1. 「**[!UICONTROL 保存]**」ボタンをクリックして、グループをリストに追加します。

## デフォルトのグループ {#default-groups}

以下のオペレーターグループがデフォルトで用意されています。

1. **[!UICONTROL 管理者]**

   このグループのオペレーターは、インスタンスに対して完全なアクセス権を持ちます。 管理者は、インターフェイスの技術面において最高レベルのアクセス権限を持つユーザーです。 このユーザーは&#x200B;**[!UICONTROL 管理者]**&#x200B;の役割を持ち、プラットフォームがすべて設定されていることを確認します。

   このグループには以下のネームド権限が設定されています。

   * **[!UICONTROL 管理者]**：ワークフロー、配信、スクリプトなどの任意のオブジェクトの実行／作成／編集／削除する権限。

1. **[!UICONTROL 配信オペレーター]**

   このグループのオペレーターは、配信の管理を担当します。配信の作成と準備に必要とされる主なリソース（キャンペーンタイポロジ、配信マッピング、デフォルトテンプレート、パーソナライゼーションブロックなど）にアクセスできます。

   このグループには以下のネームド権限が設定されています。

   * **[!UICONTROL 配信を準備]**：配信分析を作成、編集および開始する権限。
   * **[!UICONTROL 配信を開始]**：分析済みの配信を承認する権限。

1. **[!UICONTROL キャンペーンマネージャー]**

   このグループのオペレーターは、マーケティングキャンペーンを管理でき、キャンペーンにリンクされたオブジェクト（プラン、プログラム、ワークフロー、予算など）にアクセスできます。）**[!UICONTROL Campaign]**（オプションの Adobe Campaign モジュール）のフレームワーク内

   このグループには以下のネームド権限が設定されています。

   * **[!UICONTROL フォルダーを挿入]**：Adobe Campaign ツリーにフォルダーを挿入する権限（関係する分岐に対して編集権限を持っていることが前提）。
   * **[!UICONTROL ワークフロー]**：ワークフローを使用する権限。

   >[!NOTE]
   >
   >このグループのオペレーターに配信開始の権利は付与されません。

1. **[!UICONTROL コンテンツ寄稿者]**

   このグループのオペレーターは、**[!UICONTROL コンテンツ管理]**（Adobe Campaign オプションモジュール）のフレームワーク内でコンテンツフォルダーにアクセスできます。 このグループによってオペレーターに付与される権利はありません。

1. **[!UICONTROL レポートへのアクセス]**

   このグループは、特定のオペレーターに対してキャンペーンダッシュボードのレポート、スケジュール、フォーラムの各アイコンを有効にする外部オペレーター向けです。

1. **[!UICONTROL ワークフローの実行]**

   このグループのオペレーターには、キャンペーンとは関係がないワークフローを管理する権利が付与されます。

1. **[!UICONTROL ワークフロースーパーバイザー]**

   このグループのオペレーターには、キャンペーンワークフローに関するアラートが発生するとメール通知が送付されます。

1. ローカル管理、中央管理

   このグループのオペレーターは&#x200B;**[!UICONTROL 分散型マーケティング]**（Adobe Campaign オプションモジュール）を使用できます。

1. **[!UICONTROL オファーマネージャー]**

   このグループのオペレーターは、オファーを作成および管理できます。詳しくは、この[ページ](../../interaction/using/operator-profiles.md)を参照してください。
このグループには、次のネームド権限が含まれています。

   * **[!UICONTROL フォルダーを挿入]**：Adobe Campaign ツリーにフォルダーを挿入する権限（関係する分岐に対して編集権限を持っていることが前提）。
   * **[!UICONTROL フォルダーを編集]**：内部名、ラベル、関連する画像、サブフォルダーの順序など、フォルダーのプロパティを変更する権利。
