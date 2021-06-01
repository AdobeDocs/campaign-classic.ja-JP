---
product: campaign
title: '"Web トラッキングタグ：定義"'
description: '"Web トラッキングタグ：定義"'
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: 0b5575be-57e7-4eee-9c0a-e9ef4b0931bf
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 4%

---

# Web トラッキングタグ：定義{#web-tracking-tag-definition}

Webトラッキングタグは、適切なパラメーターを使用して構築されたURLで、HTTPクエリを介してリダイレクションサーバーに送信されます。

## 送信するデータの形式{#format-of-the-data-to-be-sent}

WebトラッキングURLの形式を次に示します。**https://`<name_of_redirection_server>`:`<port>`/r/`<random_number>`?`<parameters>`**

>[!NOTE]
>
>URLに乱数を追加すると、ブラウザーでのWebページのキャッシュに起因する問題を回避できます。

次の表は、リダイレクションサーバーでサポートされる特殊なパラメーターの一覧です。

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
                              <p>セッションcookie</p> 
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
                              <p>受信者識別子（セッションcookieがない場合に役立ちます）。</p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>tagid</p> 
                           </td>
                           <td>
                              <p>URLパラメーター</p> 
                           </td>
                           <td>
                              <p>追跡するWebページの識別子：これは唯一の必須パラメーターです。</p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>jobid</p> 
                           </td>
                           <td>
                              <p>URLパラメーター</p> 
                           </td>
                           <td>
                              <p>セッションCookieがない場合に使用する配信ID。 この値は
                                 は16進数で表されます。
                              </p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>rcpid</p> 
                           </td>
                           <td>
                              <p>URLパラメーター</p> 
                           </td>
                           <td>
                              <p>インターネットユーザーを識別するために使用されるパラメーター。 このパラメーターの形式は、「name=value」です。
                                 ここで、名前は受信者スキーマのフィールドです。 このパラメーターは、
                                 セッションcookieに含まれる識別子。
                              </p> 
                           </td> 
                        </tr> 
                     </tbody>  
                  </table>

**WebトラッキングURLの例**

* 「ホーム」識別子ページへのアクセス

   **https://myserver.adobe.com/r/9862?tagid=home**

* ビジネスボリュームデータの収集

   **https://myserver.adobe.com/r/4567?tagid=command&amp;amount=100&amp;article=2l**

* 受信者を検索するフィールドの指定

   **https://myserver.adobe.com/r/2353?tagid=home&amp;rcpid=saccount%3D10**

   アカウント番号が10の受信者がホームページに送信されます。

* デフォルト配信の使用

   **https://myserver.adobe.com/r/2456?tagid=home&amp;jobid=e6**

   受信者がホームページに送信されます。 このクエリで配信識別子を含むセッションCookieが送信されない限り、この情報は、識別子230（データベース16のe6）を含む配信に保存されます。

>[!NOTE]
>
>URLパラメーターを使用してリダイレクションサーバーに送信される値は、すべてURLエンコードする必要があります。 上記の例では、「=」と「|」の文字がそれぞれ「%3D」と「%7C」としてエンコードされます。

## データ送信方法{#data-transmission-methods}

次の方法が可能です。

* 追跡するWebページに組み込まれたHTML **`<img>`**&#x200B;タグの&#x200B;**&quot;src&quot;**&#x200B;属性にURLを挿入します。
* 追跡するWebページが生成されたときに、リダイレクトサーバーに直接呼び出します。
