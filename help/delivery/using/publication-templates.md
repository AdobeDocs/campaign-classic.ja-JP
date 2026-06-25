---
product: campaign
title: パブリッシュテンプレート
description: パブリッシュテンプレート
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Templates
role: User
exl-id: 3b6e4974-4551-4da2-8eca-577c4f9cbd91
TQID: https://experienceleague.adobe.com/mU7usRNlg73dYQS1PuorYpp9g4d7bNXAWBtIEE1VULk
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
subfeature_v2:
  - id: e95a583b-fcfa-4524-8666-46a29c828119
  - id: c8da4fdd-eb94-4751-a43c-f82733fb2d6e
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: f4da0e76-df77-451e-ad61-21afb7bd8810
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 844
ht-degree: 100%

---

# パブリッシュテンプレート{#publication-templates}

## パブリッシュテンプレートについて {#about-publication-templates}

パブリッシュテンプレートは、パブリッシュプロセスで使用する次のリソースを参照します。

* データスキーマ
* 入力フォーム
* 各出力ドキュメントの変換テンプレート

## パブリッシュテンプレートの識別 {#identification-of-a-publication-template}

パブリッシュテンプレートは、名前と名前空間で識別されます。

スタイルシートの識別キーは、コロンで分けられた名前空間と名前によって形成される文字列です。例：**cus:newsletter**

>[!NOTE]
>
>実際には、スキーマ、フォーム、パブリッシュテンプレートに同じキーを使用することをお勧めします。

## テンプレートの作成と設定 {#creating-and-configuring-the-template}

パブリッシュテンプレートは、デフォルトでは&#x200B;**[!UICONTROL 管理／設定／パブリッシュテンプレート]**&#x200B;ノードに保存されます。 新しいテンプレートを作成するには、テンプレートのリストの上の&#x200B;**[!UICONTROL 新規]**&#x200B;ボタンをクリックします。

パブリッシュテンプレートを設定するには、テンプレートの名前（名前と名前空間で構成される識別キー）、テンプレートのラベル、データスキーマ、テンプレートがリンクされる入力フォームを入力します。

![](assets/d_ncs_content_model.png)

>[!NOTE]
>
>ラベルは、このパブリッシュテンプレートをベースとしてコンテンツを作成する際には常に表示されます。

「**コンテンツの生成前にステータスを確認**」オプションを選択すると、ファイル生成の条件として、コンテンツインスタンスのステータスが「検証済み」になっているかを確認します。 詳しくは、[パブリッシュ](#publication)を参照してください。

変換テンプレートは出力ドキュメントごとに追加する必要があります。 変換テンプレートは必要な数だけ作成できます。

「**[!UICONTROL 名前]**」フィールドは、出力時のレンダリングのタイプを示す自由形式のラベルです。 変換テンプレートごとに、タブのパブリッシュ設定を使用できます。

### レンダリング {#rendering}

「**[!UICONTROL レンダリング]**」タブで、次の設定をおこないます。

* 出力ドキュメントの予測に使用するレンダリングのタイプ：XSL スタイルシートまたは JavaScript テンプレート
* 出力ドキュメントのフォーマット：HTML、テキスト、XML または RTF
* 構成データ（使用するスタイルシートまたは JavaScript テンプレート）があるテンプレート

### パブリッシュ {#publication}

パブリッシュでは、選択したタイプが「**[!UICONTROL ファイル]**」の場合、ファイルの形式で出力ドキュメントを生成します。

![](assets/d_ncs_content_model2.png)

次のパブリッシュオプションを使用できます。

* 出力ファイルのエンコーディング文字セットは、「**[!UICONTROL エンコード]**」フィールドで指定できます。 デフォルトでは、ラテン 1 (1252) 文字セットが使用されます。
* 「**[!UICONTROL マルチファイル生成]**」オプションは、特別なドキュメントパブリッシュモードを有効化します。 このオプションによって、出力ドキュメントの各ページの先頭にパーティションタグが入力されます。 コンテンツを生成すると、入力されているパーティションタグごとにファイルが作成されます。 このモードは、コンテンツブロックからミニサイトを生成するために使用します。 詳しくは、[マルチファイル生成](#multi-file-generation)を参照してください。
* 「**[!UICONTROL 場所]**」フィールドには、出力ファイルの名前を入力します。 ファイル名を自動生成するために、複数の変数で構成される名前にすることができます。

  変数は、 **`$(<xpath>)`** というフォーマットで入力します（**`<xpath>`** は、パブリッシュテンプレートデータスキーマのフィールドのパス）。

  ファイルの名前は、日付タイプのフィールドで構成することもできます。 このフィールドを正しく書式設定するには、フィールドのパスと出力フォーマットをパラメーターとして、**$date-format** 関数を使用します。

  デフォルトでは、ファイル名の構成フォーマットに「@name」フィールドと「@date」フィールドの変数を使用します。

  ```xml
  ct_$(@name)_$date-format(@date,'%4Y%2M%2D').htm
  ```

  生成されたファイル名は、ct_news12_20110901.htm のようになります。

  >[!NOTE]
  >
  >コンテンツの生成について詳しくは、[コンテンツインスタンスの作成](using-a-content-template.md#creating-a-content-instance)を参照してください。

### 配信 {#delivery}

このタブでは、コンテンツ上で直接配信を開始するためのシナリオを選択できます。 メールのコンテンツは、出力フォーマット（HTML またはテキスト）に基づいて自動的に入力されます。

![](assets/d_ncs_content_model3.png)

>[!NOTE]
>
>コンテンツに基づく配信作成の例については、[コンテンツインスタンスの配信](using-a-content-template.md#delivering-a-content-instance)を参照してください。

### 集約 {#aggregator}

スクリプトまたはクエリのリストからデータを集約し、コンテンツデータにより XML ドキュメントを高度なものにできます。 その目的は、リンクが参照している特定の情報を補足したり、データベースから要素を追加したりすることです。

### マルチファイル生成 {#multi-file-generation}

マルチファイル生成を有効化するには、パブリッシュモデルで「**[!UICONTROL マルチファイル生成]**」オプションを選択します。 このオプションによって、出力ドキュメントの各ページの先頭に対して、スタイルシート内にパーティションタグを指定できます。 コンテンツを生成すると、パーティションタグが出現するたびにファイルが作成されます。

パーティションタグは、次のようにスタイルシート内に組み込まれます。

**`<xsl:comment> #nl:output_replace(<name_of_file>) </xsl:comment>`**（**`<name_of_file>`** は生成するページのファイル名）

**例：**「cus:book」スキーマを使用した複数ファイル生成

原理は、複数の章をリストするメインページを生成し、外部ページに章の詳細を表示できるようにするということです。

![](assets/d_ncs_content_chunk.png)

対応するスタイルシート（「cus:book.xsl」）は次のようになります。

```xml
<?xml version="1.0" encoding="ISO-8859-1" ?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:output encoding="ISO-8859-1" method="html"/>

  <!-- Style sheet entry point -->
  <xsl:template match="/book">
    <html>
      <body>
        <h1><xsl:value-of select="@name"/></h1>
        <lu>
          <xsl:for-each select="chapter">
            <li><a target="_blank" href="chapter{@id}.htm"><xsl:value-of select="@name"/></a></li>  
          </xsl:for-each>
       </lu>
      </body>
    </html>
   </xsl:template>
</xsl:stylesheet>
```

章の詳細を生成するために、2 つ目のスタイルシート（「cus:chapter.xsl」）が必要です。

```xml
<?xml version="1.0" encoding="ISO-8859-1" ?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:output encoding="ISO-8859-1" method="html"/>

  <!-- Detail of a chapter -->
  <xsl:template match="chapter">
    <!-- Cut tag -->   
    <xsl:comment> #nl:output_replace($(path)/chapter<xsl:value-of select="@id"/>.htm)</xsl:comment>
    
    <html>
      <body>
        <h1><xsl:value-of select="@name"/></h1>
        <xsl:value-of select="page" disable-output-escaping="yes"/>
      </body>
    </html>
  </xsl:template>

  <!-- Style sheet entry point -->
  <xsl:template match="/book">
    <xsl:apply-templates/>
   </xsl:template>
</xsl:stylesheet>
```

生成するファイルに含めるページの先頭に、パーティションタグを入力します。

```xml
<xsl:comment> #nl:output_replace($(path)/<xsl:value-of select="@id"/>.htm)</xsl:comment>
```

ファイル名は、パブリッシュパスが格納された **$(path)** 変数と、入力ドキュメント内の章の識別子に対応する **`<xsl:value-of select="@id" />`** で構成されます。

パブリッシュモデルは、「cus:book.xsl」と「cus:chapter.xsl」の 2 つのスタイルシートを使用して設定する必要があります。

「**[!UICONTROL マルチファイル生成]**」オプションを変換テンプレートでアクティブにする必要があります。

![](assets/d_ncs_content_chunk2.png)

複数ファイルの生成では「**[!UICONTROL 場所]**」フィールドは使用しませんが、パブリッシュ時にエラーが発生しないよう、このフィールドにも入力する必要があります。
