---
solution: Campaign Classic
product: campaign
title: パスワードを忘れた場合
description: パスワードを忘れた場合
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: b7f44f4c18bef4cc412af878846b2c4305a17787
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 8%

---


# パスワードを忘れた場合{#lost-password}

パスワードを失った場合は、パスワードの変更や復元が可能です。
次の2つのシナリオが考えられます。

* **Adobe Campaign演算子によってパスワードが失われました**

この場合、関連する演算子のパスワードを変更できます。
これをおこなうには、以下の手順に従います。

1. オペレーター経由で管理者権限を持つ接続。
1. 演算子を右クリックします。
1. **[!UICONTROL アクション]**/**[!UICONTROL パスワードをリセット]**&#x200B;を選択します。

   ![](assets/operator-passwd.png)

1. 演算子の新しいパスワードを設定します。 演算子は、最初の再接続時にパスワードを変更することをお勧めします。

* **内部パスワードの損失（オンプレミスのお客様のみ）**

内部パスワードが失われた場合は、再初期化する必要があります。
これを行うには、次の手順を適用します。

1. **/usr/local/neolane/nl6/conf/serverConf.xml**&#x200B;ファイルを編集します。

1. **internalPassword**&#x200B;行に移動します。

   ```
   <!-- XTK authentication mode internalPassword : Password of internal account -->
   <xtk internalPassword="myPassword"/>
   ```

1. 引用符で囲んだ文字列を削除します（次の場合）。**myPassword**

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

1. これで、新しいパスワードを使用して、**内部**&#x200B;モードで接続できます。
