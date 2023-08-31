---
product: campaign
title: Web トラッキングタグの定義
description: Web トラッキングタグの定義
feature: Application Settings
role: Data Engineer, Developer
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
exl-id: 0b5575be-57e7-4eee-9c0a-e9ef4b0931bf
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 4%

---

# Web トラッキングタグ：定義{#web-tracking-tag-definition}



Web トラッキングタグは、適切なパラメーターで構築された単純な URL で、HTTP クエリを介してリダイレクトサーバーに送信されます。

## 送信するデータの形式 {#format-of-the-data-to-be-sent}

Web トラッキング URL の形式を次に示します。 **https://`<name_of_redirection_server>`:`<port>`/r/`<random_number>`?`<parameters>`**

>[!NOTE]
>
>URL に乱数を追加することで、Web ページのキャッシュに起因する問題を回避できます。

次の表に、リダイレクションサーバーでサポートされる特別なパラメーターの一覧を示します。

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
                              <p>配信識別子と受信者の識別子。</p> 
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
                              <p>トラッキングされる Web ページの識別子：これは唯一の必須パラメーターです。</p> 
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
                              <p>セッション Cookie がない場合に使用する配信 ID。 この値は 16 進数で表されます。
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
                              <p>インターネットユーザーを識別するために使用されるパラメーター。 このパラメーターの形式は「name=value」です。名前は受信者スキーマのフィールドです。 このパラメーターは、セッション Cookie に含まれる識別子よりも優先されます。
                              </p> 
                           </td> 
                        </tr> 
                     </tbody>  
                  </table>

**いくつかの Web トラッキング URL**

* 「ホーム」識別子ページにアクセス

  **https://myserver.adobe.com/r/9862?tagid=home**

* ビジネスボリュームデータの収集

  **https://myserver.adobe.com/r/4567?tagid=command&amp;amount=100&amp;article=2l**

* 受信者を検索するフィールドの指定

  **https://myserver.adobe.com/r/2353?tagid=home&amp;rcpid=saccount%3D10**

  アカウント番号が 10 の受信者がホームページに送信されます。

* デフォルトの配信の使用

  **https://myserver.adobe.com/r/2456?tagid=home&amp;jobid=e6**

  受信者がホームページに送信されます。 この情報は、配信識別子を含むセッション cookie がこのクエリで送信されない限り、識別子 230（データベース 16 の e6）を含む配信に格納されます。

>[!NOTE]
>
>URL パラメーターを使用してリダイレクションサーバーに送信する値は、すべて URL エンコードする必要があります。 上記の例では、「=」と「|」の文字がそれぞれ「%3D」と「%7C」としてエンコードされています。

## データ送信方法 {#data-transmission-methods}

次の方法が可能です。

* URL を **&quot;src&quot;** HTMLの属性 **`<img>`** タグを組み込んで、トラッキングする Web ページに貼り付けます。
* 追跡する Web ページが生成されたときに、リダイレクトサーバーに直接呼び出します。
