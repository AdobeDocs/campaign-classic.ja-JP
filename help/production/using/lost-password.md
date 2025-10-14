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
source-git-commit: 8aceafa362b80f6e34edfd91a71551a58501a3d0
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 12%

---

# パスワードを忘れた場合{#lost-password}

>[!NOTE]
>
>このページは、ネイティブ認証を使用して Campaign に接続するオペレーターにのみ適用されます。

失われたパスワードは変更または復元できます。
次の 2 つのシナリオが考えられます。

* [Adobe Campaign オペレーターによってパスワードが失われました](#password-lost-by-campaign-operator)
* [&#x200B; 内部パスワードが失われました &#x200B;](#internal-password-lost) （オンプレミスのお客様のみ）

## Campaign オペレーターによって失われたパスワード {#password-lost-by-campaign-operator}

Adobe Campaign オペレーターがパスワードを失った場合は変更できます。

>[!NOTE]
>
>この手順は、ネイティブ認証を使用して Campaign に接続するオペレーターにのみ適用されます。 Adobe IMS認証については、[&#x200B; このドキュメント &#x200B;](https://helpx.adobe.com/ie/manage-account/using/change-or-reset-password.html){target="_blank"} を参照してください。

Campaign のパスワードをリセットするには、次の手順に従います。

1. 管理者権限を持つオペレーターを介して接続します。
1. 演算子を右クリックします。
1. **[!UICONTROL アクション]**/**[!UICONTROL パスワードをリセット]** を選択します。

   ![](assets/operator-passwd.png)

1. オペレーターの新しいパスワードを設定します。 オペレーターが最初に再接続する際には、パスワードを変更することをお勧めします。

## 内部パスワードが失われました {#internal-password-lost}

>[!NOTE]
>
>この節は、オンプレミスのお客様にのみ適用されます。

内部パスワードが失われた場合、再初期化する必要があります。

それには、次の手順を適用します。

1. **/usr/local/neolane/nl6/conf/serverConf.xml** ファイルを編集します。

1. **internalPassword** 行に移動します。

   ```xml
   <!-- XTK authentication mode internalPassword : Password of internal account -->
   <xtk internalPassword="myPassword"/>
   ```

1. 引用符で囲まれた文字列（この場合は `myPassword`）を削除します。 次の行が表示されます。

   ```xml
   <!-- XTK authentication mode internalPassword : Password of internal account -->
   <xtk internalPassword=""/>
   ```

1. 変更を保存し、ファイルを閉じます。

1. `nlserver` プロセスを停止します。

1. 新しいパスワードを設定します。 それには、次のコマンドを入力します。

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

1. これで、新しいパスワードを使用して **内部** モードで接続できます。
