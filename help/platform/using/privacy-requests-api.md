---
product: campaign
title: 自動プライバシーリクエストプロセス
description: 自動プライバシーリクエストプロセスを設定する方法の説明
feature: Privacy, Privacy Tools
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: a93bac61-f615-4178-bc12-0f056e48687d
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: ht
source-wordcount: '667'
ht-degree: 100%

---

# 自動プライバシーリクエストプロセス {#automatic-privacy-request-api}



Adobe Campaign には、プライバシーリクエストの自動プロセスを設定できる **API** があります。

この API を使用した場合の一般的なプライバシープロセスは、[インターフェイスを使用](privacy-requests-ui.md)した場合と変わりません。ただし、プライバシーリクエストの作成のみが異なります。Adobe Campaign でリクエストを作成するかわりに、リクエスト情報を含む POST が Campaign に送信されます。リクエストごとに、新しいエントリが&#x200B;**[!UICONTROL プライバシーリクエスト]**&#x200B;画面に追加されます。その後、プライバシーのテクニカルワークフローにおいてリクエストが処理されます。これもインターフェイスからリクエストを追加した場合と変わりません。

API を使用してプライバシーリクエストを送信する場合、最初の削除リクエストについては、返されるデータをテストできるよう、**2 段階プロセス**&#x200B;を有効にしておくことをお勧めします。テストが終了したら、削除リクエストプロセスが自動的に実行されるよう、2 段階プロセスを無効にできます。

**[!UICONTROL CreateRequestByName]** JS API は次のように定義されます。

>[!NOTE]
>
>**gdprRequest** API を使用していた場合は引き続き使用できますが、新しい **privacyRequest** API を使用することをお勧めします。

>[!IMPORTANT]
>
>この API を使用するには、**[!UICONTROL プライバシーデータ権限]**&#x200B;ネームド権限が必要です。

```
<method library="nms:gdpr.js" name="CreateRequestByName" static="true">
 <help>Create a new GDPR Request using namespace internal name</help>
 <parameters>
  <param name="namespaceName" type="string" desc="Namespace internal name"/>
  <param name="reconciliationValue" type="string" desc="Reconciliation value"/>
  <param name="type" type="long" desc="Reconciliation value"/>
  <param name="confirmDeletePending" type="boolean" desc="Request confirm before deleting data"/>
  <param name="regulation" type="long" desc="regulation of newly created request"/>
  <param name="id" type="long" inout="out" desc="ID of newly created request"/>
 </parameters>
</method>
```

>[!NOTE]
>
>「regulation」フィールドは、Campaign Classic 20.2（ビルド 9178 以降）を使用している場合にのみ使用可能です。
>
>20.2 に移行しており既に API を使用している場合は、上記のように「regulation」フィールドを追加する必要があります。以前のビルドを使用している場合は、「regulation」フィールドなしで API を引き続き使用できます。

## 外部からの API の呼び出し {#invoking-api-externally}

外部から API を呼び出す方法の例（具体的には API を使用した認証と、プライバシー API の詳細）を以下に示します。プライバシー API について詳しくは、[API のドキュメント](https://experienceleague.adobe.com/developer/campaign-api/api/s-nms-privacyRequest.html?lang=ja)を参照してください。また、[Web サービス呼び出しに関するドキュメント](../../configuration/using/web-service-calls.md)も参照してください。

最初に、API を通じて認証を実行する必要があります。

1. URL「**`<server url>`/nl/jsp/schemawsdl.jsp?schema=xtk:session**」から **xtk:session** WSDL をダウンロードします。

1. &quot;Logon&quot; メソッドを使用し、リクエストのパラメーターとしてユーザー名とパスワードを渡します。セッショントークンを含む応答が返されます。SoapUI を使用する場合の例を以下に示します。

   ![](assets/do-not-localize/privacy-api.png)

1. 返されたセッショントークンを後続のすべての API 呼び出しの認証として使用します。これは 24 時間後に有効期限切れになります。

次に、プライバシー API を呼び出します。

1. URL **`<server url>`/nl/jsp/schemawsdl.jsp?schema=nms:privacyRequest** を使用して、WSDL をダウンロードします。

1. **[!UICONTROL CreateRequestByName]** を使用して、特定のプライバシーリクエストを作成します。

   **[!UICONTROL CreateRequestByName]** を使用する場合の例を以下に示します。上記で提供されたセッショントークンを認証として使用する方法に注目してください。応答は、作成されたリクエストの ID になります。

   ![](assets/do-not-localize/privacy-api-2.png)

   上記の手順を実行するためには、以下の点を考慮してください。

   * **nms:gdprRequest** スキーマで **queryDef** を使用すると、アクセスリクエストのステータスを確認できます。
   * **nms:gdprRequestData** スキーマで queryDef **を使用すると、アクセスリクエストの結果を取得できます。**
   * **「$(serverUrl)&#39;/nms/gdpr.jssp?id=&#39;@id」** から XML ファイルをダウンロードするには、許可リスト登録済みの IP からログインしてファイルにアクセスする必要があります。これを行うには、JSSP で生成されたファイルにアクセスできる web アプリケーションを作成します。

## JS からの API の呼び出し {#invoking-api-from-js}

Campaign Classic 内で JS から API を呼び出す方法の例を以下に示します。

>[!NOTE]
>
>「regulation」フィールドは、Campaign Classic 20.2（ビルド 9178 以降）を使用している場合にのみ使用可能です。
>
>20.2 に移行しており、既に API を使用している場合は、「regulation」フィールドを追加する必要があります。以前のビルドを使用している場合は、「regulation」フィールドなしで API を引き続き使用できます。

* **以前のビルドを GDPR パッケージと一緒に使用**&#x200B;している場合、下記のように「regulation」フィールドなしで API を引き続き使用できます。

  ```
  loadLibrary("nms:gdpr.js");
  /**************************** 
  This code calls an API to create new Privacy request on the DB.
  It requires 4 parameters below.
  Feel free to change parameter values.
  ****************************/
  // 1. Namespace internal name
  var namespaceName = "defaultNamespace1";
  // 2. Reconciliation value for privacy request
  var reconciliationValue = "example@adobe.com";
  // 3. Privacy request type
  // GDPR_REQUEST_TYPE_ACCESS = 1;
  // GDPR_REQUEST_TYPE_DELETE = 2;
  var requestType = GDPR_REQUEST_TYPE_ACCESS;
  // 4. Confirm deleting data required.
  // value : true or false
  var ConfirmDeletePending = true;
  // BEGIN
  var requestId = nms.privacyRequest.CreateRequestByName(namespaceName, reconciliationValue, requestType, ConfirmDeletePending);
  // User can use a simple queryDef with requestID as a parameter to check request status.
  ```

* **20.2 に移行**&#x200B;しており、既に API を使用している場合は、下記のように「regulation」フィールドを追加する必要があります。

  ```
  loadLibrary("nms:gdpr.js");
  /**************************** 
  This code calls an API to create new Privacy request on the DB.
  It requires 5 parameters below.
  Feel free to change parameter values.
  ****************************/
  // 1. Namespace internal name
  var namespaceName = "defaultNamespace1";
  // 2. Reconciliation value for privacy request
  var reconciliationValue = "example@adobe.com";
  // 3. Privacy request type
  // PRIVACY_REQUEST_TYPE_ACCESS = 1;
  // PRIVACY_REQUEST_TYPE_DELETE = 2;
  var requestType = PRIVACY_REQUEST_TYPE_ACCESS;
  // 4. Confirm deleting data required.
  // value : true or false
  var ConfirmDeletePending = true;
  // 5. Specify which regulation applies to newly created request. This is mandatory parameter.
  // GDPR = 1
  // CCPA = 2
  // PDPA = 3
  // LGPD = 4
  var regulation = 1;
  // BEGIN
  var requestId = nms.privacyRequest.CreateRequestByName(namespaceName, reconciliationValue, requestType, ConfirmDeletePending, regulation);
  // User can use a simple queryDef with requestID as a parameter to check request status.
  ```

* **Campaign Classic 20.2（ビルド 9178 以降）以降を使用**&#x200B;している場合は、下記のように「regulation」フィールドはオプションです。

  ```
  loadLibrary("nms:gdpr.js");
  /**************************** 
  This code calls an API to create new Privacy request on the DB.
  It requires 5 parameters below.
  Feel free to change parameter values 
  ****************************/
  // 1. Namespace internal name
  var namespaceName = "defaultNamespace1";
  // 2. Reconciliation value for privacy request
  var reconciliationValue = "example@adobe.com";
  // 3. Privacy request type
  // PRIVACY_REQUEST_TYPE_ACCESS = 1;
  // PRIVACY_REQUEST_TYPE_DELETE = 2;
  var requestType = PRIVACY_REQUEST_TYPE_ACCESS;
  // 4. Confirm deleting data required.
  // value : true or false
  var ConfirmDeletePending = true;
  // 5. Specify which regulation applies to newly created request. This is optional parameter.
  // GDPR = 1
  // CCPA = 2
  // PDPA = 3
  // LGPD = 4
  var regulation = 1;
  // BEGIN
  var requestId = nms.privacyRequest.CreateRequestByName(namespaceName, reconciliationValue, requestType, ConfirmDeletePending, regulation);
  // User can use a simple queryDef with requestID as a parameter to check request status.
  ```
