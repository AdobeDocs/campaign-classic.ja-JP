---
product: campaign
title: パーソナライズされた PDF ドキュメントの生成
description: パーソナライズされた PDF ドキュメントを生成する方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Personalization
role: User
hide: true
exl-id: e5239d99-256b-412b-be20-f64f822da9c3
TQID: https://experienceleague.adobe.com/5hETJLlKZ9iWu2k1nW-RMeDlzpSm7wFwfe3QwSEZCa4
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: e0eb8757-182f-49f3-94a4-1587d16f5094
feature_v2: id: b631758a-142d-425f-b9aa-f756d85cb979id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2: id: e95a583b-fcfa-4524-8666-46a29c828119id: c8da4fdd-eb94-4751-a43c-f82733fb2d6eid: d5bbe3da-ba85-4242-817e-54f7c4b943e0id: f4da0e76-df77-451e-ad61-21afb7bd8810
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 499
ht-degree: 100%

---

# パーソナライズされた PDF ドキュメントの生成{#generating-personalized-pdf-documents}

## 様々な PDF ドキュメントについて {#about-variable-pdf-documents}

Adobe Campaign では、LibreOffice や Microsoft Word ドキュメントから、メールの添付ファイル用に可変 PDF ドキュメントを生成することができます。

サポートされる拡張子は、「.docx」、「.doc」および「.odt」です。

ドキュメントをパーソナライズする場合、メールのパーソナライゼーションと同じ JavaScript 機能を使用します。

「**[!UICONTROL メッセージの配信中にファイルのコンテンツはパーソナライズされて PDF に変換]**」オプションを有効化する必要があります。 このオプションは、配信メールにファイルを添付する際にアクセスできます。 計算済みファイルの添付について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/emails/attaching-files.html?lang=ja){target="_blank"}を参照してください。

請求書のヘッダーのパーソナライゼーションの例：

![](assets/s_ncs_pdf_simple.png)

動的テーブルを生成する場合や URL 経由で画像を含める場合は、特定のプロセスを実行する必要があります。

## 動的テーブルの生成 {#generating-dynamic-tables}

動的テーブルを生成する手順は次のとおりです。

* 3 つの行と必要な数の列を含むテーブルを作成し、レイアウト（境界線など）を設定します。
* テーブルにカーソルを置いて、**[!UICONTROL 表／表プロパティ]**&#x200B;メニューをクリックします。 「**[!UICONTROL 表]**」タブに移動して、**NlJsTable** で始まる名前を入力します。
* 1 行目の最初のセルで、テーブルで表示する値の反復処理を可能にするループ（例：for）を定義します。
* テーブルの 2 行目の各セルに、表示する値を返すスクリプトを挿入します。
* テーブルの 3 行目（最後の行）でループを閉じます。

  動的テーブルの定義の例：

  ![](assets/s_ncs_pdf_table.png)

## 外部画像の挿入 {#inserting-external-images}

外部画像の挿入は、例えば、画像付きドキュメントの URL が受信者のフィールドに入力されており、そのドキュメントをパーソナライズしたい場合に便利です。

そのためには、パーソナライゼーションブロックを設定してから、パーソナライゼーションブロックに対する呼び出しを添付ファイルに含める必要があります。

**例：受信者の国に応じてパーソナライズされたロゴを挿入する**

**ステップ 1：添付ファイルの作成：**

* パーソナライゼーションブロックに対する呼び出し **&lt;%@ include view=&quot;blockname&quot; %>** を挿入します。
* コンテンツ（パーソナライズされている、またはパーソナライズされていない）をファイルの本文に挿入します。

![](assets/s_ncs_open_office_blocdeperso.png)

**ステップ 2：パーソナライゼーションブロックの作成：**

* Adobe Campaign コンソールの&#x200B;**[!UICONTROL リソース／キャンペーン管理／パーソナライゼーションブロック]**&#x200B;メニューに移動します。
* 「My_Logo」を内部名に持つ新しい「My Logo」パーソナライゼーションブロックを作成します。
* 「**[!UICONTROL 詳細設定...]**」リンクをクリックして、「**[!UICONTROL ブロックは次に含まれるオプションで「添付ファイル」をオンにします]**」オプションをオンにします。 これにより、パーソナライゼーションブロックの定義を直接 OpenOffice ファイルのコンテンツにコピーできます。

  ![](assets/s_ncs_pdf_bloc_option.png)

  パーソナライゼーションブロック内の 2 つのタイプの宣言を区別する必要があります。

   * パーソナライゼーションフィールドの Adobe Campaign コードにおける「開く」および「閉じる」山括弧は、エスケープ文字（それぞれ `&lt;` と `&gt;`）で置き換える必要があります。
   * OpenOffice XML コード全体が OpenOffice ドキュメントにコピーされます。

今回の例では、パーソナライゼーションブロックは次のようになります。

```
<% if (recipient.country.label == "Germany") { %>
<draw:frame svg:width="4cm" svg:height="3cm">
<draw:image xlink:href=https://..../logo_germany.png />
</draw:frame>
<% } else
if (recipient.country.label == "USA")
{ %>
<draw:frame svg:width="4cm" svg:height="3cm">
<draw:image xlink:href=https://..../logo_USA.png />
</draw:frame>
<% } %>
```

受信者の国に応じて、パーソナライズされたコンテンツが配信にリンクされているドキュメントに表示されます。

![](assets/s_ncs_pdf_result.png)
