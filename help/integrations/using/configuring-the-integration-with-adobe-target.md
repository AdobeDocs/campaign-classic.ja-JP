---
title: Adobe Target との統合の設定
seo-title: Adobe Target との統合の設定
description: Adobe Target との統合の設定
seo-description: null
page-status-flag: never-activated
uuid: b9337e92-e4e5-4cba-a559-75db7460d5c5
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-target
discoiquuid: 378d5ff9-88c0-43f1-beb8-454701e9f1d1
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0745b9c9d72538b8573ad18ff4054ecf788905f2

---


# Adobe Target との統合の設定{#configuring-the-integration-with-adobe-target}

## 前提条件 {#prerequisites}

Adobe Campaign と Adobe Target 間の統合を使用するには、次が必要です。

* Adobe Experience Cloud および Adobe Target 組織
* Adobe Campaign との接続を確立するために指定された Adobe Target ローボックス

## Adobe Campaign の設定 {#configuring-adobe-campaign}

Adobe Campaign を設定するには：

1. **[!UICONTROL Adobe Experience Cloud との統合]**&#x200B;標準パッケージをインストールします。統合パッケージのインストール方法は、標準パッケージのインストール方法と同じです。詳しくは、[パッケージのインポート](../../platform/using/working-with-data-packages.md#importing-packages)の節で説明しています。インストールすると、Digital Asset Manager を使用して共有アセットにアクセスすることができます。
1. Adobe Experience Cloud を使用して共有された画像を電子メールで使用するには、IMS（Adobe ID 接続サービス）での接続を有効にします。[IMS](../../integrations/using/about-adobe-id.md) についての節を参照してください。
1. **[!UICONTROL 管理／プラットフォーム／オプション]**&#x200B;で、Adobe Target のサーバーと組織（テナント）オプションを設定します。

   * **[!UICONTROL TNT_EdgeServer]**：統合に使用される Adobe Target のサーバー。このオプションは、デフォルトで選択されています。この値は Adobe Target の&#x200B;**[!UICONTROL ドメインサーバー]**&#x200B;に対応し、値 **/m2** が続きます。例：**tt.omtrdc.net/m2**。
   * **[!UICONTROL TNT_TenantName]**：Adobe Target の組織名。この値は Adobe Target の&#x200B;**[!UICONTROL クライアント]**&#x200B;名に対応します。
   ![](assets/tar_options.png)

