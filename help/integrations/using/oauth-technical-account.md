---
product: campaign
title: API 用のAdobeテクニカルアカウントの作成と設定
description: AdobeAPI アカウントの作成方法について説明します
role: User, Admin
level: Beginner
source-git-commit: efd09fd71069878a5096bfa3592e6ebbaa9dd4e4
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 16%

---

# Adobeのテクニカルアカウントを作成 {#create-service-account}

サーバー間認証資格情報を使用すると、アプリケーションのサーバーがアプリケーション自体の代わりにアクセストークンを生成し、API 呼び出しを行うことができます。 [詳細情報](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

## 既存の統合の移行 {#migrate-jwt}

Adobeにより、サービスアカウント（JWT）資格情報は非推奨（廃止予定）になっています。 Adobeのソリューションやアプリとの Campaign 統合では、OAuth サーバー間資格情報に依存する必要があります。

2024 年 6 月より前に Campaign とのインバウンドまたはアウトバウンドの統合を実装している場合は、Campaign 環境を v7.4.1 にアップグレードし、詳細に従ってテクニカルアカウントを OAuth に移行する必要があります [このドキュメント](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration){target="_blank"}. 既存のサービスアカウント（JWT）資格情報は、まで引き続き機能します **2025 年 1 月 27 日（Pt）**.

移行が完了したら、の説明に従って、新しい資格情報を Campaign に関連付ける必要があります。 [この節](#add-credentials).

## 新しい統合用の新しい OAuth テクニカルアカウントの作成 {#oauth-service}

新しい統合用の OAuth テクニカルアカウントを作成するには、次の手順に従います。

1. Adobe Developer コンソールにアクセスし、としてログインします **システム管理者** （組織の）。

   管理者ロールについて詳しくは、[このページ](https://helpx.adobe.com/jp/enterprise/using/admin-roles.html)を参照してください。

1. 「**[!UICONTROL 新規プロジェクトを作成]**」をクリックします。

   ![](assets/api-account-1.png)

1. 「**[!UICONTROL プロジェクトに追加]**」をクリックし、「**[!UICONTROL API]**」を選択します。

   ![](assets/api-account-2.png)

1. Campaign と統合する製品を選択し、 **[!UICONTROL 次]**.

1. を選択 **[!UICONTROL OAuth サーバー間]** 認証タイプとして、をクリックします。 **[!UICONTROL 次]**.

   ![](assets/api-account-3.png)

1. 「」を選択します **[!UICONTROL 製品プロファイル]** プロジェクトにリンクします。

   必要に応じて、新しいタグを作成できます。 [詳細情報](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html)

1. 次に、「**[!UICONTROL 設定済み API を保存]**」をクリックします。

   ![](assets/api-account-4.png)

1. プロジェクトの「資格情報」で、次を選択します。 [!DNL OAuth Server-to-Server] 次の情報をコピーします。

   * **[!UICONTROL クライアント ID]**
   * **[!UICONTROL クライアント秘密鍵]**
   * **[!UICONTROL テクニカルアカウント ID]**
   * **[!UICONTROL 組織 ID]**

## Adobe Campaignへの OAuth プロジェクト資格情報の追加 {#add-credentials}

OAuth プロジェクト資格情報をAdobe Campaignに追加するには、次の手順に従います。

1. Adobe Campaign インスタンスがインストールされている各コンテナに SSH 経由でログインします。

1. 次のコマンドをとして実行して、OAuth プロジェクト資格情報をAdobe Campaignに追加します `neolane` ユーザー。 これにより、**[!UICONTROL テクニカルアカウント]**&#x200B;資格情報がインスタンス設定ファイルに挿入されます。

   ```
   nlserver config -instance:<instance_name> -setimsoauth:ims-org-id/client-id/technical-account-id/client-secret
   ```
