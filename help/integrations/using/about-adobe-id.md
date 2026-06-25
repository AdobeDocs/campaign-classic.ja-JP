---
product: campaign
title: Adobe ID を使用して Adobe Campaign に接続
description: Adobe Campaign での Adobe IMS 実装について詳しく説明します
feature: Configuration
audience: integrations
content-type: reference
topic-tags: connecting-via-an-adobe-id
exl-id: 8dad8fa9-674c-433c-af30-8c6d0aadf525
TQID: https://experienceleague.adobe.com/i9Ncu86b4PZaAY6yROb-6kUdOgjbYNV1nE0Rj-Jb-OY
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
subfeature_v2:
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
  - id: df0d6518-6f49-46e2-b46e-3bcc513f553f
  - id: eb007b6d-6e57-46ab-9485-3f24d6102304
  - id: b1fd1501-3105-4d6b-b4d4-9af53126df75
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 194
ht-degree: 100%

---

# Adobe ID について {#about-adobe-id}

Adobe Identity Management システム（IMS）は、管理者がアプリケーションやサービスへのユーザーのアクセスを作成および管理するのに役立ちます。 各種 Adobe ID の詳細については、[こちらのページ](https://helpx.adobe.com/jp/enterprise/using/identity.html)を参照してください。

Campaign ユーザーは、[ネイティブのユーザー／パスワード認証](../../platform/using/access-management-operators.md)の代わりに、Adobe ID を使用して Adobe Campaign コンソールに接続できます。 この実装には、次のメリットがあります。

* Experience Cloud のすべてのソリューションに同じ ID を使用できます。
* Adobe Campaign を様々な統合で使用する場合にも、接続は保持されます。
* ネイティブのログイン／パスワードより安全なパスワード管理ポリシーです。
* Federated ID アカウント（外部の ID プロバイダー）の使用。

>[!IMPORTANT]
>
> Campaign v8 では、ユーザー／パスワードを使用した接続（別名ネイティブ認証）は許可されません。 **アドビでは、Campaign v8 にスムーズに移行できるように、Campaign v7.3.5 でこの移行を実行することをお勧めします。**
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
