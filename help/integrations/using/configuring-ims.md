---
product: campaign
title: IMS の設定
description: Adobe ID 経由の接続方法を説明します
feature: Configuration
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: integrations
content-type: reference
topic-tags: connecting-via-an-adobe-id
exl-id: b70ca220-1c81-4b23-b07a-a2cd694877fe
feature_v2: []
subfeature_v2:
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
  - id: df0d6518-6f49-46e2-b46e-3bcc513f553f
  - id: eb007b6d-6e57-46ab-9485-3f24d6102304
  - id: b1fd1501-3105-4d6b-b4d4-9af53126df75
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 361
ht-degree: 100%

---

# IMS の設定{#configuring-ims}

>[!IMPORTANT]
>
>Campaign のホストサービスまたは Managed Services ユーザーの場合、Adobe IMS の実装はアドビが所有します。以下の手順は、オンプレミス環境およびハイブリッド環境のお客様にのみ適用されます。
> Adobe IMS の実装は、アドビの技術管理者のみが実行する必要があります。実装プロセスを開始するには、アドビ担当者にお問い合わせください。

## 前提条件 {#prerequisites}

* Adobe Experience Cloud の組織名と組織 ID が必要です。 組織 ID を見つけるには、[このページ](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja){_blank}を参照してください。
* Experience Cloud にユーザーを追加する必要があります。 詳しくは、[このページ](https://experienceleague.adobe.com/docs/core-services/interface/administration/admin-getting-started.html?lang=ja){_blank}を参照してください。

>[!NOTE]
>
>Adobe Campaign と同期される Adobe Experience Cloud グループにユーザーがリンクされているか確認してください。 [詳細情報](#configuring-the-external-account)。

## コンソールの更新 {#updating-the-console}

この機能を使用するには、クライアントコンソールの最新バージョンを必ずインストールする必要があります。

## パッケージのインストール {#installing-the-package}

**[!UICONTROL Adobe Experience Cloud との統合]**&#x200B;のビルトインパッケージをインストールする必要があります。 統合パッケージのインストール方法は、標準パッケージのインストール方法と同じです。詳しくは、[このページ](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

![](assets/ims_6.png)

## 外部アカウントの設定 {#configuring-the-external-account}

**Adobe Experience Cloud** 外部アカウントを、**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;で設定します。

![](assets/ims_5.png)

次の情報を入力します。

* 使用する IMS サーバーの接続情報（ID および Secret）。 この情報は、アドビカスタマーケアチームによって提供されます。 詳しくは、[Adobe Experience Cloud 管理者向け FAQ](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/faq.html?lang=ja) を参照してください。

  **[!UICONTROL コールバックサーバー]**&#x200B;アドレスは **https** で指定する必要があります。 このフィールドは、お客様の Adobe Campaign インスタンスのアクセス URL に対応します。

* 組織 ID - 組織 ID を見つけるには、[このページ](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja){_blank}を参照してください。

* 関連付けマスク：このフィールドでは、Enterprise Dashboard の設定名を Adobe Campaign のグループと同期させる構文を定義することができます。 「Campaign - tenant_id - (.&#42;)」という構文を使用すると、Adobe Campaign で作成したセキュリティグループが Enterprise Dashboard の設定名「Campaign - tenant_id - internal_name」にリンクされます。

* Adobe Experience Cloud 接続情報。Adobe Experience Cloud テナントの名前です。
