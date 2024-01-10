---
product: campaign
title: Adobe IDを使用してAdobe Campaignに接続
description: Adobe CampaignでのAdobe IMS実装の詳細
feature: Configuration
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
audience: integrations
content-type: reference
topic-tags: connecting-via-an-adobe-id
exl-id: 8dad8fa9-674c-433c-af30-8c6d0aadf525
source-git-commit: 49271e291953483ee14709b26ec053217a336718
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 60%

---

# Adobe ID について {#about-adobe-id}

Adobe Identity Management システム（IMS）は、管理者がアプリケーションやサービスへのユーザーのアクセスを作成および管理するのに役立ちます。各種 Adobe ID の詳細については、[こちらのページ](https://helpx.adobe.com/jp/enterprise/using/identity.html)を参照してください。

Campaign ユーザーは、 [ネイティブユーザー/パスワード認証](../../platform/using/access-management-operators.md). この実装には、次のメリットがあります。

* Experience Cloud のすべてのソリューションに同じ ID を使用できます。
* 様々な統合でAdobe Campaignを使用する場合、接続は維持されます。
* ネイティブのログイン/パスワードよりも、パスワード管理ポリシーの方が安全です。
* Federated ID アカウント（外部の ID プロバイダー）を使用します。

<!--
>[!IMPORTANT]
>
>If you are connecting to Campaign through Adobe Identity Service (IMS), you need to upgrade to the latest build to be able to connect to Campaign after **June 30, 2021**. This upgrade is mandatory for both Campaign server and client console. 
>
>Depending on your current version, you must upgrade to one of the following releases: 
>
> * [Campaign [!DNL Gold Standard] 11](../../rn/using/gold-standard.md)
> * [Campaign 21.1.4](../../rn/using/latest-release.md)
>
>[Learn more about IMS updates](../../technotes/using/ims-updates.md)
-->

## その他のリソース

| 便利なページ | その他のリソース |
|---|---|
| [IMS の設定](../../integrations/using/configuring-ims.md) | [Experience Cloud に関する FAQ](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/organizations.html?lang=ja) |
| [IMS の実装](../../integrations/using/implementing-ims.md) | [アクセス管理](../../platform/using/access-management.md) |
| [IMS のトラブルシューティング](../../integrations/using/ims-troubleshooting.md) | [キャンペーンパッケージのインストール](../../installation/using/installing-campaign-standard-packages.md) |
