---
product: campaign
title: パスワードを忘れた場合
description: パスワードを忘れた場合
feature: Monitoring, Access Management
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 064eb41f-6685-4ac1-adc5-40f9d5a2f96d
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 15%

---

# パスワードを忘れた場合{#lost-password}



失われたパスワードを変更または復元できます。
次の 2 つのシナリオが考えられます。

* [Adobe Campaignオペレーターによって失われたパスワード](#password-lost-by-campaign-operator)
* [内部パスワードが失われました](#internal-password-lost) （オンプレミス版のお客様のみ）

## Campaign オペレーターによって失われたパスワード {#password-lost-by-campaign-operator}

Adobe Campaignのオペレーターがパスワードを失った場合は、パスワードを変更できます。
これを行うには、次の手順に従います。

1. 管理者権限を持つオペレーター経由で接続します。
1. 演算子を右クリックします。
1. 選択 **[!UICONTROL アクション]** > **[!UICONTROL パスワードをリセット]**.

   ![](assets/operator-passwd.png)

1. オペレーターの新しいパスワードを設定します。 オペレーターが最初の再接続時にパスワードを変更することをお勧めします。

## 内部パスワードが失われました {#internal-password-lost}

>[!NOTE]
>
>この節の説明はオンプレミス版のお客様のみに当てはまります。

内部パスワードが失われた場合は、再初期化する必要があります。
これをおこなうには、次の手順に従います。

1. を編集します。 **/usr/local/neolane/nl6/conf/serverConf.xml** ファイル。

1. 次に移動： **internalPassword** 行。

   ```
   <!-- XTK authentication mode internalPassword : Password of internal account -->
   <xtk internalPassword="myPassword"/>
   ```

1. 引用符で囲まれた文字列を削除します（この場合は次のようにします）。 **myPassword**

   この場合、次の行が表示されます。

   ```
   !-- XTK authentication mode internalPassword : Password of internal account -->
   <xtk internalPassword=""/
   ```

1. 変更を保存し、ファイルを閉じます。

1. 新しいパスワードを設定します。 これをおこなうには、次のコマンドを入力します。

   ```
   nlserver config -internalpassword
   HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   Enter current password.
   Password: (empty)
   Enter the new password.
   Password: 
   Confirmation 
   ```

1. これで、新しいパスワードを使用して、 **内部** モード。
