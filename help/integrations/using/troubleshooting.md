---
title: トラブルシューティング
seo-title: トラブルシューティング
description: トラブルシューティング
seo-description: null
page-status-flag: never-activated
uuid: fb51ad18-221b-4058-b206-ca2ca045c507
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: audience-sharing
discoiquuid: f3ff8c8e-22b0-4d61-9f26-11f5ca3bc0be
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0745b9c9d72538b8573ad18ff4054ecf788905f2

---


# トラブルシューティング{#troubleshooting}

エラーが発生した場合、次の要素が正しく設定されていることを確認してください。

* **外部アカウント**

   で、以 **[!UICONTROL Administration > Platform > External accounts]**&#x200B;下の外部SFTPアカウントが正しく設定されていることを確認します。 この SFTP サーバーは、担当のコンサルタントによって Adobe Experience Cloud で設定されているはずです。

   * **[!UICONTROL importSharedAudience]** :オーディエンスのインポート専用のSFTPアカウント。
   * **[!UICONTROL exportSharedAudience]** :オーディエンスの書き出し専用のSFTPアカウント。

* **AMC データソース**

   で、AMC **[!UICONTROL Administration > Platform > AMC Data sources]**&#x200B;データソースが正しく設定されていることを確認します。

People コアサービス経由でオーディエンスを共有したり、オーディエンスをインポートしたりすると、データが一部失われることがあります。ID（「訪問者 ID」または「宣言済み ID」）をプロファイルディメンションに紐付けることができたレコードだけが転送されます。Adobe Campaign によって認識されない People コアサービスセグメントからの ID はインポートされません。
