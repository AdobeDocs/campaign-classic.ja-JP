---
solution: Campaign Classic
product: campaign
title: CRM コネクタ
description: キャンペーンのCRMコネクタの概要
audience: platform
content-type: reference
topic-tags: connectors
translation-type: tm+mt
source-git-commit: 2838ced5f5d562914c0791e6a0b8f02dd61006b4
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 63%

---


# CRM コネクタ{#crm-connectors}

## CRMコネクタの概要{#about-crm-connectors}

Adobe Campaign では、Adobe Campaign プラットフォームをサードパーティのシステムにリンクするための様々な CRM コネクタが提供されています。これらの CRM コネクタにより、連絡先、アカウント、購入などを同期したり、アプリケーションを様々なサードパーティおよびビジネスアプリケーションと簡単に統合したりすることができます。

これらのコネクタを使用すると、データを迅速かつ容易に統合できます。Adobe Campaign には、CRM のテーブルを収集して選択するための専用のウィザードが用意されています。これにより、システム全体でデータを常に最新にするための双方向の同期が保証されます。

>[!NOTE]
>
>この機能は、**CRM コネクタ**&#x200B;専用パッケージを通じて Adobe Campaign で使用できます。


### 互換性のあるシステム{#compatible-crm-systems-and-limitations}

サポートされるCRMとバージョンについて詳しくは、キャンペーン[互換表](../../rn/using/compatibility-matrix.md)を参照してください。

>[!NOTE]
>
>CRM コネクタはセキュア URL（https）でのみ動作します。

### 実装の手順 {#crm-implementation-steps}

キャンペーンとMicrosoft Dynamics [を接続する手順を説明します。](../../platform/using/crm-ms-dynamics.md)

一般に、Adobe CampaignでCRMコネクタを使用するには、次の手順に従います。

1. Adobe Campaign ツリーの&#x200B;**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;ノードを使用して、新しい外部アカウントを作成します。
1. キャンペーンの接続先のCRMシステムを選択します。
1. 接続を有効にする設定を入力します。
1. 構成ウィザードを実行して、使用可能なCRMテーブルを生成します。設定ウィザードでは、テーブルを収集し、一致するスキーマを作成できます。

   **Salesforce**&#x200B;構成ウィザードの例：

   ![](assets/crm_connectors_sfdc_launch.png)

   >[!NOTE]
   >
   >設定を承認するには、Adobe Campaign コンソールからログオフし、再度ログオンする必要があります。

1. **[!UICONTROL 管理／設定／データスキーマ]**&#x200B;ノードで、Adobe Campaign で生成されたスキーマを確認します。

   **Salesforce**&#x200B;スキーマの例：

   ![](assets/crm_connectors_sfdc_table.png)

1. スキーマが作成された後、CRM 経由で列挙を Adobe Campaign に自動的に同期することができます。

   そのためには、「**[!UICONTROL 列挙を同期しています...]**」リンクをクリックし、CRM 列挙に対応する Adobe Campaign の列挙を選択します。

   >[!NOTE]
   >
   >Adobe Campaign の列挙のすべての値を CRM の値に置き換えることができます。そのためには、**[!UICONTROL 置換]**&#x200B;列の「**[!UICONTROL はい]**」を選択します。

   **Salesforce**&#x200B;定義済みリストの例：

   ![](assets/crm_connectors_sfdc_enum.png)

   「**[!UICONTROL 次へ]**」をクリックしてから「**[!UICONTROL 開始]**」をクリックし、リストのインポートを開始します。

1. **[!UICONTROL 管理／プラットフォーム／列挙]**&#x200B;メニューで、インポートされた値を確認します。

   ![](assets/crm_connectors_sfdc_exe.png)

   >[!NOTE]
   >
   > Salesforceでの複数の選択定義済みリストはサポートされていません。

1. Adobe CampaignデータとCRMシステム間でデータを同期するには、ワークフローを作成し、**[!UICONTROL CRMコネクタ]**&#x200B;アクティビティを使用する必要があります。

   ![](assets/crm_connectors_sfdc_wf.png)

   データ同期[の詳細については、このページ](../../platform/using/crm-data-sync.md)を参照してください。
