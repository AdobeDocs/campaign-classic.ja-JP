---
product: campaign
title: パスワードを忘れた場合
description: パスワードを忘れた場合
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 064eb41f-6685-4ac1-adc5-40f9d5a2f96d
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 7%

---

# パスワードを忘れた場合{#lost-password}

![](../../assets/v7-only.svg)

失われたパスワードを変更または復元できます。
次の 2 つのシナリオが考えられます。

* [Adobe Campaignオペレーターによって失われたパスワード](#password-lost-by-campaign-operator)
* [内部パスワードが失われました](#internal-password-lost) （オンプレミス版のお客様のみ）

## Campaign オペレーターによって失われたパスワード {#password-lost-by-campaign-operator}

Adobe Campaignのオペレーターがパスワードを失った場合は、パスワードを変更できます。
これは、次の手順に従って行います。

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

1. 次に移動： **internalPassword** 行

   ```
   <!-- XTK authentication mode internalPassword : Password of internal account -->
   <xtk internalPassword="myPassword"/>
   ```

1. 引用符で囲まれた文字列を削除します（この場合は次のようにします）。 **myPassword**

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

1. これで、新しいパスワードを使用して、 **内部** モード。
