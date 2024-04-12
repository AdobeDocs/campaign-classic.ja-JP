---
product: campaign
title: Web トラッキングタグの定義
description: Web トラッキングタグの定義
feature: Application Settings
role: Data Engineer, Developer
exl-id: 0b5575be-57e7-4eee-9c0a-e9ef4b0931bf
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 2%

---

# Web トラッキングタグ：定義{#web-tracking-tag-definition}



Web トラッキングタグは、適切なパラメーターで構成された URL で、HTTP クエリを介してリダイレクトサーバーに送信されます。

## 送信するデータの形式 {#format-of-the-data-to-be-sent}

Web トラッキング URL の形式は次のとおりです。 **https://`<name_of_redirection_server>`:`<port>`/r/`<random_number>`?`<parameters>`**

>[!NOTE]
>
>URL に追加される乱数は、ブラウザーが web ページをキャッシュすることで発生する問題を回避します。

次の表に、リダイレクトサーバーでサポートされる特別なパラメーターのリストを示します。

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
                              <p>配信識別子と受信者識別子。</p> 
                           </td> 
                        </tr>
                        <tr>
                           <td>
                              <p>uuid230</p> 
                           </td>
                           <td>
                              <p>永続的な cookie</p> 
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
                              <p>トラッキングされる web ページの識別子：これは唯一の必須パラメーターです。</p> 
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
                              <p>セッション Cookie がない場合に使用される配信識別子。 この値は、16 進数で表されます。
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
                              <p>インターネットユーザーを識別するために使用されるパラメーター。 このパラメーターの形式は、「name=value」です。この名前は、受信者スキーマのフィールドです。 このパラメーターは、セッション cookie に含まれる識別子よりも優先されます。
                              </p> 
                           </td> 
                        </tr> 
                     </tbody>  
                  </table>

**いくつかの web トラッキング URL**

* 「ホーム」識別子ページへの訪問

  **https://myserver.adobe.com/r/9862?tagid=home**

* 業務量データの収集

  **https://myserver.adobe.com/r/4567?tagid=command&amp;amount=100&amp;article=2l**

* 受信者を検索するフィールドの指定

  **https://myserver.adobe.com/r/2353?tagid=home&amp;rcpid=saccount%3D10**

  アカウント番号が 10 の受信者がホームページに送信されます。

* デフォルト配信の使用

  **https://myserver.adobe.com/r/2456?tagid=home&amp;jobid=e6**

  受信者がホームページに送信されます。 このクエリで配信識別子を含むセッション cookie が送信されない限り、この情報は識別子 230 で配信に保存されます（データベース 16 の e6）。

>[!NOTE]
>
>URL パラメーターを介してリダイレクトサーバーに送信される値はすべて URL エンコードする必要があります。 この例では、文字&#39;=&#39;および&#39;|&#39;は、それぞれ&#39;%3D&#39;および&#39;%7C&#39;としてエンコードされています。

## データ送信方法 {#data-transmission-methods}

以下の方法が可能です。

* に URL を挿入 **&quot;src&quot;** HTMLの属性 **`<img>`** 追跡する web ページに組み込まれたタグ。
* 追跡する web ページが生成されたら、リダイレクトサーバーへの直接呼び出しを行います。
