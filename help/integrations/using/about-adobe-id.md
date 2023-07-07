---
product: campaign
title: Campaign での Adobe ID の使用
description: Adobe IMS 統合の詳細
badge-v7: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7"
badge-v8: label="v8" type="Positive" tooltip="Also applies to Campaign v8"
audience: integrations
content-type: reference
topic-tags: connecting-via-an-adobe-id
exl-id: 8dad8fa9-674c-433c-af30-8c6d0aadf525
source-git-commit: 2bbcfbff3ce77501fb36457dc823c0ef86550bec
workflow-type: ht
source-wordcount: '190'
ht-degree: 100%

---

# Adobe ID について{#about-adobe-id}

Adobe Identity Management システム（IMS）は、管理者がアプリケーションやサービスへのユーザーのアクセスを作成および管理するのに役立ちます。各種 Adobe ID の詳細については、[こちらのページ](https://helpx.adobe.com/jp/enterprise/using/identity.html)を参照してください。

Campaign ユーザーは、Adobe ID を使用して Adobe Campaign コンソールに接続できます。統合には次のメリットがあります。

* Experience Cloud のすべてのソリューションに同じ ID を使用できます。
* Adobe Campaign で異なる統合を使用する場合にも、接続が記憶されます。
* パスワード管理ポリシーをよりセキュアにできます。
* Federated ID アカウント（外部の ID プロバイダー）を使用します。


>[!IMPORTANT]
>
>Adobe ID サービス（IMS）を通じて Campaign に接続している場合、**2021 年 6 月 30 日**&#x200B;以降も Campaign に接続できるようにするには、最新のビルドにアップグレードする必要があります。 このアップグレードは、Campaign サーバーとクライアントコンソールの両方で必須です。 
>
>現在のバージョンに応じて、次のリリースのいずれかにアップグレードする必要があります。
>
> * [Campaign [!DNL Gold Standard] 11](../../rn/using/gold-standard.md)
> * [Campaign 21.1.4](../../rn/using/latest-release.md)
>
>[ IMS 更新の詳細を説明します](../../technotes/using/ims-updates.md)。


## その他のリソース

| 便利なページ | その他のリソース |
|---|---|
| [IMS の設定](../../integrations/using/configuring-ims.md) | [Experience Cloud に関する FAQ](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/organizations.html?lang=ja) |
| [IMS の実装](../../integrations/using/implementing-ims.md) | [アクセス管理](../../platform/using/access-management.md) |
| [IMS のトラブルシューティング](../../integrations/using/ims-troubleshooting.md) | [キャンペーンパッケージのインストール](../../installation/using/installing-campaign-standard-packages.md) |
