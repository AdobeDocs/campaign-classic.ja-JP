---
product: campaign
title: Adobe Experience Cloud トリガー用の Developer Console の設定
description: Adobe Experience Cloud トリガー用の Developer Console の設定方法を学ぶ
feature: Triggers
audience: integrations
content-type: reference
index: y
internal: n
snippet: y
exl-id: ab30f697-3022-4a29-bbdb-14ca12ec9c3e
hide: true
hidefromtoc: true
source-git-commit: 8de62db2499449fc9966b6464862748e2514a774
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 100%

---

# Adobe Experience Cloud トリガー用の Developer Console の設定 {#configuring-adobe-io}

<!--
>[!CAUTION]
>
>If you are using an older version of Triggers integration through oAuth authentication, **you need to move to Adobe I/O as described below**. 
>Note that during this move to [!DNL Adobe I/O], some incoming triggers may be lost.
>
>Legacy oAuth authentication mode with Campaign has been retired on **October 20, 2021**. Hosted environments benefit from an extension until **May 25, 2022**. As an on-premise or hybrid customer, contact Adobe Customer Care to extend support to **May 2022**. You must [provide the AppID of the OAuth application](../../integrations/using/configuring-pipeline.md#step-optional) to Adobe.
-->

## 前提条件 {#adobe-io-prerequisites}

<!--
This integration only applies starting **Campaign Classic 20.2.4 and above, 19.1.8 and Gold Standard 11 releases**.
-->

この実装を開始する前に、以下の点を確認してください。

* 有効な&#x200B;**組織識別子**：組織 ID は、Adobe Experience Cloud 内の一意の識別子で、VisitorID サービスや IMS シングルサインオン（SSO）などに使用されます。[詳細情報](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja)
* 組織への&#x200B;**開発者のアクセス**。組織のシステム管理者は、**単一の製品プロファイルへの開発者の追加**&#x200B;の手順（詳しくは[このページ](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html)を参照）に従って、トリガーに関連する Adobe Analytics 製品の `Analytics - {tenantID}` 製品プロファイルに対するアクセス権を開発者に提供する必要があります。

## 手順 1：OAuth プロジェクトを作成／更新 {#creating-adobe-io-project}

>[!AVAILABILITY]
>
> サービスアカウント（JWT）資格情報はアドビによって廃止され、アドビのソリューションおよびアプリとの Campaign 統合では、OAuth サーバー間の資格情報に依存する必要があります。</br>
>
> * Campaign とのインバウンド統合を実装している場合は、[このドキュメント](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#_blank)の詳細な説明に従ってテクニカルアカウントを移行する必要があります。既存のサービスアカウント（JWT）資格情報は、2025年1月27日（PT）まで引き続き機能します。</br>
>
> * Campaign と Analytics 統合や Experience Cloud トリガー統合などのアウトバウンド統合を実装している場合は、2025年1月27日（PT）まで引き続き機能します。ただし、この日付までに、Campaign 環境を v7.4.1 にアップグレードし、テクニカルアカウントを OAuth に移行する必要があります。

Adobe Analytics コネクタの設定に進むには、Adobe Developer Console にアクセスして、OAuth サーバー間プロジェクトを作成します。

詳しくは、[こちらのページ](oauth-technical-account.md#oauth-service)を参照してください。

## 手順 2：Adobe Campaign へのプロジェクト資格情報の追加 {#add-credentials-campaign}

[このページ](oauth-technical-account.md#add-credentials)で説明されている手順に従って、OAuth プロジェクト資格情報を Adobe Campaign に追加します。

## 手順 3：パイプラインタグの更新 {#update-pipelined-tag}

[!DNL pipelined] タグを更新するには、設定ファイル（**config-&lt; instance-name >.xml**）で、認証タイプを以下のように Developer Console プロジェクトに更新する必要があります。

```
<pipelined ... authType="imsJwtToken"  ... />
```

次に、`config -reload` を実行し、[!DNL pipelined] を再起動して変更内容を反映させます。
