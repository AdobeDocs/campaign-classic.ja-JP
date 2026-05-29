---
product: campaign
title: パスワードを忘れた場合
description: パスワードを忘れた場合
feature: Monitoring, Access Management
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 064eb41f-6685-4ac1-adc5-40f9d5a2f96d
TQID: https://experienceleague.adobe.com/MaAtheK2WnozPDuEO-qPq2l9u-AOGj5aGu2TgKslgLc
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
feature_v2: []
subfeature_v2: id: c03a11ff-bdf9-4e5b-b279-f468b4293464id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 250
ht-degree: 22%

---

# パスワードを忘れた場合{#lost-password}

>[!NOTE]
>
>このページは、ネイティブ認証を使用して Campaign に接続するオペレーターにのみ適用されます。

失ったパスワードを変更または復元できます。
考えられるシナリオは2つあります。

* [Adobe Campaign オペレーターがパスワードを失いました](#password-lost-by-campaign-operator)
* [社内パスワードが失われました](#internal-password-lost) （オンプレミスのお客様のみ）

## Campaign オペレーターがパスワードを失いました {#password-lost-by-campaign-operator}

Adobe Campaignの操作者がパスワードを失った場合は、パスワードを変更できます。

>[!NOTE]
>
>この手順は、ネイティブ認証を使用してCampaignに接続するオペレーターにのみ適用されます。 Adobe IMS 認証については、[このドキュメント](https://helpx.adobe.com/ie/manage-account/using/change-or-reset-password.html){target="_blank"}を参照してください。

Campaign パスワードをリセットするには、次の手順に従います。

1. 管理者権限を持つオペレーターを介して接続します。
1. 演算子を右クリックします。
1. **[!UICONTROL アクション]**/**[!UICONTROL パスワードのリセット]**&#x200B;を選択します。

   ![](assets/operator-passwd.png)

1. オペレーターの新しいパスワードを設定します。 最初に再接続するときにパスワードを変更することをお勧めします。

## 内部パスワードが失われました {#internal-password-lost}

>[!NOTE]
>
>このセクションは、オンプレミスのお客様にのみ適用されます。

内部パスワードが失われた場合は、再初期化する必要があります。

これを行うには、次の手順を適用します。

1. **/usr/local/neolane/nl6/conf/serverConf.xml** ファイルを編集します。

1. **internalPassword**&#x200B;行に移動します。

   ```xml
   <!-- XTK authentication mode internalPassword : Password of internal account -->
   <xtk internalPassword="myPassword"/>
   ```

1. 引用符で囲んだ文字列（この場合は`myPassword`）を削除します。 次の行が表示されます。

   ```xml
   <!-- XTK authentication mode internalPassword : Password of internal account -->
   <xtk internalPassword=""/>
   ```

1. 変更を保存してファイルを閉じます。

1. `nlserver` プロセスを停止します。

1. 新しいパスワードを設定します。 これを行うには、次のコマンドを入力します。

   ```javascript
   nlserver config -internalpassword
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   Enter current password.
   Password: (empty)
   Enter the new password.
   Password: 
   Confirmation 
   ```

1. `nlserver` プロセスを開始します。

1. 新しいパスワードを使用して、**内部** モードで接続できるようになりました。
