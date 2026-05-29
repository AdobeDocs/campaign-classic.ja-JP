---
product: campaign
title: Adobe Experience Cloud Triggers について
description: Adobe Experience Cloud Triggers の実装入門
feature: Triggers
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
level: Intermediate, Experienced
exl-id: 0e337620-a49f-4e14-8c67-9279d74736f1
TQID: https://experienceleague.adobe.com/gWgUCcgsqeMw-mzVdhVodcp91lgTCCL7XGWp0f2ItKo
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
subfeature_v2:
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
  - id: df0d6518-6f49-46e2-b46e-3bcc513f553f
  - id: eb007b6d-6e57-46ab-9485-3f24d6102304
  - id: b1fd1501-3105-4d6b-b4d4-9af53126df75
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 392
ht-degree: 95%

---

# Campaign と Experience Cloud トリガーの連携{#about-adobe-experience-triggers}

[!DNL Triggers] は、パイプラインを使用して Adobe Campaign と Adobe Analytics を統合します。 パイプラインは、web サイトからユーザーのアクションまたはトリガーを取得します。 買い物かごの放棄は、トリガーの一例です。 トリガーが Adobe Campaign で処理されて、ほぼリアルタイムでメールが送信されます。

>[!CAUTION]
>
>この機能は、製品の一部としてすぐには利用できません。 この実装については、アドビ担当者／カスタマーケアに依頼することで、 この[ページ](../../integrations/using/configuring-pipeline.md#prerequisites)で詳しく説明されている手順を実行できるようになります。

[!DNL Triggers] は、ユーザーのアクションの後、短時間のうちにマーケティングアクションを実行します。 通常の応答時間は 1 時間未満です。

設定は最小限に抑えられ、サードパーティが関与しないため、より俊敏な統合が可能です。
また、マーケティング活動のパフォーマンスに影響を与えることなく、大量のトラフィックをサポートします。例えば、1時間あたり100万件のトリガーを処理できます。

![](assets/do-not-localize/book.png) [Experience Cloud トリガー](https://experienceleague.adobe.com/docs/experience-cloud/triggers/create.html?lang=ja)を作成し、重要なコンシューマーの行動を特定、定義、監視する方法を説明します。

## [!DNL Triggers] アーキテクチャ {#triggers-architecture}

[!DNL pipelined] プロセスは、Adobe Campaign マーケティングサーバーで常に動作しています。 パイプラインに接続し、イベントを取得してただちに処理します。

![](assets/triggers_2.png)

[!DNL pipelined] プロセスは、認証サービスを使用して Experience Cloud にログインし、秘密鍵を送信します。 認証サービスがトークンを返します。 トークンは、イベント取得時の認証に使用されます。

## 前提条件 {#adobe-io-prerequisites}

この実装を開始する前に、以下の点を確認してください。

* 有効な&#x200B;**組織識別子**：組織 ID は、Adobe Experience Cloud 内の一意の識別子で、VisitorID サービスや IMS シングルサインオン（SSO）などに使用されます。 [詳細情報](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja)
* 組織への&#x200B;**開発者のアクセス**。 組織のシステム管理者は、**単一の製品プロファイルへの開発者の追加**&#x200B;の手順（詳しくは[このページ](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html)を参照）に従って、トリガーに関連する Adobe Analytics 製品の `Analytics - {tenantID}` 製品プロファイルに対するアクセス権を開発者に提供する必要があります。

## 実装手順 {#implement}

Campaign と Experience Cloud のトリガーを実装するには、次の手順に従います。

1. OAuth プロジェクトを作成します。 [詳細情報](oauth-technical-account.md#oauth-service)

1. OAuth プロジェクト資格情報を Adobe Campaign に追加します。 [詳細情報](oauth-technical-account.md#add-credentials)

1. 次のように、設定ファイル **config-&lt;インスタンス名>.xml** で Developer Console プロジェクトの認証タイプを更新します。

   ```
   <pipelined ... authType="imsJwtToken"  ... />
   ```

   次に、`config -reload` を実行し、[!DNL pipelined] を再起動して変更内容を反映させます。

