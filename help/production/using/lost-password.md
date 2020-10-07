---
title: パスワードを忘れた場合
seo-title: パスワードを忘れた場合
description: パスワードを忘れた場合
seo-description: null
page-status-flag: never-activated
uuid: caac68bf-abdc-45da-9697-b689ebd37002
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: d52eeadc-19c6-4d48-995a-1c1f2ca3b5ec
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 12%

---


# パスワードを忘れた場合{#lost-password}

パスワードを失った場合は、パスワードの変更や復元が可能です。

次の2つのシナリオが考えられます。

* Adobe Campaign演算子によってパスワードが失われました。

   この場合、関連する演算子のパスワードを変更できます。 これを行うには、管理者権限を持つ演算子を介して接続し、演算子を右クリックして、 **[!UICONTROL アクション]** / **** パスワードのリセットを選択し、演算子の新しいパスワードを設定します。 オペレーターが最初の再接続時にパスワードを変更することをお勧めします。

   ![](assets/operator-passwd.png)

* **内部パスワードの損失** （オンプレミスのお客様のみ）。

   内 **部パスワードが失われた場合は** 、再初期化する必要があります。 これを行うには、次の手順を適用します。

   1. /usr/local/neolane/nl6/conf/serverConf.xml **ファイルを編集します** 。
   1. internalPassword **** 行に移動します。

      ```
      <!-- XTK authentication mode internalPassword : Password of internal account -->
       <xtk internalPassword="myPassword"/>
      ```

   1. 引用符で囲んだ文字列を削除します（次の場合）。 **myPassword**

      次の行を取得します。

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

   1. これで、新しいパスワードを使用して **内部** モードで接続できます。

