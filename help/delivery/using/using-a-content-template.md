---
title: コンテンツテンプレートの使用
seo-title: コンテンツテンプレートの使用
description: コンテンツテンプレートの使用
seo-description: null
page-status-flag: never-activated
uuid: 893b9711-593f-4865-b61a-ef0fede9a2b0
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: content-management
discoiquuid: 48f491b7-bf7b-457f-9cf2-db2bbf4eceea
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# コンテンツテンプレートの使用{#using-a-content-template}

## コンテンツテンプレートについて {#about-content-templates}

コンテンツテンプレートは、配信内で直接参照および使用できます。コンテンツ管 [理を使用した配信の作成を参照](#creating-a-delivery-via-content-management)

コンテンツインスタンスの作成にも使用できます。作成後は、これらのインスタンスを配信する準備が整います(コンテンツインスタンスの配信を参照 [)。または、書き出しの準備が整っているか](#delivering-a-content-instance)(コンテンツイン [スタンスの作成を参照](#creating-a-content-instance))。

## コンテンツ管理からの配信の作成 {#creating-a-delivery-via-content-management}

配信内のコンテンツテンプレートの入力フィールドを使用してコンテンツを作成することができます。配信コンテンツを定義するためのタブが配信ウィザードに追加されます。

![](assets/s_ncs_content_deliver_a_content.png)

選択済みの設定に基づいて、レイアウトが自動的に適用されます。To view it, click the **[!UICONTROL HTML preview]** (or **[!UICONTROL Text preview]** ) and select a recipient to test personalization elements.

![](assets/s_ncs_content_deliver_a_content_html.png)

この詳細については、完全な実装例を参照してください。配信ウ [ィザードでのコンテンツの作成](../../delivery/using/use-case--creating-content-management.md#creating-content-in-the-delivery-wizard)。

## コンテンツインスタンスの作成 {#creating-a-content-instance}

Adobe Campaign のツリー内で直接コンテンツを作成して、ワークフローで使用したり、エクスポートしたり、新しい配信に含めたりできます。

次の手順に従います。

1. ツリーのノ **[!UICONTROL Resources > Contents]** ードを選択し、右クリックして「」を選択しま **[!UICONTROL Properties]**&#x200B;す。

   ![](assets/s_ncs_content_folder_properties.png)

1. このフォルダーに対して有効にするパブリッシュテンプレートを選択します。

   ![](assets/s_ncs_content_folder_templates.png)

1. You can now create new content using the **[!UICONTROL New]** button above the content list.

   ![](assets/s_ncs_content_folder_create_a_template.png)

1. フォーム内のフィールドに入力します。

   ![](assets/s_ncs_content_folder_use_a_template.png)

1. Then click the **[!UICONTROL HTML preview]** tab to view the rendering. ここでは、データベースから取得するパーソナライゼーションフィールドは入力されていません。

   ![](assets/s_ncs_content_folder_use_a_template_preview.png)

1. 作成されたコンテンツは、使用可能なコンテンツのリストに追加されます。Click the **[!UICONTROL Properties]** link to change its label, status, or view its history.

   ![](assets/s_ncs_content_folder_template_properties.png)

1. コンテンツが承認されたら、必要に応じて、ツールバーの適切なボタンを使用してコンテンツを生成できます。

   ![](assets/s_ncs_content_folder_template_generate.png)

   >[!NOTE]
   >
   >未承認コンテンツの生成を可能にする設定ができます。そのためには、パブリッシュテンプレートの関連オプションを変更します。詳しくは、「テンプレートの作 [成と設定」を参照してください](../../delivery/using/publication-templates.md#creating-and-configuring-the-template)。

   デフォルトでは、HTML コンテンツとテキストコンテンツは、Adobe Campaign インスタンスの&#x200B;**パブリッシュ**&#x200B;フォルダーに生成されます。パブリッシュフォルダーは、**NcmPublishingDir** オプションを使用して変更できます。

## コンテンツインスタンスの配信 {#delivering-a-content-instance}

コンテンツインスタンスを作成して配信するためには、配信テンプレートをこのコンテンツの生成に使用するパブリッシュテンプレートにリンクする必要があります。詳しくは、[配信](../../delivery/using/publication-templates.md#delivery)を参照してください。

さらに、コンテンツストレージフォルダーは、このパブリッシュテンプレートから取得するコンテンツの専用フォルダーにする必要があります（1 つのコンテンツフォルダーで複数のタイプのコンテンツを生成できるようにすると、配信を自動的に生成できません）。

To create the delivery automatically based on the selected content, click the **[!UICONTROL Delivery]** icon and choose the template.

![](assets/s_ncs_content_folder_create_the_delivery.png)

テキストコンテンツと HTML コンテンツが自動的に入力されます。
