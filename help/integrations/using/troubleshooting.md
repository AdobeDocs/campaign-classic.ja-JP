---
solution: Campaign Classic
product: campaign
title: トラブルシューティング
description: トラブルシューティング
audience: integrations
content-type: reference
topic-tags: audience-sharing
translation-type: ht
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: ht
source-wordcount: '141'
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
