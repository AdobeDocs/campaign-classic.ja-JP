---
product: campaign
title: スクリプトとコーディングのガイドライン
description: Adobe Campaign（ワークフロー、JavaScript、JSSP など）での開発時に従うガイドラインの詳細を説明します。
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 1f96c3df-0ef2-4f5f-9c36-988cbcc0769f
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 35%

---

# スクリプトとコーディングのガイドライン {#scripting-coding-guidelines}



## スクリプト作成

詳しくは、[Campaign JSAPI のドキュメント](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja)を参照してください。

ワークフロー、Web アプリケーション、JSSP を使用してスクリプトを作成する場合、次のベストプラクティスに従ってください。

* SQL 文はできるだけ使用しないようにしてください。

* どうしても必要な場合は、文字列連結ではなく、パラメーター化関数（prepare 文）を使用します。

  悪い習慣：

  ```
  sqlGetInt( "select iRecipientId from NmsRecipient where sEmail ='" + request.getParameter('email') +  "'  limit 1" )
  ```

  ベストプラクティス：

  ```
  sqlGetInt( "select iRecipientId from NmsRecipient where sEmail = $(sz) limit 1", request.getParameter('email'));
  ```

  >[!IMPORTANT]
  >
  >sqlSelect はこの機能をサポートしていないため、DBEngine クラスのクエリ関数を使用する必要があります。

  ```
  var cnx = application.getConnection()
  var stmt = cnx.query("SELECT sFirstName, sLastName FROM NmsRecipient where sEmail = $(sz)", request.getParameter('email'))
  for each(var row in stmt) logInfo(row[0] + " : " + row[1])
  cnx.dispose()
  ```

SQL の挿入を避けるために、Adobe Campaignで使用する許可リストに SQL 関数を追加する必要があります。 許可リストに追加されると、式エディターで演算子に表示されるようになります。 [このページ](../../configuration/using/adding-additional-sql-functions.md)を参照してください。

>[!IMPORTANT]
>
>8140 より古いビルドを使用している場合、**XtkPassUnknownSQLFunctionsToRDBMS** オプションが&#39;1&#39;に設定されている可能性があります。 データベースを保護する場合は、このオプションを削除します（または「0」に設定します）。

ユーザー入力を使用してクエリや SQL 文にフィルターを作成する場合は、常にフィルターをエスケープする必要があります（[Campaign JSAPI ドキュメント ](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja) - データ保護：関数のエスケープを参照）。 次の関数が該当します。

* NL.XML.escape(data)
* NL.SQL.escape(data)
* NL.JS.escape(data)
* NL.XML.escapeAttribute(data)

## 新しいデータモデルの保護

### フォルダーベース

次のページを参照してください。

* [フォルダーアクセスのプロパティ](../../platform/using/access-management.md)
* [リンクされたフォルダー](../../configuration/using/configuration.md#linked-folder)

### ネームド権限

フォルダーベースのセキュリティモデルに加えて、ネームド権限を使用してオペレーターの操作を制限できます。

* 一部のシステムフィルター（sysFilter）を追加して、データの読み取りや書き込みを防ぐことができます（[ このページ ](../../configuration/using/filtering-schemas.md) を参照してください）。

  ```
  <sysFilter name="writeAccess">    
      <condition enabledIf="hasNamedRight('myNewRole')=false" expr="FALSE"/>  
  </sysFilter>
  ```

* また、スキーマで定義された一部のアクション（SOAP メソッド）を保護することもできます。 対応するネームド権限を値として使用して、アクセス属性を設定するだけです。

  ```
  <method name="grantVIPAccess" access="myNewRole">
      <parameters>
  ...
      </parameters>
  </method>
  ```

  詳しくは、[このページ](../../configuration/using/implementing-soap-methods.md)を参照してください。

>[!IMPORTANT]
>
>ネームド権限は、navtree のコマンド・ノードで使用できます。 ユーザーエクスペリエンスは向上しますが、保護は提供しません（クライアントサイドのみを使用して非表示/無効にします）。 アクセス属性を使用する必要があります。

### オーバーフローテーブル

オペレーターのアクセスレベルに応じて機密データ（スキーマの一部）を保護する必要がある場合、フォーム定義で非表示にしないでください（enabledIf／visibleIf 条件）。

エンティティ全体が画面に読み込まれます。また、列定義で表示することもできます。 それには、オーバーフローテーブルを作成する必要があります。 [ このページ ](../../configuration/using/examples-of-schemas-edition.md#overflow-table) を参照してください。

## Web アプリケーションへの Captcha の追加

パブリックのランディングページや購読ページに Captcha を追加することをお勧めします。 残念ながら、DCE （デジタルコンテンツエディター）ページに CAPTCHA を追加することは容易ではありません。 ここでは、Captcha バージョン 5 または Google reCAPTCHA を追加する方法について説明します。

DCE に Captcha を追加する一般的な方法は、パーソナライゼーションブロックを作成して、ページコンテンツ内に簡単に含めることです。 **スクリプト**&#x200B;アクティビティと&#x200B;**テスト**&#x200B;を追加する必要があります。

### パーソナライゼーションブロック

1. **[!UICONTROL リソース]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL パーソナライゼーションブロック]**&#x200B;に移動し、新しいパーソナライゼーションブロックを作成します。

1. **[!UICONTROL Web アプリケーション]** コンテンツタイプを使用し、「**[!UICONTROL カスタマイズメニューに表示]**」チェックボックスをオンにします。

   詳しくは、[このページ](../../delivery/using/personalization-blocks.md)を参照してください。

   **Campaign Captcha** の例を示します。

   ```javascript
   <%
   var captchaID = CaptchaIDGen();
   %>
   <img src="/nms/jsp/captcha.jsp?captchaID=<%=captchaID%>&width=200&height=50&minWordSize=8&maxWordSize=8"/>
   <input id="captchaValue" name="captchaValue" <%= String(ctx.vars.captchaValid) === "false" ? class="ui-state-error" : "" %>>
   <input type="hidden" name="captchaID" value="<%=captchaID%>"/>
   <%
   if( serverForm.isInputErroneous("captchaValue") ) {
   %>
   <script type="text/javascript"> 
   $("#captchaValue").addClass("ui-state-error")
   </script>
   <%
   }
   %>
   ```

   * 1 ～ 6 行目では、必要な入力をすべて生成します。
   * 7 行目から最終行では、エラーを処理します。
   * 4 行目では、Captcha のグレーボックスのサイズ（幅/高さ）と、生成されるワードの長さ（minWordSize/maxWordSize）を変更できます。
   * Google reCAPTCHA を使用する前に、Googleに登録して、新しい reCAPTCHA サイトを作成する必要があります。

     `<div class="g-recaptcha" data-sitekey="YOUR_SITE_KEY"></div>`

   「validation」ボタンは無効にできるはずですが、標準のボタンやリンクはないので、HTML自体で行う方が良いでしょう。 その方法については、[ このページ ](https://developers.google.com/recaptcha/) を参照してください。

### Web アプリケーションの更新

1. Web アプリケーションのプロパティにアクセスして、**captchaValid** という名前のブール変数を追加します。

   ![](assets/scripting-captcha.png)

1. 最後のページと&#x200B;**[!UICONTROL ストレージ]**&#x200B;アクティビティの間に、**[!UICONTROL スクリプト]**&#x200B;と&#x200B;**[!UICONTROL テスト]**&#x200B;を追加します。

   ブランチ **[!UICONTROL True]** を **[!UICONTROL ストレージ]** に接続し、もう 1 つを captcha を持つページに接続します。

   ![](assets/scripting-captcha2.png)

1. `"[vars/captchaValid]"` が True に等しいブランチ True の条件を編集します。

   ![](assets/scripting-captcha3.png)

1. **[!UICONTROL スクリプト]** アクティビティを編集します。 コンテンツは、選択した captcha エンジンによって異なります。

1. 最後に、パーソナライズされたブロックをページに追加できます。[ このページ ](../../web/using/editing-content.md) を参照してください。

   ![](assets/scripting-captcha4.png)

   ![](assets/scripting-captcha5.png)

>[!IMPORTANT]
>
>reCAPTCHA 統合の場合、（`<head>...</head>` で）HTMLにクライアントサイドのJavaScriptを追加する必要があります。
>
>`<script src="https://www.google.com/recaptcha/api.js" async defer></script>`

### キャンペーンのキャプチャ

```javascript
var captchaID = request.getParameter("captchaID");
var captchaValue = request.getParameter("captchaValue");
  
if( !CaptchaValidate(captchaID, captchaValue) ) {
  serverForm.logInputError("captchaValue",
                           "The characters you typed for the captcha must match the image ones.",
                           "captchaValue")
  ctx.vars.captchaValid = false
}
else
  ctx.vars.captchaValid = true
```

6 行目：あらゆる種類のエラーメッセージを出力できます。

### Google recaptcha

詳しくは、[ 公式ドキュメント ](https://developers.google.com/recaptcha/docs/verify) を参照してください。

```javascript
ctx.vars.captchaValid = false
var gReCaptchaResponse = request.getParameter("g-recaptcha-response");
  
// Call reCaptcha API to validate it
var req = new HttpClientRequest("https://www.google.com/recaptcha/api/siteverify")
req.method = "POST"
req.header["Content-Type"] = "application/x-www-form-urlencoded"
req.body = "secret=YOUR_SECRET_HERE&response=" + encodeURIComponent(gReCaptchaResponse)
req.execute()
var response = req.response
if( response.code == 200 ) {
  captchaRes = JSON.parse(response.body.toString(response.codePage));
  ctx.vars.captchaValid = captchaRes.success
}
  
if( ctx.vars.captchaValid == false ) {
  serverForm.logInputError("reCaptcha",
                           "Please validate the captcha",
                           "reCaptcha")
  logInfo("reCaptcha not validated")
}
```

JSON.parse を使用するには、webApp に「shared/json2.js」を含める必要があります。

![](assets/scripting-captcha6.png)

ビルド 8797 以降、verification API URL を使用するには、urlPermission ノードに次のように追加して、serverConf ファイルの許可リストに追加する必要があります。

`<url dnsSuffix="www.google.com" urlRegEx="https://www.google.com/recaptcha/api/siteverify"/>`
