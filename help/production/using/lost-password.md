---
solution: Campaign Classic
product: campaign
title: パスワードを忘れた場合
description: パスワードを忘れた場合
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 1fdee02e98ce66ec184d8587d0838557f027cf75
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 7%

---


# パスワードを忘れた場合{#lost-password}

パスワードを失った場合は、パスワードの変更や復元が可能です。
次の2つのシナリオが考えられます。

* [Adobe Campaign演算子によってパスワードが失われました](#password-lost-by-campaign-operator)
* [内部パスワードの損失](#internal-password-lost) （オンプレミスのお客様のみ）

## キャンペーン演算子{#password-lost-by-campaign-operator}によってパスワードが失われました

Adobe Campaign演算子がパスワードを失った場合は、パスワードを変更できます。
これをおこなうには、以下の手順に従います。

1. オペレーター経由で管理者権限を持つ接続。
1. 演算子を右クリックします。
1. **[!UICONTROL アクション]**/**[!UICONTROL パスワードをリセット]**&#x200B;を選択します。

   ![](assets/operator-passwd.png)

1. 演算子の新しいパスワードを設定します。 オペレーターが最初に再接続する際に、パスワードを変更することをお勧めします。

## 内部パスワードが失われました{#internal-password-lost}

>[!NOTE]
>
>この節は、オンプレミスのお客様にのみ当てはまります。

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
