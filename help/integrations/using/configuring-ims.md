---
title: IMS の設定
seo-title: IMS の設定
description: IMS の設定
seo-description: null
page-status-flag: never-activated
uuid: b659d29f-2a27-4a7b-b5ca-f44c3271dd4e
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: connecting-via-an-adobe-id
discoiquuid: 279d0548-c876-4d5f-a195-48618bd5e9d1
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# IMS の設定{#configuring-ims}

## 前提条件 {#prerequisites}

IMS との統合を使用するには：

* Adobe Experience Cloud 組織と IMS ID（Adobe Experience Cloud の初回接続時に付与されます）が必要です。
* Experience Cloud にユーザーを追加する必要があります。詳しくは、このページ（[https://marketing.adobe.com/resources/help/ja_JP/mcloud/admin_getting_started.html](https://marketing.adobe.com/resources/help/ja_JP/mcloud/admin_getting_started.html)）を参照してください。

>[!NOTE]
>
>Adobe Campaign と同期される Adobe Experience Cloud グループにユーザーがリンクされているか確認してください。[外部アカウントの設定](#configuring-the-external-account)を参照してください。

## コンソールの更新 {#updating-the-console}

この機能を使用するには、コンソールの最新バージョンを必ずインストールする必要があります。

## パッケージのインストール {#installing-the-package}

**[!UICONTROL Adobe Experience Cloud との統合]** パッケージをインストールする必要があります。統合パッケージのインストール方法は、標準パッケージのインストール方法と同じです。詳しくは、[このページ](../../installation/using/installing-campaign-standard-packages.md)で説明しています。

![](assets/ims_6.png)

## 外部アカウントの設定 {#configuring-the-external-account}

**Adobe Experience Cloud** 外部アカウントを、**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;で設定します。

>[!CAUTION]
>
>この設定は技術管理者がおこなってください。

![](assets/ims_5.png)

次の情報を入力します。

* 使用する IMS サーバーの接続情報（ID および Secret）。この情報は、Adobe サポートから提供されます。詳しくは、[Adobe Experience Cloud 管理者向け FAQ](https://marketing.adobe.com/resources/help/ja_JP/mcloud/faq.html) を参照してください。

   **[!UICONTROL コールバックサーバー]**&#x200B;アドレスは **https** で指定する必要があります。このフィールドは、お客様の Adobe Campaign インスタンスのアクセス URL に対応します。

* IMS 組織 ID：この情報は Experience Cloud（**[!UICONTROL 管理／Experience Cloud 詳細]**）で取得でき、Adobe Experience Cloud への初回接続時に付与されます。
* 関連付けマスク：このフィールドでは、Enterprise Dashboard の設定名を Adobe Campaign のグループと同期させる構文を定義することができます。「Campaign - tenant_id - (.*)」という構文を使用すると、Adobe Campaign で作成したセキュリティグループが Enterprise Dashboard の設定名「Campaign - tenant_id - internal_name」にリンクされます。

   >[!CAUTION]
   >
   >関連付けマスクは、Adobe ID を使用した接続が正常に機能するために必要です。

* Adobe Experience Cloud 接続情報、特に Adobe Experience Cloud テナント名。

