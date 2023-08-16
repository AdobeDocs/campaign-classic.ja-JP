---
product: campaign
title: IMS の設定
description: Adobe ID 経由の接続方法を説明します
feature: Configuration
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
topic-tags: connecting-via-an-adobe-id
exl-id: b70ca220-1c81-4b23-b07a-a2cd694877fe
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 100%

---

# IMS の設定{#configuring-ims}



>[!IMPORTANT]
>
>Adobe IMS の実装は必ずアドビの技術管理者がおこないます。実装プロセスを開始するには、アドビの担当者にお問い合わせください。

## 前提条件 {#prerequisites}

IMSとの統合を使用するには：

* Adobe Experience Cloud の組織名と組織 ID が必要です。 組織 ID を見つけるには、[このページ](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja){_blank}を参照してください。
* Experience Cloud にユーザーを追加する必要があります。詳しくは、[このページ](https://experienceleague.adobe.com/docs/core-services/interface/administration/admin-getting-started.html?lang=ja){_blank}を参照してください。

>[!NOTE]
>
>Adobe Campaign と同期される Adobe Experience Cloud グループにユーザーがリンクされているか確認してください。[詳細情報](#configuring-the-external-account)。

## コンソールの更新 {#updating-the-console}

この機能を使用するには、コンソールの最新バージョンを必ずインストールする必要があります。

## パッケージのインストール {#installing-the-package}

**[!UICONTROL Adobe Experience Cloud との統合]**&#x200B;のビルトインパッケージをインストールする必要があります。統合パッケージのインストール方法は、標準パッケージのインストール方法と同じです。詳しくは、[このページ](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

![](assets/ims_6.png)

## 外部アカウントの設定 {#configuring-the-external-account}

**Adobe Experience Cloud** 外部アカウントを、**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;で設定します。

>[!CAUTION]
>
>この設定は技術管理者がおこなってください。

![](assets/ims_5.png)

次の情報を入力します。

* 使用する IMS サーバーの接続情報（ID および Secret）。この情報は、Adobe サポートから提供されます。詳しくは、[Adobe Experience Cloud 管理者向け FAQ](https://experienceleague.adobe.com/docs/core-services/interface/manage-users-and-products/faq.html?lang=ja) を参照してください。

  **[!UICONTROL コールバックサーバー]**&#x200B;アドレスは **https** で指定する必要があります。このフィールドは、お客様の Adobe Campaign インスタンスのアクセス URL に対応します。

* 組織 ID：組織 ID を見つけるには、[このページ](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja){_blank}を参照してください。
* 関連付けマスク：このフィールドでは、Enterprise Dashboard の設定名を Adobe Campaign のグループと同期させる構文を定義することができます。「Campaign - tenant_id - (.&#42;)」という構文を使用すると、Adobe Campaign で作成したセキュリティグループが Enterprise Dashboard の設定名「Campaign - tenant_id - internal_name」にリンクされます。

  >[!CAUTION]
  >
  >関連付けマスクは、Adobe ID を使用した接続が正常に機能するために必要です。

* Adobe Experience Cloud 接続情報、特に Adobe Experience Cloud テナント名。
