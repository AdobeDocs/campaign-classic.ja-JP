---
title: '"Web トラッキングタグ：定義"'
seo-title: '"Web トラッキングタグ：定義"'
description: '"Web トラッキングタグ：定義"'
seo-description: null
page-status-flag: never-activated
uuid: 915ddfd8-ad1b-41ac-96ed-f7fae687c09f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: b8996508-7173-4225-95e7-b51209aae1f1
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 5%

---


# Web トラッキングタグ：定義{#web-tracking-tag-definition}

Webトラッキングタグーは、適切なパラメーターで構成されたURLで、HTTPクエリを介してリダイレクトサーバーに送信されます。

## 送信するデータの形式 {#format-of-the-data-to-be-sent}

WebトラッキングURLの形式は次のとおりです。 **https://`<name_of_redirection_server>`:`<port>`/r/`<random_number>`?`<parameters>`**

>[!NOTE]
>
>URLに乱数を追加することで、Webページのブラウザーキャッシュに起因する問題を回避できます。

次の表は、リダイレクトサーバーがサポートする特殊なパラメーターのリストを示しています。

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
                              <p>セッションCookie</p> 
                           </td>
                           <td>
                              <p>配信識別子と受信者識別子。</p> 
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
                              <p>URLパラメータ</p> 
                           </td>
                           <td>
                              <p>追跡するWebページの識別子：これは、唯一の必須パラメータです。</p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>jobid</p> 
                           </td>
                           <td>
                              <p>URLパラメータ</p> 
                           </td>
                           <td>
                              <p>セッションcookieがない場合に使用する配信識別子。 この値は16進数で表します。
                              </p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>rcpid</p> 
                           </td>
                           <td>
                              <p>URLパラメータ</p> 
                           </td>
                           <td>
                              <p>インターネットユーザーの識別に使用されるパラメーター。 このパラメーターの形式は「name=value」です。この名前は受信者スキーマのフィールドです。 このパラメーターは、セッションcookieに含まれる識別子よりも優先されます。
                              </p> 
                           </td> 
                        </tr> 
                     </tbody>  
                  </table>

**WebトラッキングURLのいくつか**

* 「ホーム」識別子ページへのアクセス

   **https://myserver.adobe.com/r/9862?tagid=home**

* ビジネス量データの収集

   **https://myserver.adobe.com/r/4567?tagid=command&amp;amount=100&amp;article=2l**

* 受信者を検索するフィールドの指定

   **https://myserver.adobe.com/r/2353?tagid=home&amp;rcpid=saccount%3D10**

   アカウント番号が10の受信者がホームページに送信されます。

* デフォルトの配信の使用

   **https://myserver.adobe.com/r/2456?tagid=home&amp;jobid=e6**

   受信者がホームページに送信されます。 このクエリで配信IDを含むセッションcookieが送信されない限り、この情報は、識別子230（データベース16のe6）と共に配信に格納されます。

>[!NOTE]
>
>URLパラメーターを介してリダイレクトサーバーに送信されるすべての値は、URLエンコードされている必要があります。 上記の例では、「=」と「|」の文字がそれぞれ「%3D」と「%7C」としてエンコードされています。

## データ送信方法 {#data-transmission-methods}

次の方法を使用できます。

* 追跡するWebページに組み込まれているHTML ******`<img>`** タグの「src」属性にURLを挿入します。
* 追跡するWebページが生成された場合、リダイレクトサーバーに直接呼び出します。

