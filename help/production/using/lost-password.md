---
product: campaign
title: パスワードを忘れた場合
description: パスワードを忘れた場合
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 064eb41f-6685-4ac1-adc5-40f9d5a2f96d
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 7%

---

# パスワードを忘れた場合{#lost-password}

パスワードを変更または復元できます。
次の2つのシナリオが考えられます。

* [Adobe Campaignのオペレーターがパスワードを失った](#password-lost-by-campaign-operator)
* [内部パスワードの紛失](#internal-password-lost) （オンプレミス版のお客様のみ）

## Campaignオペレーター{#password-lost-by-campaign-operator}によってパスワードが失われた

Adobe Campaignのオペレーターがパスワードを失った場合は、パスワードを変更できます。
それには、次の手順に従います。

1. 管理者権限を持つオペレーターを使用して接続します。
1. 演算子を右クリックします。
1. **[!UICONTROL アクション]** > **[!UICONTROL パスワードをリセット]**&#x200B;を選択します。

   ![](assets/operator-passwd.png)

1. オペレーターの新しいパスワードを設定します。 オペレーターが最初の再接続時にパスワードを変更することをお勧めします。

## 内部パスワードが失われました{#internal-password-lost}

>[!NOTE]
>
>この節の説明は、オンプレミス版のお客様のみに当てはまります。

内部パスワードが失われた場合は、再初期化する必要があります。
これをおこなうには、次の手順に従います。

1. **/usr/local/neolane/nl6/conf/serverConf.xml**&#x200B;ファイルを編集します。

1. **internalPassword**&#x200B;行に移動します。

   ```
   <!-- XTK authentication mode internalPassword : Password of internal account -->
   <xtk internalPassword="myPassword"/>
   ```

1. 引用符で囲まれた文字列を削除します（この場合は次のようにします）。**myPassword**

   次の行が得られます。

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

1. これで、新しいパスワードを使用して&#x200B;**内部**&#x200B;モードで接続できます。
