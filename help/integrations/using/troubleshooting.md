---
product: campaign
title: トラブルシューティング
description: トラブルシューティング
feature: Audiences, People Core Service Integration, Troubleshooting
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
topic-tags: audience-sharing
hide: true
hidefromtoc: true
exl-id: 61bb184e-affa-430c-8571-56e911cd5a3d
source-git-commit: b11185da8236d6100d98eabcc9dc1cf2cffa70af
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 100%

---

# トラブルシューティング{#troubleshooting}



エラーが発生した場合、次の要素が正しく設定されていることを確認してください。

* **外部アカウント**

  **[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;で、次の外部 SFTP アカウントが正しく設定されていることを確認します。この SFTP サーバーは、担当のコンサルタントによって Adobe Experience Cloud で設定されているはずです。

   * **[!UICONTROL importSharedAudience]**：オーディエンスのインポート専用の SFTP アカウント。
   * **[!UICONTROL exportSharedAudience]**：オーディエンスのエクスポート専用の SFTP アカウント。

* **AMC データソース**

  **[!UICONTROL 管理／プラットフォーム／AMC データソース]**&#x200B;で、AMC データソースが正しく設定されていることを確認します。

Experience Cloud Audience 経由でオーディエンスを共有したり、オーディエンスを読み込んだりすると、データの一部が失われることがあります。ID（「訪問者 ID」または「宣言済み ID」）をプロファイルディメンションに紐付けることができたレコードのみが転送されます。Adobe Campaign によって認識されないセグメントからの ID は読み込まれません。
