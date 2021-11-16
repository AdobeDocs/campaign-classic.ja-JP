---
product: campaign
title: Adobe Target との統合の設定
description: Adobe Target との統合の設定
audience: integrations
content-type: reference
topic-tags: adobe-target
exl-id: ae8c680f-52a6-4d00-91cd-44d1c3807546
source-git-commit: b6e24c63ece12f25b7dafe3fede9e38b3aab2427
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 71%

---

# Adobe Target との統合の設定{#configuring-the-integration-with-adobe-target}

![](../../assets/common.svg)


>[!CAUTION]
>
> ホスト型またはハイブリッド型の顧客は、この統合を設定するには、Adobe担当者にお問い合わせください。 以下の手順はオンプレミス版のお客様にのみ適用されます。

## 前提条件 {#prerequisites}

Adobe Campaign と Adobe Target 間の統合を使用するには、次が必要です。

* Adobe Experience Cloud および Adobe Target 組織
* Adobe Campaign との接続を確立するために指定された Adobe Target ローボックス

## Adobe Campaign の設定 {#configuring-adobe-campaign}

Adobe Campaign を設定するには：

1. のインストール **[!UICONTROL Adobe Experience Cloudとの統合]** 組み込みパッケージ。 [詳細情報](../../platform/using/working-with-data-packages.md#importing-packages)

   このパッケージでは、Digital Asset Manager を使用して共有アセットにアクセスできます。

1. Adobe Experience Cloud を使用して共有された画像を電子メールで使用するには、IMS（Adobe ID 接続サービス）での接続を有効にします。[詳細情報](../../integrations/using/about-adobe-id.md)
1. 参照先 **[!UICONTROL 管理/プラットフォーム/オプション]** Adobe Targetのサーバーと組織（テナント）オプションを設定するには：

   ![](assets/tar_options.png)

   * **[!UICONTROL TNT_EdgeServer]**：統合に使用される Adobe Target のサーバー。このオプションは、デフォルトで選択されています。この値は Adobe Target の&#x200B;**[!UICONTROL ドメインサーバー]**&#x200B;に対応し、値 **/m2** が続きます。例：**tt.omtrdc.net/m2**。
   * **[!UICONTROL TNT_TenantName]**：Adobe Target の組織名。この値は Adobe Target の&#x200B;**[!UICONTROL クライアント]**&#x200B;名に対応します。


>[!CAUTION]
>
>ハイブリッドアーキテクチャとホストアーキテクチャの場合、これらのオプションは、[ミッドソーシングサーバー](../../installation/using/mid-sourcing-server.md)と[実行インスタンス](../../message-center/using/configuring-instances.md#execution-instance)を含むすべてのサーバーで設定する必要があります。