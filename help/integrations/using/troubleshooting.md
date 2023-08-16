---
product: campaign
title: トラブルシューティング
description: トラブルシューティング
feature: Audiences, People Core Service Integration, Troubleshooting
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
topic-tags: audience-sharing
exl-id: 61bb184e-affa-430c-8571-56e911cd5a3d
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '153'
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

People コアサービス経由でオーディエンスを共有したり、オーディエンスをインポートしたりすると、データが一部失われることがあります。ID（「訪問者 ID」または「宣言済み ID」）をプロファイルディメンションに紐付けることができたレコードだけが転送されます。Adobe Campaign によって認識されない People コアサービスセグメントからの ID はインポートされません。
