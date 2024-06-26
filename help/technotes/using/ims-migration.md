---
title: Adobe Developer Console へのテクニカルユーザーの移行
description: Campaign テクニカルオペレーターを Adobe Developer Console のテクニカルアカウントに移行する方法を学ぶ
feature: Technote
role: Admin
exl-id: 1a409daf-57be-43c9-a3d9-b8ab54c88068
source-git-commit: af811b2df325efcaee38a967252b6952e67680d1
workflow-type: ht
source-wordcount: '1779'
ht-degree: 100%

---

# Adobe Developer Console への Campaign テクニカルオペレーターの移行 {#migrate-tech-users-to-ims}

セキュリティと認証プロセスを強化する取り組みの一環として、Campaign Classic v7.3.5 以降、Campaign Classic への認証プロセスが改善されています。テクニカルオペレーターは、[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}を使用して Campaign に接続する必要があります。新しいサーバー間の認証プロセスについて詳しくは、[Adobe Developer Console ドキュメント](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/){target="_blank"}を参照してください。**アドビでは、Campaign v8 にスムーズに移行できるように、v7 でこの移行を実行することをお勧めします。**

テクニカルオペレーターは、API 統合用に明示的に作成された Campaign ユーザープロファイルです。この記事では、Adobe Developer Console からテクニカルオペレーターをテクニカルアカウントに移行するために必要な手順について詳しく説明します。

## 影響の有無{#ims-impacts}

Campaign の外部システムから Campaign マーケティングインスタンスまたはリアルタイム Message Center インスタンスのいずれかに API 呼び出しを行っている場合は、アドビでは、以下で説明するように、Adobe Developer Console を通じてテクニカルオペレーターをテクニカルアカウントに移行することをお勧めします。

この変更は、Campaign Classic v7.3.5（および最新の [IMS 移行互換バージョン](ac-ims.md#ims-versions)）以降に適用され、Adobe Campaign v8 に移行するには&#x200B;**必須**&#x200B;となります。

## 移行プロセス {#ims-migration-procedure}

以下の手順に従って、Adobe Developer Console 内でテクニカルアカウントを作成し、新しく作成したアカウントを使用して、Adobe Campaign で API 呼び出しを行うすべての外部システムの認証方法を変更できるようにします。

手順の概要を以下に示します。

* Adobe Developer Console 内でのプロジェクトの作成
* 新しく作成したプロジェクトへの適切な API の割り当て
* プロジェクトへの必要な Campaign 製品プロファイルの付与
* 新しく作成したテクニカルアカウント資格情報を使用する API の更新
* Campaign インスタンスからの従来のテクニカルオペレーターの削除


### 移行の前提条件{#ims-migration-prerequisites}

<!--To be able to create the technical accounts which replace the technical operators, the prerequisite that the proper Campaign Product Profiles exist within the Admin Console for all Campaign instances need to be validated. You can learn more about Product Profiles within the Adobe Console in [Adobe Developer Console documentation](https://developer.adobe.com/developer-console/docs/guides/projects/){target="_blank"}.-->

* Campaign ホスト環境および Managed Services 環境のお客様

  Message Center インスタンスへの API 呼び出しの場合、Campaign v7.4.1（またはその他の[IMS 移行互換バージョン](ac-ims.md#ims-versions)）へのアップグレード中や、インスタンスのプロビジョニング中に製品プロファイル（下記）を作成する必要があります。製品プロファイルが表示されない場合は、移行マネージャーまたはカスタマーサポートに問い合わせて、IMS 移行を開始する前に作成した製品プロファイルを取得します。この製品プロファイルの名前を以下に示します。

  `campaign - <your campaign marketing instance> - messagecenter`

  Campaign へのユーザーアクセスに IMS ベースの認証を既に使用している場合は、API 呼び出しに必要な製品プロファイルが Admin Console 内に既に存在している必要があります。マーケティングインスタンスへの API 呼び出しに Campaign 内のカスタムオペレーターグループを使用する場合は、Admin Console 内でその製品プロファイルを作成する必要があります。

  それ以外の場合は、アドビのテクニカルチームが既存のオペレーターグループとネームド権限を Admin Console 内の製品プロファイルに移行できるように、アドビトランジションマネージャー（Managed Services ユーザーの場合）またはアドビカスタマーケア（他のホスト環境のユーザーの場合）に問い合わせる必要があります。

* Campaign オンプレミス環境およびハイブリッド環境のお客様

  Message Center インスタンスへの API 呼び出しの場合、次の名前の製品プロファイルを作成する必要があります。

  `campaign - <your campaign instance> - messagecenter`

  Campaign へのユーザーアクセスに IMS ベースの認証を既に使用している場合は、API 呼び出しに必要な製品プロファイルが Admin Console 内に既に存在している必要があります。マーケティングインスタンスへの API 呼び出しに Campaign 内のカスタムオペレーターグループを使用する場合は、Admin Console 内でその製品プロファイルを作成する必要があります。

  Adobe Console 内の製品プロファイルについて詳しくは、[Adobe Developer Console ドキュメント](https://developer.adobe.com/developer-console/docs/guides/projects/){target="_blank"}を参照してください。


### 手順 1 - Adobe Developer Console 内で Campaign プロジェクトを作成 {#ims-migration-step-1}

統合は、Adobe Developer Console 内の&#x200B;**プロジェクト**&#x200B;の一部として作成されます。プロジェクトについて詳しくは、[Adobe Developer Console ドキュメント](https://developer.adobe.com/developer-console/docs/guides/projects/){target="_blank"}を参照してください。

以前に作成した任意のプロジェクトを使用するか、新しいプロジェクトを作成することができます。プロジェクトを作成する手順について詳しくは、[Adobe Developer Console ドキュメント](https://developer.adobe.com/developer-console/docs/guides/getting-started/){target="_blank"}を参照してください。主な手順を以下に示します

<!--
For this migration, you must add below APIs in your project: **I/O Management API** and **Adobe Campaign**.

![](assets/do-not-localize/ims-products-and-services.png)-->

新しいプロジェクトを作成するには、Adobe Developer Console のメイン画面で「**新しいプロジェクトを作成**」をクリックします。

![](assets/New-Project.png)

「**プロジェクトを編集**」ボタンを使用すると、このプロジェクトの名前を変更できます。


### 手順 2 - プロジェクトに API を追加 {#ims-migration-step-2}

新しく作成したプロジェクト画面から、Adobe Campaign への API 呼び出しのテクニカルアカウントとしてこのプロジェクトを使用可能にするために必要な API を追加します。

プロジェクトに API を追加するには、次の手順に従います。

1. 「**API を追加**」をクリックして、プロジェクトに追加する API を選択します。
   ![](assets/do-not-translate/ims-updates-01.png)
1. Adobe Campaign カードにポインタを合わせると表示される Adobe Campaign カードの右上隅にあるチェックボックスをオンして、Adobe Campaign API を選択してプロジェクトに追加します
   ![](assets/do-not-translate/ims-updates-02.png)
1. 画面の下部にある「**次へ**」をクリックします。

### 手順 3 - 認証タイプを選択  {#ims-migration-step-3}

**API を設定**&#x200B;画面で、必要な認証タイプを選択します。このプロジェクトには **OAuth サーバー間**&#x200B;認証が必要です。選択されていることを確認し、画面の下部にある「**次へ**」をクリックします。

![](assets/do-not-translate/ims-updates-03.png)

<!--
Once your project is created in the Adobe Developer Console, add an API that uses Server-to-Server authentication. Learn how to set up the OAuth Server-to-Server credential in [Adobe Developer Console documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/){target="_blank"}.

When the API has been successfully connected, you can access the newly generated credentials including Client ID and Client Secret, as well as generate an access token.-->

### 手順 4 - 製品プロファイルを選択 {#ims-migration-step-4}

前提条件の節で説明したように、プロジェクトで使用する適切な製品プロファイルを割り当てる必要があります。この手順では、作成するテクニカルアカウントで使用する製品プロファイルを選択する必要があります。

このテクニカルアカウントを使用して Message Center インスタンスに API 呼び出しを行う場合は、Message Center に関連付けられたマーケティングインスタンスに対して、messagecenter で終わるアドビ製品プロファイルを選択する必要があります。

マーケティングインスタンスへの API 呼び出しの場合は、インスタンスとオペレーターグループに対応する製品プロファイル（`campaign - <your campaign marketing instance> - Admin` など）を選択します。

必要な製品プロファイルを選択したら、画面の下部にある「**設定済み API を保存**」をクリックします。

<!--
You can now add your Campaign product profile to the project, as detailed below:

1. Open the Adobe Campaign API.
1. Click the **Edit product profiles** button

    ![](assets/do-not-localize/ims-edit-api.png)

1. Assign all the relevant Product Profiles to the API, for example 'messagecenter', and save your changes.
1. Browse to the **Credential details** tab of your project, and copy the **Technical Account Email** value.-->

### 手順 5 - I/O Management API をプロジェクトに追加 {#ims-migration-step-5}


プロジェクト画面で「**[!UICONTROL + プロジェクトに追加]**」をクリックし、画面左上の「**[!UICONTROL API]**」を選択して、I/O Management API をこのプロジェクトに追加できるようにします。

![](assets/do-not-translate/ims-updates-04.png)

**API を追加**&#x200B;画面で、下にスクロールして **I/O Management API** カードを見つけます。これを選択するには、カードにポインタを合わせると表示されるチェックボックスをクリックします。次に、画面の下部にある「**次へ**」をクリックします。

![](assets/do-not-translate/ims-updates-05.png)


**API を設定**&#x200B;画面では、OAuth サーバー間認証が既に存在しています。画面の下部にある「**設定済み API を保存**」をクリックします。


![](assets/do-not-translate/ims-updates-06.png)

これにより、新しく作成したプロジェクトの I/O Management API 内のプロジェクト画面に戻ります。画面上部のパンくずリストのプロジェクト名をクリックすると、メインのプロジェクトの詳細ページに戻ります。


### 手順 6 - プロジェクト設定を確認 {#ims-migration-step-6}

プロジェクトを確認して、「製品とサービス」セクションに **I/O Management API** と **Adobe Campaign API** が表示され、「資格情報」セクションに **OAuth サーバー間**&#x200B;が表示され、以下のようになっていることを確認します。

![](assets/do-not-translate/ims-updates-07.png)


### 手順 7 - 設定を検証 {#ims-migration-step-7}

接続を試すには、[Adobe Developer Console 資格情報ガイド](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/#generate-access-tokens){target="_blank"}で説明しているアクセストークンの生成手順に従って、提供されているサンプル cURL コマンドをコピーします。これらの資格情報を使用して SOAP 呼び出しを作成し、Adobe Campaign インスタンスを正しく認証して接続できるかどうかをテストできます。サードパーティ API 統合にすべての変更を行う前に、この検証を行うことをお勧めします。

### 手順 8 - サードパーティ API 統合を更新 {#ims-migration-step-8}

新しく作成したテクニカルアカウントを使用するには、Adobe Campaign を呼び出すすべての API 統合を更新する必要があります。

API 統合手順について詳しくは、以下のコードサンプルを参照してください。

Adobe Identity Management System （IMS）認証を使用して WSDL ファイルを生成する際は、Postman 呼び出しに「Authorization: Bearer &lt;IMS_Technical_Token_Token>」を追加してください。

```
curl --location --request POST 'https://<instance_url>/nl/jsp/schemawsdl.jsp?schema=nms:rtEvent' \--header 'Authorization: Bearer <Technical account access token>'
```

>[!BEGINTABS]

>[!TAB SOAP Call]

```
curl --location --request POST 'https://<instance_name>.campaign.adobe.com/nl/jsp/soaprouter.jsp' \
--header 'Content-Type: text/xml; charset=utf-8' \
--header 'SOAPAction: xtk:queryDef#ExecuteQuery' \
--header 'Authorization: Bearer eyJhw' \
--data-raw '<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ExecuteQuery xmlns="urn:xtk:queryDef">
            <sessiontoken></sessiontoken>
            <entity>
                <queryDef schema="nms:recipient" operation="select">
                    <!-- fields to retrieve -->
                    <select>
                        <node expr="@lastName"/>
                        <node expr="@email"/>
                        <node expr="@firstName"/>
                    </select>
                    <!-- condition on email -->
                    <!-- <where><condition expr="@email= '\''joh@com.com'\''"/>
                </where> -->
                </queryDef>
            </entity>
        </ExecuteQuery>
  </soap:Body>
</soap:Envelope>
'
```

>[!TAB SampleCode Java]

```javascript
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import com.google.gson.Gson;
import com.google.gson.JsonObject;
 
import com.google.gson.JsonSyntaxException;
import org.apache.hc.client5.http.classic.methods.HttpPost;
import org.apache.hc.client5.http.impl.classic.CloseableHttpClient;
import org.apache.hc.client5.http.impl.classic.CloseableHttpResponse;
import org.apache.hc.client5.http.impl.classic.HttpClients;
import org.apache.hc.core5.http.HttpEntity;
import org.apache.hc.core5.http.io.entity.StringEntity;
 
 
public class TAAccessToken {
    public static void main(String[] args) throws IOException {
        String accessToken = null;
        CloseableHttpClient httpClient = HttpClients.createDefault();
        try {
            HttpPost httpPost = new HttpPost("https://ims-na1.adobelogin.com/ims/token/v3");
 
            // Request headers
            httpPost.addHeader("Content-Type", "application/x-www-form-urlencoded");
 
            String clientId = "<client_id>";
            String clientSecret = "<client_secret>";
            String scopes = "<scopes>";
 
            // Define the request body
            String requestBody = "client_id="+clientId+"&client_secret="+clientSecret+"&grant_type=client_credentials&scope="+scopes+"";
            StringEntity requestEntity = new StringEntity(requestBody);
            httpPost.setEntity(requestEntity);
 
            // Execute the request
            CloseableHttpResponse response = httpClient.execute(httpPost);
            try {
                // Get the response entity
                HttpEntity entity = response.getEntity();
                int responseCode = response.getCode();
 
                // Print the response
                if (entity != null) {
                    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(entity.getContent()));
                    String lineImsToken;
                    StringBuilder responseImsToken = new StringBuilder();
                    while ((lineImsToken = bufferedReader.readLine()) != null) {
                        responseImsToken.append(lineImsToken);
                    }
 
                    String jsonString = responseImsToken.toString();
 
                    try {
                        Gson gson = new Gson();
                        JsonObject jsonObject = gson.fromJson(jsonString, JsonObject.class);
 
                        // Get the value of a specific key
                        accessToken = jsonObject.get("access_token").getAsString();
                    }
                    catch (JsonSyntaxException | NullPointerException e) {
                        System.err.println("Error parsing JSON: " + e.getMessage());
                        e.printStackTrace();
                    }
                    System.out.println("Response Code: " + responseCode);
                    System.out.println("Response Body: " + accessToken);
                }
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                response.close();
            }
        } finally {
            httpClient.close();
        }
 
        CloseableHttpClient httpClientSoap = HttpClients.createDefault();
        try {
            HttpPost httpPostSoap = new HttpPost("https://<instance_name>.campaign.adobe.com/nl/jsp/soaprouter.jsp");
 
            // Request headers
            httpPostSoap.addHeader("Content-Type", "text/xml; charset=utf-8");
            httpPostSoap.addHeader("SOAPAction", "xtk:queryDef#ExecuteQuery");
            httpPostSoap.addHeader("Authorization", "Bearer "+accessToken);
 
            // Request body
            String xmlData = "<?xml version=\"1.0\" encoding=\"utf-8\"?>\n" +
                    "<soap:Envelope xmlns:soap=\"http://schemas.xmlsoap.org/soap/envelope/\">\n" +
                    "  <soap:Body>\n" +
                    "    <ExecuteQuery xmlns=\"urn:xtk:queryDef\">\n" +
                    "            <sessiontoken></sessiontoken>\n" +
                    "            <entity>\n" +
                    "                <queryDef schema=\"nms:recipient\" operation=\"select\">\n" +
                    "                    <!-- fields to retrieve -->\n" +
                    "                    <select>\n" +
                    "                        <node expr=\"@lastName\"/>\n" +
                    "                        <node expr=\"@email\"/>\n" +
                    "                        <node expr=\"@firstName\"/>\n" +
                    "                    </select>\n" +
                    "                    <!-- condition on email -->\n" +
                    "                    <!-- <where><condition expr=\"@email= '\''joh@com.com'\''\"/>\n" +
                    "                </where> -->\n" +
                    "                </queryDef>\n" +
                    "            </entity>\n" +
                    "        </ExecuteQuery>\n" +
                    "  </soap:Body>\n" +
                    "</soap:Envelope>";
            StringEntity requestEntity = new StringEntity(xmlData);
            httpPostSoap.setEntity(requestEntity);
 
            // Execute the request
            CloseableHttpResponse response = httpClientSoap.execute(httpPostSoap);
            try {
                // Get the response entity
                HttpEntity entity = response.getEntity();
 
                // Print the response
                if (entity != null) {
                    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(entity.getContent()));
                    String line;
                    while ((line = bufferedReader.readLine()) != null) {
                        System.out.println(line);
                    }
                }
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                response.close();
            }
        } finally {
            httpClientSoap.close();
        }
 
    }
}
```

>[!TAB SampleCodePython]

```python
import requests
 
oauth_url = 'https://ims-na1.adobelogin.com/ims/token/v3'
data = {
    'grant_type': 'client_credentials',
    'scope': '<scopes>',
    'client_id': '<client_id>',
    'client_secret': '<client_secret>'
}
 
headers = {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'application/json'
}
response = requests.post(oauth_url, data=data, headers=headers)
response = response.json()
access_token = response['access_token']
 
 
url = 'https://<instance_name>.campaign.adobe.com/nl/jsp/soaprouter.jsp'
headers = {
    'Content-Type': 'text/xml; charset=utf-8',
    'SOAPAction': 'xtk:queryDef#ExecuteQuery',
    'Authorization': 'Bearer '+access_token
}
xml_data = '''<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ExecuteQuery xmlns="urn:xtk:queryDef">
            <sessiontoken></sessiontoken>
            <entity>
                <queryDef schema="nms:recipient" operation="select">
                    <!-- fields to retrieve -->
                    <select>
                        <node expr="@lastName"/>
                        <node expr="@email"/>
                        <node expr="@firstName"/>
                    </select>
                    <!-- condition on email -->
                    <!-- <where><condition expr="@email= '\''joh@com.com'\''"/>
                </where> -->
                </queryDef>
            </entity>
        </ExecuteQuery>
  </soap:Body>
</soap:Envelope>
'''
response = requests.post(url, headers=headers, data=xml_data)
```

>[!ENDTABS]

詳しくは、[Adobe Developer Console 認証ドキュメント](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/){target="_blank"}を参照してください。

サードパーティシステムの移行前と移行後のサンプル SOAP 呼び出しを以下に示します。

移行プロセスを完了して検証すると、SOAP 呼び出しは次のように更新されます。

* 移行前：テクニカルアカウントのアクセストークンはサポートされていませんでした。

  ```sql
  POST /nl/jsp/soaprouter.jsp HTTP/1.1
  Host: localhost:8080
  Content-Type: application/soap+xml;
  SOAPAction: "nms:rtEvent#PushEvent"
  charset=utf-8
  
  <?xml version="1.0" encoding="utf-8"?>  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:nms:rtEvent">
  <soapenv:Header/>
  <soapenv:Body>
      <urn:PushEvent>
          <urn:sessiontoken>SESSION_TOKEN</urn:sessiontoken>
          <urn:domEvent>
              <!--You may enter ANY elements at this point-->
              <rtEvent type="type" email="name@domain.com"/>
          </urn:domEvent>
      </urn:PushEvent>
  </soapenv:Body>
  </soapenv:Envelope>
  ```

* 移行後：テクニカルアカウントのアクセストークンはサポートされます。アクセストークンは、ベアラートークンとして `Authorization` ヘッダーで提供されることが予想されます。以下の SOAP 呼び出しのサンプルに示すように、ここではセッショントークンの使用を無視する必要があります。

  ```sql
  POST /nl/jsp/soaprouter.jsp HTTP/1.1
  Host: localhost:8080
  Content-Type: application/soap+xml;
  SOAPAction: "nms:rtEvent#PushEvent"
  charset=utf-8
  Authorization: Bearer <IMS_Technical_Token_Token>
  
  <?xml version="1.0" encoding="utf-8"?>  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:nms:rtEvent">
  <soapenv:Header/>
  <soapenv:Body>
      <urn:PushEvent>
          <urn:sessiontoken></urn:sessiontoken>
          <urn:domEvent>
              <!--You may enter ANY elements at this point-->
              <rtEvent type="type" email="name@domain.com"/>
          </urn:domEvent>
      </urn:PushEvent>
  </soapenv:Body>
  </soapenv:Envelope>
  ```



### 手順 9 -（オプション）Campaign クライアントコンソール内でテクニカルアカウントオペレーターを更新 {#ims-migration-step-9}

この手順はオプションで、Message Center インスタンス内ではなく、マーケティングインスタンス内でのみ使用できます。特定のフォルダー権限またはネームド権限が、割り当てられたオペレーターグループ経由ではなくテクニカルオペレーターに対して定義されている場合。ここで、Admin Console で新しく作成したテクニカルアカウントユーザーを更新して、必要なフォルダー権限またはネームド権限を付与する必要があります。

テクニカルアカウントユーザーは、Campaign インスタンスに対して少なくとも 1 回の API 呼び出しが行われるまで、Adobe Campaign には存在しません。その時点で、IMS は Campaign 内にユーザーを作成します。Campaign 内でテクニカルユーザーが見つからない場合は、[手順 7](#ims-migration-step-7) で説明したように API 呼び出しを正常に送信できることを確認します。

1. 新しいテクニカルアカウントユーザーに必要な変更を適用するには、Campaign クライアントコンソール内でメールアドレスを使用してユーザーを見つけます。このメールアドレスは、上記のプロジェクトの作成と認証の手順で作成されたものです。

   このメールアドレスを見つけるには、プロジェクトの「**資格情報**」セクションにある「**OAuth サーバー間**」見出しをクリックします。

   ![](assets/do-not-translate/ims-updates-07.png)

   「**資格情報の詳細**」タブで、下にスクロールして&#x200B;**テクニカルアカウントのメール**&#x200B;を見つけて、「**コピー**」ボタンをクリックします。

   ![](assets/do-not-translate/ims-updates-08.png)

1. ここでは、Adobe Campaign クライアントコンソールで新しく作成したテクニカルオペレーターを更新する必要があります。既存のテクニカルオペレーターフォルダーの権限を新しいテクニカルオペレーターに適用する必要があります。

   このオペレーターを更新するには、次の手順に従います。

   1. Campaign クライアントコンソールのエクスプローラーから、**管理／アクセス管理／オペレーター**&#x200B;を参照します。
   1. API に使用される既存のテクニカルオペレーターにアクセスします。
   1. フォルダー権限を参照し、権限を確認します。
   1. 新しく作成したテクニカルオペレーターに同じ権限を適用します。このオペレーターのメールアドレスは、以前にコピーした&#x200B;**テクニカルアカウントメールアドレス**&#x200B;の値です。
   1. 変更内容を保存します。


>[!CAUTION]
>
>新しいテクニカルオペレーターは、Campaign クライアントコンソールに追加される API 呼び出しを 1 回以上実行する必要があります。
>

### 手順 10 - Adobe Campaign から古いテクニカルオペレーターを削除 {#ims-migration-step-10}

IMS 認証で新しいテクニカルアカウントを使用するようにすべてのサードパーティシステムを移行したら、Campaign クライアントコンソールから古いテクニカルオペレーターを削除できます。

これを行うには、Campaign クライアントコンソールにログインし、**管理／アクセス管理／オペレーター**&#x200B;に移動し、古いテクニカルユーザーを見つけて削除します。


>[!MORELIKETHIS]
>
>* [エンドユーザーの IMS への移行](migrate-users-to-ims.md)
>* [IMS 移行後の Campaign インターフェイスの更新](impact-ims-migration.md)
>* [Adobe Campaign Classic v7 最新リリースノート](../../rn/using/latest-release.md)
>* [Adobe Identity Management System（IMS）とは](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}

