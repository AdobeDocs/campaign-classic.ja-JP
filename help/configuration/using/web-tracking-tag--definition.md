---
product: campaign
title: '"Web トラッキングタグ：定義"'
description: '"Web トラッキングタグ：定義"'
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: 0b5575be-57e7-4eee-9c0a-e9ef4b0931bf
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 4%

---

# Web トラッキングタグ：定義{#web-tracking-tag-definition}

![](../../assets/v7-only.svg)

Web トラッキングタグは、適切なパラメーターを使用して構築された URL で、HTTP クエリを介してリダイレクトサーバーに送信されます。

## 送信するデータの形式 {#format-of-the-data-to-be-sent}

Web トラッキング URL の形式を次に示します。**https://`<name_of_redirection_server>`:`<port>`/r/`<random_number>`?`<parameters>`**

>[!NOTE]
>
>URL に乱数を追加すると、ブラウザーで Web ページがキャッシュされる問題を回避できます。

次の表は、リダイレクションサーバーでサポートされる特別なパラメータの一覧です。

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
                              <p>セッション cookie</p> 
                           </td>
                           <td>
                              <p>配信 ID と受信者 ID。</p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>uuid230</p> 
                           </td>
                           <td>
                              <p>永続的な Cookie</p> 
                           </td>
                           <td>
                              <p>受信者識別子（セッション cookie がない場合に役立ちます）。</p> 
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
                              <p>追跡する Web ページの識別子：これは唯一の必須パラメーターです。</p> 
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
                              <p>セッション Cookie がない場合に使用する配信 ID。 この値は
                                 は 16 進数で表されます。
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
                              <p>インターネットユーザーの識別に使用されるパラメーター。 このパラメータの形式は、"name=value",
                                 ここで、名前は受信者スキーマのフィールドです。 このパラメーターは、
                                 セッション cookie に含まれる識別子。
                              </p> 
                           </td> 
                        </tr> 
                     </tbody>  
                  </table>

**Web トラッキング URL の一部**

* 「ホーム」識別子ページへのアクセス

   **https://myserver.adobe.com/r/9862?tagid=home**

* ビジネスボリュームデータの収集

   **https://myserver.adobe.com/r/4567?tagid=command&amp;amount=100&amp;article=2l**

* 受信者を検索するフィールドの指定

   **https://myserver.adobe.com/r/2353?tagid=home&amp;rcpid=saccount%3D10**

   アカウント番号が 10 の受信者がホームページに送信されます。

* デフォルト配信の使用

   **https://myserver.adobe.com/r/2456?tagid=home&amp;jobid=e6**

   受信者がホームページに送信されます。 この情報は、配信識別子を含むセッション Cookie がこのクエリで送信されない限り、識別子 230（データベース 16 では e6）を含む配信に保存されます。

>[!NOTE]
>
>URL パラメーターを使用してリダイレクトサーバーに送信する値は、すべて URL エンコードする必要があります。 上記の例では、「=」と「|」はそれぞれ「%3D」と「%7C」としてエンコードされます。

## データ送信方法 {#data-transmission-methods}

次の方法が可能です。

* 追跡する Web ページに組み込まれたHTML **`<img>`** タグの **&quot;src&quot;** 属性に URL を挿入します。
* 追跡する Web ページが生成されたら、リダイレクトサーバーに直接呼び出します。
