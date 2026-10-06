---
product: campaign
title: ターゲティングアクティビティについて
description: ターゲティングアクティビティについて
feature: Workflows, Audiences, Targeting Activity
hide: true
exl-id: 5028ad4c-e427-4e78-962d-c5ea54390db5
TQID: 'https://experienceleague.adobe.com/gwDuL3a9gnCKW07SnGjZ113cvwbxmOMIp6-Zy-HveRo'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: a658c786-869b-4194-a780-2594d663adda
    internal-label: Data management
  - id: afa4204e-6d08-4e29-bc35-26aafb656d48
    internal-label: Profiles and audiences
subfeature_v2:
  - id: ee25c34b-ea50-427b-9369-ba0a160f7d70
    internal-label: HeatMap
  - id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22f
    internal-label: Execution activities
  - id: d1110311-2ca4-442b-be37-088a6db845ee
    internal-label: Data Management activities
  - id: fcb46c0f-76e1-48bc-9dd0-fcf9d97526cf
    internal-label: Workflows
  - id: d6330382-c886-4f7a-a4f7-74e3f36c0d9c
    internal-label: Audiences
  - id: ff84ab2f-a7c2-4ced-a3c8-5113f4348d99
    internal-label: Targeting Activity
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 100%
---
# ワークフローでのターゲティングアクティビティ{#about-targeting-activities}



ターゲティングアクティビティは、セットを定義するか、積集合、和集合、除外の各操作を使用して分割または結合することで、1 つまたは複数のターゲットを作成できます。

* **クエリ**：クエリを実行します。 [クエリの作成](query.md#creating-a-query)を参照してください。
* **増分処理クエリ**：クエリを実行し、実行を計画します。 [増分処理クエリ](incremental-query.md)の節を参照してください。
* **リスト読み込み**：リストに含まれているデータを使用します。 [リストのデータを使用：リスト読み込み](../../platform/using/import-export-workflows.md#using-data-from-a-list--read-list)を参照してください。
* **和集合**：複数のアクティビティの結果を 1 つのターゲット内にグループ化します。 [和集合](union.md)の節を参照してください。
* **積集合**：インバウンドアクティビティの結果が同じである母集団のみを抽出します。 [積集合](intersection.md)の節を参照してください。
* **除外**：別のターゲットが 1 つ以上抽出されるメインターゲットに基づいてターゲットを作成します。 [除外](exclusion.md)の節を参照してください。
* **分割**：ターゲットを複数のサブセットに分割します。 [分割](split.md)の節を参照してください。
* **セル**：各種サブセットのビューをデータ列の形式で提供し、これらのサブセットが多数ある場合に操作を容易にします。 詳しくは、[セル](cells.md)の節を参照してください。
* **オファー（セル別）**：各オファーを、母集団の各サブセットとリンクします。 [オファー（セル別）](offers-by-cell.md)の節を参照してください。
* **調査の回答**：調査中に収集した情報を取得します。 詳しくは、[この節](../../surveys/using/getting-started-with-surveys.md)を参照してください。
* **配信の概要**：配信の概要を追加できます。 [配信の概要](../../workflow/using/delivery-outline.md)の節を参照してください。
* **エンリッチメント**：ワークテーブルまたはワークフローに列を追加します。 [エンリッチメント](../../workflow/using/enrichment.md)の節を参照してください。
* **スキーマ編集**：データを変換、標準化します。必要に応じて、データのエンリッチメントもおこないます。 詳しくは、[スキーマ編集](../../workflow/using/edit-schema.md)の節を参照してください。
* **オファーエンジン**：ワークフロー内で、インタラクションオファーエンジンを呼び出します。 [オファーエンジン](../../workflow/using/offer-engine.md)の節を参照してください。
* **重複排除**：インバウンドアクティビティから重複を排除します。 [重複排除](../../workflow/using/deduplication.md)の節を参照してください。
* **ディメンションを変更**：ワークフローの構築サイクル中にターゲティングディメンションを変更します。 [ディメンションを変更](../../workflow/using/change-dimension.md)の節を参照してください。
* **購読サービス**：情報サービスに対するターゲットの購読と購読解除を管理します。 [購読サービス](../../workflow/using/subscription-services.md)の節を参照してください。
* **リストの更新**：インバウンドアクティビティの結果をリストに記録します。 [リストの更新](../../workflow/using/list-update.md)の節を参照してください。
* **データを更新**：データベース内のデータを大量に更新します。 [データを更新](../../workflow/using/update-data.md)の節を参照してください。
* **CRM コネクタ**：Adobe Campaign と CRM の間の同期を設定します。 [CRM コネクタ](../../workflow/using/crm-connector.md)の節を参照してください。
* **[!UICONTROL データソースを変更]**：ワークフロー&#x200B;**[!UICONTROL 作業用テーブル]**&#x200B;のデータソースを変更できます。 これにより、FDA、FFDA、ローカルデータベースなど、様々なデータソースにわたって、より柔軟にデータを管理できます。 [CRM コネクタ](../../workflow/using/change-data-source.md)の節を参照してください。
