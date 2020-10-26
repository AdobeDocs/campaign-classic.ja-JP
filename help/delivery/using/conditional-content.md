---
title: 条件付きコンテンツ
seo-title: 条件付きコンテンツ
description: 条件付きコンテンツ
seo-description: null
page-status-flag: never-activated
uuid: d1c38263-a163-448c-8822-8b3e776e45cf
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: personalizing-deliveries
discoiquuid: 167cc61a-fbc7-48cb-89ff-fbdbf9321c01
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '488'
ht-degree: 100%

---


# 条件付きコンテンツ{#conditional-content}

条件付きコンテンツフィールドを設定することで、例えば受信者のプロファイルに基づいて動的パーソナライゼーションを作成できます。特定の条件が成立した場合に、テキストブロックや画像を切り替えることができます。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](#conditionnal-content-video)


## E メール内での条件の使用 {#using-conditions-in-an-email}

次の例では、受信者の性別と興味の対象に基づいて動的にパーソナライズされるメッセージを作成する方法について説明します。

* データソースの「**[!UICONTROL 性別]**」フィールド（M または F）に基づいて、名前の表示に付ける「Mr.」と「Ms.」を切り替える
* 顧客が表明した関心事項や検出された関心事項に基づいて、次のようにニュースレターや優待販売案内の構成をパーソナライズする

   * 興味 1 -- > ブロック 1
   * 興味 2 -- > ブロック 2
   * 興味 3 -- > ブロック 3
   * 興味 4 -- > ブロック 4

あるフィールドの値に基づく条件付きコンテンツを作成するには、次の手順に従います。

1. パーソナライゼーションアイコンをクリックし、**[!UICONTROL 条件付きコンテンツ／If]** を選択します。

   ![](assets/s_ncs_user_conditional_content02.png)

   パーソナライゼーション要素がメッセージ本文に挿入されます。それらを設定する必要があります。

1. 次に、**If** 式のパラメーターを入力します。

   手順は次のとおりです。

   * 式の最初の要素 **`<field>`** を選択し（**If** 式を挿入すると、この要素がデフォルトでハイライトされた状態になります）、パーソナライゼーションアイコンをクリックして、この要素をテストフィールドに置き換えます。

      ![](assets/s_ncs_user_conditional_content03.png)

   * **`<value>`** を、条件が成立するためのフィールド値に置き換えます。この値は二重引用符で囲む必要があります。
   * 条件が成立したときに挿入するコンテンツを指定します。このコンテンツにはテキスト、画像、フォーム、ハイパーテキストリンクなどを含めることができます。

      ![](assets/s_ncs_user_conditional_content04.png)

1. 「**[!UICONTROL プレビュー]**」タブをクリックして、次のように、配信の受信者に応じたメッセージコンテンツの表示を確認します。

   * 条件が成立する受信者を選択した場合：

      ![](assets/s_ncs_user_conditional_content05.png)

   * 条件が成立しない受信者を選択した場合：

      ![](assets/s_ncs_user_conditional_content06.png)

さらに多くの場合分けを追加し、1 つまたは複数のフィールドに基づいてコンテンツの切り替えを定義することもできます。そのためには、**[!UICONTROL 条件付きコンテンツ／Else]** および&#x200B;**[!UICONTROL 条件付きコンテンツ／Else if]** を使用します。式の設定方法は、**If** 式の場合と同様です。

![](assets/s_ncs_user_conditional_content07.png)

>[!CAUTION]
>
>**Else** 条件や **Else if** 条件を追加した後は、JavaScript の構文を尊重するために、**%> &lt;%** の文字を削除する必要があります。

「**[!UICONTROL プレビュー]**」をクリックし、いずれかの受信者を選択して、条件コンテンツの評価結果を表示します。

![](assets/s_ncs_user_conditional_content08.png)

## 多言語の E メールの作成 {#creating-multilingual-email}

以下の例では、多言語の E メールを作成する方法について説明します。コンテンツは、受信者の優先言語に基づいて、いずれかの言語で表示されます。

1. E メールを作成し、ターゲット母集団を選択します。この例では、表示するバージョンを決定する条件は、受信者のプロファイルの&#x200B;**言語**&#x200B;の値に基づいています。この例では、これらの値は **EN**、**FR**、**ES** に設定されています。
1. E メールの HTML コンテンツで、「**[!UICONTROL ソース]**」タブをクリックし、次のコードを貼り付けます。

   ```
   <% if (language == "EN" ) { %>
   <DIV id=en-version>Hello <%= recipient.firstName %>,</DIV>
   <DIV>Discover your new offers!</DIV>
   <DIV><a href="https://www.adobe.com/products/en">www.adobe.com/products/en</A></FONT></DIV><%
    } %>
   <% if (language == "FR" ) { %>
   <DIV id=fr-version>Bonjour <%= recipient.firstName %>,</DIV>
   <DIV>Découvrez nos nouvelles offres !</DIV>
   <DIV><a href="https://www.adobe.com/products/fr">www.adobe.com/products/fr</A></DIV><%
    } %>
    <% if (language == "ES" ) { %>
   <DIV id=es-version><FONT face=Arial>
   <DIV>Olà <%= recipient.firstName %>,</DIV>
   <DIV>Descubra nuestros nuevas ofertas !</DIV>
   <DIV><a href="https://www.adobe.com/products/es">www.adobe.com/products/es</A></DIV>
   <% } %>
   ```

1. 「**[!UICONTROL プレビュー]**」タブで、優先言語が異なる受信者を選択して、E メールコンテンツをテストします。

   >[!NOTE]
   >
   >この E メールコンテンツには代替バージョンが定義されていないので、E メールを送信する前にターゲット母集団をフィルタリングしてください。

## 条件付きコンテンツを含む多言語ニュースレターの作成方法 {#conditionnal-content-video}

複数言語のニュースレターの例を使用して、配信に条件付きコンテンツを追加する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/24926?quality=12&captions=jpn)
