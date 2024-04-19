---
product: campaign
title: Campaign - Salesforce CRM コネクタ
description: Campaign と Salesforce を連携する方法を学ぶ
feature: Salesforce Integration
exl-id: 94a1f00d-e952-4edd-9012-f71c87b897ca
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: ht
source-wordcount: '349'
ht-degree: 100%

---

# Campaign と Salesforce.com の接続{#connect-to-sfdc}



このページでは、Campaign Classic を **Salesforce** に接続する方法について説明します。

データ同期は、専用のワークフローアクティビティを使用して実行します。 [詳細情報](../../platform/using/crm-data-sync.md)。


 外部アカウントを使用すれば、Salesforce データを Adobe Campaign にインポートおよび Adobe Campaign からエクスポートできます。
CRM コネクタを Salesforce 用に設定するには、次の手順に従います。

1. Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;ノードを使用して、新しい外部アカウントを作成します。
1. **[!UICONTROL Salesforce.com]** を選択します。
1. 接続を有効にするための設定を入力します。

   ![](assets/ext_account_17.png)

   Salesforce CRM 外部アカウントを Adobe Campaign で使用できるように設定するには、次の情報を提供する必要があります。

   * **[!UICONTROL アカウント]**
Salesforce CRM へのログインに使用するアカウント。

   * **[!UICONTROL パスワード]**
Salesforce CRM へのログインに使用するパスワード。

   * **[!UICONTROL クライアント識別子]**
クライアント識別子の確認方法については、この[ページ](https://help.salesforce.com/articleView?id=000205876&amp;type=1)を参照してください。

   * **[!UICONTROL セキュリティトークン]**
セキュリティトークンの確認方法については、この [ページ](https://help.salesforce.com/articleView?id=000205876&amp;type=1)を参照してください。

   * **[!UICONTROL API バージョン]**
API のバージョンを選択します。
1. 設定ウィザードを実行して、使用可能な CRM テーブルを生成します。設定ウィザードでは、テーブルを収集し、一致するスキーマを作成できます。

   ![](assets/crm_connectors_sfdc_launch.png)

   >[!NOTE]
   >
   >設定を承認するには、Adobe Campaign コンソールからログオフし、再度ログオンする必要があります。

1. **[!UICONTROL 管理／設定／データスキーマ]**&#x200B;ノードで、Adobe Campaign で生成されたスキーマを確認します。

   **Salesforce** スキーマの例：

   ![](assets/crm_connectors_sfdc_table.png)

1. スキーマを作成したら、列挙を Salesforce から Adobe Campaign に自動的に同期することができます。

   それには、「**[!UICONTROL 列挙を同期...]**」リンクをクリックし、Salesforce 列挙に対応する Adobe Campaign 列挙を選択します。



   ![](assets/crm_connectors_sfdc_enum.png)

   >[!NOTE]
   >
   >Adobe Campaign の列挙のすべての値を CRM の値に置き換えることができます。そのためには、**[!UICONTROL 置換]**&#x200B;列の「**[!UICONTROL はい]**」を選択します。


   「**[!UICONTROL 次へ]**」をクリックしてから「**[!UICONTROL 開始]**」をクリックし、リストのインポートを開始します。

1. **[!UICONTROL 管理／プラットフォーム／列挙]**&#x200B;メニューで、インポートされた値を確認します。

   ![](assets/crm_connectors_sfdc_exe.png)

   >[!NOTE]
   >
   > 複数選択列挙はサポートされていません。

これで Campaign と Salesforce.com が接続されました。 2 つのシステム間にデータの同期を設定できます。 

Adobe Campaign データと SFDC の間でデータを同期させるには、ワークフローを作成し、**[!UICONTROL CRM コネクタ]**&#x200B;アクティビティを使用する必要があります。

![](assets/crm_connectors_sfdc_wf.png)

データの同期について詳しくは、[このページ](../../platform/using/crm-data-sync.md)を参照してください。
