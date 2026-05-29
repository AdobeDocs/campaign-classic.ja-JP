---
product: campaign
title: コンテンツテンプレートの使用
description: コンテンツテンプレートの使用
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Templates
exl-id: e43dd68e-2e95-4367-9029-4622fbcb1759
TQID: https://experienceleague.adobe.com/IPR6JI-v9PMQYSpvAAepSCrY-tRosNuKvO-5Ve-K-BE
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
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
source-wordcount: 450
ht-degree: 100%

---

# コンテンツテンプレートの使用{#using-a-content-template}



## コンテンツテンプレートについて {#about-content-templates}

コンテンツテンプレートは、配信内で直接参照および使用できます。 [コンテンツ管理からの配信の作成](#creating-a-delivery-via-content-management)を参照してください。

コンテンツインスタンスの作成にも使用できます。 コンテンツインスタンスを作成したら、いつでも配信（[コンテンツインスタンスの配信](#delivering-a-content-instance)を参照）またはエクスポート（[コンテンツインスタンスの作成](#creating-a-content-instance)を参照）できます。

## コンテンツ管理による配信の作成 {#creating-a-delivery-via-content-management}

配信内のコンテンツテンプレートの入力フィールドを使用してコンテンツを作成することができます。 配信コンテンツを定義するためのタブが配信アシスタントに追加されます。

![](assets/s_ncs_content_deliver_a_content.png)

選択済みの設定に基づいて、レイアウトが自動的に適用されます。 レイアウトを確認するには、「**[!UICONTROL HTML プレビュー]**」（または「**[!UICONTROL テキストプレビュー]**」）をクリックし、パーソナライゼーション要素をテストする受信者を選択します。

![](assets/s_ncs_content_deliver_a_content_html.png)

詳しくは、完全な実装例、[配信アシスタントでのコンテンツの作成](use-case-creating-content-management.md#creating-content-in-the-delivery-assistant)を参照してください。

## コンテンツインスタンスの作成 {#creating-a-content-instance}

Adobe Campaign のツリー内で直接コンテンツを作成して、ワークフローで使用したり、エクスポートしたり、新しい配信に含めたりできます。

次の手順に従います。

1. ツリーの&#x200B;**[!UICONTROL リソース／コンテンツ]**&#x200B;ノードを選択し、右クリックして「**[!UICONTROL プロパティ]**」を選択します。

   ![](assets/s_ncs_content_folder_properties.png)

1. このフォルダーに対してアクティブにするパブリッシュテンプレートを選択します。

   ![](assets/s_ncs_content_folder_templates.png)

1. コンテンツリストの上の&#x200B;**[!UICONTROL 新規]**&#x200B;ボタンを使用して、新しいコンテンツを作成します。

   ![](assets/s_ncs_content_folder_create_a_template.png)

1. フォーム内のフィールドに入力します。

   ![](assets/s_ncs_content_folder_use_a_template.png)

1. 「**[!UICONTROL HTML プレビュー]**」タブをクリックして、レンダリングを確認します。 ここでは、データベースから取得するパーソナライゼーションフィールドは入力されていません。

   ![](assets/s_ncs_content_folder_use_a_template_preview.png)

1. 作成されたコンテンツは、使用可能なコンテンツのリストに追加されます。 コンテンツのラベルやステータスを変更したり、履歴を確認したりするには、**[!UICONTROL プロパティ]**&#x200B;リンクをクリックします。

   ![](assets/s_ncs_content_folder_template_properties.png)

1. コンテンツが承認されたら、必要に応じて、ツールバーの適切なボタンを使用してコンテンツを生成できます。

   ![](assets/s_ncs_content_folder_template_generate.png)

   >[!NOTE]
   >
   >未承認コンテンツの生成を可能にする設定ができます。 そのためには、パブリッシュテンプレートの関連オプションを変更します。 詳しくは、[パブリッシュテンプレートの作成と設定](publication-templates.md#creating-and-configuring-the-template)を参照してください。

   デフォルトでは、HTML コンテンツとテキストコンテンツは、Adobe Campaign インスタンスの&#x200B;**パブリッシュ**&#x200B;フォルダーに生成されます。 パブリッシュフォルダーは、**NcmPublishingDir** オプションを使用して変更できます。

## コンテンツインスタンスの配信 {#delivering-a-content-instance}

コンテンツインスタンスを作成して配信するためには、配信テンプレートをこのコンテンツの生成に使用するパブリッシュテンプレートにリンクする必要があります。 詳しくは、[配信](publication-templates.md#delivery)を参照してください。

さらに、コンテンツストレージフォルダーは、このパブリッシュテンプレートから取得するコンテンツの専用フォルダーにする必要があります（1 つのコンテンツフォルダーで複数のタイプのコンテンツを生成できるようにすると、配信を自動的に生成できません）。

選択したコンテンツに基づいて配信を自動的に作成するには、**[!UICONTROL 配信]**&#x200B;アイコンをクリックして、テンプレートを選択します。

![](assets/s_ncs_content_folder_create_the_delivery.png)

テキストコンテンツと HTML コンテンツが自動的に入力されます。
