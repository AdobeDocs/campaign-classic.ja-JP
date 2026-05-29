---
product: campaign
title: Web トラッキングタグの定義
description: Web トラッキングタグの定義
feature: Application Settings
role: Developer
exl-id: 0b5575be-57e7-4eee-9c0a-e9ef4b0931bf
TQID: https://experienceleague.adobe.com/UkA0XyCzaDt2qlxpODQ-zoyC0YdKs3K5qg4UacvT8ck
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 2%

---

# Web トラッキングタグ：定義{#web-tracking-tag-definition}



Web トラッキングタグは、適切なパラメーターで構築されたURLであり、HTTP クエリを介してリダイレクションサーバーに送信されます。

## 送信するデータの形式 {#format-of-the-data-to-be-sent}

Web トラッキング URLの形式は次のとおりです。**https://`<name_of_redirection_server>`:`<port>`/r/`<random_number>`?`<parameters>`**

>[!NOTE]
>
>URLにランダムな数字を追加すると、ブラウザーがweb ページをキャッシュする際に発生する問題を回避できます。

次の表に、リダイレクトサーバーでサポートされている特殊パラメーターのリストを示します。

<table>
                     <thead>
                        <tr>
                           <th>名前</th>
                           <th>タイプ</th>
                           <th>説明</th> 
                        </tr> 
                     </thead>
                     <tbody>
                        <tr>
                           <td>
                              <p>ID</p> 
                           </td>
                           <td>
                              <p>セッション Cookie</p> 
                           </td>
                           <td>
                              <p>配信IDと受信者ID。</p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>uuid230</p> 
                           </td>
                           <td>
                              <p>永続的なCookie</p> 
                           </td>
                           <td>
                              <p>受信者の識別子（セッション Cookieがない場合に便利）。</p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>tagid</p> 
                           </td>
                           <td>
                              <p>URL パラメーター</p> 
                           </td>
                           <td>
                              <p>トラッキング対象web ページの識別子：これは必須パラメーターのみです。</p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>jobid</p> 
                           </td>
                           <td>
                              <p>URL パラメーター</p> 
                           </td>
                           <td>
                              <p>セッション Cookieがない場合に使用される配信ID。この値は
                                 16進数で表します。
                              </p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>rcpid</p> 
                           </td>
                           <td>
                              <p>URL パラメーター</p> 
                           </td>
                           <td>
                              <p>インターネットユーザーを識別するために使用されるパラメーター。このパラメーターの形式は「name=value」です。
                                 ここで、名前は受信者スキーマのフィールドです。このパラメーターは、次の値よりも優先されます
                                 セッション cookieに含まれる識別子。
                              </p> 
                           </td> 
                        </tr> 
                     </tbody>  
                  </table>

**いくつかのweb トラッキング URL**

* 「ホーム」識別子ページへのアクセス

  **https://myserver.adobe.com/r/9862?tagid=home**

* 業務量データの収集

  **https://myserver.adobe.com/r/4567?tagid=command&amp;amount=100&amp;article=2l**

* 受信者を検索するフィールドの指定

  **https://myserver.adobe.com/r/2353?tagid=home&amp;rcpid=saccount%3D10**

  アカウント番号が10の受信者がホームページに送信されます。

* デフォルトの配信の使用

  **https://myserver.adobe.com/r/2456?tagid=home&amp;jobid=e6**

  受信者がホームページに送信されます。 この情報は、配信識別子を含むセッションクッキーがこのクエリで送信されない限り、識別子230 （データベース 16のe6）を持つ配信に保存されます。

>[!NOTE]
>
>URL パラメーターを介してリダイレクトサーバーに送信されるすべての値は、URL エンコードする必要があります。 指定された例では、文字&#39;=&#39;と&#39;|&#39;はそれぞれ&#39;%3D&#39;と&#39;%7C&#39;としてエンコードされていることに注意してください。

## データの伝送方法 {#data-transmission-methods}

次の方法が可能です。

* トラッキング対象のweb ページに組み込まれたHTML **`<img>`** タグの&#x200B;**&quot;src&quot;**&#x200B;属性にURLを挿入します。
* トラッキングするweb ページが生成されたときに、リダイレクトサーバーに直接呼び出します。
