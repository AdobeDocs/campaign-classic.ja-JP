---
product: campaign
title: Adobe Target との統合の設定
description: Adobe Target との統合の設定方法を学ぶ
feature: Target Integration
audience: integrations
content-type: reference
topic-tags: adobe-target
exl-id: ae8c680f-52a6-4d00-91cd-44d1c3807546
TQID: https://experienceleague.adobe.com/k6TljRgymSefOITPaogJdR7HOrl1BnnZm9jbkemrcyg
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: c5474392-5419-4296-9e41-f6f4ce4f6e9bid: d5ef99fa-df0c-4153-bf94-105ad0724167
subfeature_v2: id: cbcf4d90-26be-46e2-b16a-aebc529dc41eid: df0d6518-6f49-46e2-b46e-3bcc513f553fid: eb007b6d-6e57-46ab-9485-3f24d6102304id: b1fd1501-3105-4d6b-b4d4-9af53126df75
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 100%

---

# Adobe Target との統合の設定{#configuring-the-integration-with-adobe-target}




>[!CAUTION]
>
> ホスト環境またはハイブリッド環境のお客様は、この統合を設定する場合は、アドビ担当者にお問い合わせください。 以下の手順はオンプレミス環境のお客様にのみ当てはまります。

この統合には以下が必要です。

* Adobe Experience Cloud および Adobe Target 組織
* Adobe Campaign との接続を確立するために指定された Adobe Target ローボックス

Adobe Campaign でこの統合を設定するには、次の手順に従います。

1. **[!UICONTROL Adobe Experience Cloud との統合]**&#x200B;ビルトインのパッケージをインストールします。 [詳細情報](../../platform/using/working-with-data-packages.md#importing-packages)

   このパッケージを使用すると、Digital Asset Manager を介して共有アセットにアクセスできます。

1. Adobe Experience Cloud を介して共有された画像をメールで使用するには、IMS（Adobe ID 接続サービス）を介して接続を有効にします。 [詳細情報](../../integrations/using/about-adobe-id.md)
1. **[!UICONTROL 管理／プラットフォーム／オプション]**&#x200B;を参照して、 Adobe Target のサーバーおよび組織（テナント）オプションを設定します。

   ![](assets/tar_options.png)

   * **[!UICONTROL TNT_EdgeServer]**：統合に使用される Adobe Target のサーバー。 このオプションは、デフォルトで選択されています。 この値は Adobe Target の&#x200B;**[!UICONTROL ドメインサーバー]**&#x200B;に対応し、値 **/m2** が続きます。 例：**tt.omtrdc.net/m2**。
   * **[!UICONTROL TNT_TenantName]**：Adobe Target の組織名。 この値は Adobe Target の&#x200B;**[!UICONTROL クライアント]**&#x200B;名に対応します。


>[!CAUTION]
>
>ハイブリッドアーキテクチャとホストアーキテクチャの場合、これらのオプションは、[ミッドソーシングサーバー](../../installation/using/mid-sourcing-server.md)と[実行インスタンス](../../message-center/using/configuring-instances.md#execution-instance)を含むすべてのサーバーで設定する必要があります。