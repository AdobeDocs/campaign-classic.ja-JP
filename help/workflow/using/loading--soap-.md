---
title: 読み込み（SOAP）
seo-title: 読み込み（SOAP）
description: 読み込み（SOAP）
seo-description: null
page-status-flag: never-activated
uuid: 80597892-e363-48f6-8633-faad161064a4
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: action-activities
discoiquuid: 94178104-f8ba-4c17-8ff9-928c5d2df1b7
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c10a0a11c6e9952aa47da1f7a15188c79c62508d

---


# 読み込み（SOAP）{#loading-soap}

>[!CAUTION]
>
>「**読み込み（SOAP）**」アクティビティは、「**FDA（Federated Data Access）**」モジュールがインストールされている場合にのみ使用できます。使用許諾契約書を確認してください。

外部データベースの FDA から直接データを収集できない場合は、「**読み込み（SOAP）**」アクティビティと「**データの読み込み（RDBMS）**」アクティビティとを組み合わせて使用します。

手順は以下のようになります。

1. XML の例または WSDL のどちらを使用するか選択します。

   次の例は、Message Center モジュールのテクニカルワークフローのものです。

   ![](assets/load_soap_002.png)

1. XML の例を使用する場合は、サンプルファイルを選択してください。ファイルが分析され、結果のサンプルが作成されます。

   WSDL を使用する場合は、該当するアクセス URL を入力してスケルトンコードを生成します。選択したサービスと呼び出しが自動的に更新されて表示されます。

   ![](assets/soap_load_003.png)

1. 識別され **[!UICONTROL Click here to view and edit analysis results]** た各列を指定する場合に選択します。

   ![](assets/soap_load_001.png)

   この例を更新する場合は、を選択しま **[!UICONTROL Re-analyze the example]**&#x200B;す。

   You can also personalize the format of column data via the **[!UICONTROL Advanced parameters]** link. インポートされたデータのフォーマットについて詳しくは、この[節](../../platform/using/importing-data.md#import-wizard)を参照してください。

1. 行番号を識別子として使用するか、または SOAP 呼び出しでいくつの要素を返させることを指定することができます。
1. 関数に合わせて、次のタブスクリプトを入力してください。

   * **[!UICONTROL Initialization]**:soap接続を確立します。
   * **[!UICONTROL Iteration]**:soapサービスの呼び出しを実行します。 この関数の戻り値は、必ず WSDL の例の記述と互換性のある XML オブジェクトになります。

      このタブのコードは、null の XML オブジェクトが返されるまで、Adobe Campaign によって繰り返し呼び出されます。

   * **[!UICONTROL Finalization]**:接続を閉じたり、処理中に作成された他のリソースを解放したりします。

