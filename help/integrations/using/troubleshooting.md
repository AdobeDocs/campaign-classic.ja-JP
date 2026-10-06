---
product: campaign
title: トラブルシューティング
description: トラブルシューティング
feature: Audiences, People Core Service Integration, Troubleshooting
badge-v8: label="Also applies to v8" type="Positive" tooltip="Also applies to Campaign v8"
audience: integrations
content-type: reference
topic-tags: audience-sharing
hide: true
exl-id: 61bb184e-affa-430c-8571-56e911cd5a3d
TQID: 'https://experienceleague.adobe.com/4de9cxyepP-REa2OTWniBFWInphApeUM79sZuFGcynI'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
    internal-label: Integrations
  - id: afa4204e-6d08-4e29-bc35-26aafb656d48
    internal-label: Profiles and audiences
subfeature_v2:
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
    internal-label: Analytics integration
  - id: df0d6518-6f49-46e2-b46e-3bcc513f553f
    internal-label: Experience Manager integration
  - id: eb007b6d-6e57-46ab-9485-3f24d6102304
    internal-label: Experience Platform integration
  - id: b1fd1501-3105-4d6b-b4d4-9af53126df75
    internal-label: Target integration
  - id: d6330382-c886-4f7a-a4f7-74e3f36c0d9c
    internal-label: Audiences
  - id: a8512b64-d668-4084-b4f0-34baa899e306
    internal-label: People Core Service integration
  - id: a39dbcf0-89cb-4765-9bcb-cf9dfbe2875f
    internal-label: Troubleshooting
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 100%
---
# トラブルシューティング{#troubleshooting}



エラーが発生した場合、次の要素が正しく設定されていることを確認してください。

* **外部アカウント**

  **[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;で、次の外部 SFTP アカウントが正しく設定されていることを確認します。 この SFTP サーバーは、担当のコンサルタントによって Adobe Experience Cloud で設定されているはずです。

  * **[!UICONTROL importSharedAudience]**：オーディエンスのインポート専用の SFTP アカウント。
  * **[!UICONTROL exportSharedAudience]**：オーディエンスのエクスポート専用の SFTP アカウント。

* **AMC データソース**

  **[!UICONTROL 管理／プラットフォーム／AMC データソース]**&#x200B;で、AMC データソースが正しく設定されていることを確認します。

Experience Cloud Audience 経由でオーディエンスを共有したり、オーディエンスを読み込んだりすると、データの一部が失われることがあります。 ID（「訪問者 ID」または「宣言済み ID」）をプロファイルディメンションに紐付けることができたレコードのみが転送されます。 Adobe Campaign によって認識されないセグメントからの ID は読み込まれません。
