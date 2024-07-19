---
product: campaign
title: Adobe ID を使用して Adobe Campaign に接続
description: Adobe Campaign での Adobe IMS 実装について詳しく説明します
feature: Configuration
audience: integrations
content-type: reference
topic-tags: connecting-via-an-adobe-id
exl-id: 8dad8fa9-674c-433c-af30-8c6d0aadf525
source-git-commit: ffab91fc9fa7e60973fdda930239f5836671a341
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 100%

---

# Adobe ID について {#about-adobe-id}

Adobe Identity Management システム（IMS）は、管理者がアプリケーションやサービスへのユーザーのアクセスを作成および管理するのに役立ちます。各種 Adobe ID の詳細については、[こちらのページ](https://helpx.adobe.com/jp/enterprise/using/identity.html)を参照してください。

Campaign ユーザーは、[ネイティブのユーザー／パスワード認証](../../platform/using/access-management-operators.md)の代わりに、Adobe ID を使用して Adobe Campaign コンソールに接続できます。この実装には、次のメリットがあります。

* Experience Cloud のすべてのソリューションに同じ ID を使用できます。
* Adobe Campaign を様々な統合で使用する場合にも、接続は保持されます。
* ネイティブのログイン／パスワードより安全なパスワード管理ポリシーです。
* Federated ID アカウント（外部の ID プロバイダー）の使用。

>[!IMPORTANT]
>
> Campaign v8 では、ユーザー／パスワードを使用した接続（別名ネイティブ認証）は許可されません。**アドビでは、Campaign v8 にスムーズに移行できるように、Campaign v7.3.5 でこの移行を実行することをお勧めします。**
>
>Adobe IMS に移行する方法については、[この節](../../technotes/using/ac-ims.md)を参照してください。
>


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
| [IMS の設定](../../integrations/using/configuring-ims.md) | [Experience Cloud に関する FAQ](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/faq.html?lang=ja) |
| [IMS の実装](../../integrations/using/implementing-ims.md) | [アクセス管理](../../platform/using/access-management.md) |
| [IMS のトラブルシューティング](../../integrations/using/ims-troubleshooting.md) | [キャンペーンパッケージのインストール](../../installation/using/installing-campaign-standard-packages.md) |
