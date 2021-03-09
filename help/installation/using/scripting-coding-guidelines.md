---
solution: Campaign Classic
product: campaign
title: スクリプティングとコーディングのガイドライン
description: Adobe Campaign(ワークフロー、JavaScript、JSSPなど)で開発する際に従うガイドラインについて詳しく説明します。
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
translation-type: tm+mt
source-git-commit: f03554302c77a39a3ad68d47417ed930f43302b7
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 70%

---


# スクリプティングとコーディングのガイドライン{#scripting-coding-guidelines}

## スクリプト作成

詳しくは、[Campaign JSAPI のドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)を参照してください。

ワークフロー、Web アプリケーション、JSSP を使用してスクリプトを作成する場合、次のベストプラクティスに従ってください。

* SQL 文はできるだけ使用しないようにしてください。

* どうしても必要な場合は、文字列連結ではなく、パラメーター化関数（prepare 文）を使用します。

   悪い練習：

   ```
   sqlGetInt( "select iRecipientId from NmsRecipient where sEmail ='" + request.getParameter('email') +  "'  limit 1" )
   ```

   ベストプラクティス：

   ```
   sqlGetInt( "select iRecipientId from NmsRecipient where sEmail = $(sz) limit 1", request.getParameter('email'));
   ```

   >[!IMPORTANT]
   >
   >sqlSelectはこの機能をサポートしていないので、DBEngineクラスのクエリ関数を使用する必要があります。

   ```
   var cnx = application.getConnection()
   var stmt = cnx.query("SELECT sFirstName, sLastName FROM NmsRecipient where sEmail = $(sz)", request.getParameter('email'))
   for each(var row in stmt) logInfo(row[0] + " : " + row[1])
   cnx.dispose()
   ```

SQL インジェクションを回避するには、Adobe Campaign で使用する許可リストに SQL 関数を追加する必要があります。許可リストに追加すると、式エディターで演算子が表示されます。[このページ](../../configuration/using/adding-additional-sql-functions.md)を参照してください。

>[!IMPORTANT]
>
>8140より古いビルドを使用している場合は、**XtkPassUnknownSQLFunctionsToRDBMS**&#x200B;オプションが&#39;1&#39;に設定されている可能性があります。 データベースを保護する場合は、このオプションを削除します（または「0」に設定します）。

ユーザー入力を使用してクエリや SQL 文でフィルターを作成する場合は、常にエスケープ処理をおこなう必要があります（[Campaign JSAPI のドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)「データ保護：関数のエスケープ」を参照）。次の関数が該当します。

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

* データへの読み取り/書き込みを防ぐために、いくつかのシステムフィルター(sysFilter)を追加できます（[このページ](../../configuration/using/filtering-schemas.md)を参照）。

   ```
   <sysFilter name="writeAccess">    
       <condition enabledIf="hasNamedRight('myNewRole')=false" expr="FALSE"/>  
   </sysFilter>
   ```

* スキーマで定義された一部の操作（SOAP メソッド）を保護することもできます。アクセス属性を、対応する名前のrightを値として設定します。

   ```
   <method name="grantVIPAccess" access="myNewRole">
       <parameters>
   ...
       </parameters>
   </method>
   ```

   詳しくは、[こちらのページ](../../configuration/using/implementing-soap-methods.md)を参照してください。

>[!IMPORTANT]
>
>navtreeのコマンドノードでネームド権限を使用できます。 これにより、ユーザーエクスペリエンスは向上しますが、保護はされません（非表示／無効にするには、クライアント側のみを使用します）。アクセス属性を使用する必要があります。

### オーバーフローテーブル

オペレーターのアクセスレベルに応じて機密データ（スキーマの一部）を保護する必要がある場合、フォーム定義で非表示にしないでください（enabledIf／visibleIf 条件）。

エンティティ全体が画面で読み込まれます。また、列定義で表示することもできます。この操作をおこなうには、オーバーフローテーブルを作成する必要があります。[このページ](../../configuration/using/examples-of-schemas-edition.md#overflow-table)を参照してください。

## Web アプリケーションへの Captcha の追加

パブリックのランディングページや購読ページには Captcha を追加することをお勧めします。ただし、DCE（デジタルコンテンツエディター）ページに Captcha を追加することは簡単ではありません。ここでは、Captcha バージョン 5 または Google reCAPTCHA を追加する方法について説明します。

DCE に Captcha を追加する場合、一般的には、Captcha を含めるためのパーソナライゼーションブロックをページコンテンツ内に作成します。**スクリプト**&#x200B;アクティビティと&#x200B;**テスト**&#x200B;を追加する必要があります。

### パーソナライゼーションブロック

1. **[!UICONTROL リソース]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL パーソナライゼーションブロック]**&#x200B;に移動し、新しいパーソナライゼーションブロックを作成します。

1. **[!UICONTROL Web アプリケーション]**&#x200B;のコンテンツタイプを使用し、「**[!UICONTROL カスタマイズメニューに表示]**」をオンにします。

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
   * 4 行目では、Captcha のグレーボックスのサイズ（width/height）と、生成される単語の長さ（minWordSize/maxWordSize）を変更できます。
   * Google reCAPTCHAを使用する前に、Googleに登録し、新しいreCAPTCHAサイトを作成する必要があります。

      `<div class="g-recaptcha" data-sitekey="YOUR_SITE_KEY"></div>`
   検証ボタンを無効にすることが必要な場合もありますが、標準的なボタンやリンクは用意されていないので、HTML 自体で実現することをお勧めします。その方法については、[このページ](https://developers.google.com/recaptcha/)を参照してください。

### Web アプリケーションの更新

1. Webアプリケーションのプロパティにアクセスし、**captchaValid**&#x200B;という名前のブール変数を追加します。

   ![](assets/scripting-captcha.png)

1. 最後のページと&#x200B;**[!UICONTROL ストレージ]**&#x200B;アクティビティの間に、**[!UICONTROL スクリプト]**&#x200B;と&#x200B;**[!UICONTROL テスト]**&#x200B;を追加します。

   分岐「**[!UICONTROL はい]**」を「**[!UICONTROL ストレージ]**」に接続し、別の分岐を、Captcha を追加するページに接続します。

   ![](assets/scripting-captcha2.png)

1. ブランチTrueの条件を`"[vars/captchaValid]"`等しいTrueで編集します。

   ![](assets/scripting-captcha3.png)

1. **[!UICONTROL スクリプト]**&#x200B;アクティビティを編集します。 コンテンツは、選択したcaptchaエンジンに応じて異なります。

1. 最後に、パーソナライズしたブロックをページに追加できます。[このページ](../../web/using/editing-content.md)を参照。

   ![](assets/scripting-captcha4.png)

   ![](assets/scripting-captcha5.png)

>[!IMPORTANT]
>
>reCAPTCHA統合の場合、HTMLに（`<head>...</head>`の）クライアント側のJavaScriptを追加する必要があります。
>
>`<script src="https://www.google.com/recaptcha/api.js" async defer></script>`

### キャンペーンカプチャ

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

### Google Recaptcha

[公式文書](https://developers.google.com/recaptcha/docs/verify)を参照してください。

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

ビルド 8797 以降では、検証 API URL を使用するには、その URL を serverConf ファイルの許可リストに urlPermission ノードで追加する必要があります。

`<url dnsSuffix="www.google.com" urlRegEx="https://www.google.com/recaptcha/api/siteverify"/>`
