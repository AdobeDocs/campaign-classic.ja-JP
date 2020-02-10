---
title: パスワードが失われました
seo-title: パスワードが失われました
description: パスワードが失われました
seo-description: null
page-status-flag: never-activated
uuid: caac68bf-abdc-45da-9697-b689ebd37002
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: d52eeadc-19c6-4d48-995a-1c1f2ca3b5ec
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 5f3ceab5ee82587d9f1829792bdabf2209f793cd

---


# パスワードが失われました{#lost-password}

パスワードを失った場合は、変更または復元できます。

考えられるシナリオは2つあります。

* Adobe Campaignのオペレーターによってパスワードが失われました。

   この場合、関連する演算子のパスワードを変更できます。 これを行うには、管理者権限を持つ演算子を使用して接続し、演算子を右クリックして、/ **[!UICONTROL Actions]** /演算子の **[!UICONTROL Reset password]** 新しいパスワードを設定します。 オペレーターが最初の再接続時にパスワードを変更することをお勧めします。

   ![](assets/operator-passwd.png)

* **内部パスワード** 損失（オンプレミスのお客様のみ）。

   内部パスワ **ードが失われた** 場合は、再初期化する必要があります。 これを行うには、次の手順を適用します。

   1. /usr/local/neolane/nl6/conf/serverConf.xmlファイル **を編集** 。
   1. internalPassword行に移 **動します** 。

      ```
      <!-- XTK authentication mode internalPassword : Password of internal account -->
       <xtk internalPassword="myPassword"/>
      ```

   1. 引用符で囲んだ文字列を削除します。次の場合は削除します。myPassword ****

      この場合、次の行が取得されます。

      ```
      !-- XTK authentication mode internalPassword : Password of internal account -->
      <xtk internalPassword=""/
      ```

   1. 変更を保存し、ファイルを閉じます。
   1. 新しいパスワードを設定します。 これを行うには、次のコマンドを入力します。

      ```
      nlserver config -internalpassword
      HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
      Enter current password.
      Password: (empty)
      Enter the new password.
      Password: 
      Confirmation 
      ```

   1. これで、新しいパスワードを使用して内部モードで接続で **きます** 。

