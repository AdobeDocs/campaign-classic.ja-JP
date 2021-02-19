---
solution: Campaign Classic
product: campaign
title: CRM コネクタ
description: Campaign の CRM コネクタの基礎知識
audience: platform
content-type: reference
topic-tags: connectors
translation-type: tm+mt
source-git-commit: 2838ced5f5d562914c0791e6a0b8f02dd61006b4
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 100%

---


# CRM コネクタ{#crm-connectors}

## CRM コネクタの基礎知識 {#about-crm-connectors}

Adobe Campaign では、Adobe Campaign プラットフォームをサードパーティのシステムにリンクするための様々な CRM コネクタが提供されています。これらの CRM コネクタにより、連絡先、アカウント、購入などを同期したり、アプリケーションを様々なサードパーティおよびビジネスアプリケーションと簡単に統合したりすることができます。

これらのコネクタを使用すると、データを迅速かつ容易に統合できます。Adobe Campaign には、CRM のテーブルを収集して選択するための専用のウィザードが用意されています。これにより、システム全体でデータを常に最新にするための双方向の同期が保証されます。

>[!NOTE]
>
>この機能は、**CRM コネクタ**&#x200B;専用パッケージを通じて Adobe Campaign で使用できます。


### 対応するシステム {#compatible-crm-systems-and-limitations}

サポートされている CRM とそのバージョンについて詳しくは、Campaign の[互換性マトリックス](../../rn/using/compatibility-matrix.md)を参照してください。

>[!NOTE]
>
>CRM コネクタはセキュア URL（https）でのみ動作します。

### 実装手順 {#crm-implementation-steps}

Campaign と Microsoft Dynamics を接続する手順については、[こちらの節](../../platform/using/crm-ms-dynamics.md)を参照してください。

一般に、Adobe Campaign で CRM コネクタを使用するには、次の手順に従います。

1. Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;ノードを使用して、新しい外部アカウントを作成します。
1. Campaign の接続先となる CRM システムを選択します。
1. 接続を有効にする設定を入力します。
1. 設定ウィザードを実行して、使用可能な CRM テーブルを生成します。設定ウィザードでは、テーブルを収集し、一致するスキーマを作成できます。

   **Salesforce** 設定ウィザードの例：

   ![](assets/crm_connectors_sfdc_launch.png)

   >[!NOTE]
   >
   >設定を承認するには、Adobe Campaign コンソールからログオフし、再度ログオンする必要があります。

1. **[!UICONTROL 管理／設定／データスキーマ]**&#x200B;ノードで、Adobe Campaign で生成されたスキーマを確認します。

   **Salesforce** スキーマの例：

   ![](assets/crm_connectors_sfdc_table.png)

1. スキーマが作成された後、CRM 経由で列挙を Adobe Campaign に自動的に同期することができます。

   そのためには、「**[!UICONTROL 列挙を同期しています...]**」リンクをクリックし、CRM 列挙に対応する Adobe Campaign の列挙を選択します。

   >[!NOTE]
   >
   >Adobe Campaign の列挙のすべての値を CRM の値に置き換えることができます。そのためには、**[!UICONTROL 置換]**&#x200B;列の「**[!UICONTROL はい]**」を選択します。

   **Salesforce** 列挙の例：

   ![](assets/crm_connectors_sfdc_enum.png)

   「**[!UICONTROL 次へ]**」をクリックしてから「**[!UICONTROL 開始]**」をクリックし、リストのインポートを開始します。

1. **[!UICONTROL 管理／プラットフォーム／列挙]**&#x200B;メニューで、インポートされた値を確認します。

   ![](assets/crm_connectors_sfdc_exe.png)

   >[!NOTE]
   >
   > Salesforce の複数選択リストはサポートされていません。

1. Adobe Campaign データと CRM システムの間でデータを同期させるには、ワークフローを作成し、**[!UICONTROL CRM コネクタ]**&#x200B;アクティビティを使用する必要があります。

   ![](assets/crm_connectors_sfdc_wf.png)

   データ同期の詳細については、[こちらのページ](../../platform/using/crm-data-sync.md)を参照してください。
